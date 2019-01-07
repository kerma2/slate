# Rounds

## Fetch a round

```javascript
import { CollegeNotFound, RoundNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'
const round = 1

request
  .get(`colleges/${id}/rounds/${round}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof RoundNotFound)
      // The round could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c3339a21a6e742e0134dbb2",
  "nbr": 1,
  "dates": {
    "start": "2019-01-17T11:36:02.657Z",
    "end": "2019-01-18T11:36:02.657Z"
  },
  "officers": [
    {
      "_id": "5c3339a41a6e742e0134dbff",
      "userId": "5c3339a21a6e742e0134dbbf",
      "type": "president"
    },
    {
      "_id": "5c3339a41a6e742e0134dc00",
      "userId": "5c3339a31a6e742e0134dbc3",
      "type": "assessor"
    },
    {
      "_id": "5c3339a41a6e742e0134dc01",
      "userId": "5c3339a31a6e742e0134dbc7",
      "type": "assessor"
    },
    {
      "_id": "5c3339a41a6e742e0134dc02",
      "userId": "5c3339a31a6e742e0134dbcb",
      "type": "officer"
    }
  ],
  "lists": [
    "5c3339a41a6e742e0134dc0f",
    "5c3339a41a6e742e0134dc10",
    "5c3339a41a6e742e0134dc11",
    "5c3339a41a6e742e0134dc12"
  ]
}
```

This endpoint retrieves a specific round within a specific college.

### HTTP Route

`GET colleges/<ID>/rounds/<ROUND>`

### URL Parameters

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| ID        | The ID of the colleges in which the round is retrieved |
| ROUND     | The number of the round                                |

## Update a round

```javascript
import {
  CollegeNotFound,
  RoundNotFound,
  ValidationError,
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'
const round = 1

const data = {
  dates: {
    start: "2019-05-01",
    end: "2019-05-02"
  }
}

request
  .put(`colleges/${id}/round/${round}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof RoundNotFound)
      // The round could be found

    if (err instanceof ValidationError)
      // The round could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c3339a21a6e742e0134dbb2",
  "nbr": 1,
  "dates": {
    "start": "2019-05-01T00:00:00.0007Z",
    "end": "2019-05-02T00:00:00.0007Z"
  },
  "officers": [
    {
      "_id": "5c3339a41a6e742e0134dbff",
      "userId": "5c3339a21a6e742e0134dbbf",
      "type": "president"
    },
    {
      "_id": "5c3339a41a6e742e0134dc00",
      "userId": "5c3339a31a6e742e0134dbc3",
      "type": "assessor"
    },
    {
      "_id": "5c3339a41a6e742e0134dc01",
      "userId": "5c3339a31a6e742e0134dbc7",
      "type": "assessor"
    },
    {
      "_id": "5c3339a41a6e742e0134dc02",
      "userId": "5c3339a31a6e742e0134dbcb",
      "type": "officer"
    }
  ],
  "lists": [
    "5c3339a41a6e742e0134dc0f",
    "5c3339a41a6e742e0134dc10",
    "5c3339a41a6e742e0134dc11",
    "5c3339a41a6e742e0134dc12"
  ]
}
```

This endpoint updates a specific round within a specific college.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT colleges/<ID>/rounds/<ROUND>`

### URL Parameters

| Parameter | Description                                          |
| --------- | ---------------------------------------------------- |
| ID        | The ID of the colleges in which the round is updated |
| ROUND     | The number of the round                              |

## Fetch all officers

```javascript
import {
  CollegeNotFound,
  RoundNotFound,
  NoOfficers
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'
const round = 1

request
  .get(`colleges/${id}/rounds/${round}/officers`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could not be found

    if (err instanceof RoundNotFound)
      // The round could be found

    if (err instanceof NoColleges)
      // No officers could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "userId": "5c33403699212635c71fbaa2",
    "type": "president"
  },
  {
    "userId": "5c33403799212635c71fbaa6",
    "type": "assessor"
  },
  {
    "userId": "5c33403799212635c71fbaaa",
    "type": "assessor"
  },
  {
    "userId": "5c33403799212635c71fbaae",
    "type": "officer"
  }
]
```

This endpoint retrieves all officers within a specific round of a specific college.

### HTTP Route

`GET colleges/<ID>/rounds/<ROUND>/officers`

### URL Parameters

| Parameter | Description                                                 |
| --------- | ----------------------------------------------------------- |
| ID        | The ID of the college in which the round is contained       |
| ROUND     | The number of the round in which the officers are retrieved |

## Create an officer

```javascript
import {
  CollegeNotFound,
  RoundNotFound,
  UserNotFound,
  ValidationError,
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'
const round = 1

const data = {
  userId: "5c32ee4a2fa935441f8cc415",   // Mandatory
  type: "officer",                      // Mandatory
  colleges: [                           // Mandatory
    "5c32ee4a2fa935441f8cc411",
    "5c32ee4a2fa935441f8cc412"
  ]
}

request
  .post(`colleges/${id}/rounds/${round}/officers`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof RoundNotFound)
      // The round could be found

    if (err instanceof UserNotFound)
      // The user is not an elector in the given list of colleges

    if (err instanceof ValidationError)
      // The officer could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "userId": "5c32ee4a2fa935441f8cc415",
  "type": "officer"
},
```

This endpoint creates an officer within a specific round of a several college.

Be sure to check how to handle [ValidationError](#validationerror).

<aside class="notice">
An officer can be assigned to several colleges as long as he is an elector in at least one of these colleges.
</aside>

### HTTP Route

`POST colleges/<ID>/rounds/<ROUND>/officers`

### URL Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| ID        | The ID of the college in which the round is contained   |
| ROUND     | The number of the round in which the officer is created |

## Delete an officer

```javascript
import {
  CollegeNotFound
  RoundNotFound,
  UserNotFound,
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const collegeId = '5c32ee4a2fa935441f8cc425'
const id = '5c32ee4a2fa935441f8cc427'
const round = 1

request
  .delete(`colleges/${collegeId}/rounds/${round}/officers/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof RoundNotFound)
      // The round could be found

    if (err instanceof UserNotFound)
      // The user is not an officer in this round of this college

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific officer within a specific round of a specific college.

### HTTP Route

`DELETE colleges/<COLLEGE_ID>/rounds/<ROUND>/officers/<ID>`

### URL Parameters

| Parameter  | Description                                               |
| ---------- | --------------------------------------------------------- |
| COLLEGE_ID | The ID of the college in which the round is contained     |
| ROUND      | The number of the round in which the officer is contained |
| ID         | The ID of the officer to delete                           |
