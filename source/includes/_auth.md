# Authentication

## Verify a user

```javascript
const data = { mail: 'tina.smith@mail.com' }

request
  .post(`auth/verify`, data)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof UserNotFound)
      // The user could not be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{ "exists": true }
```

This endpoint checks if a specific user exists.

### HTTP Route

`POST auth/verify`

## Validate a user

```javascript
const data = { mail: 'tina.smith@mail.com' }

request
  .post(`auth/validation`, data)
  .then(res => console.log(res.data))
  .catch(err => {
    // Handle any errors
  })
}
```

> The above command returns JSON structured like this:

```json
{ "success": true }
```

This endpoint creates a temporary validator for a specific user.

<aside class="notice">
The validator will expire after 10min.
</aside>

<aside class="notice">
This will send a validation mail to the user.
</aside>

### HTTP Route

`POST auth/validation`

## Authenticate a user

```javascript
const data = {
  code: 'FF3371',
  mail: 'tina.smith@mail.com'
}

request
  .post(`auth/login`, data)
  .then(res => {
    // This will set the 'Authorization' headers in the axios requested instance
    request.defaults.headers.common['Authorization'] = `JWT ${res.data.token}`

    console.log(res.data)
  })
  .catch(err => {
    if (err instanceof InvalidCode)
      // Invalid validator code is invalid

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{
  "user": {
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
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVjNDkxYTY1YWZjYTY2MjA0ZTI4MWZkZCIsImlhdCI6MTU0ODMzMDg1MywiZXhwIjoxNTQ4OTM1NjUzfQ.3sH4OTWk9STic95FaoCtOP13f2qge3GRnGy79j2Fle4"
}
```

This endpoint authenticates a specifics user.

### HTTP Route

`POST auth/login`

## Register a user

```javascript
const data = {
  key: '73a5927e',
  firstname: "tina",
  lastname: "smith",
  username: "tina",
  mail: 'tina.smith@mail.com',
  year: 1,
  country: "FR",
  lang: "fr",
  curriculum: "Accounting & Finance",
  university: "Griffith College",
}

request
  .post(`auth/login`, data)
  .then(res => {
    // This will set the 'Authorization' headers in the axios requested instance
    request.defaults.headers.common['Authorization'] = `JWT ${res.data.token}`

    console.log(res.data)
  })
  .catch(err => {
    if (err instanceof BetaKeyNotFound)
      // The beta key provided does not exists

    if (err instanceof ValidationError)
      // The register form has invalid/missing fields

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{
  "user": {
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
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVjNDkxYTY1YWZjYTY2MjA0ZTI4MWZkZCIsImlhdCI6MTU0ODMzMDg1MywiZXhwIjoxNTQ4OTM1NjUzfQ.3sH4OTWk9STic95FaoCtOP13f2qge3GRnGy79j2Fle4"
}
```

This endpoint registers a specifics user.

<aside class="notice">
The beta key will delete if the register process is completed.
</aside>

<aside class="notice">
A couchdb instance (used as cloud) is automatically created for the newly created user
</aside>

### HTTP Route

`POST auth/login`
