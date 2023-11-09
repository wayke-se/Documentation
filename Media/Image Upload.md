# **Media Upload API Documentation**

## **Summary**

Media uploads are a crucial part of the Wayke platform, especially for creating or updating vehicle advertisements. This API documentation outlines the process of uploading and connecting media (images, videos, etc.) to a vehicle ad. The process involves two main steps: uploading the media and then associating it with a specific vehicle ad. This logical separation allows for efficient asynchronous media handling and ad creation.

## **Authentication**

Before uploading media and updating vehicle ads with images, users must authenticate using OAuth2 with the Wayke system client. A system client grants access to a specific branch or organization. If a system client is generated at the organization level, it provides access to all branches connected to that organization at the time the system client was created.

For more information on authentication using OAuth2, refer to the [Authentication Documentation](https://api.wayke.se/#section/Authentication/ApiKeyAuth). Note that the secret in the request to obtain a token should be URL-encoded.

## **Media Upload**

Media is uploaded to the Wayke platform in two distinct steps:

### **Step 1: Upload Image**

To upload an image, you have two options:

- **Option 1:** Upload the image as the body of the POST request.
- **Option 2:** Provide an image URL in the POST request.

Use the following endpoints for image upload:

- `/media/v2/image` :for uploading image as the request body (https://api.wayketech.se/#operation/AddImage)
- `/media/v2/image-url` :for providing an image URL (https://api.wayketech.se/#operation/AddImageByUrl)

Obtain the URL value from the response for use in the next step.

**Example of uploading an image with the image file as the body of the request:**

API Endpoint: [AddImage](https://api.wayke.se/#operation/AddImage)

```bash
curl --location 'https://api.wayke.se/media/v2/image' \
--header 'Authorization: Bearer {jwtToken}' \
--form 'File=@"example.jpeg"' \
--form 'Metadata.Purpose="Vehicle"' \
--form 'Metadata.BranchId="1bfec2d5-b3a6-4dda-9c0e-c993d55ca1b0"' \
--form 'Metadata.SortOrder="1"' \
--form 'Metadata.Description="Description"'
```

**Response:**

```json
{
    "mediaId": "9dac137b-58b9-40f0-92dc-5f6ea239177f",
    "fileId": "00000000-0000-0000-0000-000000000000",
    "url": "https://wayketestsharedstorages.blob.core.windows.net/media/9dac137b58b940f092dc5f6ea239177f/b68b041ae14d48e7ba7f6a5515ff04e4"
}
```

### **Step 2: Add Image to an Existing Ad**

After uploading the media, the next step is to associate it with an existing vehicle ad. There are two alternatives for this:

1. **Update Vehicle media**
   - Use the PUT method on the endpoint `/vehicle/{id}/media` to associate the media with an ad. Pass the file URLs in the body of the request.
   - Documentation Link: [PUT /vehicle/{id}/media](https://api.wayke.se/#tag/VehicleAd/paths/https:~1~1dealer-api.wayke.se~1vehicle~1{id}~1media/put)

2. **Update entire vehicle**
   - Use the PATCH method on the endpoint `/vehicle/{id}` to update the entire vehicle ad, which is used if there are other data points that need to be updated besides just adding media.
   - Provide the obtained URL as `fileUrl` in `ad{}` -> `media[]` -> `fileUrls[]`.

To obtain existing data about a vehicle, you can use one of the following endpoints:

- GET `/vehicle/{branchId}/vehicle/by-registration-number/{registrationNumber}`
  - [GET /vehicle/{branchId}/vehicle/by-registration-number/{registrationNumber}](https://api.wayketech.se/#tag/VehicleAd/paths/https:~1~1dealer-api.wayketech.se~1vehicle~1{branchId}~1vehicle~1by-registration-number~1{registrationNumber}/get)

- GET `/vehicle/{id}/ad` (if you know the Wayke ID)
  - [GET /vehicle/{id}/ad](https://api.wayketech.se/#operation/GetVehicleById)

Use the response from one of these endpoints and map the data to the body of the PATCH request and add the file URLs to the `media` object.

This concludes the documentation for media uploads on the Wayke platform. If you have any questions or require further assistance, please refer to the [Wayke API Documentation](https://api.wayke.se/) or contact our support team.

