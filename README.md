# Čo je toto

Tento repository je mojou snahou popísať postup môjho riešenia úloh v CTF CYBERGAME od SK-CERT a spol., ktorá sa konala od 1.3.2022 do 10.5.2022.

Viac informácií o hre, pravidlách, štatúte atď.: https://cybergame.sk-cert.sk/

Tento repository obsahuje write-up úloh ktoré sa mi podarilo v tejto súťaži vyriešiť. Hlavnú ideou týchto write-upov je zachovať znalosť a skúsenosti získane v tejto súťaži, a tiež ako učebná pomôcka pre tých ktorým je toto zaujímavé. <br/>
Postup som dokumentoval takmer počas samotnej investigácie, takže sú tu aj chyby ktoré som spravil, zle cesty ktorými som sa vybral a aj zopár predčasne objavených flagov, ktoré nepatrili k úlohe ktorú som pravé riešil ale ku niektorej z nasledujúcich. 

Pripomínam, že cybersecurity je mojou záľubou a hobby, neživím sa tým, som v tom iba v začiatkoch a toto nie je ukážka "jak se to dělá" ale skôr ako som ja na to prišiel pri študovaní a hraní sa.

Tiež sa ospravedlňujem za gramatické chyby, na škole som sa neučil Slovenčinu. Ale gramatické chyby v zadaniach nie sú moje :)

# Obsah

Hra pozostávala z niekoľko vetiev (tematických oblasti) a každá vetva mala niekoľko scenárov v rámci ktorých bolo treba vyriešiť 3 až 7 úloh. Na vyriešenie každej úlohy bolo treba nájsť vlajku (`flag`), ktorá bola vo formáte `SK-CERT{abc}`. Nasledujúce úlohy boli zamknuté, čo znamenalo, že keď sa vyrieši predchádzajúca úloha tak sa odomkne ďalšia, teda postup riešenia bol sekvenčný.

Tento repository je štruktúrovaný podlá vetiev a scenárov, tak ako boli v hre.

## MALVÉROVÁ ANALÝZA

* [SK-CERT - INITIAL: MALWARE](MALVÉROVÁ%20ANALÝZA/SK-CERT%20-%20INITIAL%20MALWARE/SK-CERT%20-%20INITIAL%20MALWARE.md) - nemám zatiaľ popísaný (3 z 3 úloh vyriešených)
* [SK-CERT - STRATENÉ KRYPTO](MALVÉROVÁ%20ANALÝZA/SK-CERT%20-%20STRATENÉ%20KRYPTO/SK-CERT%20-%20STRATENÉ%20KRYPTO.md) (5 z 5 úloh vyriešených)
* [SK-CERT - BOTNET](MALVÉROVÁ%20ANALÝZA/SK-CERT%20-%20BOTNET/SK-CERT%20-%20BOTNET.md) (6 z 7 úloh vyriešených)
* [SK-CERT - KLÁVESNICA](MALVÉROVÁ%20ANALÝZA/SK-CERT%20-%20KLÁVESNICA/SK-CERT%20-%20KLÁVESNICA.md) (4 z 4 úloh vyriešených)
* [SK-CERT - NEBEZPEČNÝ MALVÉR](MALVÉROVÁ%20ANALÝZA/SK-CERT%20-%20NEBEZPEČNÝ%20MALVÉR/SK-CERT%20-%20NEBEZPEČNÝ%20MALVÉR.md) (2 z 5 úloh vyriešených)
* [SK-CERT - OOMPALOOMPA MALVÉR](MALVÉROVÁ%20ANALÝZA/SK-CERT%20-%20OOMPALOOMPA%20MALVÉR/SK-CERT%20-%20OOMPALOOMPA%20MALVÉR.md) (1 z 5 úloh vyriešených)

## FORENZNÁ ANALÝZA

* [SK-CERT - INITIAL: FTP SERVER](FORENZNÁ%20ANALÝZA/SK-CERT%20-%20INITIAL%20FTP%20SERVER/SK-CERT%20-%20INITIAL%20FTP%20SERVER.md) (3 z 3 úloh vyriešených)
* [SK-CERT - DÁTOVÁ ANALÝZA](FORENZNÁ%20ANALÝZA/SK-CERT%20-%20DÁTOVÁ%20ANALÝZA/SK-CERT%20-%20DÁTOVÁ%20ANALÝZA.md) (5 z 5 úloh vyriešených)
* [SK-CERT - NEZNÁME USB](FORENZNÁ%20ANALÝZA/SK-CERT%20-%20NEZNÁME%20USB/SK-CERT%20-%20NEZNÁME%20USB.md) (6 z 6 úloh vyriešených)
* [SK-CERT - CHÝBAJÚCA ÚHRADA](FORENZNÁ%20ANALÝZA/SK-CERT%20-%20CHÝBAJÚCA%20ÚHRADA/SK-CERT%20-%20CHÝBAJÚCA%20ÚHRADA.md) (3 z 5 úloh vyriešených)
* [SK-CERT - UNIKNUTÁ ŠTATISTIKA](FORENZNÁ%20ANALÝZA/SK-CERT%20-%20UNIKNUTÁ%20ŠTATISTIKA/SK-CERT%20-%20UNIKNUTÁ%20ŠTATISTIKA.md) (1 z 5 úloh vyriešených)

## OBFUSKÁCIA A KRYPTO

* [SK-CERT - INITIAL: ENCODING](OBFUSKÁCIA%20A%20KRYPTO/SK-CERT%20-%20INITIAL%20ENCODING/SK-CERT%20-%20INITIAL%20ENCODING.md) (3 z 3 úloh vyriešených)
* [SK-CERT - ESOLANG](OBFUSKÁCIA%20A%20KRYPTO/SK-CERT%20-%20ESOLANG/SK-CERT%20-%20ESOLANG.md) (5 z 5 úloh vyriešených)
* [SK-CERT - STEGOSTART](OBFUSKÁCIA%20A%20KRYPTO/SK-CERT%20-%20STEGOSTART/SK-CERT%20-%20STEGOSTART.md) (4 z 4 úloh vyriešených)
* [SK-CERT - NEPODARENÝ RANSOMVÉR](OBFUSKÁCIA%20A%20KRYPTO/SK-CERT%20-%20NEPODARENÝ%20RANSOMVÉR/SK-CERT%20-%20NEPODARENÝ%20RANSOMVÉR.md) (0 z 5 úloh vyriešených)

## OSINT ANALÝZA

* [SK-CERT - INITIAL: APT 0XFF](OSINT%20ANALÝZA/SK-CERT%20-%20INITIAL%20APT%200XFF/SK-CERT%20-%20INITIAL%20APT%200XFF.md) (3 z 3 úloh vyriešených)
* [SK-CERT - PREDAJ BOTNETU](OSINT%20ANALÝZA/SK-CERT%20-%20PREDAJ%20BOTNETU/SK-CERT%20-%20PREDAJ%20BOTNETU.md) (5 z 5 úloh vyriešených)
* [SK-CERT - RANSOMVÉR](OSINT%20ANALÝZA/SK-CERT%20-%20RANSOMVÉR/SK-CERT%20-%20RANSOMVÉR.md) (5 z 5 úloh vyriešených)
* [SK-CERT - STRATENÁ OSOBA](OSINT%20ANALÝZA/SK-CERT%20-%20STRATENÁ%20OSOBA/SK-CERT%20-%20STRATENÁ%20OSOBA.md) (4 z 5 úloh vyriešených)


