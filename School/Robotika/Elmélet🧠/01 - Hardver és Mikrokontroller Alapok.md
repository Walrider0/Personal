## Az Arduino platform

- **Definíció:** Nyílt forráskódú (open-source) fizikai számítási platform interaktív projektekhez.
    
- **Kezdetek:** Eredetileg oktatási segédeszközként fejlesztették ki; az első kártyát 2005-ben adták ki.
    
- **Szoftveres gyökér:** Az Arduino IDE a művészek számára megalkotott _Processing_ nyelven alapul.
    

## [[ARM]]-alapú kártyák

A 8 bites chipek mellett megjelentek az alacsony árú, 32 bites ARM architektúrájú mikrokontrollerek is (pl. Arduino Zero, Nano 33 BLE / IoT, MKR sorozat).

- **Processzor magok:** Cortex-M0, Cortex-M0+, Cortex-M4.
    
- **Üzemi feszültség:** 3.3V (szemben a hagyományos kártyák 5V-os szintjével).
    
- **Kimeneti áramkorlát:** Lényegesen kisebb áramot tudnak leadni a kivezetéseken; például a SAMD21 mikrokontroller kivezetésenként legfeljebb 7 mA leadására képes.
    
- **Alkalmazási terület:** Vezeték nélküli hálózatok és összetett matematikai számítások.
    

## Arduino Uno R3 hardverfelépítés

- **Mikrokontroller:** Atmel ATmega328 (8 bites MCU).
    
- **Fő belső egységek:** CPU, memória (Flash, SRAM, EEPROM), valamint perifériális be-/kimeneti (I/O) csatornák.
    
- **Órajel:** Kvarckristály oszcillátor 16 MHz frekvencián ketyeg (másodpercenként 16 millió tick; ciklusonként 1 művelet végrehajtása).
    
- **Tápellátás:**
    
    - Számítógép USB portjáról, fali adapterről vagy külső tápegységről.
        
    - DC tápcsatlakozón (barrel jack) keresztül 7–12V közötti bemeneti feszültséget fogad.
        
    - A beépített feszültségszabályzó (voltage regulator) ezt stabil 5V-ra állítja be.
        
- **Beépített visszajelzők:**
    
    - `ON` LED: Tápfeszültség meglétét jelzi.
        
    - `L` LED: A 13-as digitális kivezetésre kötött beépített LED.
        
    - `TX` / `RX` LED-ek: Adatátvitelkor (soros kommunikáció) villognak bájt küldése vagy fogadása esetén.
        
    - `Reset` gomb: Újraindítja a kártyát.
        
- **I/O Kivezetések:**
    
    - Digitális kivezetések: Kétállapotú jelek fogadására/küldésére (HIGH = 5V, LOW = 0V); maximum 40 mA áramot biztosítanak 5V mellett.
        
    - Analóg bemenetek (A0–A5): 0 és 1023 közötti digitális számmá alakítják a feszültséget.
        

## Kapcsolódó témák

- [[02 - Fejlesztőkörnyezet és Programozási Alapok]]
    
- [[03 - Elektronikai Alapismeretek és Méréstechnika]]
