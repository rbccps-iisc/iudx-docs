Follow Status 
=============

* **Summary**: The ``follow-status`` API is used by devices or owners to check the status of follow requests they have made to other devices. 

Request
^^^^^^^

* **Endpoint**: Either of 

    - ``https://localhost/entity/follow-status``
    - ``https://localhost/owner/follow-status``

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

    - A JSON array of follow requests along with their status:: 

	[
	    {
		"follow-id": "1243",
		"from": "admin/app",
		"to": "admin/dev.command",
		"time": "2018-11-11 03:58:01.632034",
		"permission": "write",
		"topic": "#",
		"validity": "24",
		"status": "pending"
	    }
	]
