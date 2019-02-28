# Company

## Fetch all companies

```javascript
import { APIErrorHandler } from './src/common/utils'

request
  .get(`companies`)
  .then(res => console.log(res.data))
  .catch(APIErrorHandler)
  .catch(err => {
    // Handle any other errors
  })
```

> The above command returns JSON structured like this:

```json
[
  {
    "_id": "5c7800fcfb091b715ccfbd7f",
    "name": "SpaceX",
    "headquarter": "5c7800fdfb091b715ccfbd81",
    "infos": {
      "agreement": {
        "date": "2019-01-01T00:00:00.000Z",
        "has": true
      },
      "previous": "2016-01-01T00:00:00.000Z",
      "status": "SARL",
      "capital": -1,
      "logo": "https://i.imgur.com/kl6PnDj.png"
    }
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
  // Company Fields
  company: 
  {
    name: 'SpaceX',                             // Mandatory
    infos: 
    {
      agreement: 
      {
        date: "2019-01-01",                     // Optional (default: null)
        has: true                               // Optional (default: false)
      },
      previous: '2016-01-01',                   // Optional (default: null)
      status: 'SARL',                           // Mandatory
      captial: 100000,                          // Optional (default: -1)
      logo: 'https://i.imgur.com/kl6PnDj.png'   // Optional (default: null)
    }
  },

  // Project Fields
  project: 
  {
    shared: false,              // Optional (default: false)
    negotiating: '2019-01-01'   // Mandatory
  },

  // Establishment Fields
  establishment:
  {
    name: 'SpaceX West Office',   // Mandatory
    idcc: 180,                    // Mandatory
    siret: '0000 000 0000 000',   // Mandatory
    address:
    {
      street: 'Street Address',   // Mandatory
      city: 'City',               // Mandatory
      code: '31500',              // Mandatory
      country: 'France'           // Mandatory
    },
    representative:
    {
      firstname: 'First Name',    // Mandatory
      lastname: 'Last Name',      // Mandatory
      civility: 'm',              // Mandatory
      title: 'title',             // Mandatory
      phone: '0636363636'         // Mandatory
    },
    statuses: [ 'Workers', 'Engineer' ] // Optional
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
  "company": {
    "_id": "5c7800fcfb091b715ccfbd7f",
    "name": "SpaceX",
    "headquarter": "5c7800fdfb091b715ccfbd81",
    "infos": {
      "agreement": {
        "date": "2019-01-01T00:00:00.000Z",
        "has": true
      },
      "previous": "2016-01-01T00:00:00.000Z",
      "status": "SARL",
      "capital": -1,
      "logo": "https://i.imgur.com/kl6PnDj.png"
    }
  },
  "project": {
    "_id": "5c7800fdfb091b715ccfbd80",
    "companyId": "5c7800fcfb091b715ccfbd7f",
    "dates": {
      "createdAt": "2019-02-28T15:40:45.240Z",
      "closedAt": null,
      "archivedAt": null
    },
    "shared": false,
    "negotiating": "2019-01-01T00:00:00.000Z"
  },
  "establishment": {
    "_id": "5c7800fdfb091b715ccfbd81",
    "projectId": "5c7800fdfb091b715ccfbd80",
    "name": "SpaceX West Office",
    "state": "init",
    "idcc": 180,
    "siret": "00000000000000",
    "address": {
      "street": "Street Address",
      "city": "City",
      "code": "31500",
      "country": "France"
    },
    "representative": {
      "firstname": "First Name",
      "lastname": "Last Name",
      "civility": "m",
      "title": "title",
      "phone": "0636363636"
    },
    "statuses": [
      "Engineer",
      "Workers",
      "Ouvrier",
      "Employés",
      "Techniciens",
      "Agents de maîtrise",
      "Ingénieurs",
      "Cadres"
    ]
  }
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
  "_id": "5c7800fcfb091b715ccfbd7f",
  "name": "SpaceX",
  "headquarter": "5c7800fdfb091b715ccfbd81",
  "infos": {
    "agreement": {
      "date": "2019-01-01T00:00:00.000Z",
      "has": true
    },
    "previous": "2016-01-01T00:00:00.000Z",
    "status": "SARL",
    "capital": -1,
    "logo": "https://i.imgur.com/kl6PnDj.png"
  }
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
  name: 'New Name',
  infos: 
  {
    agreement: {
      date: '2019-02-10',
      has: true
    },
    previous: '2018-01-01',
    status: 'New Status',
    capital: 10000,
    logo: 'New Logo'
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
  "_id": "5c7800fcfb091b715ccfbd7f",
  "name": "New Name",
  "headquarter": "5c7800fdfb091b715ccfbd81",
  "infos": {
    "agreement": {
      "date": "2019-02-10T00:00:00.000Z",
      "has": true
    },
    "previous": "2018-01-01T00:00:00.000Z",
    "status": "New Status",
    "capital": 10000,
    "logo": "New Logo"
  }
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
