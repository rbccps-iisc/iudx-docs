Deregister Entity
=================

* **Summary**: The deregister entity API is used by the device owners to delete devices from the middleware

Request
^^^^^^^

* **Endpoint**: ``https://localhost/owner/deregister-entity``

* **Method**: ``POST``

* **Security Scheme**: :doc:`Owner credentials <security_schemes>` 

* **Required Headers**:

  +-----------------+-----------------------------------------+
  |   Header Name   |      Description                        |
  +=================+=========================================+
  |     entity      |  Name of the entity being deregistered  |
  +-----------------+-----------------------------------------+


Responses
^^^^^^^^^

* ``200 OK``

    - The entity has been successfully deregistered
    
* ``400 Bad Request`` 
    
    - If any of the required headers are missing from the request::

	{
	    "error": "inputs missing from headers"
	}

    - If the entity name is not valid::

	{
	    "error": "entity is not valid"
	}
	
    - If there is no such entity::

	{
	    "error": "invalid entity"
	}
	    
* ``403 Forbidden``

    - If the ``id`` provided is not a valid owner::

	{
	    "error": "id is not an owner"
	}
    
    - If the ``id`` provided is not the owner of the entity::

	{
	    "error": "you are not the owner of the entity"
	}
