# Library

## Get a list of courses

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
      "_id": "3e178bec1f764777e9a4",
      "_rev": "1-55e4c91073f288da6a30c529807a4616",
      "name": "Transactions",
      "textContent": "",
      "createdAt": 1566125914852,
      "updatedAt": 1566125914852,
      "collection": "course",
      "user": {
        "_id": "5d592f311603597b8cce2e27",
        "firstname": "quentin",
        "lastname": "kermaidic",
        "username": "kerma",
        "university": "Griffith College",
        "universityId": "5d01251918a2247dc44d6a84",
        "curriculum": "Computer Science",
        "curriculumId": "5d0124fa40614e7da37f643b",
        "year": 4,
        "country": "FR"
      }
    },
    ...
  ]
}
```

This endpoint retrieves a list of courses across all users' clouds.

<aside class="notice">
The user object defined the owner of the course.
</aside>

### HTTP Route

`GET library`
