***Mapilary API*** documentation for integration with the exsisting IT systems

Target audience for this documentation are companies which plan to integrade Mapilary products with their infrastructure/services.

## The documentation consists of the following parts

* Authentication
* Accessing and manipulation with Couriers collections
* Accessing and manipulation with Deliveries collections

Mapilary API uses JSON exclusively for all requests and replies.  

Access to the API is limited by [Role-based_access_control](http://en.wikipedia.org/wiki/Role-based_access_control).
These are the roles defined in the system:

* administrator
* dispatcher
* courier


Each of the roles can perform just a subset of specific operations. More details about the permissions 
are listed in the following chapters.