## GET Posted Sales Invoice Lines

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/PostedSalesInvoiceLines
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/PostedSalesInvoiceLines",
    "value": [
        {
            "@odata.etag": "W/\"JzE5OzMyNTAxNTU5Nzg2NDM2NTU0NzcxOzAwOyc=\"",
            "systemId": "63116016-a486-ed11-9989-6045bd0d0c6b",
            "sellToCustomerNo": "1020000",
            "documentNo": "SI000001",
            "lineNo": 10000,
            "type": "Item",
            "no": "B12141",
            "locationCode": "BLUE",
            "shipmentDate": "2021-01-04",
            "description": "Barolo Colonello Prunotto 2009 6x75",
            "unitOfMeasure": "6X75CL",
            "quantity": 14,
            "unitPrice": 191.64,
            "lineDiscount": 0,
            "lineDiscountAmount": 0,
            "amount": 2682.96,
            "amountIncludingVAT": 3219.55,
            "variantCode": "DUTY PAID",
            "unitOfMeasureCode": "6X75CL",
            "quantityBase": 84
        },
        {
            "@odata.etag": "W/\"JzIwOzE3NTM3ODYxMTc2MDQ3MDg1Njc0MTswMDsn\"",
            "systemId": "64116016-a486-ed11-9989-6045bd0d0c6b",
            "sellToCustomerNo": "1020000",
            "documentNo": "SI000001",
            "lineNo": 20000,
            "type": "Item",
            "no": "B12148",
            "locationCode": "BLUE",
            "shipmentDate": "2021-01-04",
            "description": "Barolo Colonello Prunotto 2010 6x75",
            "unitOfMeasure": "6X75CL",
            "quantity": 2,
            "unitPrice": 191.64,
            "lineDiscount": 0,
            "lineDiscountAmount": 0,
            "amount": 383.28,
            "amountIncludingVAT": 459.94,
            "variantCode": "DUTY PAID",
            "unitOfMeasureCode": "6X75CL",
            "quantityBase": 12
        }
	]
}

```

### Field Information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Sales Invoice Line | System Id | GUID |  |  |
| 1 | Sales Invoice Line | Sell-to Customer No. | String | 20 |  |
| 1 | Sales Invoice Line | Document No. | String | 20 | |
| 1 | Sales Invoice Line | Line No. | Integer |  |  |
| 1 | Sales Invoice Line | Type | Option | 20 |  |
| 1 | Sales Invoice Line | No. | String | 20 |  |
| 1 | Sales Invoice Line | Location Code | String | 10 |  |
| 1 | Sales Invoice Line | Shipment Date | Date |  |  |
| 1 | Sales Invoice Line | Description | String | 100 |  |
| 1 | Sales Invoice Line | Unit of Measure | String | 50 |  |
| 1 | Sales Invoice Line | Quantity | Decimal |  |  |
| 1 | Sales Invoice Line | Unit Price | Decimal |  |  |
| 1 | Sales Invoice Line | Line Discount % | Decimal |  |  |
| 1 | Sales Invoice Line | Line Discount Amount | Decimal |  |  |
| 1 | Sales Invoice Line | Amount | Decimal |  |  |
| 1 | Sales Invoice Line | Amount Including VAT | Boolean |  |  |
| 1 | Sales Invoice Line | Variant Code | String | 10 | Duty Status |
| 1 | Sales Invoice Line | Unit of Measure Code | String | 10 |  |
| 1 | Sales Invoice Line | Quantity (Base) | Decimal |  |  |


