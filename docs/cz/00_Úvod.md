Dokumentace ***Mapilary API*** pro implementaci do existujících řešení.


 Cílovou skupinou této dokumentace jsou společnosti, které plánují implementovat Mapilary API, do jejich existujících systémů. Tato dokumentace popisuje integrační minimum, které je nutné k používání dalších Mapilary aplikací (Mapilary Courier, Mapilary Dispatcher, Mapilary Widget)

## Dokumentace zahrnuje

* Autentifikace
* Správa kurýrů
* Správa zásilek

Mapilary API pro dotazy a odpovědi používá výhradně JSON formát.


Přístup k Mapilary API je limitovaný tzv. [Role-based_access_control](http://en.wikipedia.org/wiki/Role-based_access_control).

V systému existují role:

* administrátor
* dispečer
* kurýr

Každá z rolí má předefinovanou sadu činností, které má oprávnění vykonávat. Více informací o oprávněních je možné najít při konkrétním tytu činnosti.
