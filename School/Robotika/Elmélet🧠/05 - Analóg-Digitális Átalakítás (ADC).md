## Az ADC alapelve

A fizikai világ legtöbb jele folytonos (analóg) feszültség, míg a mikrokontroller csak diszkrét bináris számokkal dolgozik. Az Analóg-Digitális Átalakító (ADC) feladata a bejövő analóg feszültség mintavételezése és kvantálása.

### Fő jellemzők

- **Felbontás ($N$ bit):** Meghatározza, hány diszkrét szintre osztja a bemeneti feszültségtartományt ($2^N$ szint).
    
- **Feszültségtartomány:** $V_{ref-}$ és $V_{ref+}$ között.
    
- **Mintavételezési frekvencia ($f_s$):** Másodpercenkénti minták száma.
    
- **Pontosság ($n$ bit):** A konverzió precizitása.
    

### Matematikai konverzió

Az analóg $V_{in}(t)$ bemenet és a mintavételezett digitális $X[n]$ minta közötti kapcsolat:

$$X[n] = \left\lfloor 2^N \cdot \frac{V_{in}(t) - V_{ref-}}{V_{ref+} - V_{ref-}} \right\rfloor$$

_Példa (8 bites ADC, 0–5V tartomány, 3V bemenet):_

$$X = \left\lfloor 256 \cdot \frac{3 - 0}{5 - 0} \right\rfloor = \lfloor 153.6 \rfloor = 153$$

## ADC az Arduino Uno / Nano lapkákon

- **Csatornák száma:** 6 analóg bemeneti láb (A0–A5).
    
- **Felbontás:** 10 bites integrált ADC ($2^{10} = 1024$ szint: 0-tól 1023-ig).
    
- **Alapértelmezett méréstartomány:** 0V – 5V:
    
    - 0V $\rightarrow$ 0
        
    - 2V $\rightarrow$ 409
        
    - 3V $\rightarrow$ 614
        
    - 5V $\rightarrow$ 1023
        

### Referenciafeszültség (`AREF` kivezetés)

Ha a mérendő analóg jel csúcsértéke kisebb mint 5V (pl. legfeljebb 2V), a felbontás javítható külső referenciafeszültség alkalmazásával:

- A kívánt feszültséget (pl. 2V) az `AREF` kivezetésre kötjük.
    
- A kódban beállítjuk: `analogReference(EXTERNAL)`.
    
- Ekkor a 1024 lépés a 0V–2V intervallumra oszlik szét.
    
- Értékek: `DEFAULT` (0–5V tartomány) vagy `EXTERNAL` (AREF láb feszültsége).
    

## Beolvasás kódban

A beolvasást az `analogRead(pin)` függvény végzi:

C++

```
int sensorValue = analogRead(A0); // 0 és 1023 közötti értéket ad
```

## Kapcsolódó témák

- [[01 - Hardver és Mikrokontroller Alapok]]
    
- [[06 - Potenciométer és Feszültségosztó]]
    

### `06 - Potenciométer és Feszültségosztó.md`

tags:

- potentiometer
    
- voltage-divider
    
- sensors