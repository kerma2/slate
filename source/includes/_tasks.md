# Task

## Fetch all tasks

```javascript
import { ProjectNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c7856889b3d4811e2503558'

request
  .get(`projects/${id}/tasks`)
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
[
  {
    "_id": "5c79581e7d47c13c17a9beca",
    "name": "Default Task",
    "type": "action",
    "description": null,
    "date": "2019-04-01T00:00:00.000Z",
    "refs": [
      {
        "name": "Project",
        "id": "5c79581d7d47c13c17a9bec5"
      }
    ],
    "completed": false,
    "docs": ["5c79581e7d47c13c17a9bec9"],
    "parent": null,
    "children": [
      {
        "_id": "5c79581e7d47c13c17a9becb",
        "name": "First Task",
        "type": "infos",
        "description": null,
        "date": "2020-01-01T00:00:00.000Z",
        "refs": [
          {
            "name": "Establishment",
            "id": "5c79581e7d47c13c17a9bec6"
          }
        ],
        "completed": false,
        "docs": [],
        "parent": "5c79581e7d47c13c17a9beca",
        "children": [],
        "accesses": [
          {
            "rights": {
              "removable": true,
              "editable": true,
              "validate": true
            },
            "access": "admin"
          }
        ]
      },
      {
        "_id": "5c79581e7d47c13c17a9becc",
        "name": "Second Task",
        "type": "infos",
        "description": null,
        "date": "2020-01-02T00:00:00.000Z",
        "refs": [
          {
            "name": "Establishment",
            "id": "5c79581e7d47c13c17a9bec6"
          }
        ],
        "completed": false,
        "docs": [],
        "parent": "5c79581e7d47c13c17a9beca",
        "children": [],
        "accesses": [
          {
            "rights": {
              "removable": true,
              "editable": true,
              "validate": true
            },
            "access": "admin"
          }
        ]
      },
      {
        "_id": "5c79581e7d47c13c17a9becd",
        "name": "Third Task",
        "type": "infos",
        "description": null,
        "date": "2020-01-03T00:00:00.000Z",
        "refs": [
          {
            "name": "Establishment",
            "id": "5c79581e7d47c13c17a9bec6"
          }
        ],
        "completed": false,
        "docs": [],
        "parent": "5c79581e7d47c13c17a9beca",
        "children": [],
        "accesses": [
          {
            "rights": {
              "removable": true,
              "editable": true,
              "validate": true
            },
            "access": "admin"
          }
        ]
      }
    ],
    "accesses": [
      {
        "rights": {
          "removable": false,
          "editable": false,
          "validate": true
        },
        "access": "employer"
      },
      {
        "rights": {
          "removable": true,
          "editable": true,
          "validate": true
        },
        "access": "admin"
      }
    ]
  }
]
```

This endpoint retrieves all tasks within a specific project.

<aside class="notice">
This endpoint has a default recursive on task's children. 
</aside>

### HTTP Route

`GET projects/<ID>/tasks/`

### URL Parameters

| Parameter | Description                                            |
| --------- | ------------------------------------------------------ |
| ID        | The ID of the project in which the tasks are retrieved |

## Fetch important tasks

