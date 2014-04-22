Správa užívateľov zahrňuje nasledovné činnosti:

* vytvorenie nového užívateľa (metóda POST)
* zmazanie užívateľa (metóda DELETE)
* prehľad uživateľov (metóda GET)
* zmena profilu užívateľa (PATCH - updateProfile)
* zmena hesla (PATH changePassword)

Každý užívateľ v systéme musí mať pridelenú rolu, od ktorej sa odvíjajú jeho práva na
prístup a manipuláciu s údajmi. Užívateľ sa do systému prihlasuje uživateľským meno a
heslom alebo emailovou adresou a heslom.

Typy užívateľov (role):

* administrátor
* kuriér
* dispečér

***Administrátor*** je rola s neobmedzenými právami. V rámci spoločnosti odporúčame pre vyššiu bezpečnosť mať čo najnižší počet
administrátorov.
Administrátor typicky vykonáva tieto činnosti:

* vytvára a spravuje uživateľov


***Dispečerom*** sa rozumie osoba, ktorá ma na starosti priraďovanie zásielok jednotlivým kuriérom.
Dispečer typicky vykonáva tieto činnosti:

* vytváranie zásielok
* priraďovanie zásielok kuriérom


***Kuriérom*** sa rozumie osoba, ktorá má na starosti prevzatie a následné doručenie zásielky.
Kuriér typicky vykonáva tieto činnosti:

* príjíma zásielky priradené dispečerom
* označuje zásielky ako doručené

Všetky činnosti patriace pod správu užívateĺov sídlia na ***baseUrl*** /users.
Popis vstupno/výstupných parametrov, ukážok volaní s možnosťou
vyskúšať volanie API sa nachádza na adrese:
[https://mapilary.com/api-docs](https://mapilary.com/api-docs/#!/users)


Ďalej budú popísané len špeciálne prípady, ktoré môžu pomôcť pri samotnej implementácií API

### Vytvorenie užívateľa

V rámci jedného volania API je možné vytvoriť naraz jedného alebo viacerých užívateľov.
Vytvorenie užívateľa prebieha zaslaním HTTP requestu typu POST

**Vstupné parametre:**
Request headers:
URL: /users
Method: POST
Content-type: application/json

username - užívateľské meno (povinné)
password - heslo (povinné)
company  - spoločnosť (nepovinné) *
roles    - užívateľské roly ['admin', 'courier', 'dispatcher'] (povinné) **
deviceTokens - tokeny na prijímanie push notifikácii do mobilného zariadenia (nepovinné)
vehicleType - typ vozidla ['bicycle', 'motorbike', 'van', 'car'] (nepovinné)
titleBefore - titul pre menom (nepovinné)
name - meno užívateľa (nepovinné)
surname - priezvisko užívateľa (nepovinné)
age - vek (nepovinné)
phoneNr - telefónne číslo (nepovinné)
email - email (nepovinné) ***

```json
{
    "username": "johndoe",
    "password": "strong",
    "company": "mapilary",
    "roles": ["courier"],
    "deviceTokens": ["token"],
    "vehicleType": "car",
    "profile": {
        "titleBefore": "Ing.",
        "name": "John",
        "surname": "John",
        "age": 48,
        "phoneNr": "+421890345830",
        "email": "johndoe@company.com"
    }
}
```
#### Poznámky
\*  názov spoločnosti sa dedí typicky od administrátora systému, ktorý nového užívateľa vytvára
** užívateľ môže mať pridelených viacero rolí
*** ak je vyplnená emailová adresa, užívateľ má možnosť ju použiť pri prihlasovaní do systému

Metóda obsahuje aj voliteľný parameter upsert (je súčasťou URL): /users?upsert=true

Parameter upsert=true zabezpečí v prípade, že uživateľ už systéme existuje,
 aktualizáciu jeho údajov. Bez použitia upsert, by API vrátilo chybu:

```json
{
  "message": "E11000 duplicate key error index: mapilary.users.$username_1  dup key: { : \"johndoe\" }"
}
```
