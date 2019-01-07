# Task

## Fetch all tasks

```javascript
import { ProjectNotFound, NoTasks } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be5'

request
  .get(`projects/${id}/tasks`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof NoTasks)
      // No tasks could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c32b832a67a297bb5028be9",
    "name": "Default Task",
    "type": "action",
    "description": "The description of the task.",
    "date": "2019-04-01T00:00:00.000Z",
    "ref": {
      "schema": "Establishment",
      "id": "5c32b832a67a297bb5028be8"
    },
    "completed": false,
    "docs": ["5c32b832a67a297bb5028be6", "5c32b832a67a297bb5028be7"],
    "parent": null,
    "children": ["5c32b185702a5b72b178b2a3"],
    "accesses": [
      {
        "rights": {
          "removable": false,
          "editable": false,
          "validate": true
        },
        "_id": "5c32b832a67a297bb5028bea",
        "access": "employer"
      },
      {
        "rights": {
          "removable": true,
          "editable": true,
          "validate": true
        },
        "_id": "5c32b832a67a297bb5028beb",
        "access": "admin"
      }
    ]
  }
]
```

This endpoint retrieves all tasks within a specific project.

### HTTP Route

`GET projects/<ID>/tasks/`

### URL Parameters

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| ID        | The ID of the project in which the tasks are retrieved |

## Fetch important tasks

