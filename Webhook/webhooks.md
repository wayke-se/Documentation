# Wayke Webhook Documentation

## Overview

Webhooks in Wayke are user-defined HTTP callbacks that are triggered by specific events in the Wayke system. When an event occurs in Wayke, a webhook will send an HTTP POST request to the pre-configured URL, allowing for real-time data transmission and integration with external services and applications.

## Configuring Webhooks in Wayke

To set up a webhook in Wayke, follow these steps:

1. Navigate to the "Integration" menu option within the Wayke platform.
2. Provide a callback URL from your application where you want to receive webhook notifications.
3. Configure authentication for the webhook, if necessary, to ensure secure data transmission.

## Available Webhooks

Wayke supports various webhook events, including but not limited to:

- **Status Change in Process Step:** Triggered when there is a status change in any process step.
- **Vehicle Updated:** Triggered when there are updates to vehicle data.
- **New Message:** Triggered when a new message is received.
- **New Incoming Vehicle for Purchase** Triggered when a new vehicle for purhase arrives to the branch 
- **New Order:** Triggered when a new order is created.
- **New Lead from Valuation Widget:** Triggered when a new lead is generated from the valuation widget.



## Webhook Payload Examples

Below are the example payloads for each type of webhook event:

### Status Change on Process Step

```json
{
  "eventType": "Process",
  "processId": "O6qNfT-kD2EoGryJBqqG9Oc81kV",
  "processName": "Inköpsprocess",
  "stepId": "O6qNfNfvr6-0t8VUmFjnzZQk82o",
  "stepName": "Förkalkyl",
  "state": "started/pending/completed",
  "eventTime": "2023-06-05T08:11:25.9751982Z",
  "itemId": "7ca2ab6f-0593-4ae4-a7b4-1618dcc4b131",
  "registrationNumber": "CV95276",
  "vehicleIdentificationNumber": "WBA5X710XLFJ73788"
}
```

### Vehicle Updated

```json
{
  "id": "603c5053-af12-4783-b8b0-2a7589a35c07",
  "registrationNumber": "ABC123",
  "vehicleIdentificationNumber": "YV1UZBFVDN1906224",
  "status": "Unpublished"
}
```

### New Message

```json
{
    "branch": {
        "id": "1bfec2d5-b3a6-4dda-9c0e-c993d55ca1b0"
    },
    "message": {
        "id": "e8333b6a-bedf-4d3b-8461-e5ca13613d74",
        "text": "Lorem ipsum dolor sit amet, ",
        "token": "6ysz27s_74w86",
        "createdAt": "2023-03-20T18:27:50.3086451Z",
        "createdBy": {
            "id": "f9076bf3-76f8-477c-5424-08d915130698",
            "type": "user",
            "name": "Firstname Lastname",
            "telephone": "+46700000000",
            "ip": "213.67.207.91"
        },
        "conversation": {
            "id": "4dd452d8-fc46-41b6-b146-5fa1bc69f3ff",
            "title": "BFB25K - BMW M850i xDrive Gran Coupe",
            "avatarUrl": "https://test-cdn.wayketech.se/media/fbec8ca5-eaf2-4990-ab94-bfa55be4a704/88996514-d939-497a-a3ee-f2316eafd346/225x150",
            "members": [
                {
                    "id": "f9076bf3-76f8-477c-5424-08d915130698",
                    "type": "user",
                    "name": "Firstname Lastname",
                    "email": "test@mail.com",
                    "telephone": "+46700000000"
                },
                {
                    "id": "b857d1fe-03f3-4166-b0d7-8e0e8f882c1c",
                    "type": "item",
                    "name": "BMW M850i xDrive Gran Coupe",
                    "avatar": "https://test-cdn.wayketech.se/media/fbec8ca5-eaf2-4990-ab94-bfa55be4a704/88996514-d939-497a-a3ee-f2316eafd346/225x150"
                },
                {
                    "id": "1bfec2d5-b3a6-4dda-9c0e-c993d55ca1b0",
                    "type": "branch",
                    "name": "Test Branch",
                    "email": "test@wayke.se",
                    "telephone": "+46700000000",
                    "avatar": "https://test-cdn.wayketech.se/media/e0df1b495e7f49a791e4e35958984f70/6a3af0ed4184411dbf13f9f756570252"
                }
            ],
            "metadata": [
                {
                    "key": "exchange-car-regnr",
                    "value": "ABC123"
                },
                {
                    "key": "exchange-car-mileage",
                    "value": "1234"
                },
                {
                    "key": "exchange-car-info",
                    "value": "Cras ornare magna eget magna iaculis"
                },
                {
                    "key": "financial-aid",
                    "value": "Jag är intresserad av finansiering"
                },
                {
                    "key": "insurance-aid",
                    "value": "Jag är intresserad av försäkring"
                }
            ]
        }
    }
}
```

### New Incoming Vehicle for Purchase

