+++
title = "Mapping Report"
pagetitle = "Hotel-X - Mapping Report"
description = "How to query your Hotel-x content mapping"
icon = "fa-book"
weight = 3
alwaysopen = false
isDirectory = false
+++

This page shows how to query Hotel-X content mapping using Insights-X API.

Access to https://api.travelgatex.com/

# Request Format

The request input is formed by 2 mandatory inputs: requestDate, mappingReport and 3 optional inputs: supplierCode_in, clientCode_in and accessCode_in. Below the possible values for each input:

* **Mandatory fields:**.
  * **requestDate:** Range of dates when the searches were done. 
    * **gte** Searches done after this date. (YYYY-MM-DD).
    * **lte** Searches done before this date. (YYYY-MM-DD).    

  * **mappingReport:** Type of report that will be requested. Below the possible values:
    * **RATE**
    * **BOARD**
    * **ROOM**
    * **HOTEL_ROOM**
    * **PROMOTION**

* **Optional fields:**
  * **supplierCode_in:** List of suppliers.
  * **clientCode_in:** List of clients.
  * **accessCode_in:** List of accesses.

## Example:
~~~json
{
  insights {
    hotelXMappingReport(
      where: {
        requestDate: { gte: "2020-02-02", lte: "2020-02-04" }
        mappingReport: BOARD
      }
    ) {
      data {
        url
      }
    }
  }
}

~~~ 
Include authorization header with your Api Key **or** Bearer.
~~~json
{
 "Authorization" :"Apikey 12345678-1234-1234-1234-1234567890"
}

~~~
~~~json
{
 "Authorization" :"Bearer fwlrijaeiwbaiopewnaoibwaiopbnaiu"
}

~~~

# Response Format

Results are given in a csv file with an URL from Google Cloud Storage. Log into a Google account might be required before download the file.

## Example:
~~~json
{
  "data": {
    "insights": {
      "hotelXMappingReport": {
        "data": {
          "url": "http://storage...../31965.csv"
        }
      }
    }
  }
}
~~~

# File Format (RATE / BOARD / ROOM / PROMOTION)

The file contains 6 columns separated by comma:

* **supplier** Supplier code. 
* **src_code** Suppliers item's code (rate/board/room/etc). 
* **src_description** Suppliers item's description (rate/board/room/etc). 
* **context** Context code to map. 
* **dst_code** Context code. This column will be empty when src_code wasn't found in mapping file.
* **last_hit** Date of last appearance. 
* **hits** Quantity of times that code was mapped. 

Field **src_description** is an array of json struct with next fields:

* **l** Language of returned description. 
* **d** Description returned by the supplier (rate/board/room/etc).

## Example:
~~~json
[
  {
    "l": "ES",
    "d": "Spanish description"
  },  
  {
    "l": "EN",
    "d": "English description"
  }
]
~~~

## Example:

| supplier | src\_code | src\_description | context | dst\_code  | last\_hit   | hits |
| :--------- | :--------- | :--------- | :--------- | :--------- | :--------- | :--------- |
| SUP1 | full | [{"l": "ES", "d": "Full Board"}] | CTX | FB | 2020-02-04 | 24565 |
| SUP1 | extra | [{"l": "ES", "d": "Extra Drinks"}] | CTX |  | 2020-02-03 | 284 |
| SUP2 | half\_board | [{"l": "ES", "d": "Half Board"}] | CTX | HB | 2020-02-02 | 2155 |
| SUP2 | all\_inclusive | [{"l": "ES", "d": "All Inclusive"}] | CTX | AI | 2020-02-04 | 27 |

# File Format (HOTEL_ROOM)

The file contains 10 columns separated by comma:

* **supplier** Supplier code. 
* **supplier_context** Supplier's context. 
* **supplier_hotel** Hotel's code using supplier context.
* **src_code** Supplier's room code. 
* **src_description** Supplier's room  description.
* **context** Context code to map. 
* **context_hotel** Hotel code using map's context. 
* **dst_code** Room code using map's context. This column will be empty when src_code wasn't found in mapping file.
* **last_hit** Date of last appearance. 
* **hits** Quantity of times that code was mapped. 

Field **src_description** is an array of json struct with next fields:

* **l** Language of returned description. 
* **d** Description returned by the supplier (rate/board/room/etc).

## Example:
~~~json
[
  {
    "l": "ES",
    "d": "Spanish description"
  },  
  {
    "l": "EN",
    "d": "English description"
  }
]
~~~

## Example:

| supplier | supplier\_context | supplier\_hotel | src\_code | src\_description | context | context\_hotel | dst\_code  | last\_hit   | hits |
| :--------- | :--------- | :--------- | :--------- | :--------- | :--------- | :--------- | :--------- | :--------- | :--------- |
| SUP1 | CTX1 | hot1 | D2 | [{"l": "ES", "d": "Double Room"}] | CTX | chot1 | D | 2020-02-04 | 24565 |
| SUP1 | CTX1 | hot1 | T3 | [{"l": "ES", "d": "Extra Drinks"}] | CTX | chot1 |  | 2020-02-03 | 284 |
| SUP1 | CTX1 | hot2 | D2 | [{"l": "ES", "d": "Half Board"}] | CTX | chot2 | D | 2020-02-02 | 2155 |
| SUP1 | CTX1 | hot2 | D2P | [{"l": "ES", "d": "All Inclusive"}] | CTX | chot2 | DP | 2020-02-04 | 27 |

Files can be downloaded directly from the browser.
