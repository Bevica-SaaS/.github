## GET Paid Reserve

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/PaidReserves
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/PaidReserves",
    "value": [
        {
            "@odata.etag": "W/\"JzE5Ozc3MTI4MzgxNzQzNDAwNzY3NzYxOzAwOyc=\"",
            "systemId": "0efb92e7-5b75-ed11-9989-000d3a0cd6a6",
            "no": "PRES0010087",
            "systemCreatedAt": "2022-12-06T11:48:38.35Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2022-12-06T11:48:38.35Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "sourceType": "Customer",
            "sourceNo": "1010000XXXXXXXXXXXXX",
            "sourceName": "Asado Bar & Grill",
            "itemNo": "B12141",
            "itemDescription": "Barolo Colonello Prunotto 2009 6x75",
            "unitOfMeasureCode": "75CL",
            "rotationNo": "",
            "qtyPerUnitOfMeasure": 1,
            "origPaidReserveNo": "",
            "quantity": 15,
            "remainingQuantity": 15,
            "qtyBooked": 0,
            "qtyOnBroking": 0,
            "unitPrice": 11,
            "unitCost": 0,
            "condition": "",
            "provenanceSource": "1",
            "contactNomineeNo": "",
            "contactNomineeName": "",
            "documentDate": "2022-08-10",
            "postingDate": "2022-08-10",
            "documentNo": "Q001",
            "expDeliveryInstruction": " ",
            "expDeliveryShipTo": "",
            "internalInformation": "",
            "externalDocumentNo": "",
            "dutyStatusFilter": "",
            "locationFilter": ""
        }
    ]
}
```

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
|  1  | TVT Paid Reserve Information | No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Source Type  |  Enum  | '',Customer,Vendor |  |
|  1  | TVT Paid Reserve Information | Source No |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Source Name  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Item No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Item Description  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Unit of Measure Code  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Information | Rotation No. |  Code  | 50 |  |
|  1  | TVT Paid Reserve Information | Qty. per Unit of Measure  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Original Paid Reserve No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Quantity  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Remaining Quantity  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Qty. Booked  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Qty. on Broking  |  IntegerDecimal  |  |  |
|  1  | TVT Paid Reserve Information | Unit Price  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Unit Cost  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Condition  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Provenance/Source  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Contact Nominee No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Contact Nominee Name  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Document Date  |  Date  |  |  |
|  1  | TVT Paid Reserve Information | Posting Date  |  Date  |  |  |
|  1  | TVT Paid Reserve Information | Document No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Exp. Delivery Instruction  |  Enum  | '',Intro Storage,Deliver to Ship-to |  |
|  1  | TVT Paid Reserve Information | Exp. Delivery Ship-to  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Information | Internal Information  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | External Document No.  |  Code  | 35 |  |
|  1  | TVT Paid Reserve Information | Duty Status Filter  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Information | Location Filter  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Information | System Id | GUID |  |  |
|  1  | TVT Paid Reserve Information | System Created At | DateTime |  |  |
|  1  | TVT Paid Reserve Information | System Created By  | String |  |  |
|  1  | TVT Paid Reserve Information | System Modified At | DateTime |  |  |
|  1  | TVT Paid Reserve Information | System Modified By | String |  |  |

