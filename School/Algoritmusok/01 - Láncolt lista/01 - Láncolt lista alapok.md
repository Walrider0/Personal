A **láncolt lista** olyan adatstruktúra, amelyben az elemek sorrendjét a közöttük tárolt kapcsolatok adják meg. Ezeket **hivatkozásokkal**, más néven **referenciákkal** tároljuk. Egy hivatkozáson keresztül elérünk egy másik objektumot. Így az egymást követő listaelemeknek nem kell egymás mellett elhelyezkedniük a memóriában.

**Kétszeresen láncolt listában** minden elemhez megadjuk az előző és a következő szomszédját. A kapcsolatok mentén ezért előre és visszafelé is haladhatunk. Egy listaelem a következő mezőket tartalmazza:

| Mező    | Jelentés                                                                 |
| :------ | :----------------------------------------------------------------------- |
| `kulcs` | Az elemben tárolt érték, amely alapján keresünk. A példákban egész szám. |
| `elo`   | Hivatkozás az előző elemre.                                              |
| `kov`   | Hivatkozás a következő elemre.                                           |
Ezt a felépítést a `ListaElem` osztállyal írjuk le.

A `pass` olyan utasítás, amely nem végez műveletet. Helykitöltőként használható egy még meg nem írt osztály vagy függvény törzsében, mert a Python nem enged teljesen üres törzset. A megvalósítás utasításai a `pass` helyére kerülnek.

class ListaElem:

```
    def __init__(self, kulcs):
        self.kulcs = kulcs
        self.elo = None   # Az új elem még nincs más elemekhez kapcsolva.
        self.kov = None
```

- A `ListaElem` osztály egyetlen listaelem felépítését írja le. A `ListaElem(423)` hívással létrehozunk egy ilyen objektumot, amelynek mezőit az `__init__` metódus állítja be.

- A `self` az adott objektumra hivatkozik, itt az újonnan létrehozott listaelemre. A `self.kulcs = kulcs` utasításban a jobb oldali `kulcs` a kapott paraméter, a bal oldali `self.kulcs` pedig az objektum saját mezője. Ebben tároljuk el a megadott értéket.

- A `None` itt azt jelzi, hogy nincs ilyen szomszéd. Az új elem még nincs összekapcsolva más elemmel, ezért az `elo` és a `kov` mezőjének kezdeti értéke is `None`.

```
elem = ListaElem(423)
print(elem.kulcs)           # 423
print(elem.elo, elem.kov)   # None None
```
```
423
None None
```

---

### Hivatkozás, mutató és memóriacím

- Az `elem` változón keresztül az imént létrehozott objektumot érjük el. A listaelemekben is ilyen hivatkozásokat tárolunk majd, hogy az egyik elemből eljussunk a szomszédjához.

- A **memóriacím** egy adat memóriabeli helyét jelöli. A **mutató** ilyen címet tárol, és ezen keresztül „mutat” az adatra. Pythonban a mutatók szerepét objektumhivatkozások töltik be, ezért a listaelemek összekapcsolásához nem kell címeket kézzel megadnunk.

- Az `id(elem)` az objektum azonosítóját adja vissza egész számként. A kiírásával szemléltethetjük, hogy két változó ugyanazt az objektumot éri-e el.

- A `hex(szam)` egy egész szám **tizenhatos, vagyis hexadecimális alakját** adja vissza szövegként. A memóriacímeket általában így jelenítjük meg, ezért a példában is ezt a formát használjuk. A `0x` előtag a tizenhatos számrendszert jelzi.

```
masik_nev = elem
masik_elem = ListaElem(423)

print("elem:      ", hex(id(elem)))
print("masik_nev: ", hex(id(masik_nev)))
print("masik_elem:", hex(id(masik_elem)))
```
```
elem: 0x7fe67f4df230 
masik_nev: 0x7fe67f4df230 
masik_elem: 0x7fe67f5179d0
```

Az `elem` és a `masik_nev` mellett ugyanaz az azonosító jelenik meg. A `masik_nev = elem` értékadás nem másolja le az objektumot. A két változó ugyanarra az elemre hivatkozik.

