# List

## Fetch all valid lists

```javascript
import { CollegeNotFound, RoundNotFound, NoLists } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'
const round = 1

request
  .get(`colleges/${id}/rounds/${round}/lists`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could not be found

    if (err instanceof RoundNotFound)
      // The round could not be found

    if (err instanceof NoLists)
      // No lists could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c3780c84bb8ea63fc222ac5",
    "collegeId": "5c32ee4a2fa935441f8cc414",
    "roundId": "5c3780c74bb8ea63fc222a62",
    "type": "titular",
    "name": "General Mechanics Confederation",
    "slogan": "Slogan",
    "valid": true,
    "logo": "https://i.imgur.com/ZUtiogP.png",
    "profession": "5c3780c64bb8ea63fc222a56"
  }
]
```

This endpoint retrieves all valid lists within a specific round of a specific college.

<aside class="notice">
This will only return valid lists
</aside>

<aside class="notice">
A valid list does not exceed the maximum size allowed (which is the number of seats in the college which holds the list)
</aside>

### HTTP Route

`GET colleges/<ID>/rounds/<ROUND>/lists`

### URL Parameters

| Parameter | Description                                              |
| --------- | -------------------------------------------------------- |
| ID        | The ID of the college in which the round is contained    |
| ROUND     | The number of the round in which the lists are retrieved |

## Fetch all invalid lists

```javascript
import { CollegeNotFound, RoundNotFound, NoLists } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc414'
const round = 1

request
  .get(`colleges/${id}/rounds/${round}/lists/invalid`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could not be found

    if (err instanceof RoundNotFound)
      // The round could not be found

    if (err instanceof NoLists)
      // No lists could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c3780c84bb8ea63fc222ac5",
    "collegeId": "5c32ee4a2fa935441f8cc414",
    "roundId": "5c3780c74bb8ea63fc222a62",
    "type": "titular",
    "name": "General Mechanics Confederation",
    "slogan": "Slogan",
    "valid": false,
    "logo": "https://i.imgur.com/ZUtiogP.png",
    "profession": "5c3780c64bb8ea63fc222a56"
  }
]
```

This endpoint retrieves all invalid lists within a specific round of a specific college.

<aside class="notice">
This will only return invalid lists
</aside>

<aside class="notice">
An invalid list exceed the maximum size allowed (which is the number of seats in the college which holds the list)
</aside>

### HTTP Route

`GET colleges/<ID>/rounds/<ROUND>/lists/invalid`

### URL Parameters

| Parameter | Description                                              |
| --------- | -------------------------------------------------------- |
| ID        | The ID of the college in which the round is contained    |
| ROUND     | The number of the round in which the lists are retrieved |

## Create a list

```javascript
import { CollegeNotFound, RoundNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc415'
const round = 1

const data = {
  type: "titular",                          // Mandatory
  name: "General Mechanics Confederation",  // Mandatory
  slogan: "Slogan",                         // Optional
  logo: "https://i.imgur.com/ZUtiogP.png",  // Optional
  profession: '5c3780c94bb8ea63fc222acd'    // Optional
}

request
  .post(`colleges/${id}/rounds/${round}/lists`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CollegeNotFound)
      // The college could not be found

    if (err instanceof RoundNotFound)
      // The round could not be found

    if (err instanceof ValidationError)
      // The college could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32ee4a2fa935441f8cc415",
  "collegeId": "5c32ee4a2fa935441f8cc414",
  "roundId": "5c37940a91523a7844adacce",
  "type": "titular",
  "name": "General Mechanics Confederation",
  "slogan": "Slogan",
  "valid": true,
  "logo": "https://i.imgur.com/ZUtiogP.png",
  "profession": "5c3780c94bb8ea63fc222acd"
}
```

This endpoint creates a list within a specific round of a specific college.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`POST colleges/<ID>/rounds/<ROUND>/lists`

### URL Parameters

| Parameter | Description                                           |
| --------- | ----------------------------------------------------- |
| ID        | The ID of the college in which the round is contained |
| ROUND     | The number of the round in which the list is created  |

## Fetch a list

```javascript
import { ListNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc425'

request
  .get(`lists/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ListNotFound)
      // The college could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32ee4a2fa935441f8cc425",
  "collegeId": "5c32ee4a2fa935441f8cc414",
  "roundId": "5c3780c74bb8ea63fc222a62",
  "type": "titular",
  "name": "General Mechanics Confederation",
  "slogan": "Slogan",
  "valid": true,
  "logo": "https://i.imgur.com/ZUtiogP.png",
  "profession": "5c3780c64bb8ea63fc222a56"
}
```

This endpoint retrieves a specific college.

### HTTP Route

`GET lists/<ID>/`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the list to retrieve |

## Update an list

```javascript
import { ListNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc415'

const data = {
  name: 'New Name',
  slogan: 'New Slogan',
  logo: 'https://bit.ly/2RhAGZM',
  profession: '5c3780c94bb8ea63fc222ae4'
}

request
  .put(`lists/${id}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ListNotFound)
      // The college could be found

    if (err instanceof ValidationError)
      // The college could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32ee4a2fa935441f8cc415",
  "collegeId": "5c32ee4a2fa935441f8cc414",
  "roundId": "5c37940a91523a7844adacce",
  "type": "titular",
  "name": "New Name",
  "slogan": "New Slogan",
  "valid": true,
  "logo": "https://bit.ly/2RhAGZM",
  "profession": "5c3780c94bb8ea63fc222ae4"
}
```

This endpoint updates a specific list.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT lists/<ID>/`

### URL Parameters

| Parameter | Description                  |
| --------- | ---------------------------- |
| ID        | The ID of the list to update |

## Delete a list

```javascript
import { ListNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32ee4a2fa935441f8cc415'

request
  .delete(`lists/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ListNotFound)
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

This endpoint deletes a specific list.

### HTTP Route

`DELETE lists/<ID>/`

### URL Parameters

| Parameter | Description                  |
| --------- | ---------------------------- |
| ID        | The ID of the list to delete |