```javascript
import { ProjectNotFound, NoTasks } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be5'

const nb = 2

request
  .get(`projects/${id}/tasks/list/${nb}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof NoTasks)
      // No tasks could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c32b832a67a297bb5028ac8",
    "name": "Task 1",
    "type": "action",
    "description": "The task ends very soon.",
    "date": "2019-04-01T00:00:00.000Z",
    "ref": {
      "schema": "Establishment",
      "id": "5c32b832a67a297bb5028be8"
    },
    "completed": false,
    "docs": [],
    "parent": null,
    "children": [],
    "accesses": [
      {
        "rights": {
          "removable": true,
          "editable": true,
          "validate": true
        },
        "_id": "5c32b832a67a297bb5028beb",
        "access": "admin"
      }
    ]
  },
  {
    "_id": "5c32b832a67a297bb5028ac9",
    "name": "Task 2",
    "type": "action",
    "description": "The task ends soon, but not so much.",
    "date": "2019-04-10T00:00:00.000Z",
    "ref": {
      "schema": "Establishment",
      "id": "5c32b832a67a297bb5028be8"
    },
    "completed": false,
    "docs": [],
    "parent": null,
    "children": [],
    "accesses": [
      {
        "rights": {
          "removable": true,
          "editable": true,
          "validate": true
        },
        "_id": "5c32b832a67a297bb5028beb",
        "access": "admin"
      }
    ]
  }
]
```

This endpoint retrieves the most important tasks within a specific project ordered by dates ascending.

### HTTP Route

`GET projects/<ID>/tasks/list/<NB>`

### URL Parameters

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| ID        | The ID of the project in which the tasks are retrieved |
| NB        | The number of tasks to retrieve                        |

## Create a task

```javascript
import { ProjectNotFound, ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be5'

const data = {
  name: 'Name',                         // Mandatory
  type: 'infos',                        // Mandatory
  description: 'The description.',      // Optional
  date: '2019-04-05',                   // Mandatory
  docs: ['5c32b832a67a297bb5028be6'],   // Optional
  parent: '5c32b832a67a297bb5028be9',   // Optional
  accesses: [                           // Optional (the admin access is automatically added)
    {
      rights: {
        removable: false,               // Optional (default: false)
        editable: true,                 // Optional (default: false)
        validate: true                  // Optional (default: false)
      },
      access: 'employer'                // Mandatory (par access)
    }
  ]
}

request
  .post(`projects/${id}/tasks/`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof ValidationError)
      // The task could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32b832a67a297bb5028ba1",
  "name": "Name",
  "type": "infos",
  "description": "The description.",
  "date": "2019-04-05T00:00:00.000Z",
  "ref": {
    "schema": "Establishment",
    "id": "5c32b832a67a297bb5028be8"
  },
  "completed": false,
  "docs": ["5c32b832a67a297bb5028be6"],
  "parent": "5c32b832a67a297bb5028be9",
  "children": [],
  "accesses": [
    {
      "rights": {
        "removable": false,
        "editable": true,
        "validate": true
      },
      "_id": "5c32b832a67a297bb5028be2",
      "access": "employer"
    },
    {
      "rights": {
        "removable": true,
        "editable": true,
        "validate": true
      },
      "_id": "5c32b832a67a297bb5028be1",
      "access": "admin"
    }
  ]
}
```

This endpoint creates tasks within a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`POST projects/<ID>/tasks/`

### URL Parameters

| Parameter | Description                                        |
| --------- | -------------------------------------------------- |
| ID        | The ID of the project in which the task is created |

## Fetch a task

```javascript
import { ProjectNotFound, TaskNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be9'
const projectId = '5c32b832a67a297bb5028be5'

request
  .get(`projects/${projectId}/tasks/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof TaskNotFound)
      // The task could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32b832a67a297bb5028be9",
  "name": "Default Task",
  "type": "action",
  "description": "The description of the task.",
  "date": "2019-04-01T00:00:00.000Z",
  "ref": {
    "schema": "Establishment",
    "id": "5c32b832a67a297bb5028be8"
  },
  "completed": false,
  "docs": ["5c32b832a67a297bb5028be6", "5c32b832a67a297bb5028be7"],
  "parent": null,
  "children": ["5c32b185702a5b72b178b2a3"],
  "accesses": [
    {
      "rights": {
        "removable": false,
        "editable": false,
        "validate": true
      },
      "_id": "5c32b832a67a297bb5028bea",
      "access": "employer"
    },
    {
      "rights": {
        "removable": true,
        "editable": true,
        "validate": true
      },
      "_id": "5c32b832a67a297bb5028beb",
      "access": "admin"
    }
  ]
}
```

This endpoint retrieves a specific task within a specific project.

### HTTP Route

`GET project/<PROJECT_ID>/tasks/<ID>/`

### URL Parameters

| Parameter  | Description                                          |
| ---------- | ---------------------------------------------------- |
| PROJECT_ID | The ID of the project in which the task is retrieved |
| ID         | The ID of the task to retrieve                       |

## Update a task

```javascript
import {
  ProjectNotFound,
  TaskNotFound,
  InvalidAccess,
  ValidationError
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be9'
const projectId = '5c32b832a67a297bb5028be5'

// Setting a task as completed: requires 'validate' access
// Updating any other fields: requires 'editable' access
// Updating/Creating accesses: only for ADMIN

const data = {
  completed: true,
  name: 'New name',
  description: 'New description.',
  date: "2019-06-24",
  docs: ['5c32b832a67a297bb5028ca8'],   // This will not delete previous documents
  accesses: [                           // This will modify existing accesses or create new accesses
    {
      rights: {
        removable: false,
        editable: false,
        validate: true
      },
      access: 'employer'
    }
  ]
}

request
  .put(`projects/${projectId}/tasks/${id}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof TaskNotFound)
      // The task could be found

    if (err instanceof InvalidAccess)
      // The user does not have the rights to update this task

    if (err instanceof ValidationError)
      // The task could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c32b832a67a297bb5028ba1",
  "name": "New Name",
  "type": "infos",
  "description": "New description.",
  "date": "2019-06-24T00:00:00.000Z",
  "ref": {
    "schema": "Establishment",
    "id": "5c32b832a67a297bb5028be8"
  },
  "completed": true,
  "docs": ["5c32b832a67a297bb5028ca8"],
  "parent": "5c32b832a67a297bb5028be9",
  "children": [],
  "accesses": [
    {
      "rights": {
        "removable": false,
        "editable": false,
        "validate": true
      },
      "_id": "5c32b832a67a297bb5028be2",
      "access": "employer"
    },
    {
      "rights": {
        "removable": true,
        "editable": true,
        "validate": true
      },
      "_id": "5c32b832a67a297bb5028be1",
      "access": "admin"
    }
  ]
}
```

This endpoint updates a specific task within a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT project/<PROJECT_ID>/tasks/<ID>/`

### URL Parameters

| Parameter  | Description                                        |
| ---------- | -------------------------------------------------- |
| PROJECT_ID | The ID of the project in which the task is updated |
| ID         | The ID of the task to update                       |

## Delete a task

```javascript
import {
  ProjectNotFound,
  TaskNotFound,
  InvalidAccess,
  ValidationError
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be9'
const projectId = '5c32b832a67a297bb5028be5'

request
  .delete(`projects/${projectId}/tasks/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ProjectNotFound)
      // The project could be found

    if (err instanceof TaskNotFound)
      // The task could be found

    if (err instanceof InvalidAccess)
      // The user does not have the rights to delete this task

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

`DELETE project/<PROJECT_ID>/tasks/<ID>/`

### URL Parameters

| Parameter  | Description                                       |
| ---------- | ------------------------------------------------- |
| PROJECT_ID | The ID of the project in which the task is delete |
| ID         | The ID of the task to delete                      |
