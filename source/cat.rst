Catalogue
=========

* **Summary**: The catalogue API is used to browse through the list of devices registered with the middleware.

Request
^^^^^^^

* **Endpoint**: ``https://localhost/catalog``

* **Method**: ``GET``

* **Security Scheme**: None, since it is a publicly accessible API meant for entity search and discovery

Response
^^^^^^^^

* ``200 OK``:

    - A list of devices registered with the middleware along with their schemas:

     .. code-block:: JSON

	{
	    "item-metadata": [{
			"rel": "urn:X-rbccps:rels:isContentType",
			"val": "application/vnd.rbccps.catalogue+json"
		},
		{
			"rel": "urn:X-rbccps:rels:hasDescription:en",
			"val": "Catalogue test"
		},
		{
			"rel": "urn:X-rbccps:rels:supportsSearch",
			"val": "urn:X-rbccps:search:simple"
		}
	],
	"items": [{
		"refCatalogueSchema": "cdx_base_staticThing.json",
		"id": "6663e818bdf179e8090a737c230241d8sensoragent",
		"tags": [
			"air quality",
			"pollution",
			"aqm",
			"aqi"
		],
		"refCatalogueSchemaRelease": "0.2.1",
		"latitude": {
			"value": 12.84534,
			"ontologyRef": "http://www.w3.org/2003/01/geo/wgs84_pos#"
		},
		"longitude": {
			"value": 77.665444,
			"ontologyRef": "http://www.w3.org/2003/01/geo/wgs84_pos#"
		},
		"owner": {
			"name": "ELCITA",
			"website": "https://elcita.in"
		},
		"geoLocation": {
			"address": "Infosys Avenue, Electronics City Phase 1, Electronic City, Bengaluru, Karnataka 560100",
			"city": "Bangalore"
		},
		"message_schemas": {
			"type": "object",
			"properties": {
				"observation_msg": {
					"schema": "http://json-schema.org/draft-07/schema#",
					"type": "object",
					"describes": "Observation messages from climo air quality monitor ",
					"direction": "fromThing",
					"priority": "low",
					"tags": [
						"air",
						"pollution",
						"SO2",
						"CO2",
						"CO",
						"NO",
						"NO2",
						"PM2.5",
						"PM10",
						"Humidity",
						"Temperature",
						"Ozone",
						"O",
						"Noise",
						"Light",
						"UV"
					],
					"sharing": "public",
					"required": [
						"climoID",
						"timestamp"
					],
					"properties": {
						"climoID": {
							"type": "string",
							"description": "Id for the aqm unit"
						},
						"timestamp": {
							"type": "number",
							"description": "EPOCH time (milli-seconds) for the inbound message"
						},
						"SENS_LIGHT": {
							"type": "number",
							"description": "Ambient illumination incident to the right side of the climo",
							"minimum": 0,
							"maximum": 188000,
							"units": "Lux"
						},
						"SENS_AIR_PRESSURE": {
							"type": "number",
							"description": "Air pressure, no resolutions given",
							"units": "bar"
						},
						"SENS_TEMPERATURE": {
							"type": "number",
							"description": "Ambient temperature",
							"minimum": -40,
							"maximum": 70,
							"units": "celcius"
						},
						"SENS_CARBON_DIOXIDE": {
							"type": "number",
							"description": "Atmospheric CO2",
							"minimum": 0,
							"maximum": 5000,
							"units": "ppm"
						},
						"SENS_RELATIVE_HUMIDITY": {
							"type": "number",
							"description": "Relative humidity",
							"minimum": 10,
							"maximum": 95,
							"units": "percentage"
						},
						"SENS_SOUND": {
							"type": "number",
							"description": "Ambient sound level, normalized with the hearing range",
							"minimum": 45,
							"maximum": 100,
							"units": "dBA"
						},
						"SENS_PM2P5": {
							"type": "number",
							"description": "Resolution: +/- 5 ug/m3",
							"minimum": 0,
							"maximum": 500,
							"units": "ug/m3"
						},
						"SENS_PM10": {
							"type": "number",
							"description": "Resolution: +/- 5 ug/m3",
							"minimum": 0,
							"maximum": 1000,
							"units": "ug/m3"
						},
						"SENS_NITROGEN_DIOXIDE": {
							"type": "number",
							"description": "Resolution: 10 ppb",
							"minimum": 0,
							"maximum": 300,
							"units": "ppb"
						},
						"SENS_CARBON_MONOXIDE": {
							"type": "number",
							"description": "Resolution: 100 ppb",
							"minimum": 0,
							"maximum": 31000,
							"units": "ppb"
						},
						"SENS_SULPHUR_DIOXIDE": {
							"type": "number",
							"description": "Resolution: 10 ppb",
							"minimum": 0,
							"maximum": 700,
							"units": "ppb"
						},
						"SENS_NITRIC_OXIDE": {
							"type": "number",
							"description": "Resolution: 10 ppb",
							"minimum": 0,
							"maximum": 300,
							"units": "ppb"
						},
						"SENS_OZONE": {
							"type": "number",
							"description": "Resolution: 10 ppb",
							"minimum": 0,
							"maximum": 400,
							"units": "ppb"
						},
						"SENS_ULTRA_VIOLET": {
							"type": "number",
							"description": "V up to 15 UVI ",
							"minimum": 0,
							"maximum": 15,
							"units": "UVI"
						},
						"AQI_SENS_PM2P5": {
							"type": "number",
							"description": "Region wide AQI Index for PM2_5",
							"units": "dimensionless"
						},
						"AQI_SENS_PM10": {
							"type": "number",
							"description": "Region wide AQI Index for PM10",
							"units": "dimensionless"
						},
						"AQI_SENS_NITROGEN_DIOXIDE": {
							"type": "number",
							"description": "Region wide AQI Index for NO2",
							"units": "dimensionless"
						},
						"AQI_SENS_CARBON_MONOXIDE": {
							"type": "number",
							"description": "Region wide AQI Index for CO",
							"units": "dimensionless"
						},
						"AQI_SENS_SULPHUR_DIOXIDE": {
							"type": "number",
							"description": "Region wide AQI Index for SO2",
							"units": "dimensionless"
						},
						"AQI_SENS_OZONE": {
							"type": "number",
							"description": "Region wide AQI Index for O3",
							"units": "dimensionless"
						}
					},
					"additionalProperties": false
				}
			},
			"additionalProperties": false
		}
	}]
	}

