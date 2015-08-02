Mapilary API identity verification is built on [oauth2](http://tools.ietf.org/html/rfc6749) authorization framework - client credentials.


Each API request shall contain access_token (only "token" further in the text), which is being sent within the HTTP header.

### Gaining the token:

Access token can be obtained by sending POST request to the url: /token

**Input parameters:**
Request headers:
URL: /users
Method: POST
Content-type: application/json

Request payload:
userId - user name in the one of the following formats:  name#company OR user e-mail address
password - user password

```json
{
  "userId": "name#company",
  "password": "password"
}
```

**Output values:**
Response headers:
Content-type: application/json

Response payload:
access_token  - authentication token
token_type    - token type (always Bearer)
expires_in    - time to expire (in seconds)

```json
{
  "access_token": "YduMMh3/LSIClGPuN51ROEczMGCialSiIzSpbhEIJdw=",
  "token_type": "Bearer",
  "expires_in": 1200
}
```

### Token usage

When calling Mapilary API, the token shall be sent in the HTTP headers, in to the following format:

```
Authorization:Bearer access_token
```

Once the token expires, a new token has to be generated by following the same process.


### Test

[Test request](https://mapilary.com/api-docs/#!/auth/userLogin_post_0)