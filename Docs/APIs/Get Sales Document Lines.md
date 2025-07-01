## GET Sales Document Lines

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/SalesDocumentLines
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/salesDocumentLines",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzE0MDA3MzA0MDkyMTc1OTE5ODQzMTswMDsn\"",
            "systemId": "30116016-a486-ed11-9989-6045bd0d0c6b",
            "sellToCustomerNo": "1020000",
            "documentType": "Quote",
            "documentNo": "SQ000001",
            "lineNo": 10000,
            "type": "Item",
            "no": "B12141",
            "locationCode": "BLUE",
            "shipmentDate": "2022-01-04",
            "description": "Barolo Colonello Prunotto 2009 6x75",
            "unitOfMeasure": "75CL",
            "quantity": 1,
            "unitPrice": 191.64,
            "lineDiscount": 0,
            "lineDiscountAmount": 0,
            "amount": 191.64,
            "amountIncludingVAT": 229.97,
            "variantCode": "DUTY PAID",
            "unitOfMeasureCode": "6X75CL",
            "quantityBase": 6,
            "tvtTransactionType": "_x0020_",
            "requestedDeliveryDate": "0001-01-01",
            "returnReasonCode": "",
            "tvtSalesLineReasonCode": ""
        },
        {
            "@odata.etag": "W/\"JzE2OzM4OTIzODU1NDEyMzEyMDExOzAwOyc=\"",
            "systemId": "31116016-a486-ed11-9989-6045bd0d0c6b",
            "sellToCustomerNo": "1020000",
            "documentType": "Quote",
            "documentNo": "SQ000001",
            "lineNo": 20000,
            "type": "Item",
            "no": "B12148",
            "locationCode": "BLUE",
            "shipmentDate": "2022-01-04",
            "description": "Barolo Colonello Prunotto 2010 6x75",
            "unitOfMeasure": "75CL",
            "quantity": 1,
            "unitPrice": 191.64,
            "lineDiscount": 0,
            "lineDiscountAmount": 0,
            "amount": 191.64,
            "amountIncludingVAT": 229.97,
            "variantCode": "DUTY PAID",
            "unitOfMeasureCode": "6X75CL",
            "quantityBase": 6,
            "tvtTransactionType": "_x0020_",
            "requestedDeliveryDate": "0001-01-01",
            "returnReasonCode": "",
            "tvtSalesLineReasonCode": ""
        }
    ]
}

```

### Field Information


| Field Name               | Caption                  | Source Field                  |
|--------------------------|--------------------------|-------------------------------|
| systemId                 | SystemId                 | SystemId                      |
| sellToCustomerNo         | Sell-to Customer No.     | Sell-to Customer No.          |
| documentType             | Document Type            | Document Type                 |
| documentNo               | Document No.             | Document No.                  |
| lineNo                   | Line No.                 | Line No.                      |
| type                     | Type                     | Type                          |
| no                       | No.                      | No.                           |
| locationCode             | Location Code            | Location Code                 |
| shipmentDate             | Shipment Date            | Shipment Date                 |
| description              | Description              | Description                   |
| unitOfMeasure            | Unit of Measure          | Unit of Measure               |
| quantity                 | Quantity                 | Quantity                      |
| unitPrice                | Unit Price               | Unit Price                    |
| lineDiscount             | Line Discount %          | Line Discount %               |
| lineDiscountAmount       | Line Discount Amount     | Line Discount Amount          |
| amount                   | Amount                   | Amount                        |
| amountIncludingVAT       | Amount Including VAT     | Amount Including VAT          |
| variantCode              | Variant Code             | Variant Code                  |
| unitOfMeasureCode        | Unit of Measure Code     | Unit of Measure Code          |
| quantityBase             | Quantity (Base)          | Quantity (Base)               |
| tvtTransactionType       | Transaction Type         | TVTBE Transaction Type        |
| requestedDeliveryDate    | Requested Delivery Datee | Requested Delivery Date       |
| returnReasonCode         | Return Reason Code       | Return Reason Code            |
| tvtSalesLineReasonCode   | Sales Line Reason Code   | TVT Sales Line Reason Code    |

---

**Source:** [`src/API/v2.0/APISalesLine.Page.al`](src/API/v2.0/APISalesLine.Page.al)
