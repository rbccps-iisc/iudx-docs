Publish
=======

* **Summary**: The publish API is used to publish data from the devices to the middleware. To access this API, the device API key obtained after device registration must be used.

Request
^^^^^^^

* **Endpoint**: ``https://localhost/entity/publish``

* **Method**: ``POST``

* **Security Scheme**: :doc:`Device credentials <security_schemes>` 

* **Required Headers**:

  +-----------------+---------------------------------------------------------------------------+
  |   Header Name   |      Description                                                          |
  +=================+===========================================================================+
  |     to          |  Name of the device to which the message is being published               |
  +-----------------+---------------------------------------------------------------------------+
  |   subject       |  Subject of the message, e.g. ``temperature``, ``logs``, ``errors``, etc. |
  +-----------------+---------------------------------------------------------------------------+
  |  message-type   |  Either of ``public``, ``protected``, ``private`` or ``diagnostics``      |
  +-----------------+---------------------------------------------------------------------------+

* **Body**: The message from the device that conforms to the schema specified during registration

* **Example Request**::
  
   curl -ik -X POST \
   https://localhost/entity/publish
   -H 'Content-Type: application/json' \
   -H 'id: company/streetlight' \
   -H 'apikey: yJv7sxFginCYPHq4v4ji-XTLP-Ya0stw' \
   -H 'to: company/streetlight' \
   -H 'subject: data' \
   -H 'message-type: protected' \
   -d '{
         "ambientLux": "10000",
         "power": "73.26",
         "caseTemp": 34.5
       }'

Responses
^^^^^^^^^

* ``202 Accepted``

    - The message has been accepted for publishing

* ``400 Bad Request`` 
    
    - If any of the required headers are missing from the request::

	{
	    "error": "inputs missing from headers"
	}

    - If the provided ``to`` is not a valid entity::

	{
	    "error": "to is not a valid entity"
	}

    - If the provided ``message-type`` is not valid::

	{
	    "error": "message-type is not valid"
	}

    - If the provided ``to`` is different from ``id`` and ``message-type`` is other than ``command``::

	{
	    "error": "message-type can only be command"
	}

    - If the provided ``id`` is not a valid entity::

	{
	    "error": "id is not a valid entity"
	}
