

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

[[03 - Bejárat]]