
# Så laddar du upp Panorama-bilder till plattformen via API

### Steg 1: Skapa en container

Först behöver du skapa en container som dina bilder ska ligga i.

```bash
curl --location 'https://api.wayke.se/media/v2/panorama-image' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Authorization: Bearer ••••••' \
--data-urlencode 'Metadata.Purpose=Vehicle' \
--data-urlencode 'Metadata.BranchId=<branch-id>' \
--data-urlencode 'Metadata.SortOrder=0'
```

- `Metadata.Purpose`: Syftet med bilderna, t.ex. "Vehicle".
- `Metadata.BranchId`: ID:t för den specifika enheten eller filialen.
- `Metadata.SortOrder`: Ordningen bilderna ska visas i (0 är först).

**Svar:**
Du får tillbaka ett container-ID (UUID), exempel:

```
0316f21d-51cf-441d-bfef-cf90d73178a5
```

---

### Steg 2: Ladda upp bilder

När du skapat containern laddar du upp varje bild separat.

```bash
curl --location 'https://api.wayke.se/media/v2/panorama-image/<container-id>' \
--header 'Authorization: Bearer ••••••' \
--form 'File=@"/sökväg/till/din/bild1.webp"' \
--form 'SortOrder="0"'
```

- Byt ut `<container-id>` mot det ID du fick från steg 1.
- Ange sökvägen till din bildfil.
- `SortOrder` anger ordning (första bilden är normalt 0).

**Svar:**

```json
{
  "imageId": "19f28f51-6b5e-4abe-9d2a-cd6f8ff0a4e1",
  "url": "https://waykeprodsharedstorages.blob.core.windows.net/media/<container-id>/<image-id>"
}
```

Upprepa detta steg för varje panorama-bild du vill ladda upp. Spara varje bilds URL till nästa steg.

---

### Steg 3: Koppla ihop bilderna med ett fordon

Slutligen måste du binda bilderna till ett specifikt fordon.

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

- Byt ut `<vehicle-id>` mot ID:t för det aktuella fordonet.
- Ange URL:erna från varje uppladdad bild från steg 2.

När detta är klart är bilderna kopplade till fordonet och redo att användas på plattformen.