A `masik_elem` külön létrehozott objektum, ezért eltérő azonosító tartozik hozzá. **Azonos kulcs nem jelent azonos objektumot.** Az azonosítók konkrét értéke új futtatáskor eltérhet, az egyezésük vagy különbözőségük a fontos.

---

### Az `is` operátor

Az objektumok azonosságát az azonosítók kiírása nélkül is ellenőrizhetjük. Az `is` azt vizsgálja, hogy két hivatkozás **ugyanazt az objektumot** jelöli-e. A kulcsok értékét ezzel szemben a `==` operátorral hasonlítjuk össze.

Az `x is None` azt ellenőrzi, hogy `x` értéke `None`. Az `x is not None` ennek az ellentéte. Ezzel állapítjuk meg a listaműveletekben, hogy van-e aktuális elem vagy szomszéd.

```
print(elem is masik_nev)               # True
print(elem is masik_elem)              # False
print(elem.kulcs == masik_elem.kulcs)   # True
print(elem.kov is None)                # True
```


---
## 2. Az elemek összekapcsolása

Egy objektumra nemcsak egy változó, hanem egy másik objektum mezője is hivatkozhat. Ezt használjuk fel a listaelemek összekapcsolásához.

- Az `a.kov = b` utasítással beállítjuk, hogy az `a` elemet a `b` kövesse. Az `a.kov` mező ugyanarra az objektumra hivatkozik, mint a `b` változó. Nem a kulcsot másoljuk át, és nem készítünk új elemet.

- A visszafelé vezető kapcsolatot külön kell megadni. A `b.elo = a` azt rögzíti, hogy a `b` előző eleme az `a`. Kétszeresen láncolt listában mindkét irányt beállítjuk.
```
a = ListaElem(423)
b = ListaElem(356)
c = ListaElem(764)

  
a.kov = b
b.elo = a
b.kov = c
c.elo = b


print(a.kov.kulcs)   # 356, az a következő elemének kulcsa.
print(c.elo.kulcs)   # 356, a c előző elemének kulcsa.
```
```
356
356
```

Az `a.kov.kulcs` kifejezést balról jobbra olvassuk. Először elérjük az `a` következő elemét, majd kiolvassuk annak kulcsát. Az eredmény `356`. A `c.elo.kulcs` ugyanehhez az elemhez jut el a másik irányból.

A korábbi azonosítókiírással az összekapcsolást is ellenőrizhetjük. Az `a.kov` és a `b` ugyanarra az objektumra hivatkozik, ezért az `id` mindkettőnél ugyanazt az értéket adja. A `kov` mezőbe az objektumhivatkozás került, nem az azonosítót tartalmazó szám vagy szöveg.

```
print("b:    ", hex(id(b)))
print("a.kov:", hex(id(a.kov)))
print(a.kov is b)   # True
```
```
b: 0x7fe67eb08770 
a.kov: 0x7fe67eb08770 
True
```

---
### A listafej

- A szomszédokat már elérjük egymáson keresztül. A teljes lista kezeléséhez azt is rögzítenünk kell, hogy melyik az első elem. Ezt a **listafej**, röviden **fej** adja meg.

- A fej az első elemre hivatkozik. Innen indulva a `kov` mezőket követjük, és így érjük el a további elemeket. A fej tehát nem egy újabb listaelem, hanem egy hivatkozás.

- A `LancoltLista` osztály a teljes listát képviseli, és a `fej` mezőt tárolja. Ezzel szemben a `ListaElem` egyetlen elem kulcsát és szomszédaira mutató hivatkozásait tartalmazza. Üres listában a `fej` értéke `None`.
- 
```
class LancoltLista:
    def __init__(self):
        self.fej = None   # Kezdetben a lista üres.
```
A már összekapcsolt három elemet az `L` listán keresztül is elérhetővé tesszük. Ehhez az új lista `fej` mezőjét az `a` elemre állítjuk.

```
L = LancoltLista()
L.fej = a

print(L.fej.kulcs)      # 423
print(L.fej.kov is b)   # True
```
```
423 
True
```

