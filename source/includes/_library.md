# Library

## Get all courses

```javascript

const data = {
  userId: "5d7953fad0765639a7f3464d" // Optional
}

request
  .post(`library`, data)
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
      "_id": "c5c40b7d07c0c5402593",
      "_rev": "11-74bf5127050ad67198b1589e65e05079",
      "name": "Course",
      "likes": [
        "5d7953fad0765639a7f3464d"
      ],
      "comments": [
        {
          "user": "5d7953fad0765639a7f3464d",
          "message": "What a course !",
          "dates": "2019-09-12T16:19:40.606Z"
        }
      ],
      "textContent": "",
      "createdAt": 1568235481197,
      "updatedAt": 1568235495051,
      "collection": "course",
      "subject": {
        "_id": "c67180bb40ac2373b014",
        "_rev": "2-173a1aff3973743e0fd6caf942dce38e",
        "name": "Subject",
        "icon": "IconQuestionMark",
        "createdAt": 1568233491617,
        "updatedAt": 1568233491617,
        "collection": "subject"
      },
      "user": {
        "_id": "5d7953fad0765639a7f3464d",
        "firstname": "tina",
        "lastname": "smith",
        "username": "tina",
        "university": "Griffith College",
        "universityId": "5d7953f406e3c839487463b0",
        "curriculum": "Accounting & Finance",
        "curriculumId": "5d7953ea2adeba391e34f55f",
        "year": 1,
        "country": "FR"
      },
      "hasLiked": true
    }
  ],
  ...
}
```

This endpoint retrieves a list of courses across all users' clouds.

<aside class="notice">
The user object defines the owner of the course.
</aside>

<aside class="notice">
If a "userId" is passed to the request body, it will append a "hasLiked" boolean to each course. This boolean specify whether or not the user already liked the course.
</aside>

### HTTP Route

`POST library`

## Get a course with content

```javascript
const data = {
  courseId: 'c5c40b7d07c0c5402593',
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
  "_id": "c5c40b7d07c0c5402593",
  "_rev": "11-74bf5127050ad67198b1589e65e05079",
  "name": "Course",
  "likes": [
    "5d7953fad0765639a7f3464d"
  ],
  "comments": [
    {
      "user": "5d7953fad0765639a7f3464d",
      "message": "What a course !",
      "dates": "2019-09-12T16:19:40.606Z"
    }
  ],
  "textContent": "",
  "createdAt": 1568235481197,
  "updatedAt": 1568235495051,
  "collection": "course",
  "attachments": "{\"object\":\"value\",\"document\":{\"object\":\"document\",\"data\":{},\"nodes\":[{\"object\":\"block\",\"type\":\"heading\",\"data\":{\"level\":1},\"nodes\":[{\"object\":\"text\",\"leaves\":[{\"object\":\"leaf\",\"text\":\"Title\",\"marks\":[]}]}]},{\"object\":\"block\",\"type\":\"paragraph\",\"data\":{},\"nodes\":[{\"object\":\"text\",\"leaves\":[{\"object\":\"leaf\",\"text\":\"\",\"marks\":[]}]}]},{\"object\":\"block\",\"type\":\"paragraph\",\"data\":{},\"nodes\":[{\"object\":\"text\",\"leaves\":[{\"object\":\"leaf\",\"text\":\"Content.\",\"marks\":[]}]}]}]}}",
  "subject": {
    "_id": "c67180bb40ac2373b014",
    "_rev": "2-173a1aff3973743e0fd6caf942dce38e",
    "name": "Subject",
    "icon": "IconQuestionMark",
    "createdAt": 1568233491617,
    "updatedAt": 1568233491617,
    "collection": "subject"
  },
  "user": {
    "_id": "5d7953fad0765639a7f3464d",
    "firstname": "tina",
    "lastname": "smith",
    "username": "tina",
    "universityId": "5d7953f406e3c839487463b0",
    "curriculumId": "5d7953ea2adeba391e34f55f",
    "year": 1,
    "country": "FR"
  },
  "hasLiked": false
}
```

This endpoint retrieves a specific course with it's content (attachment).

### HTTP Route

`POST library/course`

## Add a like to a course

```javascript
const data = {
  courseId: 'c5c40b7d07c0c5402593',
  userId: '5d7537f565781f51b38fb78b'
}

request
  .post(`library/like`, data)
  .then((res) => console.log(res.data))
  .catch((err) => {
    // Handle any errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "c5c40b7d07c0c5402593",
  "_rev": "14-ddf118e913fc37476fb0571887ffa28d",
  "name": "Course",
  "likes": [
    "5d7953fad0765639a7f3464d",
    "5d7537f565781f51b38fb78b",
  ],
  "comments": [
    {
      "user": "5d7953fad0765639a7f3464d",
      "message": "What a course !",
      "dates": "2019-09-12T16:19:40.606Z"
    }
  ],
  "textContent": "",
  "createdAt": 1568235481197,
  "updatedAt": 1568235495051,
  "collection": "course",
  "subject": {
    "_id": "c67180bb40ac2373b014",
    "_rev": "2-173a1aff3973743e0fd6caf942dce38e",
    "name": "Subject",
    "icon": "IconQuestionMark",
    "createdAt": 1568233491617,
    "updatedAt": 1568233491617,
    "collection": "subject"
  },
  "user": {
    "_id": "5d7953fad0765639a7f3464d",
    "firstname": "tina",
    "lastname": "smith",
    "username": "tina",
    "universityId": "5d7953f406e3c839487463b0",
    "curriculumId": "5d7953ea2adeba391e34f55f",
    "year": 1,
    "country": "FR"
  },
  "hasLiked": true
}
```

This endpoint adds a like to a specific course.

### HTTP Route

`POST library/like`

## Add a comment to a course

```javascript
const data = {
  courseId: 'c5c40b7d07c0c5402593',
  userId: '5d7537f565781f51b38fb78b',
  message: 'Very nice !'
}

request
  .post(`library/comment`, data)
  .then((res) => console.log(res.data))
  .catch((err) => {
    // Handle any errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "c5c40b7d07c0c5402593",
  "_rev": "14-ddf118e913fc37476fb0571887ffa28d",
  "name": "Course",
  "likes": [
    "5d7953fad0765639a7f3464d",
    "5d7537f565781f51b38fb78b",
  ],
  "comments": [
    {
      "user": "5d7953fad0765639a7f3464d",
      "message": "What a course !",
      "dates": "2019-09-12T16:19:40.606Z"
    },
    {
      "user": "5d7537f565781f51b38fb78b",
      "message": "Very nice !",
      "dates": "2019-09-12T18:19:40.606Z"
    }
  ],
  "textContent": "",
  "createdAt": 1568235481197,
  "updatedAt": 1568235495051,
  "collection": "course",
  "subject": {
    "_id": "c67180bb40ac2373b014",
    "_rev": "2-173a1aff3973743e0fd6caf942dce38e",
    "name": "Subject",
    "icon": "IconQuestionMark",
    "createdAt": 1568233491617,
    "updatedAt": 1568233491617,
    "collection": "subject"
  },
  "user": {
    "_id": "5d7953fad0765639a7f3464d",
    "firstname": "tina",
    "lastname": "smith",
    "username": "tina",
    "universityId": "5d7953f406e3c839487463b0",
    "curriculumId": "5d7953ea2adeba391e34f55f",
    "year": 1,
    "country": "FR"
  },
  "hasLiked": true
}
```

This endpoint adds a comment to a specific course.

### HTTP Route

`POST library/comment`
