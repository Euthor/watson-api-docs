# Table of Contents

1. [Overview](#overview)
2. [HTTP Statuses](#http-statuses)
3. [Authentication](#authentication)
4. Entities
    - [Customer](#customer)
    - [Customer Lists](#customer-lists)
        - [ID Card](#id-card)
        - [Address](#addresses)
        - [Communication Means](#communication-means)
        - [Wealth](#wealth)
        - [Annual Income](#annual-income)
        - [Counterparty](#counterparty)
        - [Financial Statement](#financial-statement)
        - [Country Presence](#country-presence)
        - [Screening Risks](#screening-risks)
    - [Risk Analysis](#risk-analysis)
    - [Review](#review)
    - [Risk Trail](#risk-trail)

## Overview

### Request Headers

All requests require 2 headers:

```js
"x-access-token": "replace-this-with-your-access-token"
"Content-Type": "application/json"
```

### URL placeholders

The URL's posted for entities in this documentation usually contain
placeholders. Placeholders in URLs are denoted by square brackets, so
when you see for example:

```
URL: /api/customer/[idInternalCustomerPerson]
Method: GET
```

you are expected to replace `[idInternalCustomer]` with the Internal Customer
Number of your Customer. An actual example would be:

```
URL: /api/customer/AC001
Method: GET
```

...which will retrieve the Customer with Internal Customer Number `AC001`.

## HTTP Statuses<a name="http-statuses" />

|Code|Text|Description|
|--- |--- |--- |
|200|OK|Success. There is response data as well.|
|204|No Content|Success. There is no response data.|
|400|Bad Request|The request was invalid, usually because the request contains invalid request body data. If this is the case, the response body will contain a message indicating the invalid properties and their issues.|
|401|Unauthorized|The x-access-token is not valid or the username/password do not match when logging-in.|
|403|Forbidden|The x-access-token is valid but the associated user does not have permissions for this action.|
|404|Not Found|The entity does not exist.|
|500|Server Error|The server encountered an error.|


## Authentication<a name="authentication" />

You authenticate *each* request by passing an `x-access-token` header with a
valid token.

You are expected to cycle the access token, by logging-in again,
every now and then (ideally every other day) to ensure that a compromised
token is not indefinitely valid.

To obtain a valid token:

Method: `POST`
URL: `/api/login`

Sample Request Body:

```js
{
  "username": "administrator",
  "password": "test"
}
```

## Customer<a name="customer" />

## Create Customer

Method: `POST`
URL: `/api/customer`

### Customer Person

Sample Request Body

```js
"details": {
  "dateBirth": "1965-02-01",
  "firstName": "John",
  "maidenName": "Sierra",
  "lastName": "Doe",
  "idCountryBirth": 137,
  "idCountryNationality": 137,
  "idCountryResidence": 137,
  "idGender": 3,
  "idMaritalStatus": 1,
  "nonFaceToFace": true,
  "profession": "Accountant"
},
"main": {
  "idCustomerStatus": 1,
  "idCustomerType": 1,
  "idInternalCustomer": "JD001",
  "idUserResponsibleOfficer": 1,
  "otherInfo": "Lorem Ipsum Comment",
  "relationshipStartDate": "2001-01-19",
  "relationshipEndDate": "2004-12-24"
}
```

### Customer Organisation

Sample Request Body

```js
"details": {
  "dateIncorporation": "2001-12-20",
  "idCountryActivity": 137,
  "idCountryDomiciliary": 137,
  "idCountryIncorporation": 137,
  "idIncorporationType": 1,
  "mainBusinessActivity": "Trading",
  "registeredName": "ACME Corporation LTD",
  "registrationNo": "CY123",
  "tradeName": null
},
"main": {
  "idCustomerStatus": 1,
  "idCustomerType": 2,
  "idInternalCustomer": "AC001",
  "idUserResponsibleOfficer": 1,
  "otherInfo": null,
  "referralAgent": null,
  "relationshipStartDate": "2001-01-19",
  "relationshipEndDate": null
}
```

## Read Customer

Method: `GET`
URL: `/api/customer/[idInternalCustomerPerson]`

## Update Customer

Method: `PUT`
URL: `/api/customer/[idInternalCustomerPerson]`

### Customer Person

Sample Request Body

```js
"details": {
  "profession": "Programmer"
},
"main": {
  "otherInfo": "Lorem Ipsum Comment 2"
}
```

### Customer Organisation

Sample Request Body

```js
"details": {
  "registrationNo": "CY-456"
},
"main": {
  "otherInfo": "Lorem Ipsum Comment 2"
}
```

## Delete Customer

Method: `DELETE`
URL: `/api/customer/[idInternalCustomerPerson]`

## Customer Lists<a name="customer-lists" />

## Customer ID Card<a name="id-card"/>

### Create ID Card

URL: `/api/customer/[idInternalCustomer]/id-card`
Method: `POST`

Sample Request Body

```js
[
  {
    "idIdCardType": 3,
    "number": "CY-JD-001",
    "expirationDate": "2080-01-04",
    "copy": true
  }
]
```

### Read ID Card

URL: `/api/customer/[idInternalCustomer]/id-card`
Method: `GET`

### Update ID Card

URL: `/api/customer/[idInternalCustomer]/id-card`
Method: `PUT`

Sample Request Body

```js
{
  "copy": false,
  "number": "CY-JD-002"
}
```

### Delete ID Card

URL: `/api/customer/[idInternalCustomer]/id-card`
Method: `DELETE`
## Customer Address<a name="addresses"/>

### Create Address

URL: `/api/customer/[idInternalCustomer]/addresses`
Method: `POST`

Sample Request Body

```js
[
  {
    "streetName": "13 Nelsonos Street",
    "city": "Nicosia",
    "postcode": "2029",
    "idCountry": 137,
    "verified": true
  }
]
```

### Read Address

URL: `/api/customer/[idInternalCustomer]/addresses`
Method: `GET`

### Update Address

URL: `/api/customer/[idInternalCustomer]/addresses`
Method: `PUT`

Sample Request Body

```js
{
  "streetName": "55 Fykardou Street",
  "city": "Nicosia",
  "postcode": "2010"
}
```

### Delete Address

URL: `/api/customer/[idInternalCustomer]/addresses`
Method: `DELETE`
## Customer Communication Means<a name="communication-means"/>

### Create Communication Means

URL: `/api/customer/[idInternalCustomer]/communication-means`
Method: `POST`

Sample Request Body

```js
[
  {
    "idCommunicationMeansType": 4,
    "value": "john@doe.com"
  }
]
```

### Read Communication Means

URL: `/api/customer/[idInternalCustomer]/communication-means`
Method: `GET`

### Update Communication Means

URL: `/api/customer/[idInternalCustomer]/communication-means`
Method: `PUT`

Sample Request Body

```js
{
  "value": "john@doe.eu"
}
```

### Delete Communication Means

URL: `/api/customer/[idInternalCustomer]/communication-means`
Method: `DELETE`
## Customer Wealth<a name="wealth"/>

### Create Wealth

URL: `/api/customer/[idInternalCustomer]/wealth`
Method: `POST`

Sample Request Body

```js
[
  {
    "idWealthScale": 1,
    "idWealthStatus": 1,
    "source": "Oil Investments"
  }
]
```

### Read Wealth

URL: `/api/customer/[idInternalCustomer]/wealth`
Method: `GET`

### Update Wealth

URL: `/api/customer/[idInternalCustomer]/wealth`
Method: `PUT`

Sample Request Body

```js
{
  "source": "Lottery Winnings"
}
```

### Delete Wealth

URL: `/api/customer/[idInternalCustomer]/wealth`
Method: `DELETE`
## Customer Annual Income<a name="annual-income"/>

### Create Annual Income

URL: `/api/customer/[idInternalCustomer]/annual-income`
Method: `POST`

Sample Request Body

```js
[
  {
    "idAnnualIncomeScale": 1,
    "idAnnualIncomeStatus": 1,
    "source": "Oil Investments"
  }
]
```

### Read Annual Income

URL: `/api/customer/[idInternalCustomer]/annual-income`
Method: `GET`

### Update Annual Income

URL: `/api/customer/[idInternalCustomer]/annual-income`
Method: `PUT`

Sample Request Body

```js
{
  "source": "Lottery Winnings"
}
```

### Delete Annual Income

URL: `/api/customer/[idInternalCustomer]/annual-income`
Method: `DELETE`
## Customer Counterparty<a name="counterparty"/>

### Create Counterparty

URL: `/api/customer/[idInternalCustomer]/counterparty`
Method: `POST`

Sample Request Body

```js
[
  {
    "counterpartName": "Mary Jane",
    "idCountry": 137,
    "idFundType": 1,
    "comments": "Lorem Ipsum"
  }
]
```

### Read Counterparty

URL: `/api/customer/[idInternalCustomer]/counterparty`
Method: `GET`

### Update Counterparty

URL: `/api/customer/[idInternalCustomer]/counterparty`
Method: `PUT`

Sample Request Body

```js
{
  "comments": "Lorem Ipsum Dolor Sit Amet"
}
```

### Delete Counterparty

URL: `/api/customer/[idInternalCustomer]/counterparty`
Method: `DELETE`
## Customer Financial Statement<a name="financial-statement"/>

### Create Financial Statement

URL: `/api/customer/[idInternalCustomer]/financial-statement`
Method: `POST`

Sample Request Body

```js
[
  {
    "copy": true,
    "idStatementType": 1,
    "income": "500000.00",
    "year": 2005
  }
]
```

### Read Financial Statement

URL: `/api/customer/[idInternalCustomer]/financial-statement`
Method: `GET`

### Update Financial Statement

URL: `/api/customer/[idInternalCustomer]/financial-statement`
Method: `PUT`

Sample Request Body

```js
{
  "year": 2006
}
```

### Delete Financial Statement

URL: `/api/customer/[idInternalCustomer]/financial-statement`
Method: `DELETE`
## Customer Country Presence<a name="country-presence"/>

### Create Country Presence

URL: `/api/customer/[idInternalCustomer]/country-presence`
Method: `POST`

Sample Request Body

```js
[
  {
    "idCountry": 1,
    "year": 2005
  }
]
```

### Read Country Presence

URL: `/api/customer/[idInternalCustomer]/country-presence`
Method: `GET`

### Update Country Presence

URL: `/api/customer/[idInternalCustomer]/country-presence`
Method: `PUT`

Sample Request Body

```js
{
  "year": 2006
}
```

### Delete Country Presence

URL: `/api/customer/[idInternalCustomer]/country-presence`
Method: `DELETE`
## Customer Screening Risks<a name="screening-risks"/>

### Create Screening Risks

URL: `/api/customer/[idInternalCustomer]/screening-risks`
Method: `POST`

Sample Request Body

```js
[
  {
    "idScreeningRiskType": 1,
    "full_name": "John Sierra Doe",
    "score": 97,
    "inspected": true,
    "confirmed": false,
    "manual_addition": true
  }
]
```

### Read Screening Risks

URL: `/api/customer/[idInternalCustomer]/screening-risks`
Method: `GET`

### Update Screening Risks

URL: `/api/customer/[idInternalCustomer]/screening-risks`
Method: `PUT`

Sample Request Body

```js
{
  "confirmed": true
}
```

### Delete Screening Risks

URL: `/api/customer/[idInternalCustomer]/screening-risks`
Method: `DELETE`

## Risk Analysis<a name="risk-analysis" />

URL: `/api/customer/[idInternalCustomerPerson]/risk`
Method: `GET`

## Review<a name="review" />

URL: `/api/customer/[idInternalCustomer]/reviews`
Method: `GET`

## Risk Trail<a name="risk-trail" />

### Read Risk Trails

URL: `/api/customer/[idInternalCustomer]/risk-trails`
Method: `GET`

### Read Last Risk Trail

URL: `/api/customer/[idInternalCustomer]/risk-trails?limits=1`
Method: `GET`

### Update/Approve Risk Trail

URL: `/api/customer/risk-trails/[idRiskTrail]`
Method: `GET`

Sample Request Body:

```js
{
  idApprovalStatus: 1,
  idRiskType: 1,
  comments: 'Lorem Ipsum'
}
```
