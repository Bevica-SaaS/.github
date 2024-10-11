## GET Sales Credit Memo Header

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/PostedSalesCrMemoLines
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

### Field Information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Sales Cr.Memo Line | System Id | GUID |  |  |
| 1 | Sales Cr.Memo Line | Sell-to Customer No. | String | 20 |  |
| 1 | Sales Cr.Memo Line | Document No. | String | 20 | |
| 1 | Sales Cr.Memo Line | Line No. | Integer |  |  |
| 1 | Sales Cr.Memo Line | Type | Option | 20 |  |
| 1 | Sales Cr.Memo Line | No. | String | 20 |  |
| 1 | Sales Cr.Memo Line | Location Code | String | 10 |  |
| 1 | Sales Cr.Memo Line | Shipment Date | Date |  |  |
| 1 | Sales Cr.Memo Line | Description | String | 100 |  |
| 1 | Sales Cr.Memo Line | Unit of Measure | String | 50 |  |
| 1 | Sales Cr.Memo Line | Quantity | Decimal |  |  |
| 1 | Sales Cr.Memo Line | Unit Price | Decimal |  |  |
| 1 | Sales Cr.Memo Line | Line Discount % | Decimal |  |  |
| 1 | Sales Cr.Memo Line | Line Discount Amount | Decimal |  |  |
| 1 | Sales Cr.Memo Line | Amount | Decimal |  |  |
| 1 | Sales Cr.Memo Line | Amount Including VAT | Boolean |  |  |
| 1 | Sales Cr.Memo Line | Variant Code | String | 10 | Duty Status |
| 1 | Sales Cr.Memo Line | Unit of Measure Code | String | 10 |  |
| 1 | Sales Cr.Memo Line | Quantity (Base) | Decimal |  |  |


