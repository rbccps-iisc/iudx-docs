Share
=====

* **Summary**: The "share" API is a data exchange enabling API which is used to approve ``follow`` requests. When the share API is called by an entity, it grants the necessary permissions to the requestor's device, i.e, either read access, or write access, or both. The requested entity can poll the ``follow-requests`` API to check if any new follow requests were made to it. The requesting device, can similarly poll the ``follow-status`` API to check if the follow request was approved. Once the process completes, the requesting entity can bind to the exchange of the requested entity's exchange using the ``bind`` API (in case of read permission) or start writing to the device's command queue (in case of write permission). When the permission is for write access, the scenario is handled a little differently which is explained using the following example. Assume ``person/app`` would like to control ``company/streetlight``. After the necessary permissions are obtained, although ``person/app`` publishes to ``company/streetlight``, under the hood the message is actually published to ``person/app.publish`` with a routing key ``company/streetlight.command.#`` (if the message's routing key was #). The ``person/app.publish`` exchange is bound to ``company/streetlight``'s command queue with the above routing key. This information becomes useful when the publisher uses the AMQP protocol to publish messages.

Request
^^^^^^^

* **Endpoint**: Either of:

    - ``https://localhost/owner/share``
    - ``https://localhost/entity/share``

* **Method**: ``POST``

* **Security Scheme**: Either of

    - :doc:`Owner credentials <security_schemes>`
    - :doc:`Device credentials <security_schemes>`

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

    - The follow request has been approved

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
