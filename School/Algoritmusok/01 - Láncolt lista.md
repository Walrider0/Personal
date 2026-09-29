A **láncolt lista** (linked list) egy alapvető adatszerkezet a számítástechnikában, amely adatok tárolására és szervezésére szolgál.

## Alapvető felépítés

A láncolt lista **csomópontokból** (nodes) áll, ahol minden csomópont:

- **Adatot** tartalmaz
- **Mutatót** (pointer/referencia) a következő csomópontra

## Típusai

1. **Egyirányú láncolt lista (Singly Linked List)**
    
    - Minden csomópont csak az utána következő csomópontra mutat
    - Csak egy irányban járhatjuk be
2. **Kétirányú láncolt lista (Doubly Linked List)**
    
    - Minden csomópont az előtte és utána következő csomópontra mutat
    - Mindkét irányban járhatjuk be
3. **Körkörös láncolt lista (Circular Linked List)**
    
    - Az utolsó csomópont az első csomópontra mutat

## Előnyök

- ✅ Dinamikus méret (rugalmas)
- ✅ Hatékony beszúrás/törlés (ha ismerjük a helyet)
- ✅ Nincs szükség előre meghatározott méret foglalásra

## Hátrányok

- ❌ Lassabb keresés (nem lehet direkt indexelni)
- ❌ Extra memória szükséges mutatók tárolásához
- ❌ Lineáris hozzáférési idő

## Egyszerű példa (Python-ban)

```python
class Csomopont:
    def __init__(self, adat):
        self.adat = adat
        self.kovetkezo = None

# Láncolt lista létrehozása
csomopont1 = Csomopont(10)
csomopont2 = Csomopont(20)
csomopont3 = Csomopont(30)

# Összekötés
csomopont1.kovetkezo = csomopont2
csomopont2.kovetkezo = csomopont3
```

Szoktatva használják például: **sorokban (queues)**, **veremben (stacks)**, vagy olyan helyzetekben, ahol a méret gyakran változik.

==Órai példa :==

`class ListaElem:`  
    `def __init__(self, ertek):`  
        `self.ertek = ertek`  
        `self.kov = None`  
  
    `def __str__(self) -> str:`  
        `return f"{self.ertek}"`  
  
`Fej = ListaElem("elso")`  
  
`Fej.kov = ListaElem("masodik")`  
`Fej.kov.kov = ListaElem("harmadik")`  
  
`print(Fej.ertek)`  
`print(Fej.kov.ertek)`  
`print(Fej.kov.kov.ertek)`  
`print(Fej.kov.kov.kov)`  
  
  
  
`def kiir(Fej):`  
    `x = Fej`  
    `while x is not None:`  
        `print(x.ertek)`  
        `x = x.kov`  
  
`def kereses(Fej, kereset_ertek):`  
    `x = Fej`  
    `while x is not None and x.ertek != kereset_ertek:`  
        `x = x.kov`  
    `return x`  
  
`kiir(Fej)`  
  
`print("Keresés eredménye:")`  
`print(kereses(Fej, "masodik"))`
