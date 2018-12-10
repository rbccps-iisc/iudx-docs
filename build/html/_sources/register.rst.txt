.. _register:

Register 
========

API Specification
-----------------

* **Summary**: The register API is used to register devices and apps with the middleware. They can register as either
  devices or subscribers, the difference being that subscribers do not publish any data. Every device can have its own
  schema, or in other words, meta information about the nature of the information that the device publishes. For more 
  information on schemas visit `here <https://github.com/rbccps-iisc/smart_cities_schemas>`_

* **Endpoint**: ``https://localhost:8443/api/1.0.0/register``

* **Method**: ``POST``

* **Required Headers**:

  +-----------------+--------------------------+
  |   Header Name   |      Description         |
  +=================+==========================+
  |     apikey      |  API key of the provider |
  +-----------------+--------------------------+

* **Optional Headers**:

  +------------------+------------------------------+
  |   Header Name    |         Description          |
  +==================+==============================+
  |   security_level |    An integer between 1-5    |
  +------------------+------------------------------+

* **Body**: A valid catalogue item as mentioned `here <https://github.com/rbccps-iisc/smart_cities_schemas>`_

* **Example request**:: 
  
   curl -X POST \
     http://localhost/api/1.0.0/register \
     -H 'apikey: guest' \
     -H 'content-type: application/json' \
     -k -d '{
    
    "entitySchema": {
    "refCatalogueSchema": "generic_iotdevice_schema.json",
    "resourceType": "streetlight",
    "tags": [
      "onstreet",
      "Energy",
      "still under development!"
    ],
    "refCatalogueSchemaRelease": "0.1.0",
    "latitude": {
      "value": 13.0143335,
      "ontologyRef": "http:\/\/www.w3.org\/2003\/01\/geo\/wgs84_pos#"
    },
    "longitude": {
      "value": 77.5678424,
      "ontologyRef": "http:\/\/www.w3.org\/2003\/01\/geo\/wgs84_pos#"
    },
    "owner": {
      "name": "IISC",
      "website": "http:\/\/www.iisc.ac.in"
    },
    "provider": {
      "name": "Robert Bosch Centre for Cyber Physical Systems, IISc",
      "website": "http:\/\/rbccps.org"
    },
    "geoLocation": {
      "address": "80 ft Road, Bangalore, 560012"
    },
    "data_schema": {
      "type": "object",
      "properties": {
        "dataSamplingInstant": {
          "type": "number",
          "description": "Sampling Time in EPOCH format",
          "units": "seconds",
          "permissions": "read",
          "accessModifier": "public"
        },
        "caseTemperature": {
          "type": "number",
          "description": "Temperature of the device casing",
          "units": "degreeCelsius",
          "permissions": "read",
          "accessModifier": "public"
        },
        "powerConsumption": {
          "type": "number",
          "description": "Power consumption of the device",
          "units": "watts",
          "permissions": "read",
          "accessModifier": "public"
        },
        "luxOutput": {
          "type": "number",
          "description": "lux output of LED measured at LED",
          "units": "lux",
          "permissions": "read",
          "accessModifier": "public"
        },
        "ambientLux": {
          "type": "number",
          "description": "lux value of ambient",
          "units": "lux",
          "permissions": "read",
          "accessModifier": "public"
        },
        "targetPowerState": {
          "type": "string",
          "enum": [
            "ON",
            "OFF"
          ],
          "units": "dimensionless",
          "description": "If set to ON, turns ON the device. If OFF turns OFF the device. Writeable parameter. Writeable only allowed for authorized apps",
          "permissions": "read-write",
          "accessModifier": "protected"
        },
        "targetBrightnessLevel": {
          "type": "number",
          "description": "Number between 0 to 100 to indicate the percentage brightness level. Writeable only allowed for authorized apps",
          "units": "percent",
          "permissions": "read-write",
          "accessModifier": "protected"
        },
        "targetControlPolicy": {
          "enum": [
            "AUTO_TIMER",
            "AUTO_LUX",
            "MANUAL"
          ],
          "units": "dimensionless",
          "permissions": "read-write",
          "description": "Indicates which of the behaviours the device should implement. AUTO_TIMER is timer based, AUTO_LUX uses ambient light and MANUAL is controlled by app. Writeable only allowed for authorized apps",
          "accessModifier": "protected"
        },
        "targetAutoTimerParams": {
          "type": "object",
          "permissions": "read-write",
          "properties": {
            "targetOnTime": {
              "type": "number",
              "description": "Indicates time of day in seconds from 12 midnight when device turns ON in AUTO_TIMER. Writeable only allowed for authorized apps",
              "units": "seconds",
              "accessModifier": "protected"
            },
            "targetOffTime": {
              "type": "number",
              "description": "Indicates time of day in seconds from 12 midnight when device turns OFF in AUTO_TIMER. Writeable only allowed for authorized apps",
              "units": "seconds",
              "accessModifier": "protected"
            }
          }
        },
        "targetAutoLuxParams": {
          "type": "object",
          "permissions": "read-write",
          "properties": {
            "targetOnLux": {
              "type": "number",
              "description": "Indicates ambient lux when device turns ON in AUTO_LUX. Writeable only allowed for authorized apps",
              "units": "lux",
              "accessModifier": "protected"
            },
            "targetOffLux": {
              "type": "number",
              "description": "Indicates ambient lux when device turns OFF in AUTO_LUX. Writeable only allowed for authorized apps",
              "units": "lux",
              "accessModifier": "protected"
            }
          }
        }
      },
      "additionalProperties": false
    },
    "serialization_from_device": {
      "format": "protocol-buffers",
      "schema_ref": {
        "type": "proto 2",
        "mainMessageName": "sensor_values",
        "link": "https:\/\/raw.githubusercontent.com\/rbccps-iisc\/applications-streetlight\/master\/proto_stm\/txmsg\/sensed.proto"
      }
    },
    "serialization_to_device": {
      "format": "protocol-buffers",
      "schema_ref": {
        "type": "proto 2",
        "mainMessageName": "targetConfigurations",
        "link": "https:\/\/raw.githubusercontent.com\/rbccps-iisc\/applications-streetlight\/master\/proto_stm\/rxmsg\/actuated.proto"
      }
    },
    "id": "streetlight"
   }}'


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

