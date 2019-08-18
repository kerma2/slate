# Users

## Get users

```javascript
request
  .get(`users`)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The logged in user does not have access rights

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5d5910a495aaab1e7c756e6e",
    "firstname": "tina",
    "lastname": "smith",
    "username": "tina",
    "mail": "tina.smith@mail.com",
    "universityId": "5d59109a6c92671dd20aaaee",
    "curriculumId": "5d5910919cb03b1d9cf6f849",
    "year": 1,
    "country": "FR",
    "lang": "fr",
    "theme": "Light",
    "curriculum": "Accounting & Finance",
    "university": "Griffith College"
  },
  ...
]
```

This endpoint retrieves basic informations about all users.

<aside class="warning">
ADMIN ONLY PROTECTED ENDPOINT
</aside>

### HTTP Route

`GET users`

## Get a user

```javascript
const id = '5d5910a495aaab1e7c756e6e'

request
  .get(`users/${id}`)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The logged in user does not have access rights

    if (err instanceof UserNotFound)
      // The user could not be found

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5d5910a495aaab1e7c756e6e",
  "firstname": "tina",
  "lastname": "smith",
  "username": "tina",
  "mail": "tina.smith@mail.com",
  "universityId": "5d59109a6c92671dd20aaaee",
  "curriculumId": "5d5910919cb03b1d9cf6f849",
  "year": 1,
  "country": "FR",
  "lang": "fr",
  "theme": "Light",
  "curriculum": "Accounting & Finance",
  "university": "Griffith College"
}
```

This endpoint retrieves basic informations about a specific user.

<aside class="notice">
Users can only fetch informations about themselves.
</aside>

### HTTP Route

`GET users/<ID>`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the user to retrieve |

## Update a user

```javascript
const id = '5d5910a495aaab1e7c756e6e'

const data = {
  firstname: 'new',
  lastname: 'name'
}

request
  .put(`users/${id}`, data)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The logged in user does not have access rights

    if (err instanceof UserNotFound)
      // The user could not be found

    if (err instanceof ValidationError)
      // Some fields have invalid value

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5d5910a495aaab1e7c756e6e",
  "firstname": "new",
  "lastname": "name",
  "username": "tina",
  "mail": "tina.smith@mail.com",
  "universityId": "5d59109a6c92671dd20aaaee",
  "curriculumId": "5d5910919cb03b1d9cf6f849",
  "year": 1,
  "country": "FR",
  "lang": "fr",
  "theme": "Light",
  "curriculum": "Accounting & Finance",
  "university": "Griffith College"
}
```

This endpoint updates a specific user.

<aside class="notice">
Users can only update informations about themselves.
</aside>

### HTTP Route

`PUT users/<ID>`

### URL Parameters

| Parameter | Description                  |
| --------- | ---------------------------- |
| ID        | The ID of the user to update |

## Delete a user

```javascript
const id = '5d5910a495aaab1e7c756e6e'

request
  .delete(`users/${id}`)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The logged in user does not have access rights

    if (err instanceof UserNotFound)
      // The user could not be found

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{ "success": true }
```

This endpoint deletes a specific user.

<aside class="notice">
Users can only delete their own account.
</aside>

<aside class="notice">
This will also delete their couchdb instance.
</aside>

### HTTP Route

`DELETE users/<ID>`

### URL Parameters

| Parameter | Description                  |
| --------- | ---------------------------- |
| ID        | The ID of the user to delete |

## Compact a user's cloud

```javascript
const id = '5d5910a495aaab1e7c756e6e'

request
  .post(`users/${id}/compact`)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The logged in user does not have access rights

    if (err instanceof UserNotFound)
      // The user could not be found

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{ "success": true }
```

This endpoint compacts a specific user's couchdb instance.

This process will delete all the cached data and the temporary trash (within the couchdb instance).

<aside class="notice">
Users can only compact their own couchdb instance.
</aside>

### HTTP Route

`POST users/<ID>/compact`

### URL Parameters

| Parameter | Description                  |
| --------- | ---------------------------- |
| ID        | The ID of the user linked to the couchdb instance to compact |
