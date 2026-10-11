

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

[[05 - A műveletek időigénye]]