Bind 
=====

* **Summary**: The bind API is used to facilitate binding between exchanges and queues of different devices. When a device obtains read access to another device it can bind its queue to that device's exchange using the ``bind`` API. The binding can be done either to its regular queue or to its priority queue depending on the user's preference. 
  
Request
^^^^^^^

* **Endpoint**: Either of

    - ``https://localhost/entity/bind``
    - ``https://localhost/owner/bind``

* **Method**: ``POST``

* **Security Scheme**: Either of

    - :doc:`Device credentials <security_schemes>`
    - :doc:`Owner credentials <security_schemes>`

* **Required Headers**:
  
  +-----------------+---------------------------------------------------------------------------+
  |   Header Name   |      Description                                                          |
  +=================+===========================================================================+
  |       to        |  Name of the device to bind to                                            | 
  +-----------------+---------------------------------------------------------------------------+
  |      topic      |  Topic of the message, e.g. ``temperature``, ``logs``, ``errors``, etc.   |
  +-----------------+---------------------------------------------------------------------------+
  |   message-type  |  Either of ``public``, ``protected``, ``private`` or ``diagnostics``      |
  +-----------------+---------------------------------------------------------------------------+


Responses
^^^^^^^^^

* ``200 OK``

    - The bind was successful 

* ``400 Bad Request`` 
    
    - If any of the required headers are missing from the request::

	{
	    "error": "inputs missing from headers"
	}

    - If ``message-type`` is provided but is not valid::

	{
	    "error": "message-type is invalid"
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

    - If the message-type is ``private`` but the given ``id`` is not the owner of``to`` is not a valid entity::

	{
	    "error": "'to' is not a valid entity"
	}

    - If device is not autonomous or there is no such ACL entry::

	{
	    "error": "unauthorized"
	}

    - If the requested topic is invalid::

	{
	    "error": "invalid topic"
	}
