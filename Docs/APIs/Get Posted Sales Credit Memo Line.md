## GET Sales Posted Sales Credit Memo Lines

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

{
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/PostedSalesCrMemoLines",
    "value": [
        {
            "@odata.etag": "W/\"JzE5OzczNzQ4Mzg2MjIzNDc1MDgzMDMxOzAwOyc=\"",
            "systemId": "025533a4-5088-ed11-9989-6045bd0d024f",
            "sellToCustomerNo": "1010000",
            "documentNo": "SCR000001",
            "lineNo": 10000,
            "type": "Charge_x0020__x0028_Item_x0029_",
            "no": "P-STORAGE",
            "locationCode": "BLUE",
            "shipmentDate": "2022-12-30",
            "description": "Storage",
            "unitOfMeasure": "",
            "quantity": 11,
            "unitPrice": 1,
            "lineDiscount": 0,
            "lineDiscountAmount": 0,
            "amount": 11,
            "amountIncludingVAT": 13.2,
            "variantCode": "",
            "unitOfMeasureCode": "",
            "quantityBase": 11
        },
        {
            "@odata.etag": "W/\"JzIwOzE1NTU2NTk3MDgzODcxNjMzMDg2MTswMDsn\"",
            "systemId": "061b4a6d-e297-ed11-bff5-0022481b46da",
            "sellToCustomerNo": "1010000",
            "documentNo": "SCR000002",
            "lineNo": 10000,
            "type": "G_x002F_L_x0020_Account",
            "no": "8110",
            "locationCode": "BLUE",
            "shipmentDate": "2023-01-19",
            "description": "Cleaning",
            "unitOfMeasure": "",
            "quantity": 1,
            "unitPrice": 100,
            "lineDiscount": 0,
            "lineDiscountAmount": 0,
            "amount": 100,
            "amountIncludingVAT": 120,
            "variantCode": "",
            "unitOfMeasureCode": "",
            "quantityBase": 1
        }
    ]
}

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


