

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
