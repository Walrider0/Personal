# CISC (Complex Instruction Set Computer)

## A lényeg:

A **CISC** azt jelenti, hogy a processzor **sok és összetett utasítást** tartalmaz, amelyek egyenként sok mindent tudnak csinálni.

## Jellemzői:

### Utasítások:

- 1000+ különböző utasítás
- Összetett, sok műveletet végeznek el egy utasítással
- Különböző hosszúságúak

### Feldolgozás:

- Kevesebb utasítás szükséges egy feladat elvégzéséhez
- De minden utasítás feldolgozása **hosszabb és bonyolultabb**

## Valós példa:

```
Feladat: Memóriából szám beolvasása és összeadása

RISC módszer (ARM):
1. Betöltés → Érték beolvasása memóriából
2. Összeadás → Számok összeadása
3. Tárolás → Eredmény mentése

CISC módszer (x86):
1. MUL → EGYETLEN utasítás, amely végigmegy a memórián, 
        beolvassa az értékeket, összeadja és eltárolja őket
```

## Hol használják?

🖥️ **Desktop számítógépek** (PC-k)  
🖥️ **Laptopok**  
🖥️ **Szerverek**

Például:

- **Intel** - Core, Xeon (x86/x64)
- **AMD** - Ryzen, EPYC (x86/x64)

## CISC vs RISC összehasonlítása:

||RISC|CISC|
|---|---|---|
|Utasítások száma|~50-100|~1000+|
|Sebesség per utasítás|⚡ Gyors|🐢 Lassú|
|Energiafogyasztás|💚 Alacsony|🔋 Magas|
|Költség|💰 Olcsó|💸 Drága|
|Fő terület|Mobil, IoT|PC, szerver|

## Miért drágább és energiaigényes?

- Sokkal több tranzisztor szükséges az utasítások tárolásához
- A feldolgozás komplexebb, több energia kell
- Jól működik az asztali számítógépekben, ahol nem kritikus az akkufogyasztás

**Röviden:** A CISC a hagyományos PC-k szívverése, de nem energiahatékony – ezért nem használják mobil eszközökben. 🖥️