Správa uživatelů zahrnuje následovné činnosti:

* vytvoření nového uživatele (metoda POST)
* smazání uživatele (metoda DELETE)
* přehled uživatelů (metoda GET)
* změna profilu uživatele (PATCH - updateProfile)
* změna hesla (PATH changePassword)

Každý uživatel v systému musí mít přidělenou roli, od které se odvíjejí jeho práva na přístup a manipulaci s údaji. Uživatel se do systému přihlašuje uživatelským jména a heslem nebo emailovou adresou a heslem.

Typy uživatelů (role):

* administrátor
* kurýr
* dispečer

***Administrátor***

je role s neomezenými pravomocemi. V rámci společnosti doporučujeme pro vyšší bezpečnost mát co nejnižší počet administrátorů.

Administrátor typicky vykonává tyto činnosti:

* vytváří a spravuje uživatele

***Dispečer***

je osoba, která má na starosti přidělování zásilek jednotlivým kurýrům.

Dispečer typicky vykonává tyto činnosti:

* vytváření zásilek
* přidělování jednotlivých zásilek kurýrům

***Kurýr***

je osoba, která má na starosti převzetí a následné doručení zásilky.

Kurýr typicky vykonává tyto činnosti:

* přijímá zásilky přidělené dispečerem
* označuje zásilky jako doručené
* Všechny činnosti patřící pod správu uživatelů sídlí na baseUrl /users. Popis vstupních/výstupních parametrů. ukázek * * * volání s možností vyzkoušet volání API se nachází na adrese: https://mapilary.com/api-docs

Dále budou popsány jen speciální případy, které můžou pomoct při samotné implementaci API

### Vytvoření uživatele

V rámci jednotného volání API je možné vytvořit najednou jednoho nebo více uživatelů. Vytvoření uživatele probíhá zasláním HTTP requesu typu POST

**Vstupní paramentry:** Request headers: URL: /users Method: POST Content-type: application/json

username - uživatelské jméno (povinné) 

password - heslo (povinné) company - společnost (nepovinné) 

roles - uživatelské role ['admin', 'courier', 'dispatcher'] (povinné) 

deviceTokens - tokeny na přijímání push notigikací do mobilního zařízení (nepovinné) 

vehicleType - typ vozidla ['bicycle', 'motorbike', 'van', 'car'] (nepovinné) 

titleBefore - titul před jménem (nepovinné) 

name - křestní jméno (nepovinné) 

surname - příjmení (nepovinné) 

age - věk (nepovinné) 

phoneNr - telefonní číslo (nepovinné) 

email - email (nepovinné)

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


### Poznámky
\* název společnosti se dělí typicky na administrátora sytému, který nového uživatele vytváří 

* uživatel může mít přidělených více rolí 

*** když je vyplněná emailová adresa, uživatel má možnost jí použít při přihlašování do systému

Metoda obsahuje také volitelný parametr upsert (je součástí URL): /user?upser=true

Parametr upser=true zabezpečí v případě, že uživatel už v systému existuje, aktualizace jeho údajů. Bez použití upsert, by API vyrátilo chybu:

```json
{
  "message": "E11000 duplicate key error index: mapilary.users.$username_1  dup key: { : \"johndoe\" }"
}
```
