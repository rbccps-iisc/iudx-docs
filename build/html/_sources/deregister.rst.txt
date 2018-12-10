Deregister
==========

* **Summary**: The deregister API is used to completely remove all entries belonging to a device from the middleware. This deletes from the consumers list in Kong,
  deletes all 6 exchanges and 4 queues from RabbitMQ, removes entries in LDAP and finally deletes the document from catalogue. The owner of the specific device has 
  to initiate this action, the device cannot deregister itself. 

* **Endpoint**: ``https://localhost:8443/api/1.0.0/register``

* **Method**: ``DELETE``

* **Required Headers**:

  +-----------------+--------------------------------------+
  |   Header Name   |      Description                     |
  +=================+======================================+
  |     apikey      |  API key of the owner of the device  |
  +-----------------+--------------------------------------+

* **Body**:

  .. code-block:: JSON

   {"id":"<id_of_the_device>"}

* **Example Request**::

   curl -X DELETE \
   https://localhost:8443/api/1.0.0/register \
   -H 'Content-Type: application/json' \
   -H 'apikey: guest' \
   -d '{"id":"streetlight"}'

* **Example Response**:

  .. code-block:: JSON

   {
     "De-Registration": "success",
     "entityID": "streetlight3"
   }

* **Possible error scenarios**:

  - ``Invalid authentication credentials``: Make sure you have provided the right API key of the owner of the device
  - When the device does not belong to the owner:

    .. code-block:: JSON

     {
       "De-Registration": "failure",
       "Reason": "Device does not belong to Owner"
     }

    This means that the device being deregistered does not belong to the owner whose API key has been provided.

  - ``ID not provided``: The device ID which needs to be deregistered has not been supplied
