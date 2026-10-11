![[Greek-alphabet-189968408.png|580]]

A matematikában és az informatikában a görög betűk konvenció szerinti változókat, operátorokat, paramétereket és aszimptotikus korlátokat jelölnek. Mivel a latin ábécé betűi gyorsan elfogynak az egyenletekben, a görög betűk segítenek azonnal felismerhetővé tenni egy-egy matematikai entitás szerepét.

|**Betű**|**Név**|**Tipikus matematikai jelentés**|**Informatikai / gyakorlati példa**|
|---|---|---|---|
|$\alpha, \beta$|Alfa, Béta|Szögek a geometriában; valószínűségi együtthatók; I. és II. fajú hiba a statisztikában.|**A/B tesztelés** és statisztikai szignifikancia, szoftvertesztelési fázisok (Alpha/Beta release).|
|$\delta, \Delta$|Delta|$\Delta$: Változás, különbség.<br><br>  <br>  <br><br>$\delta$: Végtelenül kicsi változó, Kronecker-delta ($\delta_{ij} = 1$, ha $i=j$).|**Verziókövetés / Git diff:** A fájlok közötti módosulás tárolása (delta-encoding).|
|$\epsilon, \varepsilon$|Epszilón|Tetszőlegesen kicsi pozitív szám a határértékszámításban ($\epsilon$-$\delta$ definíció).|**Gépi epszilon (`eps`):** A legkisebb lebegőpontos számérték, amellyel növelve az 1-et, a gép még észleli a különbséget (pl. `1.0 + eps != 1.0`).|
|$\theta, \Theta$|Théta|Ismeretlen szög; modellparaméterek összessége; aszimptotikus pontos korlát.|**Gépi tanulás:** Neurális hálók súlyai és eltolásai ($\theta$), vagy algoritmusok átlagos bonyolultsága: $T(n) = \Theta(n \log n)$.|
|$\lambda$|Lambda|Sajátérték a lineáris algebrában; Poisson-eloszlás várható eseményszáma.|**Funkcionális programozás:** Névtelen (anonim) függvények (`lambda x: x * 2` Pythonban).|
|$\mu$|Mű|Várható érték, átlag a valószínűségszámításban és statisztikában.|**Képtömörítés / normalizálás:** Egy adathalmaz elemeinek átlagolása a bemenet z-skála transzformációjához: $z = \frac{x - \mu}{\sigma}$.|
|$\pi, \Pi$|Pí|$\pi$: Kör kerületének és átmérőjének aránya ($3,14159\dots$).<br><br>  <br>  <br><br>$\Pi$: Szorzás operátor.|**Algoritmusok:** A sorozatok szorzása $\prod_{i=1}^n x_i$, vagy a kör alapú grafikai raszterizálás és szögszámítás.|
|$\sigma, \Sigma$|Szigma|$\sigma$: Szórás; szigmoid aktivációs függvény.<br><br>  <br>  <br><br>$\Sigma$: Összegzés operátor; formális nyelvek ábécéje.|**For-ciklus / adatösszegzés:** $\sum_{i=1}^{n} a_i$ kódolása `sum()` függvénnyel; logisztikus regresszió aktiválási függvénye $\sigma(z) = \frac{1}{1 + e^{-z}}$.|
|$\phi, \Phi$|Fí|Aranymetszés arányszáma ($\phi \approx 1,618$); eloszlásfüggvény; Euler-féle fí-függvény.|**Kriptográfia:** Az RSA-titkosításban az Euler-féle $\phi(n)$ függvény segítségével számolják a privát kulcsot.|
|$\omega, \Omega$|Ómega|$\Omega$: Aszimptotikus alsó korlát; eseménytér a valószínűségszámításban.<br><br>  <br>  <br><br>$\omega$: Szögsebesség.|**Algoritmuselmélet:** A futási idő elméleti minimumának jelölése, pl. az összehasonlító rendezések alsó korlátja $\Omega(n \log n)$.|

### Gyakorlati összefüggés: A gradiens süllyedés algoritmusa

A gépi tanulásban használt gradiens süllyedés (Gradient Descent) képletében egyszerre több görög betű kap konkrét szerepet:

  

$$\theta_{t+1} = \theta_t - \eta \cdot \nabla J(\theta_t)$$

- $\theta$ (théta): A modell tanítandó paraméterei (súlyok).
 
- $\eta$ (éta): A tanulási ráta (learning rate), amely meghatározza a lépésköz nagyságát.

- $\nabla$ (nabla – görög betűkből származó szimbólum): A veszteségfüggvény többváltozós gradiense (meredeksége).

Az aszimptotikus jelölések ($O$, $\Omega$, $\Theta$) egy algoritmus futási idejének vagy memóriaigényének elméleti növekedési ütemét írják le a bemeneti méret ($n$) függvényében, elhanyagolva a hardverfüggő konstans szorzókat és az alacsonyabb rendű tagokat.

### A három jelölés lényege

