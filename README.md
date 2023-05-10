# Bahnjobs

## REST API

### Authentication

All requests require a valid authentication token. The token should be passed in the `Authorization` header as a Bearer token.

Example:

```
Authorization: Bearer <TOKEN>
```

### Jobs

#### `GET /api/jobs`

Returns a list of the last 100 jobs.

#### Params

- `page` (optional): Page number


#### `POST /api/jobs`

Create or update a job.

#### Params

- `external_url`: The URL of the job offer on an external site. If a job already exists with this URL, the existing job will be updated. Otherwise, a new job will be created.
- `sector_id`: The ID of an existing Swissrail sector (see `GET /api/sectors`)
- `title`: The title of the job
- `company_id`: The ID of an existing Swissrail company
- `contact_id` (optional): The ID of an existing Swissrail user used as a contact for the job.
- `workplace_postcode`: The postcode of the workplace of the job
- `workplace` (optional): The workplace of the job. If provided, a geolookup will be performed using Google and the postcode will be stored as `workplace_postcode`.
- `percentage_from/to` (optional): The percentage of the job (1-100). If no range is required, `percentage_from` and `percentage_to` should be set to the same value.
- `published_at` (optional): The date the job was published. If omitted, the current date and time will be used.
- `application_deadline` (optional): The date the job application deadline.
- `description` (optional): The description of the job. If HTML is provided, all except the following tags will be removed: `p`, `br`, `ol`, `ul`, `li`, `a`, `strong`, `em`, `h1`, `h2`, `h3`, `h4`, `h5`, `h6`, `blockquote`

   **Note:** The description will not be returned in the response.

#### Example Request

```jsonc
// POST /api/jobs
{
  "job": {
    "external_url": "https://example.com/job/1234",
    "title": "Example Job",
    "company_id": 1,
    "workplace": "Breitenrain, Bern", // or workplace_postcode: 3014
    "percentage_from": 80,
    "percentage_to": 100,
    "published_at": "2023-04-21T13:00:00+02:00",
    "sector_id": 2
  }
}
```

### Sectors

#### `GET /api/sectors`

Returns a list of all sectors.
