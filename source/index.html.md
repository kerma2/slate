---
title: GSVote API Reference

language_tabs:
  - javascript

toc_footers:
  - Documentation Powered by Kerma

includes:
  - auth
  - users
  - companies
  - projects
  - tasks
  - documents
  - establishments
  - colleges
  - electors
  - rounds
  - lists
  - candidates
  - errors

search: true
---

# Getting Started

## Request instance

```javascript
import axios from 'axios'

const endpoint = `${window.location.protocol}//${window.location.host}`
const request = axios.create({ baseURL: `${endpoint}/api` })
```

The request object is used to handle communications with the API.

<aside class="notice">
It should be stored in the Redux Store.
</aside>

## Authorize

```javascript
import { withCookies } from 'react-cookie'

class TopLevelComponent extends Component {
  // It is not required to get/set token in the constructor
  // This is for the sake of the example only
  constructor(props) {
    const { cookies } = this.props

    // This will set the 'Authorization' headers in the axios request instance
    request.defaults.headers.common['Authorization'] = `JWT ${cookies.get('jwt')}`
  }

  // ... component definition
}

export default withCookies(TopLevelComponent)
```

The request object must have a valid 'Authorization' header in order to communicate with the API (except for [Authentication](#authentication))

## Chain requests

```javascript
import { APIErrorHandler } from './src/common/utils'

request
  .get('url1')
  .then(res => /* response of request on url1 */)
  .then(() => request.get('url2'))
  .then(res => /* response of request on url2 */)
  .catch(APIErrorHandler)
  .catch(err => /* error for url1 or url2*/)
```

## Batch requests

```javascript
import { APIErrorHandler, sync } from './src/common/utils'

const array = [
  '5c328f1a1d430b3d610a0833',
  '5c328f1a1d430b3d610a08c4'
]

const task = function (id, index, callback) {
  request
    .get(`companies/${id}`)
    .then(res => callback(null, res.data)) // This will store the response in the results
    .catch(APIErrorHandler)
    .catch(err => {
      callback(null, err) // This will store the error in the results

      /* OR */

      callback(err) // This will stop the batch, the previous results will not be accessible
    })
}

sync(array, task)
  .then(results => /* array of responses */)
  .catch(err => /* error */)
```

A batch is a series of request made from an array of data.

<aside class="notice">
Always use the <code>sync</code> method to make batch to the API.
</aside>

<aside class="notice">
You can bind context to the <code>task</code> function: <code>task.bind(this)</code>.
</aside>
