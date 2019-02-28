# Document

## Fetch all documents

```javascript
import { ProjectNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c32b832a67a297bb5028be5'

request
  .get(`projects/${id}/documents`)
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
    "_id": "5c78405aaf73e569790d8d37",
    "name": "file.pdf",
    "refs": []
  }
]
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
import {
  InvalidRequestFormat,
  ProjectNotFound,
  ValidationError
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

class ExampleUpload extends Component {
  constructor(props) {
    super(props)

    this.stats = { file: null }
    this.handleSelectedFile = this.handleSelectedFile.bind(this)
    this.handleUpload = this.handleUpload.bind(this)
  }

  handleSelectedFile(event) {
    this.setState({ file: event.target.files[0] })
  }

  handleUpload() {
    const id = '5c32b832a67a297bb5028be5'
    const data = new FormData()

    data.append('file', this.state.file)

    request
      .post(`projects/${id}/documents`, data)
      .then(res => console.log(res.data))
      .catch(APIErrorHandler)
      .catch(err => {
        if (err instanceof InvalidRequestFormat)
          // No file was uploaded

        if (err instanceof ProjectNotFound)
          // The project could be found

        if (err instanceof ValidationError)
          // The document could be created

        // Handle any other errors
      })
  }

  render() {
    return (
      <div>
        <input type='file' onChange={this.handleSelectedFile} />
        <button onClick={this.handleUpload}>Upload</button>
      </div>
    )
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c78406aaf73e569790d8dbd",
  "name": "Name",
  "refs": []
}
```

This endpoint creates documents within a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

<aside class="notice">
Only the name and content of a document can be passed upon create. To add/update refs you must use the PUT method.
</aside>

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

const projectId = '5c32b832a67a297bb5028be5'
const id = '5c78405aaf73e569790d8d37'

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
{
  "_id": "5c78405aaf73e569790d8d37",
  "name": "file.pdf",
  "refs": []
}
```

This endpoint retrieves a specific document within a specific project.

### HTTP Route

`GET project/<PROJECT_ID>/documents/<ID>/`

### URL Parameters

| Parameter  | Description                                              |
| ---------- | -------------------------------------------------------- |
| PROJECT_ID | The ID of the project in which the document is retrieved |
| ID         | The ID of the document to retrieve                       |

## Update a document (name/refs)

```javascript
import {
  ProjectNotFound,
  DocumentNotFound,
  ValidationError
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

const projectId = '5c32b832a67a297bb5028be5'
const id = '5c78405aaf73e569790d8d37'

const data = {
  name: 'new.pdf',
  refs: [
    {
      name: 'company',
      id: '5c784059af73e569790d8d32'
    },
    {
      name: 'user',
      id: '5c784059af73e569790d8d31'
    }
  ]
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
{
  "_id": "5c78405aaf73e569790d8d37",
  "name": "new.pdf",
  "refs": [
    {
      "name": "Company",
      "id": "5c784059af73e569790d8d32"
    },
    {
      "name": "User",
      "id": "5c784059af73e569790d8d31"
    }
  ]
}
```

This endpoint updates the name of a specific document within a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

<aside class="notice">
Updating a document's name does not update it's content
</aside>

### HTTP Route

`PUT project/<PROJECT_ID>/documents/<ID>/`

### URL Parameters

| Parameter  | Description                                            |
| ---------- | ------------------------------------------------------ |
| PROJECT_ID | The ID of the project in which the document is updated |
| ID         | The ID of the document to update                       |

## Update a document (name/content)

```javascript
import {
  ProjectNotFound,
  DocumentNotFound,
  ValidationError
} from './src/common/errors'

import { APIErrorHandler } from './src/common/utils'

class ExampleUpdate extends Component {
	constructor(props) {
		super(props)

		this.stats = { file: null }
		this.handleSelectedFile = this.handleSelectedFile.bind(this)
		this.handleUpdate = this.handleUpdate.bind(this)
	}

  handleSelectedFile(event) {
    this.setState({ file: event.target.files[0] })
  }

	handleUpdate() {
    const id = '5c78405aaf73e569790d8d37'
    const projectId = '5c32b832a67a297bb5028be5'
    const data = new FormData()

    data.append('file', this.state.file)

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
	}

	render() {
		return (
			<div>
				<input type='file' onChange={this.handleSelectedFile} />
				<button onClick={this.handleUpdate}>Update</button>
			</div>
		)
	}
}
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c78405aaf73e569790d8d37",
  "name": "file.pdf",
  "refs": [
    {
      "name": "Company",
      "id": "5c784059af73e569790d8d32"
    },
    {
      "name": "User",
      "id": "5c784059af73e569790d8d31"
    }
  ]
}
```

This endpoint updates the content of a specific document within a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

<aside class="notice">
Updating a document's content also updates it's name (the new name will be the received file name).
</aside>

### HTTP Route

`PUT project/<PROJECT_ID>/documents/<ID>/`

### URL Parameters

| Parameter  | Description                                            |
| ---------- | ------------------------------------------------------ |
| PROJECT_ID | The ID of the project in which the document is updated |
| ID         | The ID of the document to update                       |

## Download a document

```javascript
import download from 'downloadjs'

import { ProjectNotFound, DocumentNotFound } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'
import { Store } from './src/common/factory'

class ExampleDownload extends Component {
	constructor(props) {
		super(props)

		this.stats = { file: null }
		this.handleDownload = this.handleDownload.bind(this)
	}

  handleDownload() {
    const id = '5c37be7581a72c1a4ddb654b'
    const projectId = '5c32b832a67a297bb5028be5'
    const store = new Store()

    request.get(`projects/${projectId}/documents/${id}`)
      .then(res => store.add('doc', res.data))
      .then(doc => request.get(`projects/${projectId}/documents/${doc._id}/download`, { responseType: 'blob' }))
      .then(res => {
        const file = new Blob([res.data], { type: 'octet/stream' })
        download(file, store.doc.name) // This will open a popup to save the file locally
      })
      .catch(APIErrorHandler)
      .catch(err => {
        if (err instanceof ProjectNotFound)
          // The project could be found

        if (err instanceof DocumentNotFound)
          // The document could be found

        // Handle any other errors
      })
  }

	render() {
		return (
			<div>
				<input type='file' onChange={this.handleSelectedFile} />
				<button onClick={this.handleDownload}>Update</button>
			</div>
		)
	}
}
```

> The above command does not returns any JSON but a Blob

This endpoint download a specific document's content within a specific project.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`GET project/<PROJECT_ID>/documents/<ID>/download`

### URL Parameters

| Parameter  | Description                                              |
| ---------- | -------------------------------------------------------- |
| PROJECT_ID | The ID of the project in which the document is contained |
| ID         | The ID of the document to download                       |

## Delete a document

```javascript
import { ProjectNotFound, DocumentNotFound} from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c37be7581a72c1a4ddb654b'
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
