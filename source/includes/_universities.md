# Universities

## Create a university

```javascript
const data = { name: 'Griffith College' }

request
  .post(`universities`)
  .then((res) => console.log(res.data))
  .catch((err) => {
    // Handle any errors
  })
```

> The above command returns JSON structured like this:

```json
{ "success": true }
```

This endpoint creates a university based on it's name.

### HTTP Route

`POST universities`

## Query universities

```javascript
const query = 'Griff'

request
  .get(`universities/${query}`)
  .then(res => console.log(res.data))
  .catch(err => {
    // Handle any errors
  })
}
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5d59109a6c92671dd20aaaee",
    "name": "Griffith College"
  },
  {
    "_id": "5d5910976c92671dd20a9e60",
    "name": "Griffith University"
  }
]
```

This endpoint retrieves a list of universities based on a user input.

<aside class="notice">
This is designed to dynamically populate a dropdown's list of choices.
</aside>

<aside class="notice">
The limit of universities fetched at once based on the query is: 10.
</aside>

### HTTP Route

`GET universities/<QUERY>`

### URL Parameters

| Parameter | Description                   |
| --------- | ----------------------------- |
| QUERY     | The QUERY entered by the user |
