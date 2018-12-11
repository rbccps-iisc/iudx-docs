Follow
======

* **Summary**: The follow API is a data exchange enabling API that is used to express interest in another entity's data. It could either be for reading, writing, or both. It is time-bound and the requestor has to explicitly mention the duration for which they would like to the data. Once the follow request is made, the ``follow-status`` API can be queried to check if the follow request is approved by the requested device.

Request
^^^^^^^

* **Endpoint**: Either of 

    - ``https://localhost/entity/follow``
    - ``https://localhost/owner/follow``

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
  |     validity    | Validity period specified in number of hours.           |
  +-----------------+---------------------------------------------------------+
  |     topic       | Topic of the message the requestor is interested in.    | 
  |                 | E.g. ``errors``, ``logs``, ``alerts``, ``data`` and     |
  |                 | so on.                                                  |
  +-----------------+---------------------------------------------------------+

* **Optional headers**:

  +-----------------+----------------------------------------------------------+
  |     Field       |     Description                                          |
  +=================+==========================================================+
  |  message-type   | Either of ``protected`` or ``diagnostics``               |
  +-----------------+----------------------------------------------------------+
  |      from       | Name of the device on behalf of which the follow request |
  |                 | is being made (When the owner calls this API)            |
  +-----------------+----------------------------------------------------------+

Responses
^^^^^^^^^

* ``202 Accepted``:

    - The follow request has been accepted for processing and is under review by the requested device or its owner (whichever may be the case)

* ``400 Bad Request`` 
    
    - If any of the required headers are missing from the request::

	{
	    "error": "inputs missing from headers"
	}

    - If ``message-type`` is provided but is not valid::

	{
	    "error": "invalid message-type"
	}

    - If the requested ``validity`` is out of range::

	{
	    "error": "validity must be in number of hours"
	}

    - If the requested ``permission`` is not valid::

	{
	    "error": "invalid permission"
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

    - If device is not autonomous::

	{
	    "error": "unauthorized"
	}

    - If the requested ``validity`` is not valid::

	{
	    "error": "invalid validity"
	}

    - If the requested topic is invalid::

	{
	    "error": "invalid topic"
	}
