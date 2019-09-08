# Library

## Get all courses

```javascript
request
  .get(`library`)
  .then((res) => console.log(res.data))
  .catch((err) => {
    // Handle any errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "docs": [
    {
      "_id": "30a9465d2a62763ebc5e",
      "_rev": "2-7a7391a3097119419e75e950324e4d2a",
      "name": "Editor",
      "textContent": "",
      "createdAt": 1567958480433,
      "updatedAt": 1567958480433,
      "collection": "course",
      "user": {
        "_id": "5d7537f565781f51b38fb78b",
        "firstname": "tina",
        "lastname": "smith",
        "username": "tina",
        "university": "Griffith College",
        "universityId": "5d7537e3bc3daf515517e07e",
        "curriculum": "Accounting & Finance",
        "curriculumId": "5d7537d17332d251361755a7",
        "year": 1,
        "country": "FR"
      },
      "subject": {
        "_id": "22e15d4a76d4afa3e562",
        "_rev": "3-0a07ac560d01259988020456734681d2",
        "name": "Finance",
        "icon": "NounEconomics615480",
        "createdAt": 1567958469850,
        "updatedAt": 1567958469850,
        "collection": "subject"
      }
    }
  ],
  ...
}
```

This endpoint retrieves a list of courses across all users' clouds.

<aside class="notice">
The user object defines the owner of the course.
</aside>

### HTTP Route

`GET library`

## Get a course with content

```javascript
const data = {
  courseId: '30a9465d2a62763ebc5e',
  userId: '5d7537f565781f51b38fb78b'
}

request
  .post(`library/course`, data)
  .then((res) => console.log(res.data))
  .catch((err) => {
    // Handle any errors
  })
```

> The above command returns JSON structured like this:

```json
{
{
  "_id": "30a9465d2a62763ebc5e",
  "_rev": "2-7a7391a3097119419e75e950324e4d2a",
  "name": "Editor",
  "textContent": "",
  "createdAt": 1567958480433,
  "updatedAt": 1567958480433,
  "collection": "course",
  "_attachments": {
    "value.json": {
      "content_type": "application/json",
      "revpos": 2,
      "digest": "md5-z/cvJ0kUEKPd/OC31po4gw==",
      "length": 296,
      "stub": true
    }
  },
  "subject": {
    "_id": "22e15d4a76d4afa3e562",
    "_rev": "3-0a07ac560d01259988020456734681d2",
    "name": "Finance",
    "icon": "NounEconomics615480",
    "createdAt": 1567958469850,
    "updatedAt": 1567958469850,
    "collection": "subject"
  },
  "user": {
    "_id": "5d7537f565781f51b38fb78b",
    "firstname": "tina",
    "lastname": "smith",
    "username": "tina",
    "university": "Griffith College",
    "universityId": "5d7537e3bc3daf515517e07e",
    "curriculum": "Accounting & Finance",
    "curriculumId": "5d7537d17332d251361755a7",
    "year": 1,
    "country": "FR"
  }
}
```

This endpoint retrieves a specific course with it's content.

<aside class="notice">
The user object defines the owner of the course.
</aside>

### HTTP Route

`POST library/course`
