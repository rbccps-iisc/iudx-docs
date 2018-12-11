Unfollow
========

* **Summary**: If the requester at any point feels that they no longer need the permissions granted to them by another device, they can invoke the ``unfollow`` API. 

Request
^^^^^^^

* **Endpoint**: Either of 

    - ``https://localhost/entity/unfollow``
    - ``https://localhost/owner/unfollow``

* **Method**: ``POST``

* **Security Scheme**: Either of 

    - :doc:`Device Credentials <security_schemes>`
    - :doc:`Owner Credentials <security_schemes>`

* **Required Headers**:

  +-----------------+---------------------------------------------------------+
  |      Field      |      Description                                        |
  +=================+=========================================================+
  |       to        | Name of the entity which the requestor is interested in |
  +-----------------+---------------------------------------------------------+
  |   permission    | Can be any of:                                          |
  |                 |   - ``read``                                            |
  |                 |   - ``write``                                           |
  |                 |   - ``read-write``                                      |
  +-----------------+---------------------------------------------------------+
  |  message-type   | Either of ``protected`` or ``diagnostics``              |
  +-----------------+---------------------------------------------------------+
  |     topic       | Topic of the message for which the follow was approved  | 
  +-----------------+---------------------------------------------------------+

* **Optional headers**:

  +-----------------+----------------------------------------------------------+
  |     Field       |     Description                                          |
  +=================+==========================================================+
  |      from       | Name of the device on behalf of which the follow request |
  |                 | is being made (When the owner calls this API)            |
  +-----------------+----------------------------------------------------------+

Responses
^^^^^^^^^

* ``200 OK``:

    - Unfollow was successful 

* ``400 Bad Request`` 
    
    - If any of the required headers are missing from the request::

	{
	    "error": "inputs missing from headers"
	}

    - If ``message-type`` is provided but is not valid::

	{
	    "error": "invalid message-type"
	}

    - If the provided ``permission`` is not valid::

	{
	    "error": "invalid permission string"
	}

* ``403 Forbidden``:

    - If the owner calls the API but the ``from`` header is missing::

	{
	    "error": "from value missing in header"
	}
    
    - When the ``from`` header is present but not valid::

	{
	    "error": "from is not a valid entity"
	}

    - When the owner calling the API is not the owner of the ``from`` device::

	{
	    "error": "you are not the owner of the 'from' entity"
	}

    - If ``to`` is not a valid entity::

	{
	    "error": "'to' is not a valid entity"
	}

    - If device is not autonomous or if there was no such acl entry::

	{
	    "error": "unauthorized"
	}

    - If the provided topic is invalid::

	{
	    "error": "invalid topic"
	}
