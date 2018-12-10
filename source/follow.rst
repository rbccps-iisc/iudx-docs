Follow
======

* **Summary**: The follow API is a data exchange enabling API that is used to express interest in another entity's data. It could either be for reading, writing, or both. It is time-bound and the requestor has to explicitly mention the duration for which they would like to the data. Once the follow request is made, the ``follow-status`` API can be queried to check if the follow request is approved by the requested device.

Request
^^^^^^^

* **Endpoint**: Either of 

    - ``https://localhost/entity/follow``
    - ``https://localhost/owner/follow``

* **Method**: ``POST``

* **Security Scheme**: Either of 

    - :doc:`Device Credentials <security_schemes>`
    - :doc:`Owner Credentials <security_schemes>`

* **Required Headers**:

  +-----------------+---------------------------------------------------------+
  |      Field      |      Description                                        |
  +=================+=========================================================+
  |    to           | Name of the entity which the requestor is interested in |
  +-----------------+---------------------------------------------------------+
  |   permission    | Can be any of:                                          |
  |                 |   - ``read``                                            |
  |                 |   - ``write``                                           |
  |                 |   - ``read-write``                                      |
  +-----------------+---------------------------------------------------------+
  |     validity    | Validity period specified in number of hours.           |
  +-----------------+---------------------------------------------------------+
  |     topic       | Topic of the message the requestor is interested in.    | 
  |                 | E.g. ``errors``, ``logs``, ``alerts``, ``data`` and     |
  |                 | so on.                                                  |
  +-----------------+---------------------------------------------------------+


Responses
^^^^^^^^^

* **Example Response**:

  .. code-block:: JSON
   
   {"status":"Follow request has been made to device1 with permission read at 2018-09-10T09:42:57.226Z"}

* **Possible error scenarios**:
  
   - ``Invalid authentication credentials`` : Make sure you have provided the right API key
   - ``Possible missing fields``: The fields required in the body, as given above, are not all present according to the format. 
