# College

## Fetch all colleges

```javascript
import { EstablishmentNotFound, NoColleges } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'

request
  .get(`establishments/${id}/colleges`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could not be found

    if (err instanceof NoColleges)
      // No colleges could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c5999a3e714bb12ea8ca950",
    "establishmentId": "5c5999a2e714bb12ea8ca946",
    "name": "Name",
    "workforce": 11,
    "seats": 3,
    "reserved": [
      {
        "nb": 0,
        "_id": "5c5999a3e714bb12ea8ca951",
        "status": "Ouvrier"
      }
    ],
    "statuses": ["Ouvrier"],
    "state": "waiting",
    "round": 1
  }
]
```

This endpoint retrieves all colleges within a specific establishment.

### HTTP Route

`GET establishments/<ID>/colleges/`

### URL Parameters

| Parameter | Description                                                     |
| --------- | --------------------------------------------------------------- |
| ID        | The ID of the establishment in which the colleges are retrieved |

## Fetch all colleges names

```javascript
import { EstablishmentNotFound, NoColleges } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'

request
  .get(`establishments/${id}/colleges/names`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could not be found

    if (err instanceof NoColleges)
      // No colleges could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
["Name 1", "Name 2", "Name 3"]
```

This endpoint retrieves all college's names within a specific establishment.

### HTTP Route

`GET establishments/<ID>/colleges/names`

### URL Parameters

| Parameter | Description                                                            |
| --------- | ---------------------------------------------------------------------- |
| ID        | The ID of the establishment in which the college's names are retrieved |

## Create a college

```javascript
import { EstablishmentNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'

const data = {
  name: "Name",             // Mandatory
  workforce: 11,            // Mandatory
  seats: 2,                 // Mandatory
  reserved: [               // Optional (default: one object per status with nb at 0)
    {
      nb: 0,
      status: "Ouvrier"
    }
  ],
  statuses: ["Ouvrier"],    // Optional
  rounds: [                 // Mandatory (for both rounds)
    {
      dates: {                // Mandatory
        locked: "2019-04-25",
        start: "2019-05-01",
        end: "2019-05-02"
      },
      titular: true,          // Mandatory (define if college has titular elections)
      substitute: true        // Mandatory (define if college has substitute elections)
    },
    {
      dates: {
        locked: "2019-04-12",
        start: "2019-05-17",
        end: "2019-05-18"
      },
      titular: true,
      substitute: true
    }

  ]
}

request
  .post(`establishments/${id}/colleges/`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could not be found

    if (err instanceof ValidationError)
      // The college could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32ee4a2fa935441f8ccac4",
  "establishmentId": "5c32ee4a2fa935441f8cc414",
  "name": "Name",
  "workforce": 11,
  "seats": 2,
  "reserved": [
    {
      "nb": 0,
      "_id": "5c5999a3e714bb12ea8ca951",
      "status": "Ouvrier"
    }
  ],
  "statuses": ["Ouvrier"],
  "state": "waiting",
  "round": 1
}
```

This endpoint creates a college within a specific establishment.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`POST establishments/<ID>/colleges/`

### URL Parameters

| Parameter | Description                                                 |
| --------- | ----------------------------------------------------------- |
| ID        | The ID of the college in which the establishment is created |

## Fetch a college

