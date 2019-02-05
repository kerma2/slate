# Authentication

## Verify a user

```javascript
import { UserNotFound, InvalidAccess } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const username = '762a14a6'

request
  .get(`users/${username}/verify`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof InvalidAccess)
      // The user is not an elector

    if (err instanceof UserNotFound)
      // The user could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "name": "SpaceX",
  "logo": "https://i.imgur.com/kl6PnDj.png",
  "round": 1,
  "dates": {
    "locked": "2019-02-06T11:28:23.904Z",
    "start": "2019-02-15T11:28:23.904Z",
    "end": "2019-02-16T11:28:23.904Z"
  }
}
```

This endpoint retrieves basic informations about a specific user.

<aside class="notice">
Only electors can be verified.
</aside>

### HTTP Route

`GET auth/<USERNAME>/verify`

### URL Parameters

| Parameter | Description                                                      |
| --------- | ---------------------------------------------------------------- |
| USERNAME  | The USERNAME of the user from which the information is retrieved |

## Authenticate a user

```javascript
import { withCookies } from 'react-cookie'
import { InvalidCredentials } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

class LogInComponent extends Component {

  // ... component definition

  componentDidMount() {
    // Clear any previous token reference
    // This is mandatory to ensure a smooth redirection flow
    cookies.remove('jwt', { path: '/' })
  }

  logIn() {
    const { cookies } = this.props

    const data = {
      username: 'name',
      password: 'pwd',
    }

    request
      .post(`auth/login`, data)
      .then(res => {
        // This is mandatory to allow the client to get route that need authorization
        cookies.set('jwt', res.data.token, { path: '/', expires: new Date(Date.now() + 864e5 * 5) })

        // This will set the 'Authorization' headers in the axios requested instance
        request.defaults.headers.common['Authorization'] = `JWT ${res.data.token}`

        console.log(res.data)

        // The 'hasAccess' function/condition need to be implemented
        // It should map the different home page to each allowed accesses in the request url
        if (hasAccess(res.data.accesses))
          // Redirect to appropriate home page
        else {
          // Redirect to other LogInComponent
        }
      })
      .catch(APIErrorHandler)
      .catch(err => {
        if (err instanceof InvalidCredentials)
          // Invalid username/password couple

        // Handle any other errors
      })

  }

  // ... component definition
}

export default withCookies(LogInComponent)
```

> The above command returns JSON structured like this:

```json
{
  "user": {
    "_id": "5c491a65afca66204e281fdd",
    "companyId": null,
    "projectId": null,
    "username": "admin",
    "mail": null,
    "fullname": "Admin",
    "civility": "m",
    "address": "none",
    "hiring": 0,
    "birth": {
      "date": "1970-01-01T00:00:00.000Z",
      "county": "none",
      "place": "none"
    }
  },
  "accesses": ["admin"],
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVjNDkxYTY1YWZjYTY2MjA0ZTI4MWZkZCIsImlhdCI6MTU0ODMzMDg1MywiZXhwIjoxNTQ4OTM1NjUzfQ.3sH4OTWk9STic95FaoCtOP13f2qge3GRnGy79j2Fle4"
}
```

This endpoint authenticates a specifics user.

<aside class="notice">
The expire date of the cookie must be 5 days to ensure better refresh performance.
</aside>

### HTTP Route

`POST auth/login`

## Authorize a user

```javascript
import { withCookies } from 'react-cookie'

class TopLevelComponent extends Component {

  // ... component definition

  // It can be in componentWillMount as well
  componentDidMount() {
    const { cookies } = this.props

    const token = cookies.get('jwt')

    if (!token)
      // Redirect to login page matching the requested url
    else
      request
        .get(`auth/login/${token}`)
        .then(res => {
          // This will set the 'Authorization' headers in the axios request instance
          request.defaults.headers.common['Authorization'] = `JWT ${token}`

          console.log(res.data)
        })
        .catch(APIErrorHandler)
        .catch(err => {
          if (err instanceof InvalidCredentials)
            // The token is invalid or has expired

          // Handle any other errors
        })
  }

  // ... component definition
}

export default withCookies(TopLevelComponent)
```

> The above command returns JSON structured like this:

```json
{
  "user": {
    "_id": "5c491a65afca66204e281fdd",
    "companyId": null,
    "projectId": null,
    "username": "admin",
    "mail": null,
    "fullname": "Admin",
    "civility": "m",
    "address": "none",
    "hiring": 0,
    "birth": {
      "date": "1970-01-01T00:00:00.000Z",
      "county": "none",
      "place": "none"
    }
  },
  "accesses": ["admin"]
}
```

This endpoint authorizes a specifics user.

<aside class="notice">
The client must identify that a verification has already been made for the session in order to avoid a verification on each redirection.
</aside>

### HTTP Route

`GET auth/login/<TOKEN>`

### URL Parameters

| Parameter | Description                        |
| --------- | ---------------------------------- |
| TOKEN     | The TOKEN of the user to authorize |
