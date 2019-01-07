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
    "_id": "5c32ee4a2fa935441f8cc425",
    "establishmentId": "5c32ee4a2fa935441f8cc414",
    "name": "Name",
    "workforce": 0.8,
    "seats": 3,
    "statuses": ["Ingénieurs", "Techniciens"],
    "state": "waiting",
    "round": 1,
    "electors": ["5c32ee4a2fa935441f8cc426"],
    "rounds": [
      {
        "_id": "5c32ee4a2fa935441f8cc426",
        "nbr": 1,
        "dates": { "start": "2019-01-17T06:14:34.712Z", "end": "2019-01-18T06:14:34.712Z" },
        "officers": ["5c32ee4a2fa935441f8cc427"],
        "lists": ["5c32ee4a2fa935441f8cc428"]
      },
      {
        "_id": "5c32ee4a2fa935441f8cc429",
        "nbr": 2,
        "dates": { "start": "2019-02-02T06:14:34.712Z", "end": "2019-02-03T06:14:34.712Z" },
        "officers": [],
        "lists": []
      }
    ]
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
  workforce: 0.5,           // Mandatory
  seats: 2,                 // Mandatory
  statuses: ["Ouvrier"],    // Optional
  rounds: [                 // Mandatory (for both rounds)
    {
      dates: {                // Mandatory
        start: "2019-05-01",
        end: "2019-05-02"
      },
      titular: true,          // Mandatory (define if college has titular elections)
      substitute: true        // Mandatory (define if college has substitute elections)
    },
    {
      dates: {
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
    "workforce": 0.5,
    "seats": 2,
    "statuses": ["Ouvrier"],
    "state": "waiting",
    "round": 1,
    "electors": [],
    "rounds": [
      {
        "_id": "5c32ee4a2fa935441f8ccac5",
        "nbr": 1,
        "dates": { "start": "2019-05-01T00:00:00.000Z", "end": "2019-05-02T00:00:00.000Z" },
        "officers": [],
        "lists": []
      },
      {
        "_id": "5c32ee4a2fa935441f8ccac5",
        "nbr": 2,
        "dates": { "start": "2019-05-17T00:00:00.000Z", "end": "2019-05-18T00:00:00.000Z" },
        "officers": [],
        "lists": []
      }
    ]
  }
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
  "establishmentId": "5c32ee4a2fa935441f8cc414",
  "name": "Name",
  "workforce": 0.8,
  "seats": 3,
  "statuses": ["Ingénieurs", "Techniciens"],
  "state": "waiting",
  "round": 1,
  "electors": ["5c32ee4a2fa935441f8cc426"],
  "rounds": [
    {
      "_id": "5c32ee4a2fa935441f8cc426",
      "nbr": 1,
      "dates": { "start": "2019-01-17T06:14:34.712Z", "end": "2019-01-18T06:14:34.712Z" },
      "officers": ["5c32ee4a2fa935441f8cc427"],
      "lists": ["5c32ee4a2fa935441f8cc428"]
    },
    {
      "_id": "5c32ee4a2fa935441f8cc429",
      "nbr": 2,
      "dates": { "start": "2019-02-02T06:14:34.712Z", "end": "2019-02-03T06:14:34.712Z" },
      "officers": [],
      "lists": []
    }
  ]
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
  "round": 1,
  "electors": [],
  "rounds": [
    {
      "_id": "5c32ee4a2fa935441f8ccac5",
      "nbr": 1,
      "dates": { "start": "2019-05-01T00:00:00.000Z", "end": "2019-05-02T00:00:00.000Z" },
      "officers": [],
      "lists": []
    },
    {
      "_id": "5c32ee4a2fa935441f8ccac5",
      "nbr": 2,
      "dates": { "start": "2019-05-17T00:00:00.000Z", "end": "2019-05-18T00:00:00.000Z" },
      "officers": [],
      "lists": []
    }
  ]
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
const status = ["Status 1"]

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
  "round": 1,
  "electors": ["5c32ee4a2fa935441f8cc426", "5c32ee4a2fa935441f8cc427", "5c32ee4a2fa935441f8cc428"],
  "rounds": [
    {
      "_id": "5c32ee4a2fa935441f8cc426",
      "nbr": 1,
      "dates": { "start": "2019-01-17T06:14:34.712Z", "end": "2019-01-18T06:14:34.712Z" },
      "officers": ["5c32ee4a2fa935441f8cc427"],
      "lists": ["5c32ee4a2fa935441f8cc428"]
    },
    {
      "_id": "5c32ee4a2fa935441f8cc429",
      "nbr": 2,
      "dates": { "start": "2019-02-02T06:14:34.712Z", "end": "2019-02-03T06:14:34.712Z" },
      "officers": [],
      "lists": []
    }
  ]
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

## Delete a status

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