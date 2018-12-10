Share
=====

* **Summary**: The "share" API is a data exchange enabling API which is used to approve "follow" requests. When the share API is called by an entity, it grants the necessary 
  permissions to the requestor's device, i.e, either read access, or write access, or both. Once the process completes, the requesting entity gets a notification in their
  <device>.notify queue aprising them of the status of the follow request they made. Consequently, the requesting entity can either bind their queue to the requested exchange,
  or start publishing to it, depending upon the granted permissions.

* **Endpoint**: ``https://localhost:8443/api/1.0.0/share``

* **Method**: ``POST``

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
  |    entityID     | Name of the owner's entity                              |
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
  |                 | Example: 10D for 10 days, 1Y for 1 year and so on       |
  +-----------------+---------------------------------------------------------+
  |  requestorID    | Name of the requesting device                           |
  +-----------------+---------------------------------------------------------+

* **Example Request**::
  
   curl -X POST \
   https://localhost:8443/api/1.0.0/share \
   -H 'Content-Type: application/json' \
   -H 'apikey: ko6A9npXespXwyK85mtfCfmHGVLFYJZMOxScjk9iUJy' \
   -d 
   '{
        "entityID": "device1",
        "permission":"read", 
        "validity": "10D",
        "requestorID":"device2"
    }'

* **Example Response**:

  .. code-block:: JSON

   {"status":"Share request approved for device2 with permission read at 2018-09-09T04:19:33.484Z"}   
  
* **Possible error scenarios**:
  
   - ``Invalid authentication credentials`` : Make sure you have provided the right API key
   - ``Possible missing fields``: The fields required in the body, as given above, are not all present according to the format. 