```json
{
  "branch": {
    "id": "1bfec2d5-b3a6-4dda-9c0e-c993d55ca1b0"
  },
  "lead": {
    "id": "db0221ff-ebf0-4610-89ff-91c8e03309d0",
    "contact": {
      "firstName": "Firstname",
      "lastName": "Lastname",
      "phoneNumber": "0700000000",
      "email": "test@mail.com"
    },
    "metadata": [
      {
        "key": "condition",
        "value": "VeryGood"
      },
      {
        "key": "registrationNumber",
        "value": "BAM14F"
      },
      {
        "key": "description",
        "value": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer congue velit nibh, at mollis sapien fermentum sit amet. Ut ut egestas magna, vel pharetra erat"
      },
      {
        "key": "milage",
        "value": "4000"
      },
      {
        "key": "pricePrediction",
        "value": "538600"
      },
      {
        "key": "conditionReductionVeryGood",
        "value": "81.0"
      },
      {
        "key": "conditionReductionGood",
        "value": "1.0"
      },
      {
        "key": "conditionReductionOk",
        "value": "1.0"
      }
    ],
    "type": "registrationOfInterestToSell",
    "createdAt": "2023-11-07T08:19:45.7867015Z"
  }
}
```


### New Incoming Ecom Order
```json

{
    "id": "7384171f-193d-4651-92a5-d9d976e0092f",
    "orderNumber": "15705218",
    "waykeId": "29eaad4a-a6df-4cdf-91fa-a5ab4149bca8",
    "price": 549800,
    "createdAt": "2023-03-20T22:31:26.6025563Z",
    "accessories": [
        {
            "articleNumber": "123",
            "manufacturer": "",
            "model": "",
            "name": "",
            "price": 12345
        }
    ],
    "vehicle": {
        "registrationNumber": "KCM81X",
        "vehicleIdentificationNumber": "WBA31CG03MCG32366",
        "manufacturer": "BMW",
        "modelSeries": "5-serie",
        "modelName": "530e xDrive Touring",
        "modelYear": 2021,
        "mileage": 4115,
        "shortDescription": "BMW 530e xDrive M-Sport Panorama Drag HiFi Navi Leasbar"
    },
    "customer": {
        "name": "Firstname Lastname",
        "givenName": "Firstname",
        "surname": "Lastname",
        "email": "test@mail.com",
        "phoneNumber": "+460700000000",
        "personalNumber": "1981xxxxxxxx",
        "address": {
            "name": "Firstname Lastname",
            "street": "Street",
            "postalCode": "42341",
            "city": "City"
        },
        "didVerifyWithBankId": true
    },
    "delivery": {
        "type": "Pickup"
    },
    "insurance": {
        "name": "BMW Försäkring",
        "personalNumber": "1981xxxxxxxx",
        "brand": "BMW",
        "estimatedDrivingDistance": "Between0And1000"
    },
    "payment": {
        "type": "Loan",
        "financialInstitution": "Finance Institute",
        "unit": "kr",
        "price": 549800,
        "loan": {
            "administrationFee": 100,
            "setupFee": 101,
            "interest": 1,
            "effectiveInterestRate": 0.0144,
            "residualValue": 0.2,
            "downPayment": 109960,
            "duration": 84,
            "monthlyCost": 4159,
            "totalResidualValue": 109960,
            "totalCost": 28016
        }
    },
    "tradeIn": {
        "estimatedValue": 568100,
        "reducedValuation": 511290,
        "condition": "VeryGood",
        "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus eu consequat dui, a iaculis orci. Nunc quis mauris quis sem gravida interdum quis eu mauris",
        "registrationNumber": "BAM14F",
        "manufacturer": "Volvo",
        "modelSeries": "XC60",
        "modelName": "XC60 T6 AWD Recharge",
        "modelYear": 2022,
        "mileage": 3000,
        "shortDescription": "Volvo XC60 XC60 T6 AWD Recharge"
    }
}
```
### New Lead from Valuation Widget
```json
{
    "branch": {
        "id": "1bfec2d5-b3a6-4dda-9c0e-c993d55ca1b0"
    },
    "lead": {
        "id": "db0221ff-ebf0-4610-89ff-91c8e03309d0",
        "contact": {
            "firstName": "Firstname",
            "lastName": "Lastname",
            "phoneNumber": "0700000000",
            "email": "test@mail.com"
        },
        "metadata": [
            {
                "key": "condition",
                "value": "VeryGood"
            },
            {
                "key": "registrationNumber",
                "value": "BAM14F"
            },
            {
                "key": "description",
                "value": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer congue velit nibh, at mollis sapien fermentum sit amet. Ut ut egestas magna, vel pharetra erat"
            },
            {
                "key": "milage",
                "value": "4000"
            },
            {
                "key": "pricePrediction",
                "value": "538600"
            },
            {
                "key": "conditionReductionVeryGood",
                "value": "81.0"
            },
            {
                "key": "conditionReductionGood",
                "value": "1.0"
            },
            {
                "key": "conditionReductionOk",
                "value": "1.0"
            }
        ],
        "type": "registrationOfInterestToSell",
        "createdAt": "2023-11-07T08:19:45.7867015Z"
    }
}
```

## Receiving and Handling Webhooks

To effectively use webhooks, your application should:

1. **Listen for POST requests** on the URL specified when setting up the webhook.
2. **Validate the request** to ensure it comes from Wayke. This typically involves checking a signature in the header against a known public key or shared secret.
3. **Parse the JSON payload** to extract the relevant data.
4. **Acknowledge receipt** by responding with a 200 HTTP status code promptly. Otherwise, Wayke may assume delivery failed and retry.
5. **Process the data** accordingly based on the type of event received.
