# Smart Urban Heatmap Dokumentation <!-- omit in toc -->

[![de](https://img.shields.io/badge/lang-de-green.svg)](de)
[![en](https://img.shields.io/badge/lang-en-red.svg)](./)


This documentation describes the **Open-Data API** of the [Smart Urban Heatmap Bern Project](https://urban-heat.meteotest.io).  

The Smart Urban Heat Map is an initiative of the [Smart City Verein Bern](https://www.smartcity-bern.ch/) to visualize urban heat in the city and region of Bern. Valuable pioneering work has been done by the Climatology Group at the [Geographical Institute of the University of Bern (GIUB)](https://www.geography.unibe.ch/index_eng.html), which has been operating an urban measurement network since 2018, consisting of around 80 stations. The Smart City Verein Bern, together with the company [Abilium GmbH](https://www.abilium.io/), the [Bern University of Applied Sciences](https://www.bfh.ch/de/forschung/forschungsbereiche/public-sector-transformation/) and the company [Meteotest](https://meteotest.ch/), has extended this measuring network into the Bern region by around 40 measuring stations.

Based on this measurement network, the Smart Urban Heatmap API offers access to detailed city climate data for the region of Bern, Switzerland. Users can retrieve current measurements of temperature, relative humidity, and location metadata, as well as location bound time series data. The data provides valuable insights for urban planning and environmental studies.

The documentation is complemented by an [interactive OpenAPI specification](Swagger) and a [python notebook](python_examples.ipynb) which includes examples of how to request and visualize the data using python.  
The notebook can be run **locally or directly in the browser** using [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/JurekMueller/SUH_Bern_API_Doc/main?labpath=python_examples.ipynb)
or [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JurekMueller/SUH_Bern_API_Doc/blob/main/python_examples.ipynb).

**Licensing Information**  
The data from the API is available under the [Creative Commons Attribution License (CC-BY)](https://creativecommons.org/licenses/by/4.0/).  
Please ensure that you provide proper attribution when using or redistributing this data in your projects or applications.  
*Attribution Example:* Data provided by the Smart Urban Heatmap Project for Bern, Switzerland.

**Table of Contents**
- [Changelog](#changelog)
- [Stations, Sensors and Temperature Bias](#stations-sensors-and-temperature-bias)
- [Endpoints](#endpoints)
- [Codebook](#codebook)
- [Example Requests](#example-requests)

## Changelog

### API Version 1.0 <!-- omit in toc -->

This is the first Version of the Smart Urban Heatmap API published on the XX.09.2023.



## Stations, Sensors and Temperature Bias

## Endpoints

### Stations <!-- omit in toc -->

Retrieves location data including most recent measured value for:

* Temperature is in Celsius (°C).
* Relative Humidity is in percentage (%).

**URL:** https://urban-heat.meteotest.io/api/1.0/stations  
**Response Formats:** `GeoJSON` (default), `csv`  
**URL Parameter:**
  * XXX  

### Timeseries <!-- omit in toc -->
Retrieves time series based on locationID for:
* Temperature is in Celsius (°C).
* Relative Humidity is in percentage (%).

**URL:** https://urban-heat.meteotest.io/api/1.0/timeseries  
**Response Formats:** `JSON` (default), `csv`  
**URL Parameter:**
  * **locationID** (required): specifies from which location to return the timeseries
  * **timeFrom** (optional, default: "-24hours"): specifies start of timeseries (Examples: "-3days","-24hours","-30minutes", "2023-08-01T00:00:00Z")
  * **timeTo** (optional, default: "now"): specifies end of timeseries (Examples: "-3days","-24hours","-30minutes", "now", "2023-08-01T00:00:00Z")

## Codebook

### Stations <!-- omit in toc -->

- **coordinates**: Array representing the geographical coordinates (in WGS84) of the location (Latitude,Longitude) 
- **locationId**: Unique identifier for the location (Example: 0F40CBFEFFE70FFE)
- **locationName**: Name of the location (Example: "Sandrain-Bern")
- **altitude**: Altitude of the location in meters (Example: 542)
- **heightAboveGround**: Height above ground in meters (Example: 2)
- **locationDescription**: Brief description of the location (Example: "Messstation an Strassenlampe")
- **activeSince**: Date and time when the station became active (Example: "2023-06-01T12:00:00Z")
- **sensorType**: Identifier for the type of sensor (Example: 1)
- **dateObserved**: Date and time of the last measurement (Example: "2023-08-01T12:00:00Z")
- **temperature**: Last temperature measured at the location in °C (Example: 22.1)
- **relativeHumidity**: Last relative humidity measured at the location in % (Example: 12)
- **operator**: Name of the station's operator (Either "Smart City Verein Bern" or "Uni Bern GIUB")

### Timeseries <!-- omit in toc -->

- **dateObserved**: Date and time of the measurement (Example: "2023-08-01T12:00:00Z")
- **temperature**: Temperature measured at the location in °C (Example: 22.1)
- **relativeHumidity**: Relative humidity measured at the location in % (Example: 12)
- **sensorType**: Identifier for the type of sensor that did the measurement (Example: 1)

## Example Requests

### Request list of stations most recent measurements  <!-- omit in toc -->
`GET https://urban-heat.meteotest.io/api/1.0/stations`

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          47.545,
          8.927
        ]
      },
      "properties": {
        "locationId": 123,
        "locationName": "Bollwerk",
        "altitude": 540,
        "heightAboveGround": 10,
        "locationDescription": "Messstation an Strassenlampe",
        "activeSince": "2023-06-01T12:00:00Z",
        "sensorType": 1,
        "dateObserved": "2023-08-01T12:00:00Z",
        "temperature": 22.1,
        "relativeHumidity": 12,
        "apparentTemperature": 21
      }
    },
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          47.379,
          8.674
        ]
      },
      "properties": {
        "locationId": 124,
        "locationName": "Neubrückstrasse",
        "altitude": 559,
        "heightAboveGround": 10,
        "locationDescription": "Messstation in Kreisverkehr",
        "activeSince": "2023-06-01T12:00:00Z",
        "sensorType": 1,
        "dateObserved": "2023-08-01T12:00:00Z",
        "temperature": 22.1,
        "relativeHumidity": 12.3,
        "apparentTemperature": 21
      }
    }
  ]
}
```

### Request timeseries for a station  <!-- omit in toc -->

`GET https://urban-heat.meteotest.io/api/1.0/timeseries?locationId=D33FCBFEFFE70FFE&timeFrom=2023-08-01T00:00:00Z&timeTo=2023-08-31T23:00:00Z`

```json
EXAMPLE TO COME
```