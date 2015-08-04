Management of the jobs (deliveries) includes the following actions:

* creating jobs
* deleting jobs
* updating job details


Mapilary API offers more methods, however these are not required to be implemented during the integration. These methods are used internally for communication among Mapilary Console, Mapilary Courier and Mapilary Dispatcher. The methods are already configured and included in Mapilary product.

All activities falling within the user management are located under ***baseUrl*** /deliveries. Description of the in/out parameters and examples of the requests to the API are located under 
[https://mapilary.com/api-docs](https://mapilary.com/api-docs/#!/deliveries)
Simply try and test it via the same web link.


### Creating jobs (deliveries)

One or multiple jobs can be created via a single API request.
Jobs are created by sending HTTP POST request.

**Input parameters:**
Request headers:
URL: /deliveries
Method: POST
Content-type: application/json

Request payload:
trackingNr  - tracking number - a unique number used to identify & check status of the job (required)
startDate   - date of the job (optional)
endDate     - the latest date, when the job can be completed (optional)
note        - free text field for a comment (optional)
priority    - priority of the job (0 - min, 10 - max) (optional)
company     - filled out automatically
duration    - duration of the job - automatically calculated time, taking into account distance between the pick-up and the drop address
state       - job status - set to "Created" when a new record is saved (optional)
**addresses** - address field *
validFrom   - beginning of the delivery window. The time, since when the consignee is present at the address (optional)
validTo     - end of the delivery window. The time, until when the consignee is present at the address (optional)
consignee   - consignee's full name (optional)
phoneNr     - consignee's phone number (mobile, ...) (optional)
email       - consignee's e-mail address (optional)
city        - name of the city (optional)
street      - name of the street (optional)
housenumber - house number (optional)
coords      - geo-location coordinates (lat/lon) (optional)

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

#### Notes

\* The address field usually contains at least 2 addresses:
    - delivery pick-up place (where the courier picks up the delivery) - type pickup
    - delivery drop place (where the courier hands over the delivery) - type drop

