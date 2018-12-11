Follow Requests
===============

* **Summary**: The ``follow-requests`` API is used by a device or its owner to check for follow requests that may be made by other devices. This API gives a list of devices which have requested for permissions along with their ``follow-id``. If the device or its owner deems that the requesting device is authorised to receive the nature of the data that it is requesting (and has sucessfully made the payment for the data), then the device can appprove the follow request using the ``share`` API.

Request
^^^^^^^

* **Endpoint**: Either of 

    - ``https://localhost/entity/follow-requests``
    - ``https://localhost/owner/follow-requests``

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

Response
^^^^^^^^

* ``200 OK``:

    - A JSON array of devices which have made a follow request, along with their details::

	[
	    {
		"follow-id": "1243",
		"from": "admin/app",
		"to": "admin/dev.command",
		"time": "2018-11-11 03:58:01.632034",
		"permission": "write",
		"topic": "#",
		"validity": "24"
	    }
	]
