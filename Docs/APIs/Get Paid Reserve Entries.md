## GET Paid Reserve Entries

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/PaidReserveEntries
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/PaidReserveEntries",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzExNjkzNjY4Nzk4MDM3NTc3MDAzMTswMDsn\"",
            "systemId": "9e1702f4-5b75-ed11-9989-000d3a0cd6a6",
            "entryNo": 106,
            "itemNo": "B12141",
            "postingDate": "2022-08-10",
            "entryType": "Stock into Paid Reserve",
            "paidReserveNo": "PRES0010087",
            "documentNo": "Q001",
            "description": "Barolo Colonello Prunotto 2009 6x75",
            "locationCode": "BLUE",
            "quantity": 15,
            "open": true,
            "quantityBase": 15,
            "remQuantityBase": 15,
            "unitCost": 0,
            "totalCost": 0,
            "unitPrice": 11,
            "totalPrice": 165,
            "sourceName": "Asado Bar & Grill",
            "reasonCode": "",
            "sourceType": "Customer",
            "sourceNo": "1010000XXXXXXXXXXXXX",
            "provenanceSource": "1",
            "condition": "",
            "origPaidReserveNo": "",
            "rotationNo": "",
            "bestBeforeDate": "0001-01-01",
            "rotationRef": "",
            "qtyBooked": 0,
            "qtyResBooked": 0,
            "reservedQuantity": 15,
            "variantCode": "DUTY FREE",
            "qtyPerUnitOfMeasure": 1,
            "unitOfMeasureCode": "75CL",
            "systemCreatedAt": "2022-12-06T11:48:53.757Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2022-12-06T11:48:53.757Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "documentDate": "2022-08-10",
            "externalDocumentNo": "",
            "documentType": " ",
            "documentLineNo": 10000,
            "internalInformation": "",
            "itemLedgerEntryNo": 2205,
            "expDeliveryInstruction": " ",
            "expDeliveryShipTo": "",
            "contactNomineeNo": "",
            "contactNomineeName": "",
            "applyToILENo": 0
        },
    ]
}
```

### Fields Information

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
|  1  | TVT Paid Reserve Led. Entry | Entry No.  |  Integer  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Item No.  | String | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Description | String  | 100 |  |
|  1  | TVT Paid Reserve Led. Entry | Posting Date  |  Date  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Entry Type  |  Enum  | Stock Into,Withdrawal Stock,Transfer Stock,Cancel,Split,Purchase|  |
|  1  | TVT Paid Reserve Led. Entry | Paid Reserve No.  | String | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Document No.  | String | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Document Line No. | Integer  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Document Date | Date  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Location Code  | String | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Quantity  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Open  |  Boolean  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Quantity (Base)  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Rem. Quantity (Base)  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Unit Cost  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Total Unit Cost  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Unit Price  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Total Unit Price  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Source Name  |  String  | 100 |  |
|  1  | TVT Paid Reserve Led. Entry | Reason Code  | String | 10 |  |
|  1  | TVT Paid Reserve Led. Entry | Source Type  |  Enum  | '',Customer,Vendor |  |
|  1  | TVT Paid Reserve Led. Entry | Source No. | String | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Provenance/Source  |  String  | 100 |  |
|  1  | TVT Paid Reserve Led. Entry | Condition  |  String  | 100 |  |
|  1  | TVT Paid Reserve Led. Entry | Contact Nominee No. | String | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Contact Nominee Name | String  | 100 |  |
|  1  | TVT Paid Reserve Led. Entry | Exp. Delivery Instructions | Enum  | '',Into Storage,Deliver to Ship-to |  |
|  1  | TVT Paid Reserve Led. Entry | Exp. Delivery Ship-to | String | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | External Document No. 5 |  |
|  1  | TVT Paid Reserve Led. Entry | Internal Information | String  | 100 |  |
|  1  | TVT Paid Reserve Led. Entry | Original Paid Reserve No.  | String | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Best Before Date  |  Date  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Rotation Ref.  | String | 50  |  |
|  1  | TVT Paid Reserve Led. Entry | Rotation No. | String | 50 |  |
|  1  | TVT Paid Reserve Led. Entry | Qty. Booked  |  Decimal  |   |  |
|  1  | TVT Paid Reserve Led. Entry | Qty. Res. (Booked)  |  Decimal  |   |  |
|  1  | TVT Paid Reserve Led. Entry | Reserved Quantity |  Decimal  |   |  |
|  1  | TVT Paid Reserve Led. Entry | Item Ledger Entry No. | Integer  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Apply to ILE No. | Integer  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Variant Code | String  | 10  |  |
|  1  | TVT Paid Reserve Led. Entry | Qty. per Unit of Measure  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Unit of Measure Code  | String | 10 |  |
|  1  | TVT Paid Reserve Led. Entry | System Id | GUID |  |  |
|  1  | TVT Paid Reserve Led. Entry | System Created At | DateTime |  |  |
|  1  | TVT Paid Reserve Led. Entry | System Created By  | String |  |  |
|  1  | TVT Paid Reserve Led. Entry | System Modified At | DateTime |  |  |
|  1  | TVT Paid Reserve Led. Entry | System Modified By | String |  |  |
