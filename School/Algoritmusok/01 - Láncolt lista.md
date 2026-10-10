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