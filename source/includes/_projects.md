# Project

## Fetch all projects

```javascript
import { CompanyNotFound, NoProjects } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b185702a5b72b178b2e9'

request
  .get(`companies/${id}/projects`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CompanyNotFound)
      // The company could not be found

    if (err instanceof NoProjects)
      // No projects could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c32b186702a5b72b178b2ea",
    "companyId": "5c32b185702a5b72b178b2e9",
    "dates": { "createdAt": "2019-01-07T01:55:18.123Z", "closedAt": null, "archivedAt": null },
    "shared": false,
    "establishments": ["5c32b185702a5b72b178b2a1"]
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

const id = '5c32b185702a5b72b178b2e9'

const data = {
  shared: true  // Optional
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
  "_id": "5c32b186702a5b72b178b2ea",
  "companyId": "5c32b185702a5b72b178b2e9",
  "dates": { "createdAt": "2019-01-07T01:55:18.123Z", "closedAt": null, "archivedAt": null },
  "shared": true,
  "establishments": []
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

const id = '5c32b186702a5b72b178b4a2'

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
  "_id": "5c32b186702a5b72b178b4a2",
  "companyId": "5c32b185702a5b72b178b2e9",
  "dates": { "createdAt": "2019-01-07T01:55:18.123Z", "closedAt": null, "archivedAt": null },
  "shared": false,
  "establishments": ["5c32b185702a5b72b178b2a1"]
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

const id = '5c32b186702a5b72b178b4a2'

const data = {
  shared: false
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
  "_id": "5c32b186702a5b72b178b4a2",
  "companyId": "5c32b185702a5b72b178b2e9",
  "dates": { "createdAt": "2019-01-07T01:55:18.123Z", "closedAt": null, "archivedAt": null },
  "shared": false,
  "establishments": []
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

const id = '5c32b186702a5b72b178b4a2'

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