```javascript
import { CollegeNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc425'

request
  .get(`colleges/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32ee4a2fa935441f8cc425",
  "establishmentId": "5c5999a2e714bb12ea8ca946",
  "name": "Name",
  "workforce": 11,
  "seats": 3,
  "reserved": [
    {
      "nb": 0,
      "_id": "5c5999a3e714bb12ea8ca951",
      "status": "Ouvrier"
    }
  ],
  "statuses": ["Ouvrier"],
  "state": "waiting",
  "round": 1
}
```

This endpoint retrieves a specific college.

### HTTP Route

`GET colleges/<ID>/`

### URL Parameters

| Parameter | Description                       |
| --------- | --------------------------------- |
| ID        | The ID of the college to retrieve |

## Update an college

```javascript
import { CollegeNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8ccac4'

const data = {
  name: 'New Name',
  workforce: '0.2',
  seats: '4'
}

request
  .put(`colleges/${id}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof ValidationError)
      // The college could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32ee4a2fa935441f8ccac4",
  "establishmentId": "5c32ee4a2fa935441f8cc414",
  "name": "New Name",
  "workforce": 0.2,
  "seats": 4,
  "statuses": ["Ouvrier"],
  "state": "waiting",
  "round": 1
}
```

This endpoint updates a specific college.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT colleges/<ID>/`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the college to update |

## Delete a college

```javascript
import { CollegeNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8ccac4'

request
  .delete(`colleges/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific college.

### HTTP Route

`DELETE colleges/<ID>/`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the college to delete |

## Add a status

```javascript
import { ValidationError, CollegeNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc425'
const status = "Status 1"

request
  .post(`colleges/${id}/statuses/${status}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof ValidationError)
      // The statuses could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32ee4a2fa935441f8cc425",
  "establishmentId": "5c32ee4a2fa935441f8cc414",
  "name": "Name",
  "workforce": 0.8,
  "seats": 3,
  "statuses": ["Ingénieurs", "Techniciens", "Status 1"],
  "state": "waiting",
  "round": 1
}
```

This endpoint adds a specific status within a specific college.

<aside class="notice">
Adding a status will automatically add to the college all electors linked to this status
</aside>

### HTTP Route

`POST colleges/<ID>/statuses/<STATUS>`

### URL Parameters

| Parameter | Description                                           |
| --------- | ----------------------------------------------------- |
| ID        | The ID of the colleges in which the status is created |
| STATUS    | The STATUS to add                                     |

## Remove a status

```javascript
import { CollegeNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc425'
const status = 'Status 1'

request
  .delete(`colleges/${id}/statuses/${status}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific status within a specific college.

<aside class="notice">
Removing a status will automatically delete from the college all electors linked to this status
</aside>

### HTTP Route

`DELETE colleges/<ID>/statuses/<STATUS>`

### URL Parameters

| Parameter | Description                                          |
| --------- | ---------------------------------------------------- |
| ID        | The ID of the college in which the status is deleted |
| STATUS    | The STATUS to delete                                 |

## Initialize a college

```javascript
import { CollegeNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc425'

request
  .get(`colleges/${id}/init`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint inits a specific college.

It generates the local key pair (used to encrypt/decrypt an urn as a file).

<aside class="notice">
This is a mandatory call before accessing one of the urn content or generating USB keys.
</aside>

### HTTP Route

`GET colleges/<ID>/init`

### URL Parameters

| Parameter | Description                         |
| --------- | ----------------------------------- |
| ID        | The ID of the college to initialize |

## Keys exchange

```javascript
import NodeRSA from 'node-rsa'

import {
  CollegeNotFound,
  InvalidRequestFormat,
  InvalidKey
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const key = new NodeRSA({ b: 2048 })
const id = '5c32ee4a2fa935441f8cc425'

request
  .post(`colleges/${id}/keys`, { vote: key.exportKey('public') })
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof InvalidRequestFormat)
      // The body of the request is invalid

    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof InvalidKey)
      // The given key is invalid

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "usb": "-----BEGIN PUBLIC KEY-----
    MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA6rXsusxtlEJjFOhXwd2V
    wrxq6+16fruU/MSBBNcEX71EvI2yHg+C+kL93g71MkEBMONnhHVsQgYEbE4xQ/rL
    ISgOm5yepigrWrS4stS5C1GW7DXuiX0onPChaQUiExoNq+dSAPMqHALkTtd9lERo
    FDms+FsswS/f//yF3ok9qz5JnCNYfBayj/6OrtoqWurfjLQWfXqtxWyB/5GCGe7C
    PWo0QyYUilhS2li26evGh3fwQBf6WTmLEksLFZ6FLHEjxOOMTAZxbODYY9r0kVgh
    XWLsghpBFVcQ9lW3eha23gu5uARM5lOPFpC6kHcZ/I2ei1MAorNp2eaNIwuwwL54
    bQIDAQAB
    -----END PUBLIC KEY-----"
}
```

This endpoint saves the public key (used to encrypt votes) within a specific college.

It generates the usb key pair (used to encrypt/decrypt the content of the usb keys).

<aside class="notice">
This is a mandatory call before any vote can occur.
</aside>

### HTTP Route

`POST colleges/<ID>/keys`

### URL Parameters

| Parameter | Description                                           |
| --------- | ----------------------------------------------------- |
| ID        | The ID of the college in which the keys are generated |

## Decrypt USB content

```javascript
import NodeRSA from 'node-rsa'

import {
  CollegeNotFound,
  InvalidRequestFormat,
  InvalidKey
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc425'
const content = { key: 'value' }

const key = new NodeRSA({ b: 2048 })
const usb = new NodeRSA()

usb.importKey(USBPublicKey, 'public')

const encrypted = usb.encrypt(content, 'base64')

request
  .post(`colleges/${id}/usb`, { content: encrypted, secure: key.exportKey('public') })
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof InvalidRequestFormat)
      // The body of the request is invalid

    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof InvalidKey)
      // 1. The given key is invalid
      // 2. The content is invalid

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "content": "QQt+ZLrEuwBO+gwTQ4IRcAzmgefULVM7UpJhZGbpPpS9tiV7GirLf4p3cRMIg/V3zpUZGPRfmL2LD9+g4LaKffz5TWuucRv056ZBcMuL9u6u3jlKr2cB99gt7pcqnkwENzf/AGcWDq/uhxFgcJPetDsoxk649u5kXH4NYZOLrvO7XQS
Q1e7HxqxLVuGiAYwO/Rua/okMr2bdwgcLvRhnK1rknB6vwUSxUMMRWbhTvUdaieUqvtlnsj06yC0PSBYUCzXBpQG/+KN3R4aOwRX0DuVF1ZuZkXWk4xrZUrHXxjYTgkSd9RY3JC1N6R5tuUybPPs57rW5NaF5WF3ml7XFEQ=="
}
```

This endpoint decrypts the given content of an usb key and encrypt it with the given secure public key.

<aside class="notice">
The content MUST be an object
</aside>

### HTTP Route

`POST colleges/<ID>/usb`

### URL Parameters

| Parameter | Description                                                     |
| --------- | --------------------------------------------------------------- |
| ID        | The ID of the college in which the usb private key is contained |

## Get public key

```javascript
import NodeRSA from 'node-rsa'

import { CollegeNotFound, InvalidAccess } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc425'

request
  .put(`colleges/${id}/public`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof InvalidAccess)
      // The college has not been controlled yet

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "key": "-----BEGIN PUBLIC KEY-----
    MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA6rXsusxtlEJjFOhXwd2V
    wrxq6+16fruU/MSBBNcEX71EvI2yHg+C+kL93g71MkEBMONnhHVsQgYEbE4xQ/rL
    ISgOm5yepigrWrS4stS5C1GW7DXuiX0onPChaQUiExoNq+dSAPMqHALkTtd9lERo
    FDms+FsswS/f//yF3ok9qz5JnCNYfBayj/6OrtoqWurfjLQWfXqtxWyB/5GCGe7C
    PWo0QyYUilhS2li26evGh3fwQBf6WTmLEksLFZ6FLHEjxOOMTAZxbODYY9r0kVgh
    XWLsghpBFVcQ9lW3eha23gu5uARM5lOPFpC6kHcZ/I2ei1MAorNp2eaNIwuwwL54
    bQIDAQAB
    -----END PUBLIC KEY-----"
}
```

This endpoint retrieves the public key (used to encrypt votes) within a specific college.

<aside class="notice">
All votes MUST be encrypted with this key before being sent to the server.
</aside>

### HTTP Route

`GET colleges/<ID>/public`

### URL Parameters

| Parameter | Description                                         |
| --------- | --------------------------------------------------- |
| ID        | The ID of the college in which the key is contained |
