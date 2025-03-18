# How to Upload Panorama Images to the Platform via API

### Step 1: Create a container

First, you need to create a container to hold your images.

```bash
curl --location 'https://api.wayke.se/media/v2/panorama-image' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Authorization: Bearer ••••••' \
--data-urlencode 'Metadata.Purpose=Vehicle' \
--data-urlencode 'Metadata.BranchId=<branch-id>' \
--data-urlencode 'Metadata.SortOrder=0'
```

- `Metadata.Purpose`: The purpose of the images, e.g., "Vehicle".
- `Metadata.BranchId`: The ID for the specific branch or unit.
- `Metadata.SortOrder`: The display order of the images (0 is first).

**Response:**
You will receive a container ID (UUID), for example:

```
0316f21d-51cf-441d-bfef-cf90d73178a5
```

---

### Step 2: Upload images

After creating the container, upload each image individually.

```bash
curl --location 'https://api.wayke.se/media/v2/panorama-image/<container-id>' \
--header 'Authorization: Bearer ••••••' \
--form 'File=@"/path/to/your/image1.webp"' \
--form 'SortOrder="0"'
```

- Replace `<container-id>` with the ID obtained from step 1.
- Provide the file path to your image.
- `SortOrder` indicates the order (the first image is typically 0).

**Response:**

```json
{
  "imageId": "19f28f51-6b5e-4abe-9d2a-cd6f8ff0a4e1",
  "url": "https://waykeprodsharedstorages.blob.core.windows.net/media/<container-id>/<image-id>"
}
```

Repeat this step for each panorama image you want to upload. Save each image URL for the next step.

---

### Step 3: Associate images with a vehicle

Finally, you must link the images to a specific vehicle.

```bash
curl --location --request PUT 'https://dealer-api.wayke.se/vehicle/<vehicle-id>/media' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer ••••••' \
--data '{
    "media": [
        {
            "fileUrls": [
                "https://waykeprodsharedstorages.blob.core.windows.net/media/<container-id>/<image-id-1>",
                "https://waykeprodsharedstorages.blob.core.windows.net/media/<container-id>/<image-id-2>"
            ]
        }
    ]
}'
```

- Replace `<vehicle-id>` with the ID of the vehicle.
- Provide URLs from each uploaded image from step 2.

Once this step is completed, the images are associated with the vehicle and ready for use on the platform.
