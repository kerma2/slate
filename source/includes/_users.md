# User

## Create a user

```javascript
import { ValidationError, InvalidRequestFormat } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const data = {
  companyId: '5c4911487d93561947c5fe48',  // Partially Mandatory
  username: 'name',                       // Mandatory
  password: 'pwd',                        // Mandatory
  fullname: 'User',                       // Mandatory
  mail: 'user@domain.com',                // Optional
  civility: 'm',                          // Mandatory
  access: 'admin'                         // Mandatory
}

request
  .post(`users`, data)
  .then(res => console.log(res.data))
  .then(() => next())
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof InvalidRequestFormat)
      // 1. The access is invalid
      // 2. No password provided
      // 3. The user is missing the companyId Ref (only for 'employer' and 'control')

    if (err instanceof ValidationError)
      // The user could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c490a5a04f33110c6195cc7",
  "companyId": null,
  "projectId": null,
  "username": "name",
  "mail": "user@domain.com",
  "fullname": "User",
  "civility": "m",
  "address": "none",
  "hiring": 0,
  "birth": {
    "date": "1970-01-01T00:00:00.000Z",
    "county": "none",
    "place": "none"
  }
}
```

This creates a user within a specific access.

Be sure to check how to handle [ValidationError](#validationerror).

<aside class="notice">
Only user with access <code>admin</code>, <code>employer</code>, <code>control</code> and <code>provider</code> can be created with this route.
</aside>

<aside class="notice">
Users <code>admin</code> and <code>control</code> must be linked to a company.
</aside>

### HTTP Route

`POST user/`

## Fetch a user

```javascript
import { UserNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c490cd192f0f21359f5e1ed'

request
  .get(`users/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof UserNotFound)
      // The user could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c490cd192f0f21359f5e1ed",
  "companyId": null,
  "projectId": "5c490cd092f0f21359f5e1d1",
  "username": "ba4f1d85",
  "mail": null,
  "fullname": "Worker 1",
  "civility": "m",
  "address": "Address",
  "hiring": 31536000000,
  "birth": {
    "date": "1990-01-01T00:00:00.000Z",
    "county": "County",
    "place": "City/Town"
  }
}
```

This endpoint retrieves a specific user.

### HTTP Route

`GET users/<ID>/`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the user to retrieve |

## Update an user

```javascript
import { UserNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c490cd192f0f21359f5e1ed'

const data = {
  mail: "new@mail.com",
  fullname: 'Worker 1',
  civility: 'mme',
  address: 'New Address',
  hiring: 44444000000,
  birth: {
    date: '1991-03-02T17:17:17.000Z',
    county: 'New County',
    place: 'New City/Town'
  }
}

request
  .put(`users/${id}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof UserNotFound)
      // The user could be found

    if (err instanceof ValidationError)
      // The user could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c490cd192f0f21359f5e1ed",
  "companyId": null,
  "projectId": "5c490cd092f0f21359f5e1d1",
  "username": "ba4f1d85",
  "mail": "new@mail.com",
  "fullname": "Worker 1",
  "civility": "mme",
  "address": "New Address",
  "hiring": 44444000000,
  "birth": {
    "date": "1991-03-02T17:17:17.000Z",
    "county": "New County",
    "place": "New City/Town"
  }
}
```

This endpoint updates a specific user.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT users/<ID>/`

### URL Parameters

| Parameter | Description                  |
| --------- | ---------------------------- |
| ID        | The ID of the user to update |

## Delete a list

```javascript
import { UserNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c490cd192f0f21359f5e1ed'

request
  .delete(`users/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof UserNotFound)
      // The user could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific user.

<aside class="notice">
Depending on accesses, deleting a user will remove any reference of the user in any model. 
</aside>

### HTTP Route

`DELETE users/<ID>/`

### URL Parameters

| Parameter | Description                  |
| --------- | ---------------------------- |
| ID        | The ID of the user to delete |
