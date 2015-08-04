Mapilary API na overenie identity používa autentifikáciu, ktorá vychádza z protokolu [oauth2](http://tools.ietf.org/html/rfc6749) - client credentials.

Každé volanie API (request) musí obsahovať tzv. access_token (ďalej len token), ktorý je posielaný v http hlavičke.


### Získanie token-u:

Access token sa získa poslaním POST requestu na url: /token

**Vstupné parametre:**
Request headers:
URL: /users
Method: POST
Content-type: application/json

Request payload:
userId - meno užívateľa vo formáte meno#spolocnost alebo emailová adresa užívateľa
password - heslo užívateľa

```json
{
  "userId": "meno#spolocnost",
  "password": "heslo"
}
```

**Návratové hodnoty:**
Response headers:
Content-type: application/json

Response payload:
access_token - autorizačný token
token_type - typ tokenu (vždy Bearer)
expires_in - expiračný čas token (v sekundách)

```json
{
  "access_token": "YduMMh3/LSIClGPuN51ROEczMGCialSiIzSpbhEIJdw=",
  "token_type": "Bearer",
  "expires_in": 1200
}
```

### Používanie tokenu

Pri volaní API je potrebné získaný token zasielať v HTTP hlavičkách v nasledovnom tvare:

```
Authorization:Bearer access_token
```

Po vypršaní platnosti tokena je nutné vygenerovať nový, rovnakým spôsobom.
