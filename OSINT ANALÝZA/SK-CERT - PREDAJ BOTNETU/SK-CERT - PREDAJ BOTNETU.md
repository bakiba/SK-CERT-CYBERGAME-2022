# SK-CERT - PREDAJ BOTNETU
> Z overeného zdroja sme dostali informáciu že zakladateľ botnetu “OctoBotDisaster” predal prístupy. Je potrebné zistiť kto daný botnet kúpil <br/>
Reported Difficulty: 1 


## 1 Verejný zdroj
> Je potrebné nájsť informácie o danom botnete

Google nic nedal, skusame Bing ktory nachadza GitHub repo: https://github.com/3mp7yv01d/OctoBotDisaster a mame prvy flag.

![](images/2022-03-07-22-19-16.png)

```
flag: SK-CERT{f1r57_fl4g}
```

## 2 Analýza zdroja	
> Je potrebné získať informácie z nájdeného zdroju

Pozerame sa na bot.c a nic tam zaujimave nie je, nic nenaznacuje ze treba to kompilovat alebo hladat flag niekde v kode. Pozerame sa dalej na GitHub uzivatela `3mp7yv01d`, nema ziadne ine repo, vidime ale ze spravil 3 commity do `OctoBotDisaster`, pozrieme sa na commit history https://github.com/3mp7yv01d/OctoBotDisaster/tree/b9605c01205a7ae79883dcdff3e1a2dfef83ed04 a nachadzame dalsi flag:

![](images/2022-03-07-22-32-30.png)

```
flag: SK-CERT{574r71ng_w17h_051n7}
```

## 3 Discord
> Čo nového na discorde? Pokračujeme analýzou discordového serveru

Z predchazajucej ulohy je aj link na discord server, pozrieme sa tam, dame vyhladavat "SK-CERT" a mame dalsi flag:

![](images/2022-03-07-22-36-27.png)

```
flag:SK-CERT{7r4n54c710n_c0mpl373}
```

## 4 Sociálna sieť
> Je tu ešte viac na zistenie?

## 5 Zo siete na sieť
> Zamknuté Sociálna sieť
