## Alapfogalmak

Az elektromosság az elektronok áramlása egy anyagon keresztül, zárt áramkörben.

|**Jellemző**|**Leírás**|**Mértékegység**|**Jele**|
|---|---|---|---|
|**Feszültség (Voltage, $V$)**|Elektromotoros erő; potenciálkülönbség két pont között|Volt|V|
|**Áramerősség (Current, $I$)**|Másodpercenként átáramló elektromos töltésmennyiség|Amper|A|
|**Ellenállás (Resistance, $R$)**|Az anyag áramlással szembeni korlátozó mértéke|Ohm|Ω|

### Víz-analógia

- **Telep / Táp:** Vízpumpa, amely nyomáskülönbséget (feszültséget) állít elő.
    
- **Áram:** A csőben áramló víz mennyisége.
    
- **Ellenállás:** Csőszűkület, amely gátolja a szabad áramlást.
    
- **Fogyasztó (pl. izzó):** Vízturbina, amely munkát végez.
    

## Feszültségesés és Ohm törvénye

- **Áramlás iránya:** A magasabb potenciálú pont felől az alacsonyabb felé halad; a 0V-os referenciaszint a föld (**GND**).
    
- **Feszültségesés:** Az a feszültségmennyiség, amelyet az adott alkatrész felemészt. Az áramkör alkatrészei a teljes rendelkezésre álló tápfeszültséget elfogyasztják (a GND-re érve 0V marad).
    
- **Ohm törvénye:**
    

$$V = I \cdot R \qquad I = \frac{V}{R} \qquad R = \frac{V}{I}$$

## Ellenállások színkódjai

Furatszerelt alkatrészeknél 4 vagy 5 színes sáv jelzi az értéket és pontosságot:

- Az első 2 (vagy 3) sáv az értékes jegyeket jelöli.
    
- Az utolsó előtti sáv a szorzó ($10^n$).
    
- Az utolsó, hézaggal elválasztott sáv a tűrés (tolerancia):
    
    - **Arany:** $\pm 5\%$
        
    - **Ezüst:** $\pm 10\%$
        
    - **Sáv nélkül:** $\pm 20\%$
        

## Próbapanel (Breadboard)

- Forrasztásmentes áramkörépítésre szolgál.
    
- **Tápvonalak (Power rails):** A széleken futó, függőlegesen összekötött sávok, `+` (piros) és `-` (kék/fekete) jelöléssel.
    
- **Középső árok (Ravine):** Elválasztja a két oldali sorokat, megszakítva az elektromos kapcsolatot. Ideális a DIP (Dual In-line Package) tokozású IC-k elhelyezésére.
    ![[breadboard-1327459505.jpg|478]]

## Mérés multiméterrel

A multiméter hibakeresésre és áramköri paraméterek ellenőrzésére szolgál:

- **Csatlakozóhüvelyek:**
    
    - `COM`: Fekete mérőzsinór helye (mindig ide csatlakozik).
        
    - `mAVΩ`: Piros mérőzsinór helye a legtöbb méréshez (feszültség, ellenállás, kis áramok).
        
    - `10A`: Piros mérőzsinór helye kizárólag nagy áramerősség mérésénél.
        
- **Folytonossági teszt (Continuity):** Dióda/hangszóró szimbólum; sípol, ha a két pont között fémes összeköttetés van (zárt hurok vizsgálata).
    
- **Feszültségmérés:** Párhuzamosan kell az alkatrészre érinteni a mérőcsúcsokat. Ha a kijelző negatív értéket mutat, a mérőzsinórok fel vannak cserélve. Ha 1-est mutat a szélén, a méréshatár túl kicsire van állítva.
    
- **Ellenállásmérés:** Csak feszültségmentesített áramkörben mérhető; a szondákat az alkatrész két lábához érintve a polaritás mindegy.
    

## Kapcsolódó témák

- [[04 - Alapvető Komponensek (LED, Nyomógomb, Dőléskapcsoló)]]
    
- [[06 - Potenciométer és Feszültségosztó]]
    

### `04 - Alapvető Komponensek (LED, Nyomógomb, Dőléskapcsoló).md`

tags:

- components
    
- led
    
- button
    
- sensors