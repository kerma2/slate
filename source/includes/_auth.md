# Authentication

## Authenticate a user

```javascript
import { withCookies } from 'react-cookie'
import { InvalidCredentials } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

class LogInComponent extends Component {

  // ... component definition

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
        cookies.set('jwt', res.data, { path: '/', expires: new Date(Date.now() + 864e5 * 5) })

        console.log(res.data)
      })
      .then(() => next())
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
"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVjNDkxNmIxNTY2YjY2MWNmMzQxNWFhMyIsImlhdCI6MTU0ODI5MzgxMCwiZXhwIjoxNTQ4ODk4NjEwfQ.IcNimx1wnNSzFqEocX5160WkF0uKMPQc2DBUkB_vVzA"
```

This authenticates a specifics user.

<aside class="notice">
The expire date of the cookie must be 5 days to ensure better refresh performance.
</aside>

### HTTP Route

`POST user/`
