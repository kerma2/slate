# Document

## Fetch all documents

```javascript
import { ProjectNotFound, NoDocuments } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be5'

request
  .get(`projects/${id}/documents`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof NoDocuments)
      // No documents could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
TODO
```

This endpoint retrieves all documents within a specific project.

### HTTP Route

`GET projects/<ID>/documents/`

### URL Parameters

| Parameter | Description                                                |
| --------- | ---------------------------------------------------------- |
| ID        | The ID of the project in which the documents are retrieved |

## Create a document

```javascript
import { ProjectNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be5'

const data = {
  // TODO
}

request
  .post(`projects/${id}/documents/`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof ValidationError)
      // The document could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
TODO
```

This endpoint creates documents within a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`POST projects/<ID>/documents/`

### URL Parameters

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| ID        | The ID of the project in which the document is created |

## Fetch a document

```javascript
import { ProjectNotFound, DocumentNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be9'
const projectId = '5c32b832a67a297bb5028be5'

request
  .get(`projects/${projectId}/documents/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof DocumentNotFound)
      // The document could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
TODO
```

This endpoint retrieves a specific document within a specific project.

### HTTP Route

`GET project/<PROJECT_ID>/documents/<ID>/`

### URL Parameters

| Parameter  | Description                                              |
| ---------- | -------------------------------------------------------- |
| PROJECT_ID | The ID of the project in which the document is retrieved |
| ID         | The ID of the document to retrieve                       |

## Update a document

```javascript
import {
  ProjectNotFound,
  DocumentNotFound,
  ValidationError
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be9'
const projectId = '5c32b832a67a297bb5028be5'

const data = {
  // TODO
}

request
  .put(`projects/${projectId}/documents/${id}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof DocumentNotFound)
      // The document could be found

    if (err instanceof ValidationError)
      // The document could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
TODO
```

This endpoint updates a specific document within a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT project/<PROJECT_ID>/documents/<ID>/`

### URL Parameters

| Parameter  | Description                                            |
| ---------- | ------------------------------------------------------ |
| PROJECT_ID | The ID of the project in which the document is updated |
| ID         | The ID of the document to update                       |

## Delete a document

```javascript
import {
  ProjectNotFound,
  DocumentNotFound,
  ValidationError
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be9'
const projectId = '5c32b832a67a297bb5028be5'

request
  .delete(`projects/${projectId}/documents/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof DocumentNotFound)
      // The document could be found

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

`DELETE project/<PROJECT_ID>/documents/<ID>/`

### URL Parameters

| Parameter  | Description                                           |
| ---------- | ----------------------------------------------------- |
| PROJECT_ID | The ID of the project in which the document is delete |
| ID         | The ID of the document to delete                      |
