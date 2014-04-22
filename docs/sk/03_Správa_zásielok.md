Správa zásielok zahrňuje nasledovné činnosti:

* vytvorenie zásielky
* zmazanie zásielky
* aktualizácia zásielky

API obsahuje aj ďalšie metódy, ktoré ale z pohľadu implementátora, nie je potrebné implemetovať.
Ide o metódy, ktoré sú využívané interne aplikáciami Mapilary Console, Mapilary Courier a Mapilary Dispatcher.
Tieto aplikácie sú súčasťou dodávaného riešenia.

Všetky činnosti patriace pod správu zásielok sídlia na ***baseUrl*** /deliveries.
Popis vstupno/výstupných parametrov, ukážok volaní s možnosťou
vyskúšať volanie API sa nachádza na adrese:
[https://mapilary.com/api-docs](https://mapilary.com/api-docs/#!/deliveries)


### Vytvorenie zásielky

V rámci jedného volania API je možné vytvoriť naraz jednu alebo viacero zásielok.
Vytvorenie zásielky prebieha zaslaním HTTP requestu typu POST

**Vstupné parametre:**
Request headers:
URL: /deliveries
Method: POST
Content-type: application/json

Request payload:
trackingNr - číslo zásielky pre sledovanie jej stavu a polohy (povinný)
startDate  - dátum doručenia zásielky (nepovinný) *
endDate    - najneskorší dátum doručenia (nepovinný) **
note       - poznámka (nepovinný)
priority   - priorita zásielky (0 - min, 10 - max) (nepovinný)
company    - vyplnené automaticky
duration   - trvanie doručenia - vypočítaný údaj na základe vzdialenosti miest doručenia (pickup) a odovzdania (drop) zásielky
state      - stav zásielky (pri vytváraní nastavený na Created) (nepovinný)
**addresses** - pole adries ***
validFrom - určuje čas od ktorého sa adresát na danej adrese nachádza (nepovinné)
validTo - určuje čas do ktorého sa adresát na danej adrese nachádza (nepovinné)
consignee - celé meno adresáta (nepovinné)
phoneNr - telefonický kontakt na adresáta (mobil, ...) (nepovinné)
email - emailová adresa adresáta (nepovinné)
city - mesto (nepovinné)
street - ulica (nepovinné)
housenumber - popisné číslo (nepovinné)
coords - súradnice (lat/lon) (nepovinné)

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

*** Pole adries typicky obsahuje minimálne dve adresy:

* miesto prijatia zásielky kuriérom - type pickup
* miesto odovzdania zásielky kuriérom (adresát) - type drop

