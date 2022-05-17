# SK-CERT - NEPODARENÝ RANSOMVÉR
> Známa skupina Fibonacci FIN rozšírila portfólio svojich služieb o ransomvér. Ransomvér má však našťastie detské chybičky… <br/>
Reported Difficulty: 3

## 1 Neinicializovaný
> Už prvá iterácia ransomvéru používala silnú symetrickú šifru AES. Autori však pri implementácii vynechali dôležité úvodné kroky… Toto je súbor, zašifrovaný ransomvérom: https://drive.google.com/file/d/1a3GhrCgE2cgppE6CxZW_tw8z709al81j/view?usp=sharing

> Body: 9

:exclamation: *Ďalšie kroky boli pridané po súťaži na základe pomoci od iných súťažiacich ktorým patri vďaka!*

Z priloženého odkazu sťahujeme zip súbor v ktorom sa nachádza `flag.txt.encrypted` ktorý je zašifrovaný:

![](images/2022-05-13-10-57-45.png)

Zadanie hovorí, že bola požitá AES šifra ale že dôležité kroky boli vynechane, rozmýšľam aké by to mohli byt kroky... Poznám princíp AES ale nič hlbšie. Skúsime použiť známy CyberChef v ktorom nachádzame `AES Decrypt` ktorý vyžaduje zadať `Key` a `IV` a zvoliť `Mode`. 

![](images/2022-05-13-11-11-14.png)

Žeby tie vynechane doležíte kroky boli Key a IV? CyberChef žiada aby sme tam niečo vložili tak skúšame dať `0`... vyhodí to:

![](images/2022-05-13-11-12-59.png)

Tak skúsime tam dať 16 bajtový kľuč, teda 32 núl. Dáme to podobne aj do IV. Pri zvolenom default `CBC` móde to nič neukazuje, skúšame ďalšie a pri `CTR` móde máme krásne dešifrovaný flag:

![](images/2022-05-13-11-16-13.png)

```
flag: SK-CERT{00_z3r0_r4nd0mn355_0000}
```

P.S. v diskusii na diskorde bol uvedený aj ďalší spôsob ako toto dešifrovať pomocou `openssl enc -aes-256-ctr -K 0 -iv 0 -in flag.txt.encrypted`

![](images/2022-05-13-11-19-51.png)

## 2 Recyklácia
> Autori sa poučili a nastavili kvalitný kľúč a inicializačný vektor. Stále im však čosi nedocvaklo… Toto je obsah adresára, zašifrovaného ransomvérom: [link po sutazi nefunguje](#2-recyklácia)

> Body: 9

Z priloženého odkazu sťahujeme zip súbor v ktorom sa nachádzajú dva súbory `Strategia_kybernetickej_bezpecnosti_2021.pdf.encrypted` a `flag.txt.encrypted`. Slovo "recyklácia" nás navádza na situáciu znovu použitia rovnakého kľúča a inicializačného vektora pri šifrovaní. Z mojej limitovanej znalosti kryptografie, tuším že sa tato úloha da vyriešiť bez kľúča a IV, spomínam si že som také niečo kedysi čítal... tak ideme googliť a nachádzame tento link https://crypto.stackexchange.com/questions/2991/why-must-iv-key-pairs-not-be-reused-in-ctr-mode ktorý nám potvrdzuje že keď mame šifrovaný text C1 a k nemu prislúchajúci plaintext P1 a ďalší šifrovaný text C2 ktorý bol šifrovaný rovnakým kľúčom ako C1, tak na dešifrovanie C2 nepotrebujeme nič iné okrem C1, P1 a C2. Takže:
  * C1 = `Strategia_kybernetickej_bezpecnosti_2021.pdf.encrypted`
  * C2 = `flag.txt.encrypted`
  * P1 = plaintext zodpovedajúci `Strategia_kybernetickej_bezpecnosti_2021.pdf.encrypted`

To P1 skúsime pohľadať, mám pocit že to je nejaký verejný dokument... netrvalo viac ako zopár klikov a získavame P1: https://www.nbu.gov.sk/wp-content/uploads/kyberneticka-bezpecnost/Strategia_kybernetickej_bezpecnosti_2021.pdf

Teraz nám treba spraviť `C1 XOR P1 XOR C2`... ako toto spraviť jednoducho som sa inšpiroval týmto článkom: https://rmn0x01.github.io/2019/10/31/writeup-slashroot4-quals-reuse/. Nainštaloval som `pwn` package do Pythonu a dal do kopy tento `decode.py`:

```python
from pwn import *

c1 = open('Strategia_kybernetickej_bezpecnosti_2021.pdf.encrypted','rb').read()
p1 = open('Strategia_kybernetickej_bezpecnosti_2021.pdf','rb').read()
c2 = open('flag.txt.encrypted','rb').read()

p2 = xor(c2,xor(c1,p1))

k = open('tmp','wb+')
k.write(p2)
k.close()
```

Potom som vykonal script `python3 decode.py` a skúsil či je tam flag: `strings tmp | grep SK-CERT`

![](images/2022-05-13-14-41-30.png)

```
flag: SK-CERT{r3cyc11n6_g0n3_s0_wr0n6}
```

## 3 Tajomstvá
> Zákazníka skolila nová verzia ransomvéru. Zjavne už každý súbor šifruje inak. Tu sú nejaké vzorky.

> Body: 9

## 4 Vzory
> Zamknuté Tajomstvá

> Body: 9

## 5 Počítač do šrotu
> Zamknuté Vzory

> Body: 9

