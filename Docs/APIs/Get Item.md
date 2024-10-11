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

Coming soon

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
| 1 | Item |  SystemCreatedAt | Date |  | | 
| 1 | Item |  SystemCreatedBy | String |  | | 
| 1 | Item |  SystemId | String |  | | 
| 1 | Item |  SystemModifiedAt | Date |  | | 
| 1 | Item |  SystemModifiedBy | String |  | | 
