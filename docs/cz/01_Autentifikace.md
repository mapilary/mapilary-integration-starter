

Mapilary API na ověření identity používání autentifikace, která vychází z protokolu [oauth2](http://tools.ietf.org/html/rfc6749) - client credentials.

Každé volné API (request) musí obsahovat tzv. access_token (dále jen token), který je posílaný v http hlavičce.


### Získání token-u:

Access token se získá posláním POST requestu na url: /token

**Vstupní parametry:**
Request headers:
URL: /users
Method: POST
Content-type: application/json

Request payload:
userId - jméno uživatele ve formátu jméno#společnost nebo emailová adresa uživatele
password - heslo uživatele


```json
{
  "userId": "jméno#společnosti",
  "password": "heslo"
}
```

**Návratové hodnoty:**
Response headers:
Content-type: application/json

Response payload:
access_token - autorizační token
token_type - typ tokenu (vždy Bearer)
expires_in - expirační čas token (v sekundách)

```json
{
  "access_token": "YduMMh3/LSIClGPuN51ROEczMGCialSiIzSpbhEIJdw=",
  "token_type": "Bearer",
  "expires_in": 1200
}
```

### Používání tokenu

Při volání API je potřebné získaný token zaslat na HTTP v hlavičkách v následujícím tvaru:

```
Authorization:Bearer access_token
```

Po vypršení platnosti token je nutné vygenerovat nový, stejným způsobem.


### Test

[testovací volání](https://mapilary.com/api-docs/#!/auth/userLogin_post_0)

