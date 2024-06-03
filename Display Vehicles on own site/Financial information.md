# Fetch Financial Information for a Vehicle

We offer two different solutions for obtaining financial information on a vehicle. The first implementation was created in 2017, and the updated version was released in 2024. It is possible to utilize the same implementation for both versions if your organization is transitioning between them.

### What's the Difference:

1. **Old Version (2017)**
   - Each vehicle can have only one financial institution with information on interest, fees, down payment, residual value, and loan length.

2. **New Updated Version (2024)**
   - Each vehicle can carry multiple financial options from the same or different financial institutions. Each financial option still provides details on interest, fees, down payment, residual value, and loan length. Additionally, this version supports different interest rates for various down payments and different residual values based on the loan length.
   - We have created "packages" to present different alternatives to the end customer. This allows a dealer to create different packages from the same financial option or institution, for example showing a short-term financial product with a large down payment and a long-term financial product with a low down payment, helping the customer understand the possibilities. Packages can have locked settings to present fixed offers. Using packages is optional.
   - As a dealer, you can also communicate information to the user as text within a package.

## Example API Requests

All endpoint works for both old and new configurations.

### List All payment alternatives (new and recommended)
Retrieve a list of all financial packages that the vehicle should expose with price information from the default settings of the package. This provides all the data needed to describe the car with a monthly cost.

If using the old configuration, this endpoint will return the same financial configuration as `/payment/{vehicleId}` but in a list. Which means you can migrate to this endpoint before switching to the new configuration.

```bash
curl 'https://ecom.wayke.se/payment/{vehicleId}/list'
```
Optionally, `branchId` could be supplied as a query parameter if the vehicle has multiple associated branches, which is usually not the case.


### Get Single (deprecated)
Retrieve the most prioritized financial package from the new implementation or the only financial institution from the old version, with the same information as the list endpoint. This is the old endpoint, it will work with the new configuration in a transition period but will only return a single financial option.

```bash
curl 'https://ecom.wayke.se/payment/{vehicleId}'
```

### Customize Financial Package
Customize each financial package with different inputs for loan length, down payment, and residual value. This endpoint recalculates the offer and provides the same payload as the previous endpoints. Since the `list` endpoint can return different financial options (which can have different interest rates), you must supply `financialOptionId` if you plan to have multiple 

```bash
curl 'https://ecom.wayke.se/payment/{waykeId}' \
  -H 'content-type: application/json' \
  --data-raw '{
    "duration": [months of loan],
    "downPayment": [down payment],
    "residual": [residual value as percentage],
    "financialOptionId": [financialOptionId if applicable]
  }'
```

## Migration to new 2024 version

Steps to migrate to new version.

* Update implementation to use the `payment/{vehicleId}/list` endpoint
* Configure new financial options in Dealer

When both those steps are complete removing the old financial configurations will transition ecom to use your new settings.