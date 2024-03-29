# SK-CERT - NEBEZPEČNÝ MALVÉR
> Externá firma nás informovala o výskyte nového linuxového malvéru. Malvér údajne umožňuje vzdialený prístup do siete a vykonáva útoky s finančným dopadom. Firma dokázala zistiť, že za tým je tento súbor (heslo do zipu je cybergame2022): https://drive.google.com/file/d/1ImyJIMRkNw47h0M45CKgxT3byDzZ0slz/view?usp=sharing
a požiadali nás o analýzu. <br/>
Reported Difficulty: 3

:exclamation: *Súbory a zadania z tejto súťaže môžete stiahnuť z https://ulozto.net/file/9qLDe5asaCHJ/*

## 1 Kill switch
> Je možné malvér deaktivovať?

> Body: 9

<details>
<summary>Zobraziť riešenie</summary>

Zo stihnutého súboru máme file `iodine-infected` a pomocou `file iodine-infected` zisťujeme, že je to Linux ELF 64-bit executable. `strings` nám žiadny flag nenašiel. Virustotal nič neudáva.
Google nám hovorí, že `iodine` je software ktorý umožňuje tunelovať IPv4 dáta cez DNS server. 
Po spustení súboru, vidíme, že sa deje nejaký DNS query:

![](images/2022-04-15-10-44-35.png)

Skusmé pozrieť pomocou Wireshark čo sa deje na sieti keď pustime tento súbor ešte raz a jeden z DNS query príkazov nám odhalil flag:

![](images/2022-04-15-10-47-57.png)

Toto ale nie je prvý flag, asi bude pre jednu z ďalších úloh. 

Ideme skúsiť ťažšiu cestu, skúsiť debug a pozrieť sa čo nám niečo kód neodhalí. Otváram binárku v [GHIDRA debuggeri](https://ghidra-sre.org/), aj keď netuším ako to všetko funguje, ale dúfam, že niečo tam uvidím :).

Po nejakom čase pozerania, nasledovná funkcia mi padla do oka:

![](images/2022-04-17-18-33-19.png)

Neviem to ani vysvetliť (čo hovorí ako som na tom zle) ale som prišiel na to ak sa mi podarí aby `curl https://lnjkabnsklmjgfkdjbngsbnsdreotijp.sghb` fungovalo, teda vrátilo `0`, vypľuje mi to flag.. dúfam...

Problém ako donútiť aby curl vrátilo `0` som vyriešil pridaním `lnjkabnsklmjgfkdjbngsbnsdreotijp.sghb` do môjho DNSka, a potom ešte som naštartoval Burp local proxy a pridal jeho certifikát to Trusted root... a vyšlo to:

![](images/2022-04-17-18-36-43.png)

```
flag: SK-CERT{h4rdc0r3_4nt1d3bug}
```
</details>

## 2 Inject
> Je potrebné zistiť ako malvér vykonáva svoju ďalšiu fázu.

> Body: 9

<details>
<summary>Zobraziť riešenie</summary>

Ak použijeme [gdb](https://man7.org/linux/man-pages/man1/gdb.1.html) na debugovanie, viďme, že sú tam nejaké antidebug kontroly:

![](images/2022-04-18-15-05-39.png)

Z kódu vidím, že je tam funkcia, ktorá zisťuje `/proc/self/status` a pri trosku googlenia vyzerá, že je to [technika](https://programmer.ink/think/linux-anti-debugging-notes.html) ktorá zisťuje ci je prítomný `TracerPid` ktorý je `non-0` pri debugovani.

![](images/2022-04-18-16-17-53.png)

Tu moja snaha asi konci... debuging je niečo čo sa definitívne musím naučiť. 
</details>

## 3 Zadné vrátka   
> Ako sa útočníci dotanú do siete?

> Body: 9

<details>
<summary>Zobraziť riešenie</summary>

Tu som skúsil použiť flag čo som našiel pri mojom prvom pokuse pri hľadaní riešenia prvej úlohy, a zobralo to.

```
flag: SK-CERT{dn5_3ncryp70r}
```
</details>

## 4 Fáza 2
> Zamknuté Inject

> Body: 9

## 5 ET volá domov
> Zamknuté Fáza 2

> Body: 9