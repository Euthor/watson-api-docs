## Table of Contents

1. [Overview](#overview)
    - [Request Headers] (#Request Headers)
    - [ID Card](#id-card)
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
