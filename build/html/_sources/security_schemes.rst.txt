.. _security_schemes:

Security Schemes
================

The following subsection enumerates the various security schemes used for accessing all the APIs in the IUDX middleware. Every scheme pertains to a role which is associated with a set of actions, and hence, is authorised only to a restricted subset of the APIs. In any of the security schemes, if either the ``id`` or the ``apikey`` is incorrect, the respective API will give back a ``403 Forbidden`` Although this response is not limited to the situation stated thereof, it is deliberately kept that way for security reasons. Therefore, the above response arising due to incorrect ``id`` or ``apikey`` will not be specifically stated in the detailed description of the individual APIs. However, other situations causing this error, for the specific API, will be covered. 

Admin Credentials
-----------------

This scheme is used by the administrator of the middleware for registering and deregistering users. Its structure is as follows:

    +------------------+--------------------------------+
    | Header	       | Description                    |
    +==================+================================+
    |	id	       | ID of the middleware admin     |
    +------------------+--------------------------------+
    |	apikey	       | Apikey of the middleware admin |
    +------------------+--------------------------------+

These credentials are found in vars/admin.passwd of the repository's base directory, after a successful installation. The ID of the admin user is ``admin``


Owner Credentials
-----------------

The term ``owner`` corresponds to a user or an organisation which has been registered with the middleware by the adminstrator. These owners usually have numerous devices under their control, which they would like to ``onboard`` with the middlware. E.g. A company ``BigCompany`` can be the owner of all the sensors deployed in its office complex.  

    +------------------+--------------------------------+
    | Header	       | Description                    |
    +==================+================================+
    |	id	       | ID of the owner                |
    +------------------+--------------------------------+
    |	apikey	       | Apikey of the owner            |
    +------------------+--------------------------------+

These credentials are obtained after the middleware admin registers the owner. The owner can then use the apikey provided to onboard new devices, authorise data exchange requests on behalf of the device, make changes to device configurations in the middleware, block or unblock some of the devices they own, and many such other tasks which are detailed later on.


Device Credentials
------------------

This refers to the device ID and apikey obtained after the owner registers the device with the middleware

    +------------------+--------------------------------+
    | Header	       | Description                    |
    +==================+================================+
    |	id	       | ID of the device               |
    +------------------+--------------------------------+
    |	apikey	       | Apikey of the device           |
    +------------------+--------------------------------+

The device credentials can be used to access various APIs like publish, subscribe, follow, share etc. The exact details of device API access mechanisms will be dealt with at a later stage.



