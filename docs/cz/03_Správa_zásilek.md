Správa zásilek zahrnuje následující činnosti:

* vytvoření zásilky
* smazání zásilky
* aktualizace zásilky

API obsahuje také další metody, které ale z pohledu implementátora nejsou potřebné implementovat.
Jde o metody, které jsou využívané interně aplikacemi Mapilary Console, Mapilary Courier a Mapilary Dispatcher.
Tyto aplikace jsou součástí dodávaného řešení.


Všechny činnosti patřící pod správu zásilek sídlí na ***baseUrl*** /deliveries.

Popis vstupních/výstupních parametrů, ukázek volání s možností vyzkoušet si API volání se nachází na adrese:
[https://mapilary.com/api-docs](https://mapilary.com/api-docs/#!/deliveries)


### Vytvoření zásilky

V rámci jednoho volání API je možné vytvořit najednou jednu nebo více zásilek.
Vytvoření zásilky probíhá zasláním HTTP requestu typu POST

**Vstupní paramatry:**
Request headers:
URL: /deliveries
Method: POST
Content-type: application/json

Request payload:
trackingNr - číslo zásilky pro sledování jejího stavu a polohy (povinný)
startDate  - datum doručení zásilky (nepovinný) *
endDate    - nejzazší datum doručení (nepovinný) **
note       - poznámka (nepovinný)
priority   - priorita zásilky (0 - min, 10 - max) (nepovinný)
company    - vyplněné automaticky
duration   - trvání doručení - vypočítaný údaj na základě vzdálenosti do místa vyzvednutí (pickup) a doručení (drop) zásilky
state      - stav zásilky (při vytváření zásilky na Created) (nepovinný)
**addresses** - pole adres ***
validFrom - určuje čas od kterého se adresát na dané adrese nachází (nepovinné)
validTo - určuje čas do kterého se adresát na dané adrese nachází (nepovinné)
consignee - celé jméno adresáta (nepovinné)
phoneNr - telefonický kontakt na adresáta (mobil, ...) (nepovinné)
email - emailová adresa adresáta (nepovinné)
city - město (nepovinné)
street - ulica (nepovinné)
housenumber - číslo popisné (nepovinné)
coords - souřadnice (lat/lon) (nepovinné)

    {
        "trackingNr": "AZ90157",
        "startDate": "2012-09-09T08:00:00.000Z",
        "endDate": "2012-09-09T08:30:00.000Z",
        "duration": 30,
        "company": "mapilary",
        "note": "delivery from previous day",
        "priority": 2,
        "state": "Delayed",
        "addresses": [
            {
                "type": "pickup",
                "validFrom": "2013-06-27T19:36:18.371Z",
                "validTo": "2013-06-27T23:36:18.371Z",
                "consignee": "Barrett Leblanc",
                "phoneNr": "+1 (818) 416-2951",
                "email": "barrettleblanc@accidency.com",
                "city": "Harrodsburg",
                "street": "Bayview Avenue",
                "countryCode": "New Jersey",
                "coords": {
                    "latitude": 60.270045,
                    "longitude": -119.875044
                }
            },
            {
                "type": "drop",
                "validFrom": "2013-07-07T15:09:25.466Z",
                "validTo": "2013-07-08T04:09:25.466Z",
                "consignee": "Julia Woodard",
                "phoneNr": "+1 (980) 547-3940",
                "email": "juliawoodard@accidency.com",
                "city": "Bentley",
                "street": "Moffat Street",
                "housenumber": "13",
                "countryCode": "Georgia",
                "coords": {
                    "latitude": -66.730811,
                    "longitude": 52.468852
                }
            }
        ]
    }

### Poznámky

*** Pole adres typicky obsahuje minimálně dvě adresy:
* místo přijetí zásilky kurýrem - type pickup
* místo odevzdání zásilky kurýrem (adresát) - type drop


