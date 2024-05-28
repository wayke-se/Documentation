# Fetch Financial Information for a Vehicle

We offer two different solutions for obtaining financial information on a vehicle. The first implementation was created in 2017, and the updated version was released in 2024. It is possible to utilize the same implementation for both versions if your organization is transitioning between them.

### What's the Difference:

1. **Old Version (2017)**
   - Each vehicle can have only one financial institution with information on interest, fees, down payment, residual value, and loan length.

2. **New Updated Version (2024)**
   - Each vehicle can carry multiple financial packages from the same or different financial institutions. Each financial institution still provides details on interest, fees, down payment, residual value, and loan length. Additionally, this version supports different interest rates for various down payments and different residual values based on the loan length.

We have created "packages" to present different alternatives to the end customer. This allows a dealer to create two different packages from the same financial institution, showing a short-term financial product with a large down payment and a long-term financial product with a low down payment, helping the customer understand the possibilities. Packages can have locked settings to present fixed offers.

As a dealer, you can also communicate information to the user as text within a package.

## Example API Requests

### List All Packages (Only for Updated Version)
Retrieve a list of all financial packages that the vehicle should expose with price information from the default settings of the package. This provides all the data needed to describe the car with a monthly cost.

```bash
curl --location 'https://ecom.wayke.se/payment/{vehicleId}/list?branchId={branchId}' \
--header 'x-api-key: [Your API Key Here]'
```

### List Top Package (Available for Both Versions)
Retrieve the most prioritized financial package from the new implementation or the only financial institution from the old version, with the same information as the list endpoint.

```bash
curl --location 'https://ecom.wayke.se/payment/{vehicleId}' \
--header 'x-api-key: [Your API Key Here]'
```

### Customize Financial Package (Available for Both Versions)
Customize each financial package with different inputs for loan length, down payment, and residual value. This endpoint recalculates the offer and provides the same payload as the previous endpoints.

```bash
curl --location 'https://ecom.wayke.se/payment/{waykeId}' \
  -H 'content-type: application/json' \
  --data-raw '{
    "duration": [months of loan],
    "downPayment": [down payment],
    "residual": [residual value as percentage],
    "financialOptionId": [financialOptionId if applicable]
  }'
```
