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
