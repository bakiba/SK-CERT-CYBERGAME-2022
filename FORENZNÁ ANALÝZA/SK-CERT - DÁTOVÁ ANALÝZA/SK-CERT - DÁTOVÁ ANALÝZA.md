# SK-CERT - DÁTOVÁ ANALÝZA
> Ozvala sa nám spoločnosť, ktorá dostala hlásenie že majú infikovaný počítač ransomvérom. Ten je špecifický tým že posiela vygenerovaný privátny kľuč na útočníkov server. Prikladáme vám pcap: https://drive.google.com/file/d/13arhVaKNFD_g2qCjuDBrECmpN6MKd4Rw/view?usp=sharing <br/>
Reported Difficulty: 1

:exclamation: *Súbory a zadania z tejto súťaže môžete stiahnuť z https://ulozto.net/file/9qLDe5asaCHJ/*

## 1 Kontrola
> Z dodaného PCAP súboru je potrebné zistiť či naozaj je spoločnosť infikovaná, a pokiaľ áno, tak je potrebné zistiť o aký privátny kľuč sa odosiela. Vlajka je IP adresa serveru na ktorý sa kľuč odoslal.

> Body: 3

Otvoríme `part1.pcap` vo Wireshark a pustime sa do analýzy. Musím uznať, že som to išiel skratkou a skúšal rôzne IP adresy z komunikácie kým som nenatrafil na tu pravú: `194.182.66.53`

```
flag: 194.182.66.53
```

## 2 Windows?
> Zdrojová IP počítača ktorý odosielal privátny kľuč, patrí lokálnemu počítaču s WIndows. Je potrebné zistiť ako prenikli do tohto systému. Prikladáme bezpečnostný log v XML formáte.
https://drive.google.com/file/d/1pmJNCfgnpTCMewCaRioqagYj0_VLcold/view?usp=sharing
Vlajka je dátum a čas prvého prieniku (Formát Y-m-d H:i:s)

> Body: 3

V tomto kroku mame security log v xml, otvoríme ho v Libre Office Calc a pozrieme sa na rôzne eventy čo tam mame. Z počtu rôznych logov vidíme vysoký výskyt 4625 čo je Failed Login.

![](images/2022-03-06-12-36-54.png)

Keď si vyfiltrujeme všetky 4625 eventy vidíme, že všetky majú FailureReason `%%2313` čo je `Unknown user name or bad password. (529)`, targetuser je `victim` a zdrojom je `LinuxServerWebServer`. Vyzerá to na bruteforce login ktorý, ak predpokladáme, že bol enty point, náš flag by mal byť prvý successfull login attempt po poslednom failed:

![](images/2022-03-06-12-55-59.png)

```
flag: 2022-02-22 20:40:08
```

## 3 Ktorý proces?
> Po bruteforce útoku a prihlásení, útočník spustil malvér. Je potrebné zistiť meno procesu. Vlajka je meno procesu (Formát: meno_procesu.format)

> Body: 3

V Libre Office vyfiltrujeme všetky eventy s ProcessName a NewProcessName a hľadáme niečo podozrivé po čase prvého successfull loginu útočníka a o chvíľku to máme:

![](images/2022-03-06-13-10-07.png)

```
flag: YouWillCryRansomware3000.exe
```

## 4 Otvorený test
> Kompromitovaný LinuxServerWebServer je náše testovacie prostredie, aplikácie na serveri sú dostupné iba z lokálnej siete, ale telnet server je otvorený do sveta. Prikladáme Pcap s potrebnými dátami. https://drive.google.com/file/d/1y3pOvG9PDGf7Sg7HtgOGvfjpk6qlVYor/view?usp=sharing
Vlajka je EpochTime prieniku do systému (bez milisekúnd).

> Body: 3

Po otvorení `web.pcap` súboru, poobzeráme sa trošku okolo a uvidíme, že sa niekto snaží prihlásiť cez telnet session:

![](images/2022-03-06-15-43-26.png)

Skúsime hľadať "Login" v paketoch s cieľom nájsť prvý success login, a po niekoľko desiatok klikoch narážame na "Last Login" message ktorá sa objavuje po úspešnom prihlásení sa.

![](images/2022-03-06-15-48-16.png)

Pre istotu pôjdeme ešte zopár paketov vyššie aby sme sa uistili, že to bol útočník ktorý uhádol login a heslo. Po prezretí zopár desiatok paketov predtým vidíme, že útočník uhádol login `bob` a heslo `adminbob` a paket číslo `6262` môžeme poväzovať ako okamih prieniku do systému ktorý ma EpochTime (bez milisekúnd)

![](images/2022-03-06-15-53-52.png)

```
flag: 1645560004
```

## 5 Stará joomla
> Z logov sme zistili že útočník vyhackoval aj našu joomlu na testovacom serveri. Z posledného PCAP súboru je potrebné zistiť aký exploit útočník použil.
Vlajka je url odkial útočník exploit stiahol (Formát: www.stránka_exploitu.doména/cesta_k_exploitu)

> Body: 3

Pri pozeraní zopár ďalších paketov vidíme, že útočník prvé čo spravil je `wget https://www.exploit-db.com/download/47465`, rýchly náhľad do toho url nám potvrdzuje že ide o Joomla expoit.

![](images/2022-03-06-16-16-09.png)

```
flag: www.exploit-db.com/download/47465
```