Management of the users includes the following actions:

* creating a new user (POST method)
* deleting the existing user (DELETE method)
* displaying list of the users  (GET method)
* changing the user profiles (PATCH - updateProfile)
* changing the passwords (PATCH - changePassword)

Each user must have assigned one of the roles. The role defines user's access level and specific permissions 
for the data manipulation. The user logs in to the system via a username & password OR e-mail address & password. 

User Roles:

* administrator
* dispatcher
* courier

***Administrator*** is the role with unlimited permissions. For the sake of security, we advise configuring a single administrator for each company.
Administrator usually performs the following actions:

* creating and managing user accounts


***Dispatcher*** is a person, who primarily assigns jobs (deliveries) to the couriers.
Dispatcher usually performs the following actions:

* creating and managing jobs
* assigning jobs to the couriers


***courier*** is a person, who performs the job in the field. (e.g. picking up the parcels and delivering them to the consignees)
Courier usually performs the following actions:

* accepting jobs assigned by the dispatcher
* marking the jobs as completed (e.g. parcel successfully delivered)

All activities falling within the user management are located under ***baseUrl*** /users.
Description of the in/out parameters and examples of the requests to the API are located under 
[https://mapilary.com/api-docs](https://mapilary.com/api-docs/#!/users)
Simply try and test it via the same web-link.


This documentation will further discuss only the cases which help with the API integration.

### Creating a new user

One or multiple users can be created via a single API request.
Users are created by sending HTTP POST request.

**Input Parameters:**
Request headers:
URL: /users
Method: POST
Content-type: application/json

username    - user's nickname - used to log in to the application (required field)
password    - user's password (required field)
company     - company name (optional field) *
roles       - user role(s) ['admin', 'courier', 'dispatcher'] (required field) **
deviceTokens- the tokens required for accepting push notifications by the mobile device (optional)
vehicleType - type of the vehicle used by the courier ['bicycle', 'motorbike', 'van', 'car'] (optional)
titleBefore - title before the name (optional)
name        - name of the user (optional)
surname     - surname of the user (optional)
age         - age of the user (optional)
phoneNr     - user's phone number (optional)
email       - e-mail (optional) ***

```json
{
    "username": "johndoe",
    "password": "strong",
    "company": "mapilary",
    "roles": ["courier"],
    "deviceTokens": ["token"],
    "vehicleType": "car",
    "profile": {
        "titleBefore": "M.S..",
        "name": "John",
        "surname": "John",
        "age": 48,
        "phoneNr": "+421890345830",
        "email": "johndoe@company.com"
    }
}
```
#### Notes
\*  The company name is typically inherited from the administrator's name (who is creating the new user)
** each user can have more roles assigned
*** if the e-mail address is entered, the user can use it to log in to the system

The method also contains an optional parameter upsert (which is part of the URL): /users?upsert=true

Parameter upsert=true ensures update of the users's data (in case the user already exists in the system). 
In case the upsert parameter is not set, API returns an error:

```json
{
  "message": "E11000 duplicate key error index: mapilary.users.$username_1  dup key: { : \"johndoe\" }"
}
```