Az `L.fej = a` értékadás után az `L` listából elérhető a három összekapcsolt elem:

```
L.fej ──> [423] <──> [356] <──> [764]
```

A nyilak hivatkozásokat jelölnek. A kétirányú nyíl két külön kapcsolatot jelent, amelyeket az `elo` és a `kov` mezőkben tárolunk.

Az első elem `elo` mezője és az utolsó elem `kov` mezője `None`. A lista **nem ciklikus**, mert a végéről nem kapcsolódunk vissza az elejére. **Nem rendezett**, mert nem követeljük meg a kulcsok növekvő vagy csökkenő sorrendjét.

### Továbblépés a kapcsolatok mentén

A lista feldolgozásához egy külön változóval követjük, hogy éppen melyik elemnél tartunk. Az `x = L.fej` után az `x` és az `L.fej` ugyanarra az első elemre hivatkozik.

Az `x = x.kov` utasítás az `x` hivatkozását állítja át a következő elemre. A lista fejét és az elemek mezőit nem módosítja.

```
x = L.fej
x = x.kov


print(x.kulcs)       # 356
print(L.fej.kulcs)   # 423
```

A kiírás eredménye `356`, majd `423`. Az `x` már a második elemre hivatkozik, az `L.fej` viszont továbbra is az elsőre.

Más történik, ha nem az `x` hivatkozását állítjuk át, hanem **az elért objektum egyik mezőjét módosítjuk**. Az `x` és a `b` most ugyanazt a második elemet jelöli. Az `x.kulcs` módosítása ezért a `b.kulcs` lekérdezésekor is látható. A példa végén visszaállítjuk a `356` kulcsot.

```
x.kulcs = 20
print(b.kulcs)   # 20, ugyanannak az elemnek a kulcsát olvassuk ki.


b.kulcs = 356    # Visszaállítjuk az eredeti kulcsot.
print(x.kulcs)   # 356
```

## 3. Bejárás

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

## 4. Önálló feladat - Keresés kulcs alapján

A bejárás során minden elemet feldolgoztunk. **Kereséskor** arra vagyunk kíváncsiak, hogy található-e a listában egy megadott kulcsú elem. Ha megtaláltuk, nem kell tovább haladnunk.

Készítsd el a `keres(L, k)` függvényt. Az `L` a vizsgált lista, a `k` a keresett kulcs. A keresés a fejtől induljon, és a `kov` hivatkozásokat követve haladjon.

A függvény **a megtalált elemre mutató hivatkozást** adja vissza, ne a kulcsot vagy az elem sorszámát. Ha a kulcs többször szerepel, az első előfordulást adja vissza. Sikertelen kereséskor és üres listában az eredmény `None` legyen. A függvény a lista fejét, kulcsait és kapcsolatait ne módosítsa.

```
def keres(L, k):
    x = L.fej
    # A kulcsot csak akkor vizsgáljuk meg, ha van aktuális elem.
    while x is not None and x.kulcs != k:
        x = x.kov
    return x   # A megtalált elemre mutató hivatkozás vagy None.
```

Egy elem kulcsát csak akkor érhetjük el, ha valóban van aktuális elem. Összetett feltételnél az `and` bal oldala értékelődik ki először. Ha ez hamis, a jobb oldal már nem kerül sorra. A feltételek sorrendjét ennek megfelelően válaszd meg.

A függvény visszatérési értékét a `talalat` változóban tároljuk. A kapott hivatkozáson keresztül csak sikeres keresés esetén érjük el az elem mezőit.

```
talalat = keres(L, 356)
if talalat is not None:
    print("Megtalált kulcs:", talalat.kulcs)

```
```
Megtalált kulcs: 356
```

A keresés működését több esettel is ellenőrizzük. Az `assert` a megadott feltételt vizsgálja. Hamis feltételnél hibát jelez, és az adott cella futása megáll. Igaz feltételnél a következő utasítással folytatódik a végrehajtás.

