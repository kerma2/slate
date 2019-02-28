# Project

## Fetch all projects

```javascript
import { CompanyNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c7804542077997c741e6f96'

request
  .get(`companies/${id}/projects`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CompanyNotFound)
      // The company could not be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c7804542077997c741e6f97",
    "companyId": "5c7804542077997c741e6f96",
    "dates": {
      "createdAt": "2019-02-28T15:55:00.679Z",
      "closedAt": null,
      "archivedAt": null
    },
    "shared": false,
    "negotiating": "2019-01-01T00:00:00.000Z"
  }
]
```

This endpoint retrieves all projects within a specific company.

### HTTP Route

`GET companies/<ID>/projects/`

### URL Parameters

| Parameter | Description                                               |
| --------- | --------------------------------------------------------- |
| ID        | The ID of the company in which the projects are retrieved |

## Create a project

```javascript
import { CompanyNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c7804542077997c741e6f96'

const data = {
  shared: true,               // Optional (default: false)
  negotiating: '2018-01-01'   // Mandatory
}

request
  .post(`companies/${id}/projects/`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CompanyNotFound)
      // The company could not be found

    if (err instanceof ValidationError)
      // The project could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c78046a2077997c741e7026",
  "companyId": "5c7804542077997c741e6f96",
  "dates": {
    "createdAt": "2019-02-28T15:55:22.798Z",
    "closedAt": null,
    "archivedAt": null
  },
  "shared": true,
  "negotiating": "2018-01-01T00:00:00.000Z"
}
```

This endpoint creates project within a specific company.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`POST companies/<ID>/projects/`

### URL Parameters

| Parameter | Description                                           |
| --------- | ----------------------------------------------------- |
| ID        | The ID of the company in which the project is created |

## Fetch a project

```javascript
import { ProjectNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c7804542077997c741e6f97'

request
  .get(`projects/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c7804542077997c741e6f97",
  "companyId": "5c7804542077997c741e6f96",
  "dates": {
    "createdAt": "2019-02-28T15:55:00.679Z",
    "closedAt": null,
    "archivedAt": null
  },
  "shared": false,
  "negotiating": "2019-01-01T00:00:00.000Z"
}
```

This endpoint retrieves a specific project.

### HTTP Route

`GET project/<ID>/`

### URL Parameters

| Parameter | Description                       |
| --------- | --------------------------------- |
| ID        | The ID of the project to retrieve |

## Update a project

```javascript
import { ProjectNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c7804542077997c741e6f97'

const data = {
  shared: false,
  negotiating: "2019-02-10"
}

request
  .put(`projects/${id}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof ValidationError)
      // The company could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c7804542077997c741e6f97",
  "companyId": "5c7804542077997c741e6f96",
  "dates": {
    "createdAt": "2019-02-28T15:55:00.679Z",
    "closedAt": null,
    "archivedAt": null
  },
  "shared": false,
  "negotiating": "2019-02-10T00:00:00.000Z"
}
```

This endpoint updates a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT projects/<ID>/`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the project to update |

## Delete a project

```javascript
import { ProjectNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c7804542077997c741e6f97'

request
  .delete(`projects/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint deletes a specific company.

### HTTP Route

`DELETE projects/<ID>/`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the project to delete |
