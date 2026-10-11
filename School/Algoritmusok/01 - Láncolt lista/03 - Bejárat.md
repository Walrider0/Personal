
A **bejárás** a korábban látott továbblépés ismétlése. Sorban elérjük a lista elemeit, és mindegyiken elvégzünk egy műveletet. Ez lehet például kiírás, összegzés vagy számlálás.

A `kiir(L)` függvényben az aktuális elemet az `x` jelöli. Kezdetben az első elemre hivatkozik, amelyet az `L.fej` mezőből érünk el. Amíg `x` nem `None`, kiírjuk az elem kulcsát, majd az `x = x.kov` utasítással továbblépünk.

Az utolsó elem `kov` mezője `None`, ezért az utolsó továbblépés után a ciklus befejeződik. Csak az `x` hivatkozását állítjuk át, így a lista feje és az elemek mezői változatlanok maradnak.

```
def kiir(L):
    x = L.fej   # Külön változóval járjuk be a listát, a fej nem változik.
    print("fej", end=" -> ")
    while x is not None:
        print(x.kulcs, end=" -> ")
        x = x.kov   # Az utolsó elem után x értéke None lesz.
    print("None")
```

A bejárásban a `print` a kulcsok megjelenítését végzi. Alapértelmezés szerint minden kiírás után új sort kezdene. Az `end=" -> "` beállítással ehelyett egy nyilat írunk, így az elemek egy sorba kerülnek. Az utolsó `print("None")` jelzi a lista végét, és lezárja a sort.

A függvényt a korábban összekapcsolt háromelemű `L` listán próbáljuk ki.

```
kiir(L)    # fej -> 423 -> 356 -> 764 -> None
fej -> 423 -> 356 -> 764 -> None
```

Ugyanez a bejárás **üres listában** is működik. Ekkor nincs első elem, ezért az `x = L.fej` után az `x`értéke rögtön `None`. A ciklus egyszer sem fut le, és a kimenet `fej -> None` lesz. Az üres esethez nincs szükség külön elágazásra.

```
ures = LancoltLista()
kiir(ures)                  # fej -> None
print(ures.fej is None)     # True

```
### Elemszám meghatározása

A bejárás útvonala akkor sem változik, ha kiírás helyett megszámoljuk az elemeket. Minden elért elemnél növelünk egy számlálót, majd továbblépünk a következőre. A számláló kezdeti értéke `0`, így üres listában is megfelelő eredményt kapunk.

Készítsd el az `elemszam(L)` függvényt, amely visszaadja a darabszámot. A függvény a listát ne módosítsa.

```
def elemszam(L):
    darab = 0   # Üres listában ez marad a visszaadott érték.
    x = L.fe
    while x is not None:
        darab += 1   # Minden elért elemet egyszer számolunk meg.
        x = x.kov
    return darab
```
```
print(elemszam(L))               # 3
print(elemszam(LancoltLista()))  # 0
```
[[04 - Keresés kulcs alapján]]
