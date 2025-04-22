## GET Items

Retrieve the properties and relationships of a Item object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/items
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/items",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzE1OTY1OTUyNjQ5NTkxMTQzMDg0MTswMDsn\"",
            "systemId": "42f03390-73ad-ef11-8a6d-6045bd0f8a1b",
            "webItemId": "{95AB57A4-8ADA-4DCD-A570-1CF8F6E5DAF9}",
            "published": true,
            "deleted": false,
            "webLastModDateTime": "2024-11-28T10:29:02.263Z",
            "itemNo": "B12141",
            "blocked": false,
            "description": "Barolo Colonello Prunotto 2009 6x75",
            "baseUoMCode": "75CL",
            "baseUoMDescription": "75 cl",
            "salesUoMCode": "6X75CL",
            "salesUoMDescription": "6x75cl",
            "salesUoMQtyPer": 6,
            "unitVolume": "75cl",
            "unitPriceWithDuty": 26.99,
            "unitPriceWithOutDuty": 24.75,
            "stockQuantityBase": 5928,
            "bottlePerCase": "6",
            "purchasingCode": "",
            "unitWeight": 44.5,
            "salesUnitWeight": 444,
            "webUoMCode": "6X75CL",
            "webUoMDescription": "6x75cl",
            "webUoMQtyPer": 6,
            "webSaleOnlyUnit": "_x0020_",
            "webCatalogue": "12",
            "drinkFrom": "",
            "drinkTo": "",
            "appellation": "",
            "appellationDescription": "",
            "regionCode": "PIEMONTE",
            "regionDescription": "Piemonte",
            "subRegionCode": "LANGHE",
            "subRegionDescription": "Langhe",
            "classificationCode": "DOCG",
            "date1": "0001-01-01",
            "date2": "0001-01-01",
            "date3": "0001-01-01",
            "class1": "DISTRIBUTION",
            "class2": "",
            "class3": "",
            "class4": "",
            "class5": "",
            "number1": 0,
            "number2": 0,
            "number3": 0,
            "number5": 0,
            "number4": 0,
            "option1": "_x0020_",
            "option3": "_x0020_",
            "option2": "_x0020_",
            "option4": "_x0020_",
            "option5": "_x0020_",
            "colourCode": "RED",
            "colourDescription": "Red",
            "systemCreatedAt": "2024-11-28T10:29:00.61Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2024-11-28T10:29:02.263Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b"
        }
    ]
}

```

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
| 1 | Item |  Web Id | String | 50 | | 
| 1 | Item |  Published | Boolean |  | | 
| 1 | Item |  Deleted | Boolean |  | | 
| 1 | Item |  Last Mod. Date Time | Date |  | | 
| 1 | Item |  Item No. | String | 20 | | 
| 1 | Item |  Blocked | Boolean |  | | 
| 1 | Item |  Description | String | 100 | | 
| 1 | Item |  Base UoM Code | String | 10 | | 
| 1 | Item |  Base UoM Description | String | 100 | | 
| 1 | Item |  Sales UoM Code | String | 10 | | 
| 1 | Item |  Sales UoM Description | String | 100 | | 
| 1 | Item |  Sales UoM Qty Per | Decimal |  | | 
| 1 | Item |  Unit Volume | Decimal |  | | 
| 1 | Item |  UnitPriceWithDuty | Decimal |  | | 
| 1 | Item |  UnitPriceWithOutDuty | Decimal |  | | 
| 1 | Item |  StockQuantityBase | Decimal |  | | 
| 1 | Item |  Bottles Per Case | Decimal |  | | 
| 1 | Item |  Purchasing Code | String | 10 | | 
| 1 | Item |  Unit Weight | Decimal |  | | 
| 1 | Item |  Sales Unit Weight | Decimal |  | | 
| 1 | Item |  Web UoM Code | String | 10 | | 
| 1 | Item |  Web UoM Description | String | 100 | | 
| 1 | Item |  Web UoM Qty Per | Decimal |  | | 
| 1 | Item |  Web Sale Only Unit | Decimal |  | | 
| 1 | Item |  Web Catalogue | String |  | | 
| 1 | Item |  Drink From | String | 10 | | 
| 1 | Item |  Drink To | String | 10 | | 
| 1 | Item |  Appellation Code | String | 20 | | 
| 1 | Item |  Appellation Description | String | 50 | | 
| 1 | Item |  Region Code | String | 20 | | 
| 1 | Item |  Region Description | String | 50 | | 
| 1 | Item |  SubRegion Code | String | 20 | | 
| 1 | Item |  SubRegion Description | String | 50 | | 
| 1 | Item |  Classification Code | String | 20 | | 
| 1 | Item |  TVT Date 1 | Date |  | | 
| 1 | Item |  TVT Date 2 | Date |  | | 
| 1 | Item |  TVT Date 3 | Date |  | | 
| 1 | Item |  TVT Class 1 | String | 20 | | 
| 1 | Item |  TVT Class 2 | String | 20 | | 
| 1 | Item |  TVT Class 3 | String | 20 | | 
| 1 | Item |  TVT Class 4 | String | 20 | | 
| 1 | Item |  TVT Class 5 | String | 20 | | 
| 1 | Item |  TVT Number 1 | Decimal |  | | 
| 1 | Item |  TVT Number 2 | Decimal |  | | 
| 1 | Item |  TVT Number 3 | Decimal |  | | 
| 1 | Item |  TVT Number 5 | Decimal |  | | 
| 1 | Item |  TVT Number 4 | Decimal |  | | 
| 1 | Item |  TVT Option 1 | String | 20 | | 
| 1 | Item |  TVT Option 3 | String | 20 | | 
| 1 | Item |  TVT Option 2 | String | 20 | | 
| 1 | Item |  TVT Option 4 | String | 20 | | 
| 1 | Item |  TVT Option 5 | String | 20 | | 
| 1 | Item |  Colour Code | String | 20 | | 
| 1 | Item |  Colour Description | String | 50 | | 
| 1 | Item |  SystemCreatedAt | Date |  | | 
| 1 | Item |  SystemCreatedBy | String |  | | 
| 1 | Item |  SystemId | String |  | | 
| 1 | Item |  SystemModifiedAt | Date |  | | 
| 1 | Item |  SystemModifiedBy | String |  | | 
