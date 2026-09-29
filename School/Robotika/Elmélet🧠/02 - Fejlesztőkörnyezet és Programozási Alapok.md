## Az Arduino IDE

- **Vázlatok (Sketches):** Az Arduino alá írt programok neve vázlat, kiterjesztésük: `.ino`.
    
- **Vázlatfüzet (Sketchbook):** A kódok tárolására kijelölt alapértelmezett mappa, amely a _File > Sketchbook_ menüből érhető el, elérési útja pedig a _Preferences_ ablakban módosítható.
    
- **Fő gombsor:**
    
    - _Verify:_ Kód ellenőrzése / szintaktikai fordítása.
        
    - _Upload:_ Kód lefordítása és feltöltése a mikrokontrollerre.
        
    - _New, Open, Save:_ Fájlkezelés.
        
    - _Serial Monitor:_ Soros monitor megnyitása a kommunikáció teszteléséhez.
        

## Beállítás és Feltöltés

Feltöltés előtt a _Tools_ menüben be kell állítani:

1. **Board:** A csatlakoztatott kártya típusa (pl. "Arduino Uno").
    
2. **Port:** A soros kommunikációs port (pl. "COM3 (Arduino Uno)").
    

### A kód útja a mikrokontrollerbe

1. A számítógépen az IDE fordítóprogramja (Compiler) bináris gépi kóddá alakítja a C/C++ vázlatot.
    
2. Feltöltés indításakor a kártya automatikusan újraindul.
    
3. Bekapcsol a **Bootloader**: a mikrokontroller Flash memóriájában lévő kis szoftver, amely reset után néhány másodpercig aktív, megvillogtatja a 13-as kivezetés LED-jét, és külső programozó hardver nélkül fogadja a soros vonalon érkező gépi kódot.
    
4. A program beíródik a mikrokontroller Flash programmemóriájába, és a CPU megkezdi a futtatást a portok felé.
    

## Alapvető kódszerkezet

Minden vázlatnak tartalmaznia kell két kötelező, visszatérési érték nélküli (`void`) függvényt:

C++

```
void setup() {
  // Csak egyszer fut le a kártya indulásakor vagy újraindulásakor.
  // Ide kerülnek az inicializálások: lábak iránya, soros port indítása.
}

void loop() {
  // A setup() lefutása után folyamatosan, végtelen ciklusban ismétlődik.
  // Ide kerül a működési logika.
}
```

## Alapvető I/O függvények

- `pinMode(pin, mode)`: Beállítja a kivezetés irányát. A paraméter értéke `INPUT` vagy `OUTPUT` lehet.
    
- `digitalWrite(pin, value)`: Kimenetként konfigurált láb állapotát állítja be. Értéke `HIGH` (5V) vagy `LOW` (0V).
    
- `delay(ms)`: Blokkoló függvény; a megadott ezredmásodpercig (ms) teljesen felfüggeszti a mikrokontroller kódfuttatását.
    

C++

```
const unsigned int LED_PIN = 13;
const unsigned int PAUSE = 500;

void setup() {
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_PIN, HIGH);
  delay(PAUSE);
  digitalWrite(LED_PIN, LOW);
  delay(PAUSE);
}
```

## Kapcsolódó témák

- [[01 - Hardver és Mikrokontroller Alapok]]
    
- [[04 - Alapvető Komponensek (LED, Nyomógomb, Dőléskapcsoló)]]
    

### `03 - Elektronikai Alapismeretek és Méréstechnika.md`

tags:

- electronics
    
- basics
    
- measurement
    
- multimeter