# Electors

## Fetch all electors

```javascript
import { CollegeNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'

request
  .get(`colleges/${id}/electors`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The establishment could not be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "collegeId": "5c32ee4a2fa935441f8cc414",
    "userId": "5c3325f3ebed061153bdfcfa",
    "serial": "A01",
    "status": "Ouvrier"
  },
  {
    "collegeId": "5c32ee4a2fa935441f8cc414",
    "userId": "5c3325f3ebed061153bdfcfb",
    "serial": "A02",
    "status": "Ouvrier"
  },
  {
    "collegeId": "5c32ee4a2fa935441f8cc414",
    "userId": "5c3325f3ebed061153bdfcfc",
    "serial": "A03",
    "status": "Ouvrier"
  }
]
```

This endpoint retrieves all electors within a specific college.

### HTTP Route

`GET colleges/<ID>/electors/`

### URL Parameters

| Parameter | Description                                               |
| --------- | --------------------------------------------------------- |
| ID        | The ID of the college in which the electors are retrieved |

## Create electors

```javascript
import _ from 'lodash'

import { EstablishmentNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler, parseError } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'

const data = [
  {
    mail: "user1@mail.com",         // Optional
    fullname: "Name1 Surname",      // Mandatory
    civility: "M",                  // Mandatory
    address: "Address",             // Mandatory
    hiring: 31536000000,            // Mandatory
    birth: {
      date: "1980-01-01",           // Mandatory
      county: "County/Department",  // Mandatory
      place: "Place/City"           // Mandatory
    },
    serial: "A04",                  // Mandatory
    status: "Ouvrier"               // Mandatory
  },
  {
    mail: "user2@mail.com",         // Optional
    fullname: "Name2 Surname",      // Mandatory
    civility: "M",                  // Mandatory
    address: "Address",             // Mandatory
    hiring: 31536000000,            // Mandatory
    birth: {
      date: "1980-01-01",           // Mandatory
      county: "County/Department",  // Mandatory
      place: "Place/City"           // Mandatory
    },
    serial: "A05",                  // Mandatory
    status: "Ouvrier"               // Mandatory
  }
]

request
  .post(`establishments/${id}/users/`, data)
  .then(res => {
    const hasError = _.some(_.map(res.data, item => !_.isEmpty(data.error)))

    if (!hasError) {
      // All user were successfully created
      console.log(res.data)

    } else {
      // Some user could not be created (none was saved)
      console.log(res.data)

      _.forEach(res.data, item => {
        if (item.valid) {
          // This user has valid data
          return
        }

        const error = parseError(item)

        if (error instanceof ValidationError)
          // The user has invalid data

      })
    }
  })
  .catch(APIErrorHandler)
  .catch(errors => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could not be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
WITHOUT ERRORS:
[
  {
    "collegeId": "5c32ee4a2fa935441f8cc414",
    "userId": "5c3325f3ebed061153bdfcfa",
    "serial": "A04",
    "status": "Ouvrier"
  },
  {
    "collegeId": "5c32ee4a2fa935441f8cc414",
    "userId": "5c3325f3ebed061153bdfcfb",
    "serial": "A05",
    "status": "Ouvrier"
  }
]

WITH ERRORS:
[
  { "valid": true }
  {
    "name": "ValidationError",
    "status": 400,
    "message": "Establishment validation failed",
    "mandatory": [],
    "duplicate": [ "users.serial" ],
    "invalid": [],
    "cast": []
  }
]
```

This endpoint creates several electors within a specific establishment.

Be sure to check how to handle [ValidationError](#validationerror).

<aside class="notice">
All requests in batch are always processed.
</aside>

<aside class="notice">
If any user creation fails, no user will be saved to the database.
</aside>

<aside class="notice">
On error, the response object will holds whether or not each user has valid data or the error specific to the user.
</aside>

### HTTP Route

`POST establishments/<ID>/users/`

### URL Parameters

| Parameter | Description                                                   |
| --------- | ------------------------------------------------------------- |
| ID        | The ID of the establishment in which the electors are created |

## Set electors cards status

```javascript
import _ from 'lodash'

import { UserNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c330fce4902e37249045e84'

const data = [
  {
    userId: '5c330fce4902e37249045e85',   // Mandatory
    sent: true                            // Mandatory
  },
  {
    userId: '5c330fce4902e37249045e86',   // Mandatory
    sent: true                            // Mandatory
  },
  {
    userId: '5c330fce4902e37249045e87',   // Mandatory
    sent: false                           // Mandatory
  }
]

request
  .post(`establishments/${id}/users/cards`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(errors => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could not be found

    if (err instanceof UserNotFound)
      // A user in the batch could not be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[{ "success": true }, { "success": true }, { "success": true }]
```

This endpoint sets several elector's card status within a specific establishment.

### HTTP Route

`POST establishments/<ID>/users/cards`

### URL Parameters

| Parameter | Description                                                            |
| --------- | ---------------------------------------------------------------------- |
| ID        | The ID of the establishment in which the elector's card status are set |

## Fetch an elector

```javascript
import { CollegeNotFound, UserNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const collegeId = '5c32ee4a2fa935441f8cc414'
const id = '5c3325f3ebed061153bdfcfa'

request
  .get(`colleges/${collegeId}/elector/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof UserNotFound)
      // The college could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "collegeId": "5c32ee4a2fa935441f8cc414",
  "userId": "5c3325f3ebed061153bdfcfa",
  "serial": "A01",
  "status": "Ouvrier"
}
```

This endpoint retrieves a specific elector within a specific college.

### HTTP Route

`GET colleges/<COLLEGE_ID>/electors/<ID>`

### URL Parameters

| Parameter  | Description                                              |
| ---------- | -------------------------------------------------------- |
| COLLEGE_ID | The ID of the colleges in which the elector is retrieved |
| ID         | The ID of the elector                                    |

## Update an elector

```javascript
import {
  CollegeNotFound,
  UserNotFound,
  InvalidUpdate,
  ValidationError,
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const collegeId = '5c32ee4a2fa935441f8cc414'
const id = '5c3325f3ebed061153bdfcfa'

const data = {
  serial: 'A10',
  status: 'Techniciens',
}

request
  .put(`colleges/${collegeId}/elector/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof UserNotFound)
      // The elector could be found

    if (err instanceof InvalidUpdate)
      // The elector can not be updated anymore

    if (err instanceof ValidationError)
      // The college could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "collegeId": "5c32ee4a2fa935441f8cc414",
  "userId": "5c3325f3ebed061153bdfcfa",
  "serial": "A10",
  "status": "Techniciens"
}
```

<aside class="notice">
Modifying an elector's status will automatically remove him from his current college and move him to the new one (if need be).
</aside>

This endpoint updates a specific elector.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT colleges/<COLLEGE_ID>/electors/<ID>`

### URL Parameters

| Parameter  | Description                                            |
| ---------- | ------------------------------------------------------ |
| COLLEGE_ID | The ID of the colleges in which the elector is updated |
| ID         | The ID of the elector                                  |

## Delete an elector

```javascript
import { CollegeNotFound, UserNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const collegeId = '5c32ee4a2fa935441f8cc414'
const id = '5c3325f3ebed061153bdfcfa'

request
  .delete(`colleges/${collegeId}/elector/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof UserNotFound)
      // The elector could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific elector.

### HTTP Route

`DELETE colleges/<COLLEGE_ID>/electors/<ID>`

### URL Parameters

| Parameter  | Description                                            |
| ---------- | ------------------------------------------------------ |
| COLLEGE_ID | The ID of the colleges in which the elector is deleted |
| ID         | The ID of the elector                                  |
