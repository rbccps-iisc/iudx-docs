Reject Follow
=============

* **Summary**: The reject follow API is used when the device or its owner deems that the requesting entity is not authorised to the permissions that it is seeking through the ``follow`` request. This API rejects the ``follow`` request and updates the follow status to ``rejected``.

Request
^^^^^^^

* **Endpoint**: Either of

    - ``https://localhost/entity/reject-follow``
    - ``https://localhost/owner/reject-follow``

* **Method**: ``POST``

* **Security Scheme** : Either of

    - :doc:`Device Credentials <security_schemes>`
    - :doc:`Owner Credentials <security_schemes>`

* **Required Headers**:

  +-----------------+-------------------------------------------------------+
  |   Header Name   |      Description                                      |
  +=================+=======================================================+
  |     follow-id   |  ID of the follow request made by another entity. Can | 
  |                 |  be obtained by calling the ``follow-requests`` API   |
  +-----------------+-------------------------------------------------------+

Responses
^^^^^^^^^

* ``200 OK``:

    - The follow request has been rejected

* ``400 Bad Request``:

    - If any of the required headers are missing from the request::

	{
	    "error": "inputs missing from headers"
	}

    - If the device is not autonomous::

	{
	    "error": "unauthorized"
	}

    - If the ``follow-id`` is invalid::

	{
	    "error": "invalid follow-id"
	}
