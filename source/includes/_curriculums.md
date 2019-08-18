# Curriculums

## Create a curriculum

```javascript
const data = { name: 'Computer Science' }

request
  .post(`curriculums`)
  .then((res) => console.log(res.data))
  .catch((err) => {
    // Handle any errors
  })
```

> The above command returns JSON structured like this:

```json
{ "success": true }
```

This endpoint creates a curriculum based on it's name.

### HTTP Route

`POST curriculums`

## Query curriculums

```javascript
const query = 'Com'

request
  .get(`curriculums/${query}`)
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
    "_id": "5d5910939cb03b1d9cf6f859",
    "name": "Communication & Media Studies"
  },
  {
    "_id": "5d5910939cb03b1d9cf6f85a",
    "name": "Complementary Medicine"
  },
  {
    "_id": "5d5910939cb03b1d9cf6f85b",
    "name": "Computer Science"
  }
]
```

This endpoint retrieves a list of curriculum based on a user input.

<aside class="notice">
This is designed to dynamically populate a dropdown's list of choices.
</aside>

<aside class="notice">
The limit of curriculums fetched at once based on the query is: 10.
</aside>

### HTTP Route

`GET curriculums/<QUERY>`

### URL Parameters

| Parameter | Description                   |
| --------- | ----------------------------- |
| QUERY     | The QUERY entered by the user |
