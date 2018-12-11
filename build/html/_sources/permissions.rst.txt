Permissions
===========

* **Summary**: The permissions API is used to get all the permissions that a device has previously obtained from other devices.

Request
^^^^^^^

* **Endpoint**: Either of 

    - ``https://localhost/entity/permissions``
    - ``https://localhost/owner/permissions``

* **Method**: ``GET``

* **Security Scheme**: Either of 

    - :doc:`Device Credentials <security_schemes>`
    - :doc:`Owner Credentials <security_schemes>`

* **Required Headers**: Only those required for the security scheme

* **Optional Headers**: If the owner is invoking this API on behalf of the device then these headers are required.


  +-----------------+---------------------------------------------------------+
  |      Field      |      Description                                        |
  +=================+=========================================================+
  |     entity      | Name of the entity on behalf of which the API is being  |
  |                 | invoked                                                 |
  +-----------------+---------------------------------------------------------+

Responses
^^^^^^^^^

* ``200 OK``:

    - A JSON array of devices and the respective permissions that have been obtained on them:: 

	[
	    {
		"entity": "admin/dev.command",
		"permission": "write"
	    }
	]
