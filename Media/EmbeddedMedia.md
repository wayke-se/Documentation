# **Embedded Media API Documentation**

## **Summary**

Embedded media is a crucial part of the Wayke platform, especially for creating or updating vehicle advertisements with video content. This API documentation outlines the process of adding embedded video URLs to a vehicle ad. Unlike image uploads, no video files are uploaded to Wayke servers - instead, you provide URLs to videos hosted on supported platforms. The process involves two main steps: registering the embedded media URL and then associating it with a specific vehicle ad. This logical separation allows for efficient asynchronous media handling and ad creation.

**Supported video formats:**
- YouTube URLs
- Vimeo URLs
- Direct .mp4 file URLs

## **Authentication**

Before uploading embedded media and updating vehicle ads with videos, users must authenticate using OAuth2 with the Wayke system client. A system client grants access to a specific branch or organization. If a system client is generated at the organization level, it provides access to all branches connected to that organization at the time the system client was created.

For more information on authentication using OAuth2, refer to the [Authentication Documentation](https://api.wayke.se/#section/Authentication/ApiKeyAuth). Note that the secret in the request to obtain a token should be URL-encoded.

## **Embedded Media Registration**

Embedded media is registered to the Wayke platform in two distinct steps:

### **Step 1: Register Embedded Video URL**

To register an embedded video, provide the video URL from a supported platform in the POST request. Note that no video file is uploaded - only the URL reference is stored.

**Supported video sources:**
- YouTube videos (e.g., `https://www.youtube.com/watch?v=...`)
- Vimeo videos (e.g., `https://vimeo.com/...`)
- Direct .mp4 file URLs (e.g., `https://example.com/video.mp4`)

Use the following endpoint for embedded video registration:

- `/media/v2/embedded-video` :for registering embedded video URL reference

Obtain the URL value from the response for use in the next step.

**Example of registering an embedded video (Vimeo):**

API Endpoint: [AddEmbeddedVideo](https://api.wayke.se/#operation/AddEmbeddedVideo)

```bash
curl --location 'https://api.wayke.se/media/v2/embedded-video' \
--header 'Authorization: Bearer {jwtToken}' \
--header 'Content-Type: application/json' \
--data '{
  "purpose": "Vehicle",
  "branchId": "51577a27-7c62-42da-8fda-0b158c160868",
  "sortOrder": 1,
  "url": "https://vimeo.com/449787858"
}'
```

**Response:**

```json
{
    "mediaId": "9dac137b-58b9-40f0-92dc-5f6ea239177f",
    "fileId": "00000000-0000-0000-0000-000000000000",
    "url": "https://vimeo.com/449787858"
}
```

### **Step 2: Add Embedded Media to an Existing Ad**

After uploading the embedded media, the next step is to associate it with an existing vehicle ad. There are two alternatives for this:

1. **Update Vehicle media**
   - Use the PUT method on the endpoint `/vehicle/{id}/media` to associate the media with an ad. Pass the file URLs in the body of the request.
   - Documentation Link: [PUT /vehicle/{id}/media](https://api.wayke.se/#tag/VehicleAd/paths/https:~1~1dealer-api.wayke.se~1vehicle~1{id}~1media/put)

   **Example payload:**
   ```json
   {
       "media": [
           {
               "fileUrls": [
                   "https://vimeo.com/449787858"
               ]
           }
       ]
   }
   ```

2. **Update entire vehicle**
   - Use the PATCH method on the endpoint `/vehicle/{id}` to update the entire vehicle ad, which is used if there are other data points that need to be updated besides just adding media.
   - Provide the obtained URL as `fileUrl` in `ad{}` -> `media[]` -> `fileUrls[]`.

To obtain existing data about a vehicle, you can use one of the following endpoints:

- GET `/vehicle/{branchId}/vehicle/by-registration-number/{registrationNumber}`
  - [GET /vehicle/{branchId}/vehicle/by-registration-number/{registrationNumber}](https://api.wayketech.se/#tag/VehicleAd/paths/https:~1~1dealer-api.wayketech.se~1vehicle~1{branchId}~1vehicle~1by-registration-number~1{registrationNumber}/get)

- GET `/vehicle/{id}/ad` (if you know the Wayke ID)
  - [GET /vehicle/{id}/ad](https://api.wayketech.se/#operation/GetVehicleById)

Use the response from one of these endpoints and map the data to the body of the PATCH request and add the file URLs to the `media` object.

## **Important Notes**

- **No video uploads**: The Wayke platform does not host video files. Only URL references to externally hosted videos are stored.
- **Supported formats**: Only YouTube, Vimeo, and direct .mp4 URLs are supported.
- **Video hosting**: Ensure that videos are publicly accessible and hosted on reliable platforms.

This concludes the documentation for embedded media on the Wayke platform. If you have any questions or require further assistance, please refer to the [Wayke API Documentation](https://api.wayke.se/) or contact our support team.
