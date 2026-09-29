## 1. Fénykibocsátó Dióda (LED)

- **Polaritás:** A félvezető diódák csak egy irányban vezetik az áramot.
    
    - **Anód (+):** Hosszabb kivezetés.
        
    - **Katód (-):** Rövidebb kivezetés, a műanyag peremen lecsapott oldal jelzi.
        
- **Működési paraméterek:**
    
    - Nyitófeszültség (Forward voltage, $V_f$): Színtől függően 1.8V és 3.6V között.
        
    - Maximális áram: Általában maximum 20 mA.
        
- **Előtét-ellenállás számítása:** Ha az Arduino kimenete 5V, az áramot 15 mA-re korlátozzuk, a LED feszültségesése után maradó értékre alkalmazzuk Ohm törvényét: tipikusan **220 Ω vagy 330 Ω** szükséges.
    

## 2. Nyomógomb (Push Button)

- **Mechanikai felépítés:** 4 lábbal rendelkezik, a szemközti oldalak belső összeköttetésben állnak. Lenyomáskor a két oldal záródik.
    
- **Prelling (Bouncing):** Lenyomáskor és felengedéskor a mechanikus fémérintkezők néhány milliszekundumig rezegnek, bizonytalan ki-be kapcsolási jelet generálva.
    
- **Prellmentesítés (Debouncing):** 10–50 ms közötti szoftveres várakozással (`delay`) kivárjuk a jel stabilizálódását.
    

## 3. Lebegő bemenet és Felhúzó ellenállás

- **Lebegő láb (Floating pin):** Ha egy bemenetként beállított kivezetésre semmi sincs kötve, környezeti zajok miatt véletlenszerűen váltakozik HIGH és LOW állapot között.
    
- **Pull-up ellenállás célja:**
    
    1. Gombnyomáskor korlátozza a VCC-ből a föld felé folyó áramot.
        
    2. Nyitott gombnál határozott 5V (HIGH) szinten tartja a bemeneti lábat.
        
- **Méretezési szabály:** A bemeneti láb impedanciája ($R_2$) 100 kΩ és 100 MΩ között mozog. A felhúzó ellenállás ($R_1$) legfeljebb a bemeneti impedancia tizede legyen, hogy a feszültségosztás ne rontsa le a HIGH logikai szintet.
    
    - _Példa:_ 5V tápfeszültségnél 1 mA gombnyomási áramhoz:
        

$$R = \frac{V}{I} = \frac{5\text{ V}}{0.001\text{ A}} = 5000\ \Omega = 5\text{ k}\Omega$$

- **Belső felhúzó ellenállás:** Az ATmega328 tartalmaz egy belső, szoftveresen bekapcsolható 20 kΩ-os felhúzó ellenállást:
    
    C++
    
    ```
    pinMode(BUTTON_PIN, INPUT_PULLUP);
    ```
    
    (Megjegyzés: `INPUT_PULLUP` esetén a gomb nyitott állapota `HIGH`, megnyomott állapota `LOW` szintet ad.)
    
- **Lekérdezés:** `digitalRead(pin)` függvénnyel (`HIGH` vagy `LOW` értéket ad vissza).
    

## 4. Dőléskapcsoló (Tilt Switch - pl. SW-520D)

- Két érintkezőt és egy szabadon mozgó fémgolyót tartalmazó hengeres alkatrész.
    
- Függőleges helyzetben a golyó rövidre zárja a két kivezetést (zárt kapcsolóként működik).
    
- Megdöntve a golyó elgurul, a kapcsolat megszakad (nyitott kapcsoló).
    

## Kapcsolódó témák

- [[02 - Fejlesztőkörnyezet és Programozási Alapok]]
    
- [[03 - Elektronikai Alapismeretek és Méréstechnika]]
    
- [[05 - Analóg-Digitális Átalakítás (ADC)]]
    

### `05 - Analóg-Digitális Átalakítás (ADC).md`

tags:

- adc
    
- analog
    
- arduino