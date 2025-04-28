# How to Upload Sphere Images to the Platform via API

### **Step 1: Upload Sphere Image**

Obtain the URL value from the response for use in the next step.

API Endpoint: [AddSphere](https://api.wayke.se/#operation/AddSphereImage)

```bash
curl --location 'https://api.wayke.se/media/v2/sphere-image' \
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

### **Step 2: Add Sphere Image to an Existing Ad**

After uploading the sphere image, the next step is to associate it with an existing vehicle ad. There are two alternatives for this:

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

