## GET Sales Price List Prices

Retrieve the properties and relationships of a Sales Price List Line object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
GET 

businesscentralPrefix/SalesListPrices
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Do not supply a request body for this method.

### Response

Here is an example of the response

```json
     "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/hallgarten.onmicrosoft.com/uat/api/tvisiontech/webbevica/v2.0/$metadata#companies(27d762be-3ccf-ef11-8a6d-7c1e52028c94)/salesListPrices",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzEzMTk0MjQyNDQ2MzYyMjgyNzUwMTswMDsn\"",
            "systemId": "7abadc89-faea-ef11-9345-7c1e52034c5a",
            "itemNo": "4671112E",
            "variantCode": "DUTY PAID",
            "salesType": "Item",
            "assignToType": "Customer",
            "assignToNo": "00226102",
            "salesCode": "00226102",
            "unitOfMeasureCode": "",
            "startingDate": "2025-01-31",
            "endingDate": "2025-03-31",
            "currencyCode": "£",
            "unitPrice": 6.86,
            "priceIncludesVAT": false,
            "minimumQuantity": 0,
            "lineDiscountPercen": 0,
            "systemCreatedAt": "2025-02-14T17:38:52.533Z",
            "systemCreatedBy": "3bf82623-e2d2-4cb0-ae6e-de5395ec449c",
            "systemModifiedAt": "2025-02-14T18:11:21.757Z",
            "systemModifiedBy": "3bf82623-e2d2-4cb0-ae6e-de5395ec449c",
            "tvtwsWebLastModDateTime": "2025-02-14T17:53:31.837Z",
            "tvtwsWebItemPublished": false,
            "currencyCodeFilter": ""
        }
```
### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|	1	|	Price List Line	|	Item No	|	String	|	20	|
|	1	|	Price List Line	|	Variant Code	|	String	|	10	|
|	1	|	Price List Line	|	Sales Type	|	Type	|		|
|	1	|	Price List Line	|	Sales Code	|	String	|	10	|
|	1	|	Price List Line	|	Unit of Measure Code	|	String	|	10	|
|	1	|	Price List Line	|	Currency code	|	String	|		|
|	1	|	Price List Line	|	Ending Date	|	date	|		|
|	1	|	Price List Line	|	Unit Price	|	decimal	|		|
|	1	|	Price List Line	|	Price Includes VAT	|	Boolean	|		|
|	1	|	Price List Line	|	Minimum Quantity	|	decimal	|		|
