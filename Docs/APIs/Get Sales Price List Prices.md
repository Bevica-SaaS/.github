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
{
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/salesListPrices",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzExMzI1NjIzMDM1MDA0Mjk2OTA1MTswMDsn\"",
            "systemId": "7596e64b-d7f0-ee11-a1ff-7c1e5202d8ad",
            "itemNo": "B12141",
            "variantCode": "DUTY FREE",
            "salesType": "Item",
            "salesCode": "S00002",
            "unitOfMeasureCode": "",
            "endingDate": "0001-01-01",
            "currencyCode": "£",
            "unitPrice": 31,
            "priceIncludesVAT": false,
            "minimumQuantity": 0,
            "systemCreatedAt": "2024-04-02T09:56:41.433Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2024-11-28T10:29:02.527Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "tvtwsWebLastModDateTime": "0001-01-01T00:00:00Z",
            "tvtwsWebItemPublished": true,
            "currencyCodeFilter": ""
        }
    ]
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
