# SK-CERT - STRATENÉ KRYPTO
>Dostali sme hlásenia, že niektorým ľuďom zmizli kryptomeny. Jediná podobnosť medzi týmito hláseniami je tento dokument (Heslo do zip je cybergame2022): https://drive.google.com/file/d/1JxTfveNIuUPP3IPG8xf_sk0oIUX5Tma_/view?usp=sharing <br/>
Reported Difficulty: 1

## 1 ODT
>Je potrebné zistiť či tento dokument obsahuje niečo zaujímavé

Po stiahnuti dokumentu z prilozeneho odkazu, zistime ze je to OpenOffice Document file, asi to bude nejake macro, takze po nainstalovani LibreOffice otvorime bitcoin.odt a hned mame upozornenie ze macra mozu obsahovat virus. Po otvoreni macra, hned mame nas prvy flag:

![](images/2022-03-05-14-00-36.png)

```
flag: SK-CERT{h3ll4_3v1l_m4cr0}
```

## 2 Čo spúšťame?
>Vyzerá to tak, že macro spúšťa nejaký ďalší program, je potrebné zistiť aký.

Hladanie dalsieho flagu bolo trosku zamotane kedze prve podozrive miesto po dekodovani ASCII (https://testguild.com/qtp-ascii-chr-code-chart/) odhalilo flag `SK-CERT{wh3re_my_crypt0_g03s}`, ale to nebol ten spravny.

![](images/2022-03-05-14-09-58.png)

Po dlhsiom patrani, sme sa dostali na debug funkcii ktore boli na zaciatku kodu, a po ich sledovani pri debugovani sme nasli dalsi flag ktory uz bol spravny:

![](images/2022-03-05-14-10-23.png)

```
flag: SK-CERT{w3_w4nt_s0m3_w4kk3t5}
```

## 3 Čo ďalej?
>Zistite kam sa posielaju ukradnuté kryptopenaženky.

Tak tu sme hned skusili flag `SK-CERT{wh3re_my_crypt0_g03s}` ktory sme nasli v predchadzajucom ktoku pri dekodovni podozriveho ASCII retazca:

```
chr(13) & chr(83) & chr(75) & chr(45) & chr(67) & chr(69) & chr(82) & chr(84) & chr(123) & chr(119) & chr(104) & chr(51) & chr(114) & chr(101) & chr(95) & chr(109) & chr(121) & chr(95) & chr(99) & chr(114) & chr(121) & chr(112) & chr(116) & chr(48) & chr(95) & chr(103) & chr(48) & chr(51) & chr(115) & chr(125)
```
```
flag: SK-CERT{wh3re_my_crypt0_g03s}
```

## 4 Skládačka
>Zistili sme kam sa odosielajú kryptopenaženky. Skúste zistiť ako funguje malvér v prípade, že vykradne nejaké kryptopenaženky.

Kedze macro hlada krypto penazenky aby dostal do dalsej faze exekucie, tak mu tam jednu dame, ideme na https://www.myetherwallet.com/wallet/create/software?type=keystore vygenerujeme softwerovu penazenku a pokracujeme v debugovani. Tu ale narazame na problem lebo strana co ma prijimat crypto nefunguje a macro mam tu pada:

![](images/2022-03-05-14-14-27.png)

Tak to odosielanie proste zakomentujeme a skusime to znovu.

![](images/2022-03-05-14-14-40.png)

Dalsia cast kodu stahuje 70te vydanie phrack magazinu (http://phrack.org/issues/70/5.html) v ktorom boli „zakodovany“ dalsi flag:

![](images/2022-03-05-14-15-24.png)

```
flag: SK-CERT{50m3_k1nd_0f_m4lw4r3}
```

## 5 Finálna vlajka
>Z predošlej časti ste zistili že sa stahuje nejaký script, je potrebné zistiť čo je zač.

Z toho pastebinu z predoslej ulohy sa nam stiahne powershell payload do `C:\Users\Public\Documents\script.ps1`. Samozrejme ze ten powershell je obfuscovany:

![](images/2022-03-05-14-16-02.png)

Vyzera to na obfuskaciu sposobom vymeny pismena za jeho ASCII kod kde sa este medzi kazde pismeno vlozil jeden z tychto znakov (vidno na konci): `.SplIt('crWXoq~,:a' )|foreacH {( [INT] $_-AS [CHAr])} ) )`
Asi najjednoduhsi sposob ako toto vyriesit je odstranit exekuciu cez IEX, ktory je tiez zakodovany ako ASCII kod na zaciatku skriptu: `& ( $shEllid[1]+$sHeLLiD[13]+'x')` za `write-host` a jednoducho to spustit.

![](images/2022-03-05-14-18-43.png)

Vysledok nie je uplne idealny, vidime ze je tam este dalsia nejaka obfuskacia trapnou vymeno znakov, ale co ale je vidno je nas posledny flag:
![](images/2022-03-05-14-19-06.png)

```
flag: SK-CERT{p0w3r5h3ll_k3yl0g}
```