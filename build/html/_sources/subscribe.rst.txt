Subscribe
=========

* **Summary**: The subscribe API is used to get messages from a queue. This is a destructive action on the message as 
  it will no longer be available in the queue after subscription. This API is not streaming, i.e. as data arrives into the 
  queue it is not pushed to the subscribers. However, it needs to be polled regularly to check for new messages.


Request
^^^^^^^

* **Endpoint**: ``https://localhost/entity/subscribe``

* **Method**: ``GET``

* **Security Scheme**: :doc:`Device Credentials <security_schemes>`

* **Optional Headers**:

  +-----------------+--------------------------------------------------------------+
  |   Header Name   |      Description                                             |
  +=================+==============================================================+
  |  message-type   |  Either of ``priority``, ``command`` or ``notification``.    |
  |		    |  If this field is empty then the supplied ``id`` is taken    |
  |		    |  as the default queue name                                   |
  +-----------------+--------------------------------------------------------------+
  |  num-messages   | Number of messages to subscribe to. Defaults to 10           |
  +-----------------+--------------------------------------------------------------+


Responses
^^^^^^^^^

* ``200 OK``
  
    - Gives back messages from the queue
	
	.. code-block:: JSON
    
	    [{
		"sent-by": "admin/dev",
		"from": "admin/dev.protected",
		"subject": "streetlight data",
		"content-type": "application/json",
		"body": {
		    "ambientLux": 10000,
		    "power": 73.26,
		    "caseTemp": 34.5
		}
	    }]
* ``400 Bad Request`` 
    
    - If any of the required headers are missing from the request::

	{
	    "error": "inputs missing from headers"
	}

    - If the provided ``id`` is not a valid entity::

	{
	    "error": "id is not a valid entity"
	}

    - If ``message-type`` is provided but is invalid::

	{
	    "error": "invalid message-type"
	}

    - If ``num-messages`` is provided but is not valid::

	{
	    "error": "num-messages is not valid"
	}