```javascript
import { ProjectNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c7856889b3d4811e2503558'
const nb = 2

request
  .get(`projects/${id}/tasks/list/${nb}`)
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
[
  {
    "_id": "5c7858fb495a9c15945b644b",
    "name": "First Task",
    "type": "infos",
    "description": null,
    "date": "2020-01-01T00:00:00.000Z",
    "refs": [
      {
        "name": "Establishment",
        "id": "5c7858fb495a9c15945b6446"
      }
    ],
    "completed": false,
    "docs": [],
    "parent": "5c7858fb495a9c15945b644a",
    "children": [],
    "accesses": [
      {
        "rights": {
          "removable": true,
          "editable": true,
          "validate": true
        },
        "access": "admin"
      }
    ]
  },
  {
    "_id": "5c7858fb495a9c15945b644c",
    "name": "Second Task",
    "type": "infos",
    "description": null,
    "date": "2020-01-02T00:00:00.000Z",
    "refs": [
      {
        "name": "Establishment",
        "id": "5c7858fb495a9c15945b6446"
      }
    ],
    "completed": false,
    "docs": [],
    "parent": "5c7858fb495a9c15945b644a",
    "children": [],
    "accesses": [
      {
        "rights": {
          "removable": true,
          "editable": true,
          "validate": true
        },
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

const id = '5c7856889b3d4811e2503558'

const data = {
  name: 'Name',                       // Mandatory
  type: 'infos',                      // Mandatory
  description: 'Description',         // Optional (default: null)
  date: '2019-03-01',                 // Mandatory
  ref: [                              // Optional (default: [])
    {
      schema: 'Establishment',        // Mandatory (by ref)
      id: '5c7858fb495a9c15945b6446'  // Mandatory (by ref)
    }
  ],
  docs: ['5c7858fb495a9c15945b6449'], // Optional (default: [])
  parent: '5c7858fb495a9c15945b644a', // Optional (default: null)
  accesses: [                         // Optional
    {
      access: 'employer',             // Mandatory (by access)
      rights: {
        removable: true,              // Optional (default: false)
        editable: true,               // Optional (default: false)
        validate: true                // Optional (default: false)
      }
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
  "_id": "5c785917495a9c15945b64cf",
  "name": "Name",
  "type": "infos",
  "description": "Description",
  "date": "2019-03-01T00:00:00.000Z",
  "refs": [],
  "completed": false,
  "docs": ["5c7858fb495a9c15945b6449"],
  "parent": "5c7858fb495a9c15945b644b",
  "children": [],
  "accesses": [
    {
      "rights": {
        "removable": true,
        "editable": true,
        "validate": true
      },
      "access": "employer"
    },
    {
      "rights": {
        "removable": true,
        "editable": true,
        "validate": true
      },
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

const id = '5c7858fb495a9c15945b644a'
const projectId = '5c7856889b3d4811e2503558'

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
  "_id": "5c7858fb495a9c15945b644a",
  "name": "Default Task",
  "type": "action",
  "description": null,
  "date": "2019-04-01T00:00:00.000Z",
  "refs": [
    {
      "name": "Project",
      "id": "5c7858fb495a9c15945b6445"
    }
  ],
  "completed": false,
  "docs": ["5c7858fb495a9c15945b6449"],
  "parent": null,
  "children": [
    {
      "_id": "5c7858fb495a9c15945b644b",
      "name": "First Task",
      "type": "infos",
      "description": null,
      "date": "2020-01-01T00:00:00.000Z",
      "refs": [
        {
          "name": "Establishment",
          "id": "5c7858fb495a9c15945b6446"
        }
      ],
      "completed": false,
      "docs": [],
      "parent": "5c7858fb495a9c15945b644a",
      "children": [
        {
          "_id": "5c785917495a9c15945b64cf",
          "name": "Name",
          "type": "infos",
          "description": "Description",
          "date": "2019-03-01T00:00:00.000Z",
          "refs": [],
          "completed": false,
          "docs": ["5c7858fb495a9c15945b6449"],
          "parent": "5c7858fb495a9c15945b644b",
          "children": [],
          "accesses": [
            {
              "rights": {
                "removable": true,
                "editable": true,
                "validate": true
              },
              "access": "employer"
            },
            {
              "rights": {
                "removable": true,
                "editable": true,
                "validate": true
              },
              "access": "admin"
            }
          ]
        }
      ],
      "accesses": [
        {
          "rights": {
            "removable": true,
            "editable": true,
            "validate": true
          },
          "access": "admin"
        }
      ]
    },
    {
      "_id": "5c7858fb495a9c15945b644c",
      "name": "Second Task",
      "type": "infos",
      "description": null,
      "date": "2020-01-02T00:00:00.000Z",
      "refs": [
        {
          "name": "Establishment",
          "id": "5c7858fb495a9c15945b6446"
        }
      ],
      "completed": false,
      "docs": [],
      "parent": "5c7858fb495a9c15945b644a",
      "children": [],
      "accesses": [
        {
          "rights": {
            "removable": true,
            "editable": true,
            "validate": true
          },
          "access": "admin"
        }
      ]
    },
    {
      "_id": "5c7858fb495a9c15945b644d",
      "name": "Third Task",
      "type": "infos",
      "description": null,
      "date": "2020-01-03T00:00:00.000Z",
      "refs": [
        {
          "name": "Establishment",
          "id": "5c7858fb495a9c15945b6446"
        }
      ],
      "completed": false,
      "docs": [],
      "parent": "5c7858fb495a9c15945b644a",
      "children": [],
      "accesses": [
        {
          "rights": {
            "removable": true,
            "editable": true,
            "validate": true
          },
          "access": "admin"
        }
      ]
    }
  ],
  "accesses": [
    {
      "rights": {
        "removable": false,
        "editable": false,
        "validate": true
      },
      "access": "employer"
    },
    {
      "rights": {
        "removable": true,
        "editable": true,
        "validate": true
      },
      "access": "admin"
    }
  ]
}
```

This endpoint retrieves a specific task within a specific project.

<aside class="notice">
This endpoint has a default recursive on task's children. 
</aside>

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

const id = '5c7858fb495a9c15945b644a'
const projectId = '5c7856889b3d4811e2503558'

// Setting a task as completed: requires 'validate' access
// Updating any other fields: requires 'editable' access
// Updating/Creating accesses: only for ADMIN

const data = {
	name: 'New Name',
  description: 'New Description',
  date: '2019-03-10',
  docs: [],             // This will not delete previous document refs
  completed: true,
  accesses: [           // This will modify existing accesses or create new accesses
    {
      access: 'officer',
      rights: {
        removable: true
      }
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
  "_id": "5c7858fb495a9c15945b644a",
  "name": "New Name",
  "type": "action",
  "description": "New Description",
  "date": "2019-03-10T00:00:00.000Z",
  "refs": [
    {
      "name": "Project",
      "id": "5c7858fb495a9c15945b6445"
    }
  ],
  "completed": true,
  "docs": ["5c7858fb495a9c15945b6449"],
  "parent": null,
  "children": [
    "5c7858fb495a9c15945b644b",
    "5c7858fb495a9c15945b644c",
    "5c7858fb495a9c15945b644d",
    "5c785917495a9c15945b64cf"
  ],
  "accesses": [
    {
      "rights": {
        "removable": false,
        "editable": false,
        "validate": true
      },
      "access": "employer"
    },
    {
      "rights": {
        "removable": true,
        "editable": true,
        "validate": true
      },
      "access": "admin"
    },
    {
      "rights": {
        "removable": true,
        "editable": false,
        "validate": false
      },
      "access": "officer"
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

const id = '5c7858fb495a9c15945b644a'
const projectId = '5c7856889b3d4811e2503558'

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
