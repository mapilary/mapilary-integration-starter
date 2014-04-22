Dokumentácia ***Mapilary API*** pre implementáciu do existujúcich riešení.

Cieľovou skupinou tejto dokumentácie sú spoločnosti, ktoré plánujú implementovať Mapilary API,
do ich existujúcich systémov. Táto dokumentácia popisuje integračné minimum, ktoré je nutné k
 používaniu ďalších Mapilary aplikácií (Mapilary Courier, Mapilary Dispatcher).

## Dokumentácia zahŕňa

* Autentifikáciu
* Správu kuriérov
* Správu zásielok

Mapilary API pre všetky dopyty a odpoveď používa výhradne JSON formát.

Prístup k Mapilary API je limitovaný tzv. [Role-based_access_control](http://en.wikipedia.org/wiki/Role-based_access_control).
V systéme existujú roli:

* administrátor
* dispatcher
* kuriér

Každá z rolí ma predefinovaný sadu činností, ktoré má oprávnenie vykonávať. Viac informácií o oprávneniach je možné nájsť pri konkrétnom type činnosti.