|**Jelölés**|**Név**|**Jelentés**|**Hétköznapi analógia**|
|---|---|---|---|
|**$O(g(n))$**|Nagy O|**Aszimptotikus felső korlát:** A futásidő legfeljebb olyan gyorsan nő, mint $g(n)$.|_"Legfeljebb 5 ezer forintba fog kerülni."_|
|**$\Omega(g(n))$**|Nagy Ómega|**Aszimptotikus alsó korlát:** A futásidő legalább olyan gyorsan nő, mint $g(n)$.|_"Legalább 2 óráig tart a munka."_|
|**$\Theta(g(n))$**|Nagy Théta|**Szoros (pontos) korlát:** A futásidő pontosan $g(n)$ ütemében nő, mert egyszerre $O(g(n))$ és $\Omega(g(n))$.|_"Pontosan a megbeszélt ársávban maradunk."_|

### A leggyakoribb tévhit

Sokan összemossák a matematikai korlátokat az algoritmus futási eseteivel:

- **Hiba azt hinni**, hogy $O$ = legrosszabb eset (Worst Case), $\Omega$ = legjobb eset (Best Case), $\Theta$ = átlagos eset (Average Case).
    
- A valóságban a legrosszabb, legjobb és átlagos eset az **adatok elrendezésére** (bemeneti forgatókönyvekre) vonatkozik, míg az $O, \Omega, \Theta$ tisztán **matematikai korlátok**, amelyek bármelyik esetre külön-külön is alkalmazhatók.
    

### Kódpéldák és értelmezésük

#### 1. Lineáris keresés: amikor nincs globális $\Theta$

Python

```
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1
```

- **Legjobb eset (Best Case):** A keresett elem a 0. indexen van.
    
    - Pontosan 1 összehasonlítás: $\Theta(1)$ (felső korlátja $O(1)$, alsó korlátja $\Omega(1)$).
        
- **Legrosszabb eset (Worst Case):** Az elem nincs a listában, vagy az utolsó pozíción van.
    
    - Pontosan $n$ összehasonlítás: $\Theta(n)$ (felső korlátja $O(n)$, alsó korlátja $\Omega(n)$).
        
- **A teljes algoritmus általános viselkedése (bármely bemenetre):**
    
    - **$O(n)$**: A függvény soha nem igényel többet egy $c \cdot n$ lépésszámnál.
        
    - **$\Omega(1)$**: Az algoritmus nem tud 0 lépésben lefutni; legalább 1 összehasonlítás mindenképp lefut.
        
    - **$\Theta$-korlát nem létezik a teljes algoritmusra**, mert az alsó korlát ($\Omega(1)$) és a felső korlát ($O(n)$) nem egyezik meg.
        

#### 2. Maximumkeresés: amikor az algoritmus mindig $\Theta(n)$

Python

```
def find_maximum(arr):
    max_val = arr[0]
    for val in arr[1:]:
        if val > max_val:
            max_val = val
    return max_val
```

- Függetlenül attól, hogy a tömb növekvően, csökkenően vagy véletlenszerűen rendezett, a ciklusnak **mindenképp meg kell vizsgálnia mind az $n-1$ további elemet**.
    
- **Felső korlát:** $O(n)$ — nem végez több mint $n$ lépést.
    
- **Alsó korlát:** $\Omega(n)$ — nem úszhatja meg $n$-nél kevesebb összehasonlítással.
    
- Mivel az alsó és felső korlát megegyezik: **futásideje minden esetben $\Theta(n)$**.
    

#### 3. Beágyazott ciklus (Négyzetes mátrix bejárása): $\Theta(n^2)$

Python

```
def sum_matrix(matrix, n):
    total = 0
    for i in range(n):
        for j in range(n):
            total += matrix[i][j]
    return total
```

- A belső művelet pontosan $n \times n = n^2$ alkalommal hajtódik végre.
    
- **$\Omega(n^2)$**: Legalább $n^2$ műveletet el kell végeznie.
    
- **$O(n^2)$**: Legfeljebb $n^2$ műveletet végez.
    
- **$\Theta(n^2)$**: A futási idő növekedése szigorúan kvadratikus.
    
- _(Megjegyzés: Matematikailag az is igaz, hogy az algoritmus $O(n^3)$ vagy $O(2^n)$, hiszen nem fut lassabban ezeknél sem, de a $\Theta(n^2)$ adja meg az egyetlen pontos, feszes becslést.)_
    

### Matematikai definíció

Ha $f(n)$ jelöli a lépésszámot és $g(n)$ a viszonyítási függvényt pozitív $n$-ekre egy $n_0$ küszöbérték felett:

$$O(g(n)) \iff \exists\, c > 0, n_0 : f(n) \le c \cdot g(n)$$

$$\Omega(g(n)) \iff \exists\, c > 0, n_0 : f(n) \ge c \cdot g(n)$$

$$\Theta(g(n)) \iff \exists\, c_1, c_2 > 0, n_0 : c_1 \cdot g(n) \le f(n) \le c_2 \cdot g(n)$$