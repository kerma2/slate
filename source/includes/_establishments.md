# Establishment

## Fetch all establishments

```javascript
import { ProjectNotFound, NoEstablishments } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32d8e48dde18253603bd06'

request
  .get(`projects/${id}/establishments`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could not be found

    if (err instanceof NoEstablishments)
      // No establishments could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c32d8e58dde18253603bd09",
    "projectId": "5c32d8e48dde18253603bd06",
    "name": "Name",
    "state": "init",
    "colleges": ["5c32d8e48dde18253603bd07"],
    "users": ["5c32d8e48dde18253603bd08"],
    "statuses": ["Ouvrier", "Employés", "Techniciens", "Agents de maîtrise", "Ingénieurs", "Cadres"]
  }
]
```

This endpoint retrieves all establishments within a specific project.

### HTTP Route

`GET projects/<ID>/establishments/`

### URL Parameters

| Parameter | Description                                                     |
| --------- | --------------------------------------------------------------- |
| ID        | The ID of the project in which the establishments are retrieved |

## Create an establishment

```javascript
import { ProjectNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b185702a5b72b178b2e9'

const data = {
  name: "Name",   // Mandatory
  statuses: [     // Optional
    "Custom Status",
    "Moar Status"
  ]
}

request
  .post(`projects/${id}/establishments/`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could not be found

    if (err instanceof ValidationError)
      // The establishment could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32d8e58dde18253603bd09",
  "projectId": "5c32d8e48dde18253603bd06",
  "name": "Name",
  "state": "init",
  "colleges": [],
  "users": [],
  "statuses": [
    "Custom Status",
    "Moar Status",
    "Ouvrier",
    "Employés",
    "Techniciens",
    "Agents de maîtrise",
    "Ingénieurs",
    "Cadres"
  ]
}
```

This endpoint creates an establishment within a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`POST projects/<ID>/establishments/`

### URL Parameters

| Parameter | Description                                                 |
| --------- | ----------------------------------------------------------- |
| ID        | The ID of the project in which the establishment is created |

## Fetch an establishment

```javascript
import { EstablishmentNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32d8e58dde18253603bd09'

request
  .get(`establishments/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32d8e58dde18253603bd09",
  "projectId": "5c32d8e48dde18253603bd06",
  "name": "Name",
  "state": "init",
  "colleges": [],
  "users": [],
  "statuses": [
    "Custom Status",
    "Moar Status",
    "Ouvrier",
    "Employés",
    "Techniciens",
    "Agents de maîtrise",
    "Ingénieurs",
    "Cadres"
  ]
}
```

This endpoint retrieves a specific establishment.

### HTTP Route

`GET establishment/<ID>/`

### URL Parameters

| Parameter | Description                             |
| --------- | --------------------------------------- |
| ID        | The ID of the establishment to retrieve |

## Update an establishment

```javascript
import { EstablishmentNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32d8e58dde18253603bd09'

const data = {
  name: "New Name"
}

request
  .put(`establishments/${id}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could not be found

    if (err instanceof ValidationError)
      // The establishment could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32d8e58dde18253603bd09",
  "projectId": "5c32d8e48dde18253603bd06",
  "name": "New Name",
  "state": "init",
  "colleges": [],
  "users": [],
  "statuses": [
    "Custom Status",
    "Moar Status",
    "Ouvrier",
    "Employés",
    "Techniciens",
    "Agents de maîtrise",
    "Ingénieurs",
    "Cadres"
  ]
}
```

This endpoint updates a specific establishment.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT establishments/<ID>/`

### URL Parameters

| Parameter | Description                           |
| --------- | ------------------------------------- |
| ID        | The ID of the establishment to update |

## Delete a establishment

```javascript
import { EstablishmentNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32d8e58dde18253603bd09'

request
  .delete(`establishments/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific project.

### HTTP Route

`DELETE establishments/<ID>/`

### URL Parameters

| Parameter | Description                           |
| --------- | ------------------------------------- |
| ID        | The ID of the establishment to delete |

## Fetch all statuses

```javascript
import { EstablishmentNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32d8e58dde18253603bd09'

request
  .get(`establishments/${id}/statuses`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
["Custom Status", "Moar Status", "Ouvrier", "Employés", "Techniciens", "Agents de maîtrise", "Ingénieurs", "Cadres"]
```

This endpoint retrieves all statuses within a specific establishment.

### HTTP Route

`GET establishments/<ID>/statuses/`

### URL Parameters

| Parameter | Description                                                      |
| --------- | ---------------------------------------------------------------- |
| ID        | The ID of the establishments in which the statuses are retrieved |

## Create statuses

```javascript
import { ValidationError, EstablishmentNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32d8e58dde18253603bd09'

const data = [
  "Status 1",
  "Status 2",
  "Status 3",
]

request
  .post(`establishments/${id}/statuses`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could be found

    if (err instanceof ValidationError)
      // The statuses could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  "Status 1",
  "Status 2",
  "Status 3",
  "Custom Status",
  "Moar Status",
  "Ouvrier",
  "Employés",
  "Techniciens",
  "Agents de maîtrise",
  "Ingénieurs",
  "Cadres"
]
```

This endpoint creates statuses within a specific establishment.

### HTTP Route

`POST establishments/<ID>/statuses/`

### URL Parameters

| Parameter | Description                                                    |
| --------- | -------------------------------------------------------------- |
| ID        | The ID of the establishments in which the statuses are created |

## Update a status

```javascript
import { EstablishmentNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32d8e58dde18253603bd09'
const status = 'Status 1'

const data = 'A Real Name'

request
  .put(`establishments/${id}/statuses/${status}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could be found

    if (err instanceof ValidationError)
      // The status could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  "A Real Name",
  "Status 2",
  "Status 3",
  "Custom Status",
  "Moar Status",
  "Ouvrier",
  "Employés",
  "Techniciens",
  "Agents de maîtrise",
  "Ingénieurs",
  "Cadres"
]
```

This endpoint updates a specific status within a specific establishment.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT establishments/<ID>/statuses/<STATUS>`

### URL Parameters

| Parameter | Description                                                |
| --------- | ---------------------------------------------------------- |
| ID        | The ID of the establishment in which the status is updated |
| STATUS    | The STATUS to update                                       |

## Delete a status

```javascript
import { EstablishmentNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32d8e58dde18253603bd09'
const status = 'Status 2'

request
  .delete(`establishments/${id}/statuses/${status}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof EstablishmentNotFound)
      // The establishment could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific status within a specific project.

<aside class="notice">
Removing a status will automatically delete all electors linked to this status as well any reference within colleges
</aside>

### HTTP Route

`DELETE establishments/<ID>/statuses/<STATUS>`

### URL Parameters

| Parameter | Description                                                |
| --------- | ---------------------------------------------------------- |
| ID        | The ID of the establishment in which the status is deleted |
| STATUS    | The STATUS to delete                                       |
