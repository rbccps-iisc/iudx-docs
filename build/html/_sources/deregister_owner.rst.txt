Deregister Owner
================

* **Summary**: The deregister owner API is used by the administrator to delete owners from the middleware

Request
^^^^^^^

* **Endpoint**: ``https://localhost/admin/deregister-owner``

* **Method**: ``POST``

* **Security Scheme**: :doc:`Admin credentials <security_schemes>` 

* **Required Headers**:

  +-----------------+-----------------------------------------+
  |   Header Name   |            Description                  |
  +=================+=========================================+
  |	  owner     |  Name of the owner being deregistered   |
  +-----------------+-----------------------------------------+


Responses
^^^^^^^^^

* ``200 OK``
	
    - The owner has been successfully deregistered

* ``400 Bad Request`` 
	
    - If any of the required headers are missing from the request::

	{
	    "error": "inputs missing from headers"
	}

    - If the owner name is not valid::

	{
	    "error": "not a valid owner"
	}
	    
* ``403 Forbidden``

    - If this API is being called from outside localhost::

	{
	    "error": "this api can only be called from localhost"
	}

    - If a user other than admin tries to invoke this API::
	
	{
	    "error": "only admin can call this api"
	}
	
    - If the name of the owner being deleted is reserved, i.e is one of ``admin``, ``validator`` or ``database``::

	{
	    "error": "cannot delete user"
	}
