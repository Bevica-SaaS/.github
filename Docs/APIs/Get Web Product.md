## GET Web Products

Retrieve the properties and relationships of a web Item object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/webProducts
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/webProducts",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzE3MTA5ODI1MzE5NDM5NTUzMDUxMTswMDsn\"",
            "systemId": "5abce6cd-9c7f-ed11-9989-002248004f60",
            "code": "1",
            "webProductID": "{60E1BEFE-C317-4FFB-ABB6-787DAA87FAF0}",
            "lastModification": "2022-12-19T13:00:32.203Z",
            "published": 0,
            "marketingDescription": "test 1 ",
            "categoryDescription": "White Sparkling",
            "countryCode": "FR",
            "countryDescription": "France",
            "regionCode": "",
            "regionDescription": "",
            "subRegionCode": "",
            "subRegionDescription": "",
            "producerCode": "AGRAPART",
            "producerName": "",
            "itemClassification": "",
            "alcoholPercent": "12.3%",
            "vintage": "2005",
            "grapes": "",
            "attributes": "",
            "tags": "FR,,,,2005,,,12.3%,White Sparkling,",
            "systemCreatedAt": "2022-12-19T12:58:17.473Z",
            "systemCreatedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00",
            "systemModifiedAt": "2022-12-19T13:00:32.203Z",
            "systemModifiedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00"
        }
    ]
}
```

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1       |  Web Product      |  Code        | String |  20          |           |
|  1       |  Web Product      |  Web Product Id  | String |  20      |           |
|  1       |  Web Product      |  Web Last Md. Date Time  | DateTime     |           |
|  1       |  Web Product      |  Published  | Boolean    |               ||
|  1       |  Web Product      |  Last Modification  | DateTime          ||
|  1       |  Web Product      |  Marketing Description  |String |100 |
|  1       |  Web Product      |  Category Code  |String | 20 |
|  1       |  Web Product      |  Category Description  |String | 50 |
|  1       |  Web Product      |  Country Code  |String | 20 |
|  1       |  Web Product      |  Country Description  |  String | 50|
|  1       |  Web Product      |  Region Code  |String | 20 |
|  1       |  Web Product      |  Region Description  |String | 50 |
|  1       |  Web Product      |  SubRegion Code  |String | 20 |
|  1       |  Web Product      |  SubRegion Description  |String | 50 |
|  1       |  Web Product      |  Producer  |String | 20 |
|  1       |  Web Product      |  Item Classification  |String | 20 |
|  1       |  Web Product      |  Alcohol Percent  |Decimal ||
|  1       |  Web Product      |  Vintage  |String | 10 |
|  1       |  Web Product      |  Grapes  |String |  |
|  1       |  Web Product      |  Attributes  |String |  |
|  1       |  Web Product      |  Tags  |String |  |
|  1       |  Web Product      | System Id | GUID |  |  |
|  1       |  Web Product      | System Created At | DateTime |  |  |
|  1       |  Web Product      | System Created By  | String |  |  |
|  1       |  Web Product      | System Modified At | DateTime |  |  |
|  1       |  Web Product      | System Modified By | String |  |  |
<!-- |  1..1    |  SKU\Variant  |  Web Item Id  |String | XXX |
|  1..1    |  SKU\Variant  |  Published  |Boolean ||
|  1..1    |  SKU\Variant  |  Deleted  |Boolean ||
|  1..1    |  SKU\Variant  |  Web Last Mod. Date Time  | DateTime ||
|  1..1    |  SKU\Variant  |  Item No.  |String | XXX |
|  1..1    |  SKU\Variant  |  Blocked  | Boolean ||
|  1..1    |  SKU\Variant  |  Last Modification  | DateTime ||
|  1..1    |  SKU\Variant  |  Description  |String | XXX |
|  1..1    |  SKU\Variant  |  Base UoM Code  |String | XXX |
|  1..1    |  SKU\Variant  |  Base UoM Description  |String | XXX |
|  1..1    |  SKU\Variant  |  Sales UoM Code  |String | XXX |
|  1..1    |  SKU\Variant  |  Sales UoM Description  |String | XXX |
|  1..1    |  SKU\Variant  |  Sales UoM Qty Per  | Decimal ||
|  1..1    |  SKU\Variant  |  Unit Volume  | Decimal ||
|  1..1    |  SKU\Variant  |  Unit Price With Duty  |Decimal ||
|  1..1    |  SKU\Variant  |  Unit Price WithOut Duty  |Decimal ||
|  1..1    |  SKU\Variant  |  Stock Quantity Base  |Decimal ||
|  1..1    |  SKU\Variant  |  Bottles Per Case | Decimal||
|  1..1    |  SKU\Variant  |  Purchasing Code | String||
|  1..1    |  SKU\Variant  |  Unit Weight | Decimal||
|  1..1    |  SKU\Variant  |  Sales Unit Weight | Decimal||
|  1..1    |  SKU\Variant  |  Web UoM Code | String||
|  1..1    |  SKU\Variant  |  Web UoM Description | String||
|  1..1    |  SKU\Variant  |  Web Sale Only Unit | Decimal||
|  1..1    |  SKU\Variant  |  Web Catalogue  | String|| -->