Success Response
----------------

* **Code**: ``200 OK``

* **Response Body**
  
  .. code-block:: JSON
  
   {
    "Registration": "success",
    "entityID": "streetlight",
    "apiKey": "MZW68JGDCbxFVTUndReIUTNIC5cEIS3Glho14XZfZhp",
    "subscriptionEndPoint": "https://smartcity.rbccps.org/api/{version}/follow?id=streetlight",
    "accessEndPoint": "https://smartcity.rbccps.org/api/{version}/db?id=streetlight",
    "publicationEndPoint": "https://smartcity.rbccps.org/api/{version}/publish?id=streetlight",
    "resourceAPIInfo": "https://rbccps-iisc.github.io"
   }

 This API key will be used to uniquely identify this device. It is recommended that the obtained key is "burnt" into the device after registration.

Error Responses
---------------

1. **Problem**: If the provider key is wrong
   
   .. code-block:: JSON
   
    {
     "message": "Invalid authentication credentials"
    }
 
   **Solution**: Use a valid provider API key (Refer <Konga>)


2. **Problem**: If the schema does not conform to any of the base schemas or if the catalogue server refuses to accept the schema in its present form
 
   .. code-block:: JSON
   
    {
     "Registration": "failure",
     "Reason": "uCat update Failure"
    }

   **Solution**: Please revisit the `link <https://github.com/rbccps-iisc/smart_cities_schemas>`_ on how to construct meaningful schemas.


3. **Problem**: If the ID you are using has already been used previously
   
   .. code-block:: JSON
   
    {
     "Registration": "failure",
     "Reason": "ID already used. Please Use a Unique ID for Registration."
    } 
   
   **Solution**: Try using another ID for the device and register again


4. **Problem**: If the schema is not a valid JSON

   .. code-block:: JSON
  
    {
     "Registration": "Failure",
     "Reason": "JSON parse error"
    }
  
   **Solution**: Use a tool like `JSONLint <https://jsonlint.com/>`_ to validate your JSON


5. **Problem**: If the security level used is outside the valid range

   .. code-block:: JSON
    
    {
     "Registration": "Failure",
     "Reason": "Security level must be between 1-5"
    }
  
   **Solution**: Use a security level between 1-5
