Unfollow 
========

* **Summary**: The unfollow API is a complement of the ``unshare`` API for the requestor. If the requestor at any point feels that he/she no longer 
  needs the permissions granted by a device, they can call the ``unfollow`` API. This will delete entries from LDAP and unbind the queue if bound. 

* **Endpoint**: ``https://localhost:8443/api/1.0.0/follow``

* **Method**: ``DELETE``

* **Required Headers**:

  +-----------------+-------------------------+
  |   Header Name   |      Description        |
  +=================+=========================+
  |     apikey      |  API key of the device  |
  +-----------------+-------------------------+

* **Body**: The body must contain certain specific fields as mentioned below:

  +-----------------+---------------------------------------------------------+
  |      Field      |      Description                                        |
  +=================+=========================================================+
  |    entityID     | Name of the entity which the requestor is interested in |
  +-----------------+---------------------------------------------------------+
  |   permission    | Can be any of:                                          |
  |                 |   - ``read``                                            |
  |                 |   - ``write``                                           |
  |                 |   - ``read-write``                                      |
  +-----------------+---------------------------------------------------------+
  |    validity     | Of the form <Integer><Metric>                           |
  |                 |                                                         |
  |                 | Metric can be any of:                                   |
  |                 |   - ``Y``: Year                                         |
  |                 |   - ``M``: Month                                        |
  |                 |   - ``D``: Day                                          |
  |                 |                                                         |
  |                 | Example: 10D for 10 days, 1Y  for 1 Year and so on      |
  +-----------------+---------------------------------------------------------+
  |  requestorID    | Name of the requesting device                           |
  +-----------------+---------------------------------------------------------+

* **Example Request**::
  
   curl -X DELETE \
   https://localhost:8443/api/1.0.0/follow \
   -H 'Content-Type: application/json' \
   -H 'apikey: ko6A9npXespXwyK85mtfCfmHSDLFYJZMOxScjk9iUJy' \
   -d 
   '{
        "entityID": "device1",
        "permission":"read", 
        "validity": "10D",
        "requestorID":"device2"
    }'

* **Example Response**::
  
   Successfully unfollowed device1


* **Possible error scenarios**:
  
   - ``Invalid authentication credentials`` : Make sure you have provided the right API key
   - ``Possible missing fields``: The fields required in the body, as given above, are not all present according to the format. 
