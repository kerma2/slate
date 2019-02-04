# Round

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
    "locked": "2019-01-31T03:26:09.026Z",
    "start": "2019-02-09T03:26:09.026Z",
    "end": "2019-02-10T03:26:09.026Z"
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
    locked: "2019-04-05",
    start: "2019-05-10",
    end: "2019-05-12"
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
    "locked": "2019-05-05T00:00:00.000Z",
    "start": "2019-05-10T00:00:00.0007Z",
    "end": "2019-05-12T00:00:00.0007Z"
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
  CollegeNotFound,
  RoundNotFound,
  UserNotFound
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

## Fetch urns content

```javascript
import {
  CollegeNotFound,
  RoundNotFound,
  InvalidAccess
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc427'
const round = 1

request
  .get(`colleges/${id}/rounds/${round}/urns`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof RoundNotFound)
      // The round could be found

    if (err instanceof InvalidAccess)
      // The urns have not been created yet

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "name": "Worker College",
    "type": "titular",
    "round": 1,
    "dates": {
      "start": "2019-02-07T08:44:02.172Z",
      "end": "2019-02-08T08:44:02.172Z"
    },
    "votes": [
      {
        "_id": "5c4e89391bec7c7580044e4a",
        "listId": "5c4e889441f56c74b4ec66bb",
        "ballot": "JUTJGkXK6e+J/TqQnTukFk4tQcQarIZGBkwv+5By4yeaiqFZWvdQOuYjVPeM+nK75uExnNM8m9oJ9OixJRegPJG3y1kYcEfCULpdlo2BnnXdzCUL+7l+q16hntdIzMRXop1EEkfNPD4hqWOpp1nHkQUZ5+fdWQBVpDl7NTHobtq3t0DOimDK5piYmgARKdMFHZpRfy+1xkASpekvp471DqLmy6zGMj9GTJywFkrp07vNFxXDpoDJLkd2kKCkfI2ZnNWwq4BqVZx0aH5u+jiIsL6xoWgi9l18pLKsks89x11FDkeW/gcttHczKRLhE4gglgU/vaa5uBOLJOfUk/1ntA==",
        "date": "2019-02-07T08:46:49.086Z",
        "__v": 0
      },
      {
        "_id": "5c4e8975ec850c75cacc393b",
        "listId": "5c4e889441f56c74b4ec66bb",
        "ballot": "nf7t19gs0jRzYzhehFgVgRDa74z/xmWIHiixwGIh+gfIYOGA+cDcam2/JSk3RO3f9L7HG0gMNNDnOLMydBidNqRZ+/kE+652TBr5gF+klM1xoptGYTiP9IKZv0YHzAo46tOisKFIbMS1dBSOAu2Tk/5GolfRjWWZBBHn1Zxr3GYQVFfnXPmmajetoHFwbP5L6CMxswJCty9qkyKYX7UUrrO11zEJ32D+97bIyVJOxXpzuusOcZ7XXydk8Bn6aRHOYC3Sx7fqSSLSTVCo52PO/ZGmLNpwpwyBAUHGAbBCO9o0nbXPhbeN3e8Cl8tJDn2FlQFTA0GtM6VZtS40Lk68RA==",
        "date": "2019-02-07T08:47:49.557Z",
        "__v": 0
      }
    ]
  },
  {
    "name": "Worker College",
    "type": "substitute",
    "round": 1,
    "dates": {
      "start": "2019-02-07T09:44:02.172Z",
      "end": "2019-02-08T09:44:02.172Z"
    },
    "votes": []
  }
]
```

This endpoint retrieves the content of all urns within a specific round of a specific college.

<aside class="notice">
Each vote is encrypted with the public vote key given during the college's keys exchange.
</aside>

### HTTP Route

`GET colleges/<ID>/rounds/<ROUND>/urns`

### URL Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| ID        | The ID of the college in which the round is contained   |
| ROUND     | The number of the round in which the urns are contained |

## Insert a vote

```javascript
import {
  InvalidRequestFormat,
  CollegeNotFound,
  RoundNotFound,
  InvalidAccess,
  UrnNotFound,
  LockedUrn
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'
const type = 'titular' // Or 'substitute'
const round = 1

const ballot = {
  listId: '5c32ee4a2fa935441f8cc412',
  candidates: [
    {
      userId: '5c32ee4a2fa935441f8cc411',
      checked: true
    },
    {
      userId: '5c32ee4a2fa935441f8cc410',
      checked: false
    }
  ]
}

request
  .post(`colleges/${id}/rounds/${round}/vote/${type}`, {ballot: })
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof InvalidRequestFormat)
      // The body of the request is invalid

    if (err instanceof CollegeNotFound)
      // The college could be found

    if (err instanceof RoundNotFound)
      // The round could be found

    if (err instanceof InvalidAccess)
      // The elections have not yet started

    if (err instanceof UrnNotFound)
      // The round has urn with given type

    if (err instanceof LockedUrn)
      // The urn is either encrypted or inactive

    if (err instanceof NoUrnConnection)
      // The server is not connected to the urn

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "todo",
  "name": "file name.pdf"
}
```

This endpoint inserts a vote within a specific urn of a specific round from a specific college.

### HTTP Route

`POST colleges/<ID>/rounds/<ROUND>/vote/<TYPE>`

### URL Parameters

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| ID        | The ID of the colleges in which the round is retrieved |
| ROUND     | The number of the round in which the urn is contained  |
| TYPE      | The type of the urn in which to vote is inserted       |
