## GET Sales Prices

Retrieve the properties and relationships of a Sales Prices object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
GET 

businesscentralPrefix/salesPrices
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

    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/salesPrices",
    "value": [
        {
            "@odata.etag": "W/\"JzE5Ozc3NDU3MTMwNTk2MTQzMDgxODMxOzAwOyc=\"",
            "systemId": "a2b0fad7-b5b6-ed11-9a88-000d3a86b91d",
            "itemNo": "B12141",
            "variantCode": "DUTY FREE",
            "salesType": "Campaign",
            "salesCode": "CP1001",
            "unitOfMeasureCode": "",
            "endingDate": "0001-01-01",
            "currencyCode": "£",
            "unitPrice": 10,
            "priceIncludesVAT": false,
            "minimumQuantity": 0,
            "systemCreatedAt": "2023-02-27T15:46:15.657Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2023-02-27T15:47:35.56Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "tvtwsWebLastModDateTime": "2023-02-27T15:47:35.56Z",
            "tvtwsWebItemPublished": false
        }
    ]
}
```
### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|	1	|	Sales Prices	|	Item No	|	String	|	20	|
|	1	|	Sales Prices	|	Variant Code	|	String	|	10	|
|	1	|	Sales Prices	|	Sales Type	|	Type	|		|
|	1	|	Sales Prices	|	Sales Code	|	String	|	10	|
|	1	|	Sales Prices	|	Unit of Measure Code	|	String	|	10	|
|	1	|	Sales Prices	|	Currency Code	| String |		|
|	1	|	Sales Prices	|	Ending Date	|	Date	|		|
|	1	|	Sales Prices	|	Unit Price	|	Decimal	|		|
|	1	|	Sales Prices	|	Price Includes VAT	|	Boolean	|		|
|	1	|	Sales Prices	|	Minimum Quantity	|	Decimal	|		|
|   1   |   Sales Prices      | System Id | GUID |  |  |
|  1    |   Sales Prices      | System Created At | DateTime |  |  |
|  1    |   Sales Prices      | System Created By  | String |  |  |
|  1    |   Sales Prices      | System Modified At | DateTime |  |  |
|  1    |   Sales Prices      | System Modified By | String |  |  |
