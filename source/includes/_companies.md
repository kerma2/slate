# Company

## Fetch all companies

```javascript
import { APIErrorHandler } from './src/common/utils'

request
  .get(`companies`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof NoCompanies)
      // No companies could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c328f1a1d430b3d610a0833",
    "name": "Name",
    "infos": {
      "siret": "00000000000000",
      "headquarters": "Headquarters",
      "logo": "https://i.imgur.com/kl6PnDj.png",
      "theme": {}
    },
    "projects": ["5c328f1a1d430b3d610a0834", "5c328f1a1d430b3d610a0835"]
  },
  {
    "_id": "5c328f1a1d430b3d610a08c4",
    "name": "Name",
    "infos": {
      "siret": "00000000000001",
      "headquarters": "Headquarters",
      "logo": "https://i.imgur.com/kl6PkRt.png",
      "theme": {}
    },
    "projects": ["5c328f1a1d430b3d610a08c5", "5c328f1a1d430b3d610a08c6"]
  }
]
```

This endpoint retrieves all companies.

### HTTP Route

`GET companies/`

## Create a company

```javascript
import { APIErrorHandler } from './src/common/utils'

const data = {
  name: "My Company",                         // Mandatory
  infos: {
    siret: "00000000000002",                  // Mandatory and Unique
    headquarters: "Headquarters",             // Mandatory
    logo: "https://i.imgur.com/kl6PnDj.png"   // Optional
  }
}

request
  .post(`companies/`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ValidationError)
      // The company could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c328f1a1d430b3d610a08a4",
  "name": "My Company",
  "infos": {
    "siret": "00000000000002",
    "headquarters": "Headquarters",
    "logo": "https://i.imgur.com/kl6PnDj.png",
    "theme": {}
  },
  "projects": []
}
```

This endpoint creates company.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`POST companies/`

## Fetch a company

```javascript
import { APIErrorHandler } from './src/common/utils'

const id = '5c328f1a1d430b3d610a0833'

request
  .get(`companies/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CompanyNotFound)
      // The company could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c328f1a1d430b3d610a0833",
  "name": "Name",
  "infos": {
    "siret": "00000000000000",
    "headquarters": "Headquarters",
    "logo": "https://i.imgur.com/kl6PnDj.png",
    "theme": {}
  },
  "projects": ["5c328f1a1d430b3d610a0834", "5c328f1a1d430b3d610a0835"]
}
```

This endpoint retrieves a specific company.

### HTTP Route

`GET companies/<ID>`

### URL Parameters

| Parameter | Description                       |
| --------- | --------------------------------- |
| ID        | The ID of the company to retrieve |

## Update a company

```javascript
import { APIErrorHandler } from './src/common/utils'

const id = '5c328f1a1d430b3d610a08a4'

const data = {
  name: "New Name",
  infos: {
    headquarters: "New Headquarters",
    logo: "https://bit.ly./AfgTyH"
  }
}

request
  .put(`companies/${id}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ValidationError)
      // The company could not be created

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c328f1a1d430b3d610a08a4",
  "name": "New Name",
  "infos": {
    "siret": "00000000000002",
    "headquarters": "New Headquarters",
    "logo": "https://bit.ly./AfgTyH",
    "theme": {}
  },
  "projects": []
}
```

This endpoint updates a specific company.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT companies/<ID>`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the company to update |

## Delete a company

```javascript
import { APIErrorHandler } from './src/common/utils'

const id = '5c328f1a1d430b3d610a08a4'

request
  .delete(`companies/${id}`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof CompanyNotFound)
      // The company could be found

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint updates a specific company.

### HTTP Route

`DELETE companies/<ID>`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the company to delete |
