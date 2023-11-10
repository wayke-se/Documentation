# Wayke Search API Documentation

## Overview

This documentation outlines the integration process with Wayke's Search APIs to display vehicles on your site. There are three primary methods to showcase vehicles:

1. Javascript/React components for listings and display single vehicle functionalities
2. A Content Management System (CMS) in Wayke dealer that allows building the entire website with listings and display vehicles features
3. Direct API integration

For details on search and display components, visit the [npm package](https://www.npmjs.com/package/@wayke-se/components-react). For information about the CMS, please contact support.



## Authentication for Wayke's Search APIs
Wayke's search APIs require authentication to ensure that only authorized users have access to their data. This authentication is achieved using an API key, which must be included in every request to the API.

### Obtaining an API Key
To start using Wayke's APIs, you first need to obtain an API key. This key is provided by Wayke Support. Contact them to request a key.

### Using the API Key
Once you have received your API key, use it to authenticate your requests to the API. This is done by including the API key as a value in the `x-api-key` header parameter.

#### Example API Request
Here is an example of how you can include your API key in an HTTP request:

```http
GET /your-api-resource HTTP/1.1
Host: api.wayketech.se
x-api-key: [Your API Key Here]
```

Replace `[Your API Key Here]` with the API key you received from Wayke.

### Additional Information
For more detailed information about the authentication process, visit the official documentation at [Wayke API Documentation](https://api.wayketech.se/#section/Authentication/ApiKeyAuth).


## Using the Search and Display Vehicles API
Wayke's APIs are optimized for real-time use, utilizing Elastic Search. Below you'll find how to interact with the various endpoints to list and display vehicle details.

### Endpoint to List Vehicles

#### GET `https://api.wayke.se/search/vehicles`

This endpoint supports:
- Pagination
- Sorting
- Faceting (e.g., by manufacturer, model, and mileage)

**Sample Request:**

```bash
curl --location 'https://api.wayke.se/search/vehicles' \
--header 'x-api-key: [Your API Key Here]'
```

**Using Facets Example:**

```bash
curl --location 'https://api.wayke.se/search/vehicles?manufacturer=Volvo&mileage.max=1500&mileage.min=500&modelSeries=V60' \
--header 'x-api-key: [Your API Key Here]'
```
Endpoint documentation: https://api.wayke.se/#tag/search/paths/https:~1~1api.wayke.se~1search~1vehicles/get

### Endpoint to Display Vehicle Details

#### GET `https://api.wayke.se/search/vehicle?id={waykeId}`

**Sample Request:**

```bash
curl --location 'https://api.wayke.se/search/vehicle?id=c6df719d-436d-4a5c-bc3b-525b7fe3c14d' \
--header 'x-api-key: [Your API Key Here]'
```

Endpoint documentation: https://api.wayke.se/#tag/search/paths/https:~1~1api.wayke.se~1search~1vehicle/get

### Endpoint for Specific Dealership Details

#### GET `https://api.wayke.se/search/organizations`

**Sample Request:**

```bash
curl --location 'https://api.wayke.se/search/organizations?branch=7edd8c28-95fd-49d6-9cde-231f39fa9275' \
--header 'x-api-key: [Your API Key Here]'
```
Endpoint documentation: https://api.wayke.se/#tag/Organizations/paths/https:~1~1api.wayke.se~1search~1organizations/get

## Conclusion

Wayke's Search API offers a flexible and efficient way to integrate vehicle search and display functionalities into your website. By following this guide, you can implement a robust vehicle listing and detail display that leverages real-time data. For any further assistance or to obtain your API key, reach out to Wayke support.
