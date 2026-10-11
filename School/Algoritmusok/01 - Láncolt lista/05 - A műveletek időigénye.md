

A bejárás és a keresés ugyanazokat a kapcsolatokat követi, de nem feltétlenül jut el ugyanannyi elemhez. Az időigénnyel azt jellemezzük, hogyan változik a szükséges lépések száma a lista elemszámának növekedésével. Az elemszámot `n` jelöli.
[[Görög betűk jelentései]] - Θ

| Művelet                                                       | Időigény | Indok                                                  |
| :------------------------------------------------------------ | :------- | :----------------------------------------------------- |
| Egy továbblépés egy meglévő elem `kov` hivatkozásán keresztül | Θ(1)     | A következő elem közvetlenül elérhető a mezőből.       |
| A teljes lista bejárása és kiírása                            | Θ(n)     | Minden elemet feldolgozunk.                            |
| Az elemszám meghatározása bejárással                          | Θ(n)     | Minden elemet egyszer számolunk meg.                   |
| Keresés kulcs alapján, legrosszabb esetben                    | Θ(n)     | Előfordulhat, hogy minden elemet meg kell vizsgálnunk. |

A **konstans**, Θ(1) időigény azt jelenti, hogy a lépések száma nem függ a lista hosszától. A **lineáris**, Θ(n) időigénynél a lépések száma az elemszámmal arányosan nő. A hivatkozások kezelését és egy kulcs összehasonlítását elemi műveletnek tekintjük.

A `423 → 356 → 764` listában a `423` keresésekor már az első elemnél megállunk. Ez a keresés legjobb esete, amelynek időigénye Θ(1). A `764` és a hiányzó `999` keresésekor mindhárom elemet megvizsgáljuk. A teljes bejárás és az elemszámlálás ezzel szemben minden esetben végighalad a listán.