Az `is` operátorral azt is ellenőrizzük, hogy a visszaadott hivatkozás az eredeti `a` vagy `c` objektumot jelöli-e. A hiányzó kulcsot és az üres listát is kipróbáljuk.

```
assert keres(L, 423) is a
assert keres(L, 764) is c
assert keres(L, 999) is None
assert keres(LancoltLista(), 423) is None
print("Mind a négy keresési ellenőrzés sikeres.")
```

## 5. A műveletek időigénye

A bejárás és a keresés ugyanazokat a kapcsolatokat követi, de nem feltétlenül jut el ugyanannyi elemhez. Az időigénnyel azt jellemezzük, hogyan változik a szükséges lépések száma a lista elemszámának növekedésével. Az elemszámot `n` jelöli.
[[Görög betűk jelentései]] - Θ

| Művelet                                                       | Időigény | Indok                                                  |
| :------------------------------------------------------------ | :------- | :----------------------------------------------------- |
| Egy továbblépés egy meglévő elem `kov` hivatkozásán keresztül | Θ(1)     | A következő elem közvetlenül elérhető a mezőből.       |
| A teljes lista bejárása és kiírása                            | Θ(n)     | Minden elemet feldolgozunk.                            |
| Az elemszám meghatározása bejárással                          | Θ(n)     | Minden elemet egyszer számolunk meg.                   |
| Keresés kulcs alapján, legrosszabb esetben                    | Θ(n)     | Előfordulhat, hogy minden elemet meg kell vizsgálnunk. |

A **konstans**, Θ(1) időigény azt jelenti, hogy a lépések száma nem függ a lista hosszától. A **lineáris**, Θ(n) időigénynél a lépések száma az elemszámmal arányosan nő. A hivatkozások kezelését és egy kulcs összehasonlítását elemi műveletnek tekintjük.

A `423 → 356 → 764` listában a `423` keresésekor már az első elemnél megállunk. Ez a keresés legjobb esete, amelynek időigénye Θ(1). A `764` és a hiányzó `999` keresésekor mindhárom elemet megvizsgáljuk. A teljes bejárás és az elemszámlálás ezzel szemben minden esetben végighalad a listán.

## 6. Gyakorlás - Lista építése és keresés

Hozz létre egy új `G` listát négy új `ListaElem` objektumból. A kulcsok sorrendje `423 → 356 → 764 → 123` legyen. Az `elo` és a `kov` mezőket közvetlen értékadásokkal állítsd be, majd a fejet az első elemre állítsd. Minden szomszédos elempárt mindkét irányban kapcsolj össze.

Írd ki a listát a `kiir` függvénnyel, majd írd ki az elemszámát az `elemszam` függvénnyel. Keresd meg a `356` kulcsú elemet, és a kapott hivatkozáson keresztül írd ki az előző, majd a következő szomszédjának kulcsát. Végül írd ki a hiányzó `999` keresésének eredményét.

A kiírás, az elemszámlálás és a keresés után is ugyanaz a négy elem alkossa a listát, változatlan kapcsolatokkal.

**Elvárt kimenet:**

```
fej -> 423 -> 356 -> 764 -> 123 -> None
4
423 764
None
```

```
G = LancoltLista()
elso = ListaElem(423)
masodik = ListaElem(356)
harmadik = ListaElem(764)
negyedik = ListaElem(123)

#Minden szomszédos elempárhoz két külön hivatkozás tartozik.
elso.kov = masodik
masodik.elo = elso
masodik.kov = harmadik
harmadik.elo = masodik
harmadik.kov = negyedik
negyedik.elo = harmadik
G.fej = elso

kiir(G)
print(elemszam(G))
talalat = keres(G, 356)
if talalat is not None:
    print(talalat.elo.kulcs, talalat.kov.kulcs)
print(keres(G, 999))

#A lekérdezések a lista kapcsolatait nem változtatták meg.
assert G.fej is elso and elso.elo is None
assert elso.kov is masodik and masodik.elo is elso
assert masodik.kov is harmadik and harmadik.elo is masodik
assert harmadik.kov is negyedik and negyedik.elo is harmadik
assert negyedik.kov is None

```
