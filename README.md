# Risk Score Key-Value Storage

## Overview

A Simple custom component capable of storing and querying data quickly at scale

## Getting Started

1. `git clone https://github.com/HarperDB/risk-score.git`
1. `cd risk-score`
1. `harperdb run .`

This assumes you have the Harper stack already installed. [Install Harper](https://docs.harperdb.io/docs/deployments/install-harperdb) globally.

## Usage

### Auth

Uses Basic auth passed in `Authorization` header

### Endpoints

| Endpoint                                                             | Description                                 |
| -------------------------------------------------------------------- | ------------------------------------------- |
| `/RisqTable`                                                         | Direct REST endpoint for the RisqTable table |
| `/risq`       | Allows PUT opperation using shorthand property keys                |

For a full description of what the REST API can do and how to use if your can refer to its [documentation](https://docs.harperdb.io/docs/developers/rest).

### Examples

##### *Upsert a new record.*

```
PUT /risq/bc01f3f7-5bda-4fdc-ad92-85a2cdf49d34

Headers:
Authorization: xxxxxxxxxxx

BODY: 
{
   "di": "d0c2a04e3c9d54b50e9f70b5d64d47e6a4c5c9c3e6f543a1a2f98cfa8c9d2e3f",
   "d": "allow",
   "r": 60
}

Response: 204 No Content
```

##### *Retrieve record by id.*

```
GET /risq/bc01f3f7-5bda-4fdc-ad92-85a2cdf49d34

Headers:
Authorization: xxxxxxxxxxx

Response: 200
{
    "deviceId": "d0c2a04e3c9d54b50e9f70b5d64d47e6a4c5c9c3e6f543a1a2f98cfa8c9d2e3f",
    "decision": "allow",
    "riskScore": 11,
    "correlationId": "bc01f3f7-5bda-4fdc-ad92-85a2cdf49d34"
}
```

## Data Model

### RisqTable Table

| Name                      | Description                                                                         |
| ------------------------- | ----------------------------------------------------------------------------------- |
| `correlationId` | ***(Primary Key; String)***  |
| `deviceId`         | ***(String)***  |
| `decision`                | ***(String)*** |
| `riskScore`                  | ***(Int)*** |

