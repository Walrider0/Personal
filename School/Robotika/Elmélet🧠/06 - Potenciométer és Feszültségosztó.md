## A feszültségosztó elve

Két sorba kapcsolt ellenálláson ($R_1, R_2$) azonos áram folyik át, a tápfeszültség ($V_{in}$) pedig az ellenállások arányában oszlik meg rajtuk (Kirchhoff-huroktörvény: $V_{in} = V_{R1} + V_{R2}$). A kimeneti feszültség az alsó ellenálláson mérve:

$$V_{out} = V_{in} \cdot \left( \frac{R_2}{R_1 + R_2} \right)$$

## A Potenciométer felépítése

- Háromkivezetéses változtatható ellenállás, amely állítható feszültségosztóként működik.
    
- Egy körív alakú rezisztív pályát és egy elforduló tengelyhez rögzített fém csúszkát (wiper) tartalmaz.
    
- **Kivezetések:**
    
    - Két szélső láb: Tápfeszültség ($V_{ref}$ / 5V) és Föld (0V / GND).
        
    - Középső láb (csúszka): Kimeneti analóg feszültség.
        
- **Alkalmazása:** Pozíciószenzorként a tengely elfordulási szögével arányos, lineáris analóg kimeneti feszültséget biztosít.
    

## Mintaprogram és Értékskálázás

Az analóg bemeneten kapott 10 bites értéket (0–1023) gyakran át kell méretezni egy másik tartományra (például 8 bites kimenethez: 0–255) a `map()` függvénnyel:

C++

```
const int potPin = A0;
int value = 0;
byte potValue = 0;

void setup() {
  Serial.begin(9600);
}

void loop() {
  value = analogRead(potPin);                     // 0 .. 1023
  potValue = map(value, 0, 1023, 0, 255);         // Lineáris skálázás 0 .. 255 közé
  
  Serial.print("Raw: ");
  Serial.print(value);
  Serial.print(" -> Mapped: ");
  Serial.println(potValue);
  delay(100);
}
```

### A `map()` függvény működése

A bemeneti $[a_1, a_2]$ tartománybeli $x$ értéket az alábbi összefüggéssel transzformálja a $[b_1, b_2]$ tartományba:

$$y = b_1 + \frac{(x - a_1) \cdot (b_2 - b_1)}{a_2 - a_1}$$

## Kapcsolódó témák

- [[03 - Elektronikai Alapismeretek és Méréstechnika]]
    
- [[05 - Analóg-Digitális Átalakítás (ADC)]]