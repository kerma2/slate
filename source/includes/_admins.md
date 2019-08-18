# Admins

## Authenticate an admin

```javascript
const data = {
  username: 'admin',
  password: 'SomePassword123'
}

request
  .post(`admin/login`, data)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof AdminNotFound)
      // The admin could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "admin": {
    "_id": "5d5910a2c8b3561e5e51f354",
    "firstname": "admin",
    "lastname": "nate",
    "username": "admin",
    "type": "Admin"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVkNTkxMGEyYzhiMzU2MWU1ZTUxZjM1NCIsImlhdCI6MTU2NjEyMDE3M30.aWkuxvxh0KnhjGixTxEs6rKS0iQ75HDyti9WpY0Jils"
}
```

This endpoint authenticates a specific admin.

### HTTP Route

`POST admin/login`

## Get admins

```javascript
request
  .get(`admin`)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The logged in user does not have access rights

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{
  "admins": [
    {
      "_id": "5d5910a2c8b3561e5e51f354",
      "firstname": "admin",
      "lastname": "nate",
      "username": "admin",
      "type": "Admin"
    },
    ...
  ]
}
```

This endpoint retrieves the list of all admins.

<aside class="warning">
ADMIN ONLY PROTECTED ENDPOINT
</aside>

### HTTP Route

`GET admin`

## Create an admin

```javascript
const data = {
  firstname: "admin",
  lastname: "nate",
  username: "admin",
  password: "SomePassword123"
}

request
  .post(`admin/create`, data)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The logged in user does not have access rights

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{
  "admin": {
    "_id": "5d5910a2c8b3561e5e51f354",
    "firstname": "admin",
    "lastname": "nate",
    "username": "admin",
    "type": "Admin"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVkNTkxMGEyYzhiMzU2MWU1ZTUxZjM1NCIsImlhdCI6MTU2NjEyMDU2NX0.zaHtAGytlbdM_IpaoyG8WD4I0qDCCrf1AZi14lZm6NU"
}
```

This endpoint creates a specifics admin.

<aside class="warning">
ADMIN ONLY PROTECTED ENDPOINT
</aside>

### HTTP Route

`POST admin/create`

## Get beta keys

```javascript
request
  .get(`admin/beta/keys`)
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The logged in user does not have access rights

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{
  "keys": [
    "d8fde80b",
    "b90b98c0",
    "340ed558",
    "05155c1b",
    "2084b2c8",
    "992abfde",
    "fad2c06b",
    "90084fc2",
    "31d2ed7c"
  ]
}
```

This endpoint retrieves all currently stored beta keys.

<aside class="warning">
ADMIN ONLY PROTECTED ENDPOINT
</aside>

### HTTP Route

`GET admin/beta/keys`

## Create beta keys

```javascript

const nb = 5

request
  .post(`admin/beta/keys`, { nb })
  .then(res => console.log(res.data))
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The logged in user does not have access rights

    // Handle any other errors
  })
}
```

> The above command returns JSON structured like this:

```json
{
  "keys": [
    "d8fde80b",
    "b90b98c0",
    "340ed558",
    "05155c1b",
    "2084b2c8",
    "992abfde",
    "fad2c06b",
    "90084fc2",
    "31d2ed7c",
    "4bc6dd4f",
    "51b46e65",
    "fad319bb",
    "e25d5f99",
    "bcbbf91e"
  ]
}
```

This endpoint creates a given number of beta keys but it retrieves all currently stored beta keys whatsoever.

<aside class="warning">
ADMIN ONLY PROTECTED ENDPOINT
</aside>

### HTTP Route

`POST admin/beta/keys`
