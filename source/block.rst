Block 
=====

* **Summary**: The block API can be used either by the device owner or the middleware admin to temporaily block a device from operation. 

Request
^^^^^^^

* **Endpoint**: Either of:
    
    - ``https://localhost/owner/block``
    - ``https://localhost/admin/block``

* **Method**: ``POST``

* **Security Scheme**: Either of:

    - :doc:`Owner credentials <security_schemes>` 
    - :doc:`Admin credentials <security_schemes>` 

* **Required Headers**:

  +-----------------+-------------------------------------+
  |   Header Name   |      Description                    |
  +=================+=====================================+
  |     entity      |  Name of the entity being blocked   |
  +-----------------+-------------------------------------+


Responses
^^^^^^^^^

* ``200 OK``

    - The entity has been successfully blocked 
    
* ``400 Bad Request`` 
    
    - If any of the required headers are missing from the request::

	{
	    "error": "inputs missing from headers"
	}

    - If the provided ``id`` is not a valid owner::

	{
	    "error": "id is not a valid owner"
	}
	
* ``403 Forbidden``

    - If the ``id`` is admin but the request is not from localhost::

	{
	    "error": "admin can only use from localhost"

	}

    - If the ``id`` provided is not the owner of the entity::

	{
	    "error": "you are not the owner of the entity"
	}
