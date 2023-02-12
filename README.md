<a href="https://www.hyphen.earth/"><img src="https://github.com/Hyphen-Global-AG/hyphen-climate-framework/blob/main/.github/Hyphen_logo_final_hor.png?raw=true" alt="Hyphen Global AG" width="400"/></a>


# Hyphen Climate Portal

The Hyphen Climate API and Oracle Network allows organizations to interact with and verify GHG and ODS data provided by ICOS (Integrated Carbon Observation System - "https://www.icos-cp.eu/index.php/"), NOAA and other scientific organizations undearneath the WMO via the Blockchain. 

As more and more public sector guidance rolls out and regulatory oversight focuses on climate risk mitigation, the Hyphen Framework is ready to serve relevant GHG and ODS data to smart contracts automating and augmenting climate action.

Our Framework is built on a [REST](https://de.wikipedia.org/wiki/Representational_State_Transfer)-based [API](https://en.wikipedia.org/wiki/API#:~:text=An%20application%20programming%20interface%20%28API%29%20is%20a%20connection,connection%20or%20interface%20is%20called%20an%20API%20specification.), [Solidity](https://en.wikipedia.org/wiki/Solidity) Smart Contracts, Avalanche [Blockchain](https://en.wikipedia.org/wiki/Blockchain) and the [Chainlink](https://chain.link/) [Oracle](https://www.gemini.com/cryptopedia/what-is-chainlink-and-how-does-it-work) network.

Find more information on Hyphen Global and our initiatives on our website https://www.hyphen.earth/

<a href="https://chain.link/"><img src="https://coingawk.com/wp-content/uploads/2020/01/Chainlink_logo.jpg" alt="Chainlink" width="300"/></a>
<a href="https://www.icos-cp.eu/index.php/"><img src="https://www.icos-cp.eu/sites/default/files/2020-04/ICOS_logo_rgb_regular.png" alt="Integrated Carbon Observation System" width="200"/></a>

# Portal DataSets (Atmospheric Gases)

Gases: CH4(PPB), CO(PPM), CO2(PPM), N2O(PPM).  
Organisations: ICOS (https://www.icos-cp.eu/), NOAA (https://www.noaa.gov/).


# Oracles SmartContracts for Greenhouse Gases Daily Averages 

- Documentation Update outstanding (08/02/2023)

# Hyphen Climate Rest API

**Base Endpoint**

Endpoint: `https://portal-api.hyphen.earth/`

- All endpoints return a JSON object
- All endpoints return `200` code in a successful case

-------------------------------------------------------------------------------------------------------

### /api/station_gas_measured

**Description:** 
Returns information about what we have in our database:  
- averagingIntervals;  
- stations;  
- gases;  
- responsibleOrganizations;  
- gasesMeasured: **a list of measurements ranges for each gas/averagingInterval combination;**  
- stationGasMeasuredCombinations: a list of measurements ranges for each station/gas/averagingInterval combination.  

#### GET
##### Parameters: No parameters 

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_measured`

-------------------------------------------------------------------------------------------------------

### /api/stations

**Description:** Returns a list of all measurement stations

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| PageNumber | query | Number of a page | No | integer |
| PageSize | query | Items count per one page | No | integer |

##### Example 
Request URL: `https://portal-api.hyphen.earth/api/stations`

-------------------------------------------------------------------------------------------------------

### /api/stations/{id}

**Description:** Returns specific measurement station

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | Station ID number | Yes | long |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/stations/1007`

-------------------------------------------------------------------------------------------------------

### /api/layers

**Description:** Returns a list of all data objects.

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| themeName | query | Theme of climate data (like atmospheric, oceanic) | No | string |
| samplingHeight | query | Station measurement sampling height | No | double |
| time_from | query | Data acquisition start time | No | dateTime |
| time_to | query | Data acquisition end time | No | dateTime |
| station_id | query | Station ID number | No | long |
| dataTypeLabel | query | Descption of the data object | No | string |
| dataLevel | query | Data level | No | integer |
| PageNumber | query | Number of a page | No | integer |
| PageSize | query | Items count per one page | No | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/layers`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage

**Description:** Returns a daily average measurement

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| stationCode | query | Station code, e.g.: `HPB, WAO, ZEP, ZSF` | Yes | string |
| gasName | query | Gas name, e.g.: `CO2, CH4` | Yes | string |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `M`  | Yes | integer |
| day | query | Day, format: `D` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage?stationCode=HPB&gasName=CO2&year=2022&month=11&day=11`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_detailed

**Description:** Returns detailed daily average measurement 

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| stationCode | query | Station code, e.g.: `HPB, WAO, ZEP, ZSF` | Yes | string |
| gasName | query | Gas name, e.g.: `CO2, CH4` | Yes | string |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `M`  | Yes | integer |
| day | query | Day, format: `D` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_detailed?stationCode=HPB&gasName=CO2&year=2022&month=11&day=11`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_latest

**Description:** Returns the latest daily average measurement

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| stationCode | query | Station code, e.g.: `HPB, WAO, ZEP, ZSF` | Yes | string |
| gasName | query | Gas name, e.g.: `CO2, CH4` | Yes | string |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_latest?stationCode=HPB&gasName=CO2`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_latest_detailed

**Description:** Returns the detailed latest daily average measurement

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| stationCode | query | Station code, e.g.: `HPB, WAO, ZEP, ZSF` | Yes | string |
| gasName | query | Gas name, e.g.: `CO2, CH4` | Yes | string |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_latest_detailed?stationCode=HPB&gasName=CO2`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_combinations_oneStationAllGases_specifiedDate

**Description:** Returns a list of daily average measurements of specific station of all gases

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| stationCode | query | Station code, e.g.: `HPB, WAO, ZEP, ZSF` | Yes | string |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `M`  | Yes | integer |
| day | query | Day, format: `D` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_combinations_oneStationAllGases_specifiedDate?stationCode=HPB&year=2022&month=11&day=11`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_combinations_allStationsAllGases_specifiedDate

**Description:** Returns a list of daily average measurements of all stations of all gases

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `M`  | Yes | integer |
| day | query | Day, format: `D` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_combinations_allStationsAllGases_specifiedDate?year=2022&month=12&day=31`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_combinations_allStationsOneGas_specifiedDate

**Description:** Returns a list of daily average measurements of all stations of specific gas

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| gasName | query | Gas name, e.g.: `CO2, CH4` | Yes | string |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `M`  | Yes | integer |
| day | query | Day, format: `D` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_combinations_allStationsOneGas_specifiedDate?gasName=CH4&year=2022&month=11&day=11`
