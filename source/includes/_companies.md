# Company

## Fetch all companies

```javascript
import { NoCompanies } from './src/common/errors'
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
      "sirets": ["00000000000000"],
      "idcc": 1000,
      "headquarters": "Headquarters",
      "status": "SARL",
      "city": "City",
      "capital": -1,
      "logo": "https://i.imgur.com/kl6PnDj.png",
      "theme": {}
    },
    "representative": {
      "name": null,
      "civility": null,
      "title": null
    },
    "projects": ["5c328f1a1d430b3d610a0834", "5c328f1a1d430b3d610a0835"]
  }
]
```

This endpoint retrieves all companies.

### HTTP Route

`GET companies/`

## Create a company

```javascript
import { ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const data = {
  name: "My Company",                         // Mandatory
  infos: {
    sirets: ["00000000000002"],               // Mandatory and Unique
    idcc: 1000,                               // Mandatory
    capital: 1000000,                         // Optional (default: -1)
    status: "SARL",                           // Mandatory
    city: "City",                             // Mandatory
    headquarters: "Headquarters",             // Mandatory
    logo: "https://i.imgur.com/kl6PnDj.png"   // Optional
  },
  representative: {
    name: "Name Surname",                     // Optional
    civility: "M",                            // Optional
    title: "Representative Status"            // Optional
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
    "sirets": ["00000000000002"],
    "idcc": 1000,
    "headquarters": "Headquarters",
    "status": "SARL",
    "city": "City",
    "capital": 1000000,
    "logo": "https://i.imgur.com/kl6PnDj.png",
    "theme": {}
  },
  "representative": {
    "name": "Name Surname",
    "civility": "m",
    "title": "Representative Status"
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
import { CompanyNotFound } from './src/common/errors'
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
    "sirets": ["00000000000000"],
    "idcc": 1000,
    "headquarters": "Headquarters",
    "status": "SARL",
    "city": "City",
    "capital": 1000000,
    "logo": "https://i.imgur.com/kl6PnDj.png",
    "theme": {}
  },
  "representative": {
    "name": "Name Surname",
    "civility": "m",
    "title": "Representative Status"
  },
  "projects": ["5c328f1a1d430b3d610a0834", "5c328f1a1d430b3d610a0835"]
}
```

This endpoint retrieves a specific company.

### HTTP Route

`GET companies/<ID>/`

### URL Parameters

| Parameter | Description                       |
| --------- | --------------------------------- |
| ID        | The ID of the company to retrieve |

## Update a company

```javascript
import { ValidationError } from './src/common/errors'
import { APIErrorHandler } from './src/common/utils'

const id = '5c328f1a1d430b3d610a08a4'

const data = {
  name: "New Name",
  infos: {
    sirets: ["10000000000000", "20000000000000"], // This will COMPLETELY replace any existing siret
    headquarters: "New Headquarters",
    status: "SAS",
    city: "New City",
    capital: 17000000,
    idcc: 2000,
    logo: "https://bit.ly./AfgTyH"
  },
    representative: {
    name: "New Name Surname",
    civility: "MME",
    title: "New Representative Status"
  }
}

request
  .put(`companies/${id}`, data)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    if (err instanceof ValidationError)
      // The company could not be updated

    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5c328f1a1d430b3d610a08a4",
  "name": "New Name",
  "infos": {
    "sirets": ["10000000000000", "20000000000000"],
    "idcc": 2000,
    "headquarters": "New Headquarters",
    "status": "SAS",
    "city": "New City",
    "capital": 17000000,
    "logo": "https://bit.ly./AfgTyH",
    "theme": {}
  },
    "representative": {
    "name": "New Name Surname",
    "civility": "mme",
    "title": "New Representative Status"
  },
  "projects": []
}
```

This endpoint updates a specific company.

Be sure to check how to handle [ValidationError](#validationerror).

### HTTP Route

`PUT companies/<ID>/`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the company to update |

## Delete a company

```javascript
import { CompanyNotFound } from './src/common/errors'
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

This endpoint deletes a specific company.

### HTTP Route

`DELETE companies/<ID>/`

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| ID        | The ID of the company to delete |
