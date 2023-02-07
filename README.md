<a href="https://www.hyphen.earth/"><img src="https://github.com/Hyphen-Global-AG/hyphen-climate-framework/blob/main/.github/Hyphen_logo_final_hor.png?raw=true" alt="Hyphen Global AG" width="400"/></a>


# Hyphen Climate API & Smart Contract Framework

The Hyphen Climate API and Smart Contract Framework allow organizations to interact with and verify GHG and ODS data provided by ICOS (Integrated Carbon Observation System - "https://www.icos-cp.eu/index.php/") and other scientific organizations via the Blockchain. 

As more and more public sector guidance rolls out and regulatory oversight focuses on climate risk mitigation, the Hyphen Framework is ready to serve relevant GHG and ODS data to smart contracts automating and augmenting climate action.

Our Framework is built on a [REST](https://de.wikipedia.org/wiki/Representational_State_Transfer)-based [API](https://en.wikipedia.org/wiki/API#:~:text=An%20application%20programming%20interface%20%28API%29%20is%20a%20connection,connection%20or%20interface%20is%20called%20an%20API%20specification.), [Solidity](https://en.wikipedia.org/wiki/Solidity) Smart Contracts, [Ethereum](https://en.wikipedia.org/wiki/Ethereum) [Blockchain](https://en.wikipedia.org/wiki/Blockchain) and the [Chainlink](https://chain.link/) [Oracle](https://www.gemini.com/cryptopedia/what-is-chainlink-and-how-does-it-work) network.

Find more information on Hyphen Global and our initiatives on our website https://www.hyphen.earth/

<a href="https://chain.link/"><img src="https://www.anyblockanalytics.com/wp-content/uploads/2019/12/Chainlink-v2.2.png" alt="Chainlink" width="300"/></a>
<a href="https://www.icos-cp.eu/index.php/"><img src="https://www.icos-cp.eu/sites/default/files/2020-04/ICOS_logo_rgb_regular.png" alt="Integrated Carbon Observation System" width="200"/></a>
<a href="https://ethereum.org/en/"><img src="https://logospng.org/download/ethereum/logo-ethereum-4096.png" alt="Ethereum" width="200"/></a>
# Quick Start

Our Framework allows to query and verify [atmospheric gas timeseries from ICOS](https://data.icos-cp.eu/portal/#%7B%22filterCategories%22%3A%7B%22project%22%3A%5B%22icos%22%5D%2C%22level%22%3A%5B1%2C2%5D%2C%22stationclass%22%3A%5B%22ICOS%22%5D%2C%22theme%22%3A%5B%22atmosphere%22%5D%7D%2C%22filterKeywords%22%3A%5B%22N2O%22%5D%7D) (Prototype).

**3 simple steps**
1. Query for a specific DataSet
2. Download Data
3. Verify file hash

# ICOS DataSets

- [N2O](https://en.wikipedia.org/wiki/Nitrous_oxide) / [ICOS Data](https://data.icos-cp.eu/portal/#%7B%22filterCategories%22%3A%7B%22project%22%3A%5B%22icos%22%5D%2C%22level%22%3A%5B1%2C2%5D%2C%22stationclass%22%3A%5B%22ICOS%22%5D%2C%22theme%22%3A%5B%22atmosphere%22%5D%7D%2C%22filterKeywords%22%3A%5B%22N2O%22%5D%7D) (Prototype)

# Consumer Smart Contract

COMMENT: we need to document all contracts and review what methods belong to what contract, wich ones are private (only for oracle owner / node operators) and which ones are for endconsumers. 

Contract Code (GIT): https://github.com/Hyphen-Global-AG/hyphen-climate-framework/blob/main/ClimateConsumer.sol

- Solidity version (pragma solidity ^0.8.7;)
- Compile with Remix (https://remix.ethereum.org/) using Injected Web3, set deployed address in remix (At Address) - 

**Hyphen Climate Framework Contract Address**

*NOTE 16/02/2022 - oracle contract addresses updated.

(Ethereum - Rinkeby)
> 0xD04f581A8B5fb464BCfFBc24f9719846d9071Bc3
Etherscan Rinkeby: [0xD04f581A8B5fb464BCfFBc24f9719846d9071Bc3](https://rinkeby.etherscan.io/address/0xD04f581A8B5fb464BCfFBc24f9719846d9071Bc3)

(Ethereum - Mainnet)
> 0x352e2178BdccB5306D3e42F3a593a0692d49319B
Etherscan Mainnet: [0x352e2178BdccB5306D3e42F3a593a0692d49319B](https://etherscan.io/address/0x352e2178BdccB5306D3e42F3a593a0692d49319B)

**Parameter Definitions**

| Parameter | Description | DataType |
| ------ | ------ | ------ |
| stationId | Id of measurement station | string | 
| heightId | measurement height | string | 
| startDate | measurement start date | string | 
| startTime | measurement end date | string | 
| endTime | measurement start time | string | 
| payment | measurement end time | uint256 | 
| requestId | Id of request | bytes32 | 
| callbackFunctionId | Id of callbackFunction | bytes4 | 
| expiration | expiration time | uint256 | 
| hash | FileHash | bytes32 | 
| JobId | Id of Job | string | 
| oracle | Oracle Address | address | 
| oracleFee | Oracle call fee amount | uint256 | 

**Contract Methods**

| Method | Description | Parameter (use in order!) |
| ------ | ------ | ------ |
| requestClimateHash | Returns file hash via Chainlink Oracle | stationId, heightId, startDate, endDate, startTime, endTime |
| getFileHashforParams | Returns the file hash after it has been delivered by Oracle | stationId, heightId, startDate, endDate, startTime, endTime |
| generateRequestHash | Generates a hash of input parameters | stationId, heightId, startDate, endDate, startTime, endTime |
| fullfillClimateHash* | Fullfills hash request | requestId, hash |
| cancelRequest | cancel the current request | requestId, payment, callbackFunctionId, expiration |
| setJobId | set the Job ID in the Chainlink node | jobId |
| setOracle | sets the Oracle for the contract | oracle |
| setOracleFee | sets the fee for the oracle call in LINK | oracleFee |
| transferOwnership (TBD) | transfer ownership to recipient's address | address |
| whitdrawLink (TBD) | transfer LINK tokens from this contract instance to reciepient's address | address |
| getChainlinkToken | get the address of the Chainlink token (rarely needed) | -- |
| hashes | map containing the relation between request and file hashes | -- |
| jobId | returns the Job ID | -- |
| oracle | returns contract oracle address | -- |
| ORACLE_PAYMENT | returns the fee for Chainlink usage in LINK | -- |
| owner | returns contract owner address | -- |
\* private methods

# Hyphen Climate Rest API

**Base Endpoint**

Endpoint: `https://portal-api.hyphen.earth/`

- All endpoints return a JSON object
- All endpoints return `200` code in a successful case

-------------------------------------------------------------------------------------------------------

### /api/stations

**Description:** Returns a list of all measurement stations

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| PageNumber | query | Number of a page | No | integer |
| PageSize | query | Amount of times per one page | No | integer |

##### Example 
Request URL: `https://portal-api.hyphen.earth/api/stations`

-------------------------------------------------------------------------------------------------------

### /api/stations/{id}

**Description:** Returns all measurement stations of specific station

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | Station ID number | Yes | long |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/stations/1007`

-------------------------------------------------------------------------------------------------------

### /api/layers

**Description:** Returns a list of all layers

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| themeName | query | Climate data type | No | string |
| samplingHeight | query | Station height | No | double |
| time_from | query | Time from | No | dateTime |
| time_to | query | Time to | No | dateTime |
| station_id | query | Station ID number | No | long |
| dataTypeLabel | query | Descption of the layer | No | string |
| dataLevel | query | Data level | No | integer |
| PageNumber | query | Number of a page | No | integer |
| PageSize | query | Amount of times per one page | No | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/layers`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage

**Description:** Returns a daily average measurement

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| cpmetaStationId | query | Station name: e.g. `HPB` | Yes | string |
| gasName | query | Gas name: e.g. `CO2, CH4, WAO, ZEP, ZSF` | Yes | string |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `MM`  | Yes | integer |
| day | query | Day, format: `DD` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage?cpmetaStationId=HPB&gasName=CO2&year=2022&month=11&day=11`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_detailed

**Description:** Returns detailed daily average measurement 

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| cpmetaStationId | query | Station name: e.g. `HPB` | Yes | string |
| gasName | query | Gas name: e.g. `CO2, CH4, WAO, ZEP, ZSF` | Yes | string |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `MM`  | Yes | integer |
| day | query | Day, format: `DD` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_detailed?cpmetaStationId=HPB&gasName=CO2&year=2022&month=11&day=11`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_latest

**Description:** Returns the latest daily average measurement

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| cpmetaStationId | query | Station name: e.g. `HPB` | Yes | string |
| gasName | query | Gas name: e.g. `CO2, CH4, WAO, ZEP, ZSF` | Yes | string |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_latest?cpmetaStationId=HPB&gasName=CO2`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_latest_detailed

**Description:** Returns the latest detailed daily average measurement

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| cpmetaStationId | query | Station name: e.g. `HPB` | Yes | string |
| gasName | query | Gas name: e.g. `CO2, CH4, WAO, ZEP, ZSF` | Yes | string |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_latest_detailed?cpmetaStationId=HPB&gasName=CO2`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_combinations_oneStationAllGases_specifiedDate

**Description:** Returns a list of daily average measurement of specific station of all gases

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| cpmetaStationId | query | Station name: e.g. `HPB` | Yes | string |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `MM`  | Yes | integer |
| day | query | Day, format: `DD` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_combinations_oneStationAllGases_specifiedDate?cpmetaStationId=HPB&year=2022&month=11&day=11`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_combinations_allStationsAllGases_specifiedDate

**Description:** Returns a list of daily average measurement of all stations of all gases

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `MM`  | Yes | integer |
| day | query | Day, format: `DD` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_combinations_allStationsAllGases_specifiedDate?year=2022&month=12&day=31`

-------------------------------------------------------------------------------------------------------

### /api/station_gas_allheights_dailyaverage_combinations_allStationsOneGas_specifiedDate

**Description:** Returns a list of daily average measurement of all stations of specific gases

#### GET
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| gasName | query | Gas name: e.g. `CO2, CH4, WAO, ZEP, ZSF` | Yes | string |
| year | query | Year, format: `YYYY` | Yes | integer |
| month | query | Month, format: `MM`  | Yes | integer |
| day | query | Day, format: `DD` | Yes | integer |

##### Example
Request URL: `https://portal-api.hyphen.earth/api/station_gas_allheights_dailyaverage_combinations_allStationsOneGas_specifiedDate?gasName=CH4&year=2022&month=11&day=11`
