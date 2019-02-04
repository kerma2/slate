# Candidate

## Fetch all candidates

```javascript
import { ListNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'

request
  .get(`list/${id}/candidates`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ListNotFound)
      // The list could not be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "userId": "5c379bec037d637ffad359bc",
    "rank": 1
  },
  {
    "userId": "5c379bec037d637ffad359c0",
    "rank": 2
  }
]
```

This endpoint retrieves all candidates within a specific list.

### HTTP Route

`GET list/<ID>/candidates/`

### URL Parameters

| Parameter | Description                                              |
| --------- | -------------------------------------------------------- |
| ID        | The ID of the list in which the candidates are retrieved |

## Create candidates

```javascript
import _ from 'lodash'

import { ListNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler, parseError } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'

const data = [
  {
    userId: '5c32ee4a2fa935441f8cc415'  // Mandatory
    rank: 1                             // Optional
  },
  {
    userId: '5c32ee4a2fa935441f8cc416'  // Mandatory
    rank: 2                             // Optional
  },
  {
    userId: '5c32ee4a2fa935441f8cc417'  // Mandatory
    rank: 3                             // Optional
  }
]

request
  .post(`lists/${id}/candidates/`, data)
  .then(res => {
    const hasError = _.some(_.map(res.data, item => !_.isEmpty(data.error)))

    if (!hasError) {
      // All candidates were successfully created
      console.log(res.data)

    } else {
      // Some candidates could not be created (none was saved)
      console.log(res.data)

      _.forEach(res.data, item => {
        if (item.valid) {
          // This candidate has valid data
          return
        }

        const error = parseError(item)

        if (error instanceof ValidationError)
          // This candidate has invalid data

        // An other error occurred for this candidate
      })
    }
  })
  .catch(APIErrorHandler)
  .catch(errors => {
    if (err instanceof ListNotFound)
      // The establishment could not be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
WITHOUT ERRORS:
[
  {
    "userId": "5c32ee4a2fa935441f8cc415",
    "rank": 1
  },
  {
    "userId": "5c32ee4a2fa935441f8cc416",
    "rank": 2
  },
  {
    "userId": "5c32ee4a2fa935441f8cc417",
    "rank": 3
  }
]

WITH ERRORS:
[
  { "valid": true },
  { "valid": true },
  {
    "name": "ValidationError",
    "status": 400,
    "message": "List validation failed",
    "mandatory": [],
    "duplicate": [ "candidates.rank" ],
    "invalid": [],
    "cast": []
  }
]
```

This endpoint creates several candidates within a specific list.

Be sure to check how to handle [ValidationError](#validationerror).

<aside class="notice">
All requests in batch are always processed.
</aside>

<aside class="notice">
If any candidate creation fails, no candidate will be saved to the database.
</aside>

<aside class="notice">
On error, the response object will holds whether or not each candidate has valid data or the error specific to the candidate.
</aside>

### HTTP Route

`POST lists/<ID>/candidates/`

### URL Parameters

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| ID        | The ID of the list in which the candidates are created |

## Update candidates

```javascript
import { ListNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'

const data = [
  {
    userId: '5c32ee4a2fa935441f8cc415'
    rank: 2
  },
  {
    userId: '5c32ee4a2fa935441f8cc416'
    rank: 3
  },
  {
    userId: '5c32ee4a2fa935441f8cc417'
    rank: 1
  }
]

request
  .put(`list/${collegeId}/candidates/`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ListNotFound)
      // The college could be found

    if (err instanceof ValidationError)
      // The elector could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "userId": "5c32ee4a2fa935441f8cc415",
    "rank": 2
  },
  {
    "userId": "5c32ee4a2fa935441f8cc416",
    "rank": 3
  },
  {
    "userId": "5c32ee4a2fa935441f8cc417",
    "rank": 1
  }
]
```

This endpoint updates all candidates within a specific list.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT list/<ID>/candidates/`

### URL Parameters

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| ID        | The ID of the list in which the candidates are updated |

## Delete an candidate

```javascript
import { ListNotFound, UserNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const listId = '5c32ee4a2fa935441f8cc414'
const id = '5c32ee4a2fa935441f8cc415'

request
  .delete(`list/${collegeId}/candidates/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ListNotFound)
      // The college could be found

    if (err instanceof UserNotFound)
      // The candidate could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific candidate within a specific list.

<aside class="notice">
Deleting a candidate will automatically change the rank of all other candidates to fit the new candidate's array size.
</aside>

### HTTP Route

`DELETE list/<LIST_ID>/candidates/<ID>`

### URL Parameters

| Parameter | Description                                          |
| --------- | ---------------------------------------------------- |
| LIST_ID   | The ID of the list in which the candidate is deleted |
| ID        | The ID of the candidate                              |
