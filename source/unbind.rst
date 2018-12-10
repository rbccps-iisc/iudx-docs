Unbind 
=======

* **Summary**: The unbind API is used to enable unbinding queues and exchanges. Unbinding can be done when the default bindings between the exchanges 
  and queues does not suit the user. It can also be done when the device temporarily does not need to receive data from another device but wishes to 
  keep the share entry intact.

* **Endpoint**: ``https://localhost:8443/api/1.0.0/bind/<queue>/<exchange>``

  +--------------+-------------------------------------------------------------------+ 
  |  Field       | Description                                                       | 
  +==============+===================================================================+ 
  | <queue>      | Name of the queue which needs to be bound to an exchange.         | 
  +--------------+-------------------------------------------------------------------+ 
  | <exchange>   | Exchange name. If this does not belong to the owner, the process  |
  |              |                                                                   | 
  |              | of ``follow`` and ``share`` must happen.                          | 
  +--------------+-------------------------------------------------------------------+ 

* **Method**: ``DELETE``

* **Required Headers**:

  +-----------------+-------------------------+
  |   Header Name   |      Description        |
  +=================+=========================+
  |     apikey      |  API key of the device  |
  +-----------------+-------------------------+

* **Optional Headers**:

  +------------------+--------------------------------------------------------------+
  |   Header Name    |                Description                                   |
  +==================+==============================================================+
  |   routingKey     |   Topic with which the exchange must be bound to the queue   |
  +------------------+--------------------------------------------------------------+

* **Example Request**::
  
   curl -X DELETE \
   https://localhost:8443/api/1.0.0/bind/app/streetlight.protected \
   -H 'apikey: SLJTRxPdAVrslmHxcFPfQNWykVOIiIZ2hdiy0FSQOhB' \
   -H 'routingKey: #'

* **Response**::

   Unbind Queue OK

* **Possible error scenarios**:

   - ``Invalid authentication credentials``: Make sure you have provided the right API key
   - ``You do not have access to unbind this queue``: Make sure that you have the permission to unbind 
     the queue. A queue can be unbound from an exchange in two scenarios only
      
      - If the exchange and queue belong to the same owner
      - If the exchange belongs to a different owner but the owner has ``share`` d with the current device
