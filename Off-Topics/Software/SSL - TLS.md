
Az **SSL** (Secure Sockets Layer) és a **TLS** (Transport Layer Security) olyan titkosítási protokollok, amelyek biztonságos, titkosított kapcsolatot hoznak létre két számítógép – leggyakrabban a webböngésződ és egy webszerver – között az interneten. Amikor egy weboldal címe előtt a kis lakat ikont vagy a `https://` előtagot látod, a háttérben ez a technológia dolgozik.

### Mi a különbség köztük?

A lényeg röviden: **a TLS az SSL modernebb, biztonságosabb utódja.**

  

|**Szempont**|**SSL (Secure Sockets Layer)**|**TLS (Transport Layer Security)**|
|---|---|---|
|**Fejlesztő**|Netscape (1995 körül)|IETF (szabványosító szervezet, 1999-től)|
|**Állapot**|Elavult, sérülékeny, hivatalosan visszavont (SSL 2.0, 3.0)|Aktív iparági szabvány (TLS 1.2 és TLS 1.3)|
|**Biztonság**|Ismert sebezhetőségek (pl. POODLE támadás)|Korszerű rejtjelezés, gyorsabb és jóval biztonságosabb|

> **Miért mond mégis mindenki SSL-t?**
> 
>   
> 
> Bár a modern web kizárólag TLS-t használ, a köznyelvben és a marketingben megmaradt az elnevezés: a webszolgáltatók még mindig „SSL tanúsítványként” értékesítik azt, ami valójában TLS kapcsolatot épít fel.
> 
>   

### Milyen feladatokat lát el?

1. **Titkosítás (Adatvédelem):** Az adatokat olvashatatlan kóddá alakítja. Ha valaki lehallgatja a hálózatot (például egy nyilvános kávézói Wi-Fi-n), nem látja a jelszavaidat, bankkártyaadataidat vagy a megnyitott oldalakat.
    
      
    
2. **Hitelesítés (Azonosítás):** Digitális tanúsítvány segítségével igazolja, hogy a böngésző valóban a felkeresni kívánt szerverhez kapcsolódik (pl. tényleg a bankodhoz, nem pedig egy adathalász másolathoz).
    
      
    
3. **Integritás (Adatvédelem módosítás ellen):** Garantálja, hogy az átküldött üzenet útközben nem sérült meg, és illetéktelenek nem írták át a tartalmát.
    
      
    

### Hogyan működik a folyamat? (A „Kézfogás”)

Mielőtt bármilyen weboldaladat átmenne a hálózaton, a böngésző és a szerver egy úgynevezett **TLS Handshake** (kézfogási folyamat) során egyeztet egymással:

  

1. **Client Hello:** A böngésző beköszön, és megadja, milyen titkosítási verziókat és algoritmusokat támogat.
    
      
    
2. **Server Hello & Tanúsítvány:** A szerver kiválasztja a protokollt, majd elküldi a digitális tanúsítványát.
    
      
    
3. **Ellenőrzés:** A böngésző meggyőződik arról, hogy a tanúsítványt megbízható hitelesítésszolgáltató (Certificate Authority) állította-e ki, és nem járt-e le.
    
      
    
4. **Közös kulcs létrehozása:** Aszimmetrikus rejtjelezés segítségével közösen kiszámolnak egy ideiglenes titkos kulcsot.
    
      
    
5. **Titkosított adatforgalom:** Innentől kezdve ezen a közös kulcson keresztül, gyors szimmetrikus titkosítással folyik az összes kommunikáció.