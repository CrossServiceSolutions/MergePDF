# Merge PDFs API

## Overview

This API allows users to merge multiple PDF files into a single PDF document. Users can upload multiple PDF files, and the service will combine them into a single output file.

The API is available under a **fair use policy**. For unrestricted usage, users can create an account via [https://login.cross-service-solutions.com](https://login.cross-service-solutions.com).

---

## Endpoint

### POST Request

**URL:**  
`https://api.cross-service-solutions.com/solutions/solutions/free/63`

### Headers

```http
Content-Type: multipart/form-data
```

### Request Body (Form-Data)

| Parameter  | Type            | Description                                              |
|-----------|----------------|----------------------------------------------------------|
| `files`   | multiple_files  | The PDF files to be uploaded and merged. Must be of type `application/pdf`. |

### Response

#### Success (201 Created)

Upon successful merging, the API returns the following JSON response:

```json
{
    "id": number,
    "solutionBluePrintId": number,
    "name": "string",
    "status": "string",
    "steps": [
        {
            "name": "string",
            "status": "string"
        }
    ],
    "output": null
}
```

### Cookies

The response sets the following cookies:

- **`Solution_id`**: A unique identifier for the solution.
- **`Solution_UUID`**: A unique UUID associated with the solution.

These cookies are required for retrieving the final merged PDF.

---

## Follow-up Request

### GET Request

**URL:**  
`https://api.cross-service-solutions.com/solutions/solutions/free/63`

To retrieve the processed file, send a `GET` request to the same endpoint, including the cookies (`Solution_id` and `Solution_UUID`) from the initial response.

### Headers

```http
Cookie: Solution_id=<value>; Solution_UUID=<value>
```

### Response

The `GET` request will return the merged PDF file once processing is complete. The result of the merging can be found under the **`output`** key.

```json
{
    "id": number,
    "solutionBluePrintId": number,
    "name": "string",
    "status": "string",
    "steps": [
        {
            "name": "string",
            "status": "string"
        }
    ],
    "output": {
        "result": "string",
        "data": null,
        "files": [
            {
                "name": "string",
                "path": "string"
            }
        ]
    }
}
```
