## Table of Contents

1. [Overview](#overview)
    - [Request Headers](#request-headers)
    - [URL placeholders](#url-placeholders)
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

### Request Headers<a name="request-headers" />

All requests require 2 headers:

```js
"x-access-token": "replace-this-with-your-access-token"
"Content-Type": "application/json"
```

### URL placeholders<a name="url-placeholders" />

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

Sample Response:

```js
{
    "success": true,
    "token": "eyJhbGciOiJIUzI1N..."
}
```

## Customer<a name="customer" />

## Create Customer

Method: `POST`
URL: `/api/customer`

### Customer Person

Sample Request Body

```js
{
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
}
```

### Customer Organisation

Sample Request Body

```js
{
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
}
```

Sample Response for both Individual and Organisation:
```js
{
    "idAuditTrail": 17,
    "idRiskTrail": 12
}
```

## Read Customer

Method: `GET`
URL: `/api/customer/[idInternalCustomerPerson]`

Sample Response:

```js
{
    "singles": {
        "main": {
            "idCustomer": 3,
            "idUserLastModified": 2,
            "idInternalCustomer": "200",
            "relationshipStartDate": "2017-02-01",
            "relationshipEndDate": null,
            "referralAgent": null,
            "otherInfo": null,
            "idCustomerStatus": 1,
            "idCustomerType": 1,
            "idUserResponsibleOfficer": 2,
            "idUser": 5,
            "printName": "200"
        },
        "details": {
            "idCustomer": 3,
            "firstName": "John",
            "maidenName": null,
            "lastName": "Doe",
            "dateBirth": "1940-11-12",
            "nonFaceToFace": false,
            "idCountryNationality": 137,
            "idCountryBirth": 137,
            "idCountryResidence": 137,
            "idGender": 1,
            "idMaritalStatus": 6,
            "profession": null
        }
    },
    "lists": {
        "addresses": {
            "contents": [
                {
                    "idAddress": 1,
                    "idCustomer": 3,
                    "idCountry": 137,
                    "streetName": "Makariou",
                    "postcode": "4787",
                    "city": "Nicosia",
                    "filename": " ",
                    "verified": false,
                    "id": 1
                }
            ],
            "deletedRows": [],
            "id": "idAddress"
        },
        "screeningRisks": {
            "contents": [],
            "deletedRows": [],
            "id": "idScreeningRisk"
        },
        "communicationMeans": {
            "contents": [
                {
                    "idCommunicationMeans": 136,
                    "idCommunicationMeansType": 1,
                    "value": "99999999",
                    "idCustomer": 3,
                    "id": 1
                },
                {
                    "idCommunicationMeans": 7,
                    "idCommunicationMeansType": 4,
                    "value": "test.email@email.com",
                    "idCustomer": 3,
                    "id": 7
                }
            ],
            "deletedRows": [],
            "id": "idCommunicationMeans"
        },
        "annualIncomeEntries": {
            "contents": [
                {
                    "idAnnualIncome": 1,
                    "source": "Salesperson",
                    "idAnnualIncomeScale": 2,
                    "idAnnualIncomeStatus": 1,
                    "idCustomer": 3,
                    "id": 1
                }
            ],
            "deletedRows": [],
            "id": "idAnnualIncome"
        },
        "stakesOut": {
            "contents": [],
            "deletedRows": [],
            "id": "idStake"
        },
        "rolesOut": {
            "contents": [],
            "deletedRows": [],
            "id": "idCustomerAssociation"
        },
        "wealthEntries": {
            "contents": [],
            "deletedRows": [],
            "id": "idWealth"
        },
        "documents": {
            "contents": [],
            "deletedRows": [],
            "id": "idDocument"
        },
        "idCards": {
            "contents": [
                {
                    "idIdCard": 2,
                    "idIdCardType": 4,
                    "idCustomer": 3,
                    "number": "624323",
                    "filename": null,
                    "copy": true,
                    "expirationDate": "2020-11-25",
                    "id": 2
                }
            ],
            "deletedRows": [],
            "id": "idIdCard"
        },
        "events": {
            "contents": [],
            "deletedRows": [],
            "id": "idEvent"
        }
    },
    "checkedLists": {
        "checkedDocuments": {
            "contents": [ 
					1,
					5
				],
            "added": [],
            "removed": [],
            "listId": "npkxth",
            "types": [
                {
                    "id": 1,
                    "name": "Reference letter"
                },
                {
                    "id": 2,
                    "name": "Due Diligence QUESTIONAIRE"
                },
                {
                    "id": 3,
                    "name": "Signature"
                },
                {
                    "id": 4,
                    "name": "World Compliance Questionnaire"
                },
                {
                    "id": 5,
                    "name": "Tax Declaration"
                },
                {
                    "id": 6,
                    "name": "Memorandum and Articles of Association"
                },
                {
                    "id": 7,
                    "name": "Group/ Organization Chart"
                },
                {
                    "id": 8,
                    "name": "Certificate of directors"
                },
                {
                    "id": 9,
                    "name": "Certificate of shareholders"
                },
                {
                    "id": 10,
                    "name": "Certificate of registered office"
                },
                {
                    "id": 11,
                    "name": "Certificate of good standing"
                },
                {
                    "id": 12,
                    "name": "Trust deed"
                },
                {
                    "id": 13,
                    "name": "Board resolution"
                },
                {
                    "id": 14,
                    "name": "Engagement letter"
                },
                {
                    "id": 15,
                    "name": "Company relationship form"
                }
            ]
        },
        "checkedActivityRisks": {
            "contents": [],
            "added": [],
            "removed": [],
            "listId": "kenpiu",
            "types": [
                {
                    "id": 1,
                    "name": "Art Dealer"
                },
                {
                    "id": 2,
                    "name": "High Value transactions"
                },
                {
                    "id": 3,
                    "name": "Precious stones"
                },
                {
                    "id": 4,
                    "name": "High Risk trading / Casino gaming"
                },
                {
                    "id": 5,
                    "name": "Internet based business"
                },
                {
                    "id": 6,
                    "name": "Cash based business"
                },
                {
                    "id": 7,
                    "name": "Electronic Money Institution"
                },
                {
                    "id": 8,
                    "name": "Business generating high volumes of cash"
                },
                {
                    "id": 9,
                    "name": "Money Service Business"
                },
                {
                    "id": 10,
                    "name": "Art Dealer"
                },
                {
                    "id": 11,
                    "name": "Precious stones"
                },
                {
                    "id": 12,
                    "name": "High risk trading / Casino gaming"
                },
                {
                    "id": 13,
                    "name": "Internet based business"
                },
                {
                    "id": 14,
                    "name": "Cash based business"
                },
                {
                    "id": 15,
                    "name": "Electronic Money Institution"
                },
                {
                    "id": 16,
                    "name": "High Value transactions"
                },
                {
                    "id": 17,
                    "name": "Money Service Business"
                },
                {
                    "id": 18,
                    "name": "Business generating high volumes of cash"
                },
                {
                    "id": 19,
                    "name": "Bearer Shares"
                }
            ]
        },
        "checkedBehaviorRisks": {
            "contents": [
				3,
				5
			],
            "added": [],
            "removed": [],
            "listId": "sdvfkd",
            "types": [
                {
                    "id": 1,
                    "name": "Frequent changes of address"
                },
                {
                    "id": 2,
                    "name": "Avoidance of authorities"
                },
                {
                    "id": 3,
                    "name": "Difficult to reach"
                },
                {
                    "id": 4,
                    "name": "Criminal proceedings"
                },
                {
                    "id": 5,
                    "name": "Unwillingness to provide (KYC) documentation/information requested"
                },
                {
                    "id": 6,
                    "name": "Unwillingness to provide details on source of funds"
                },
                {
                    "id": 7,
                    "name": "Provides unusual suspicious ID docs that cannot be easily verified"
                },
                {
                    "id": 8,
                    "name": "Client acting nervous"
                },
                {
                    "id": 9,
                    "name": "Client in depth knowledge of AML requirements"
                },
                {
                    "id": 10,
                    "name": "Frequent changes of address"
                },
                {
                    "id": 11,
                    "name": "Reluctant to provide information"
                },
                {
                    "id": 12,
                    "name": "Not clear business activity"
                },
                {
                    "id": 13,
                    "name": "Difficult to reach"
                },
                {
                    "id": 14,
                    "name": "Avoidance of authorities"
                }
            ]
        },
        "checkedEnhancedChecks": {
            "contents": [
                3
            ],
            "added": [],
            "removed": [],
            "listId": "pehsld",
            "types": [
                {
                    "id": 1,
                    "name": "Second Identification Document"
                },
                {
                    "id": 2,
                    "name": "Registered Mail with required response"
                },
                {
                    "id": 3,
                    "name": "Called customer at home phone number"
                },
                {
                    "id": 4,
                    "name": "Home visit"
                },
                {
                    "id": 5,
                    "name": "Visited their offices"
                },
                {
                    "id": 6,
                    "name": "Lawyer Certification"
                },
                {
                    "id": 7,
                    "name": "Received Apostilled documents"
                },
                {
                    "id": 8,
                    "name": "Called at their offices"
                },
                {
                    "id": 9,
                    "name": "Visited their website"
                }
            ]
        }
    }
}
```

## Update Customer

Method: `PUT`
URL: `/api/customer/[idInternalCustomerPerson]`

### Customer Person

Sample Request Body

```js
{
  "details": {
    "profession": "Programmer"
  },
  "main": {
    "otherInfo": "Lorem Ipsum Comment 2"
  }
}
```

### Customer Organisation

Sample Request Body

```js
{
  "details": {
    "registrationNo": "CY-456"
  },
  "main": {
    "otherInfo": "Lorem Ipsum Comment 2"
  }
}
```

Sample Response for both Individual and Organisation:
```js
{
    "idAuditTrail": 21,
    "idRiskTrail": 14
}
```


## Delete Customer

Method: `DELETE`
URL: `/api/customer/[idInternalCustomerPerson]`

The response has no body (empty)

## Customer Lists<a name="customer-lists" />

Customer Lists can be passed an Array with 1 **or more** elements. For brevity
only 1 element is passed in the sample request bodies for the following lists.

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

Sample Response

```js
{
    "idAuditTrail": 30,
    "idRiskTrail": 13
}
```

### Read ID Card

URL: `/api/customer/[idInternalCustomer]/id-card`
Method: `GET`

Sample Response:

```js
[
    {
        "idIdCard": 4,
        "idIdCardType": 4,
        "idCustomer": 5,
        "number": "704473",
        "filename": null,
        "copy": false,
        "expirationDate": "2018-04-07",
        "id": 4
    },
    {
        "idIdCard": 7,
        "idIdCardType": 2,
        "idCustomer": 5,
        "number": "12345",
        "filename": null,
        "copy": true,
        "expirationDate": "2020-01-01",
        "id": 7
    }
]
```


### Update ID Card

URL: `/api/customer/[idInternalCustomer]/id-card/[idIdCard]`
Method: `PUT`

Sample Request Body

```js
{
  "copy": false,
  "number": "CY-JD-002"
}
```

Sample Response

```js

{
    "idAuditTrail": 32,
    "idRiskTrail": 13
}
```

### Delete ID Card

URL: `/api/customer/[idInternalCustomer]/id-card/[idIdCard]`
Method: `DELETE`

Sample Response

```js

{
    "idAuditTrail": 55,
    "idRiskTrail": 26
}
```

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


Sample Response

```js
{
    "idAuditTrail": 35,
    "idRiskTrail": 15
}
```


### Read Address

URL: `/api/customer/[idInternalCustomer]/addresses`
Method: `GET`


Sample Response

```js
[
    {
        "idAddress": 2,
        "idCustomer": 4,
        "idCountry": 137,
        "streetName": "Digeni Akrita",
        "postcode": "4498",
        "city": "Limassol",
        "filename": " ",
        "verified": false,
        "id": 2
    },
    {
        "idAddress": 6,
        "idCustomer": 4,
        "idCountry": 137,
        "streetName": "Mpizaniou",
        "postcode": "4493",
        "city": "Limassol",
        "filename": null,
        "verified": true,
        "id": 6
    }
]
```

### Update Address

URL: `/api/customer/[idInternalCustomer]/addresses/[idAddress]`
Method: `PUT`

Sample Request Body

```js
{
  "streetName": "55 Fykardou Street",
  "postcode": "2010",
  "verified": false
}
```

Sample Response:

```js
{
    "idAuditTrail": 37,
    "idRiskTrail": 15
}
```

### Delete Address

URL: `/api/customer/[idInternalCustomer]/addresses/[idAddress]`
Method: `DELETE`

Sample Response:

```js
{
    "idAuditTrail": 39,
    "idRiskTrail": 15
}
```

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

Sample Response

```js
{
    "idAuditTrail": 40,
    "idRiskTrail": 15
}
```

### Read Communication Means

URL: `/api/customer/[idInternalCustomer]/communication-means`
Method: `GET`

Sample Response

```js
[
    {
        "idCommunicationMeans": 8,
        "idCommunicationMeansType": 1,
        "value": "99999999",
        "idCustomer": 4,
        "id": 8
    },
    {
        "idCommunicationMeans": 10,
        "idCommunicationMeansType": 3,
        "value": "98561898",
        "idCustomer": 4,
        "id": 10
    },
    {
        "idCommunicationMeans": 36,
        "idCommunicationMeansType": 4,
        "value": "john@doe.com",
        "idCustomer": 4,
        "id": 36
    }
]
```

### Update Communication Means

URL: `/api/customer/[idInternalCustomer]/communication-means/[idCommunicationMeans]`
Method: `PUT`

Sample Request Body

```js
{
  "value": "john@doe.eu"
}
```

Sample Response

```js
{
    "idAuditTrail": 41,
    "idRiskTrail": 15
}
```

### Delete Communication Means

URL: `/api/customer/[idInternalCustomer]/communication-means/[idCommunicationMeans]`
Method: `DELETE`

Sample Response

```js
{
    "idAuditTrail": 42,
    "idRiskTrail": 15
}
```


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

Sample Response

```js
{
    "idAuditTrail": 43,
    "idRiskTrail": 15
}
```


### Read Wealth

URL: `/api/customer/[idInternalCustomer]/wealth`
Method: `GET`

Sample Response

```js
[
    {
        "idWealth": 1,
        "idCustomer": 4,
        "idWealthScale": 6,
        "idWealthStatus": 1,
        "source": "Oil Investments",
        "id": 1
    },
    {
        "idWealth": 2,
        "idCustomer": 4,
        "idWealthScale": 2,
        "idWealthStatus": 2,
        "source": "Inheritance",
        "id": 2
    }
]
```

### Update Wealth

URL: `/api/customer/[idInternalCustomer]/wealth/[idWealth]`
Method: `PUT`

Sample Request Body

```js
{
  "source": "Lottery Winnings"
}
```

Sample Response

```js
{
    "idAuditTrail": 46,
    "idRiskTrail": 15
}
```

### Delete Wealth

URL: `/api/customer/[idInternalCustomer]/wealth/[idWealth]`
Method: `DELETE`

Sample Response

```js
{
    "idAuditTrail": 47,
    "idRiskTrail": 16
}
```

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

Sample Response

```js
{
    "idAuditTrail": 48,
    "idRiskTrail": 16
}
```

### Read Annual Income

URL: `/api/customer/[idInternalCustomer]/annual-income`
Method: `GET`

Sample Response

```js
[
    {
        "idAnnualIncome": 2,
        "source": "Politician",
        "idAnnualIncomeScale": 2,
        "idAnnualIncomeStatus": 1,
        "idCustomer": 4,
        "id": 2
    },
    {
        "idAnnualIncome": 6,
        "source": "Oil Investments",
        "idAnnualIncomeScale": 1,
        "idAnnualIncomeStatus": 1,
        "idCustomer": 4,
        "id": 6
    }
]
```

### Update Annual Income

URL: `/api/customer/[idInternalCustomer]/annual-income/[idAnnualIncome]`
Method: `PUT`

Sample Request Body

```js
{
  "source": "Lottery Winnings"
}
```

Sample Response:

```js
{
    "idAuditTrail": 49,
    "idRiskTrail": 17
}
```

### Delete Annual Income

URL: `/api/customer/[idInternalCustomer]/annual-income[idAnnualIncome]`
Method: `DELETE`

Sample Response:

```js
{
    "idAuditTrail": 53,
    "idRiskTrail": 17
}
```

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
  },
  {
    "counterpartName": "John Doe",
    "idCountry": 128,
    "idFundType": 2,
    "comments": "The comments"
  }
]
```

Sample Response:

```js
{
    "idAuditTrail": 54,
    "idRiskTrail": 18
}
```

### Read Counterparty

URL: `/api/customer/[idInternalCustomer]/counterparty`
Method: `GET`

Sample Response:

```js
[
    {
        "idFund": 1,
        "idFundType": 1,
        "idCountry": 137,
        "comments": "Lorem Ipsum",
        "counterpartName": "Mary Jane",
        "id": 1
    },
    {
        "idFund": 2,
        "idFundType": 2,
        "idCountry": 128,
        "comments": "The comments",
        "counterpartName": "John Doe",
        "id": 2
    }
]
```

### Update Counterparty

URL: `/api/customer/[idInternalCustomer]/counterparty/[idFund]`
Method: `PUT`

Sample Request Body

```js
{
  "comments": "Lorem Ipsum Dolor Sit Amet"
}
```

Sample Response:

```js
{
    "idAuditTrail": 55,
    "idRiskTrail": 18
}
```

### Delete Counterparty

URL: `/api/customer/[idInternalCustomer]/counterparty/[idFund]`
Method: `DELETE`

Sample Response:

```js
{
    "idAuditTrail": 56,
    "idRiskTrail": 18
}
```

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

Sample Response:

```js
{
    "idAuditTrail": 56,
    "idRiskTrail": 18
}
```

### Read Financial Statement

URL: `/api/customer/[idInternalCustomer]/financial-statement`
Method: `GET`

Sample Response:

```js
[
    {
        "idStatement": 1,
        "idStatementType": 1,
        "year": 2005,
        "income": 500000,
        "expenses": null,
        "copy": true,
        "id": 1
    }
]
```

### Update Financial Statement

URL: `/api/customer/[idInternalCustomer]/financial-statement/[idStatement]`
Method: `PUT`

Sample Request Body

```js
{
  "year": 2006
}
```

Sample Response:

```js
{
    "idAuditTrail": 58,
    "idRiskTrail": 18
}
```

### Delete Financial Statement

URL: `/api/customer/[idInternalCustomer]/financial-statement/[idStatement]`
Method: `DELETE`

Sample Response:

```js
{
    "idAuditTrail": 60,
    "idRiskTrail": 19
}
```

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

Sample Response:

```js
{
    "idAuditTrail": 61,
    "idRiskTrail": 19
}
```

### Read Country Presence

URL: `/api/customer/[idInternalCustomer]/country-presence`
Method: `GET`

Sample Response:

```js
[
    {
        "idCountryPresence": 1,
        "idCountry": 1,
        "year": 2005,
        "id": 1
    },
    {
        "idCountryPresence": 3,
        "idCountry": 90,
        "year": 2009,
        "id": 3
    }
]
```

### Update Country Presence

URL: `/api/customer/[idInternalCustomer]/country-presence/[idCountryPresence]`
Method: `PUT`

Sample Request Body

```js
{
  "year": 2006
}
```

Sample Response:

```js
{
    "idAuditTrail": 65,
    "idRiskTrail": 19
}
```

### Delete Country Presence

URL: `/api/customer/[idInternalCustomer]/country-presence/[idCountryPresence]`
Method: `DELETE`

Sample Response:

```js
{
    "idAuditTrail": 66,
    "idRiskTrail": 20
}
```

## Customer Screening Risks<a name="screening-risks"/>

### Create Screening Risks

URL: `/api/customer/[idInternalCustomer]/screening-risks`
Method: `POST`

Sample Request Body

```js
[
  {
    "idScreeningRiskType": 1,
    "full_name": "Donald Trump",
    "score": 97,
    "inspected": true,
    "confirmed": false,
    "manual_addition": true
  }
]
```

Sample Response:

```js
{
    "idAuditTrail": 69,
    "idRiskTrail": 21
}
```

### Read Screening Risks

URL: `/api/customer/[idInternalCustomer]/screening-risks`
Method: `GET`


Sample Response:

```js
[
    {
        "idScreeningRisk": 3,
        "idCustomer": 15,
        "idScreeningRiskType": 2,
        "identifier": "10101729617",
        "score": 100,
        "inspected": true,
        "confirmed": false,
        "type": "PEP List",
        "full_name": "Donald John Jr. Trump",
        "json": "{\"ID\":\"10101729617\",\"Relative_ID\":\"10101192552\",\"Title\":\"Mr.\",\"Gender\":\"Male\",\"First_Name\":\"Donald John Jr.\",\"Last_Name\":\"Trump\",\"Full_Name\":\"\",\"Other_Names\":\"Trump, Don\",\"Alternative_Script\":\"\",\"Function\":\"Relatives of High Officials, Son of Donald John Trump, CATEGORY: Close Relatives of PEPs\",\"Category\":\"Close Relatives of PEPs\",\"DOB\":\"31.12.1977\",\"POB\":\"Manhattan, New York, United States of America\",\"Country\":\"United States of America\",\"Code\":\"USA\",\"Additional_Information\":\"\",\"Country_Of_Origin\":\"\",\"Country_Of_Activity\":\"\"}",
        "md5": "3dafa6c51cd6b6af7d1e1c66fcbc3002",
        "manual_addition": false,
        "id": 3
    },
    {
        "idScreeningRisk": 4,
        "idCustomer": 15,
        "idScreeningRiskType": 2,
        "identifier": "10101192552",
        "score": 100,
        "inspected": true,
        "confirmed": true,
        "type": "PEP List",
        "full_name": "Donald John Trump",
        "json": "{\"ID\":\"10101192552\",\"Relative_ID\":\"10101192552\",\"Title\":\"Mr.\",\"Gender\":\"Male\",\"First_Name\":\"Donald John\",\"Last_Name\":\"Trump\",\"Full_Name\":\"\",\"Other_Names\":\"\",\"Alternative_Script\":\"\",\"Function\":\"Executive Office of the President, White House Office, President of the United States of America, CATEGORY: Heads of State, Major Government Offices and Support; OTHER FUNCTION: Armed Forces, Commander-in-Chief, CATEGORY: Military; OTHER FUNCTION: Executive Office of the President, National Security Council, Chairperson, CATEGORY: Heads of State, Major Government Offices and Support\",\"Category\":\"Heads of State, Major Government Offices and Support; Military\",\"DOB\":\"14.06.1946\",\"POB\":\"Queens, New York City, New York, United States of America\",\"Country\":\"United States of America\",\"Code\":\"USA\",\"Additional_Information\":\"Net Worth: $2.9 B; Source: television, real estate\",\"Country_Of_Origin\":\"\",\"Country_Of_Activity\":\"\"}",
        "md5": "9104e278e9b2458b2686e1841472f541",
        "manual_addition": false,
        "id": 4
    },
    {
        "idScreeningRisk": 6,
        "idCustomer": 15,
        "idScreeningRiskType": 1,
        "identifier": null,
        "score": 100,
        "inspected": true,
        "confirmed": false,
        "type": null,
        "full_name": "Donald Trump",
        "json": null,
        "md5": null,
        "manual_addition": true,
        "id": 6
    }
]
```

### Update Screening Risks

URL: `/api/customer/[idInternalCustomer]/screening-risks/[idScreeningRisk]`
Method: `PUT`

Sample Request Body

```js
{
  "confirmed": true
}
```

Sample Response:

```js
{
    "idAuditTrail": 71,
    "idRiskTrail": 21
}
```

### Delete Screening Risks

URL: `/api/customer/[idInternalCustomer]/screening-risks/[idScreeningRisk]`
Method: `DELETE`

Sample Response:

```js
{
    "idAuditTrail": 72,
    "idRiskTrail": 21
}
```

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
