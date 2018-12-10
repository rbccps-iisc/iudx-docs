Register Owner
==============

* **Summary**: The register owner API is used by the administrator to register new owners with the middleware

Request
^^^^^^^

* **Endpoint**: ``https://localhost/admin/register-owner``

* **Method**: ``POST``

* **Security Scheme**: :doc:`Admin credentials <security_schemes>` 

* **Required Headers**:

  +-----------------+---------------------------------------+
  |   Header Name   |      Description                      |
  +=================+=======================================+
  |	  owner     |  Name of the owner being registered   |
  +-----------------+---------------------------------------+


Responses
^^^^^^^^^

* ``201 Created``
	
    - The owner has been successfully created::
      
	{   
	    "id": "streetlight-owner",
	    "apikey": "BdPujwdwmMXpcXRpAuwwNfasGeTHeYgK"
	}
    
* ``400 Bad Request`` 
    
    - If the owner name is not valid::

	{
	    "error": "entity should be a valid owner"
	}
	
    - If any headers are missing from the request::

	{
	    "error": "inputs missing from headers"
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
	
    - If the name of the owner being created is reserved, i.e is one of ``admin``, ``validator`` or ``database``::

	{
	    "error": "cannot create the user"
	}
	
* ``409 Conflict``
    
    - If the owner id is already in use::

	{   
	    "error": "id already used"
	}

.. TODO move these descriptions to background section 

API key
^^^^^^^

The API key is a globally unique identifier that is tied specifically to a device. It is non-temporal and used to identify one particular device *only*
unless otherwise needed. (See <Group API key>) Once a device is registered, all further communications with the middleware from the device must use the API key.

API key can be requested in five security levels. They are as follows:
  
#. **Level 1**: 64 bit
#. **Level 2**: 128 bit
#. **Level 3**: 256 bit
#. **Level 4**: 512 bit
#. **Level 5**: 1024 bit

Depending upon the criticality of the device in the infrastructure, the desired security level can be requested for. The default level in the absence of 
an explicit header mentioning it, will be 3 i.e. 256 bit security.
