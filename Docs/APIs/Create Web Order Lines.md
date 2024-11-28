## Create Web Order Lines

Retrieve the properties and relationships of a Web Lines object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
POST

businesscentralPrefix/webOrderLines
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Here is an example of the request

```json
   
{

    "orderGroup": "GROUP_A",
    "orderId": "PFLOW997",
    "lineId": "1",
    "productId": "B12141",
    "unitOfMeasureId": "6X75CL",
    "description": "Barolo Colonello, Prunotto 2009 6x75",
    "paidReserveNo": "PRES0010144",
    "quantity": 40,
    "unitPrice": 0,
}

```


### Response

Here is an example of the response

```json
{
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/webOrderLines",
    "value": [
        {
            "@odata.etag": "W/\"JzE5OzEyNjA1MTc0NDE5MzU2ODQzODYxOzAwOyc=\"",
            "systemId": "82b0bab8-54bf-ed11-9a88-000d3a86ba5f",
            "orderGroup": "GROUP_A",
            "orderId": "PFLOW997",
            "lineId": "1",
            "productId": "B12141",
            "unitOfMeasureId": "6X75CL",
            "description": "Barolo Colonello, Prunotto 2009 6x75",
            "paidReserveNo": "PRES0010144",
            "quantity": 40,
            "unitPrice": 0,
            "systemCreatedAt": "2023-03-10T15:03:32.95Z",
            "systemCreatedBy": "ce53a24b-ca42-4195-af5e-f3027962c9ec",
            "systemModifiedAt": "2023-03-10T15:14:32.5Z",
            "systemModifiedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00"
        }
}
```

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      | Mandatory | Required |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |--- |--- |
| 1  | Web Order Lines | System Id | GUID |  |  |
| 1  | Web Order Lines | Order Group | String | 50 | Key |  |  |
| 1  | Web Order Lines | Order Id | String | 50 | Key (Unique External Reference) | Y | Y |
| 1  | Web Order Lines | Line Id | String | 50 | Key (Unique External Reference) | Y | Y |
| 1  | Web Order Lines | Product Id | String | 50 | Web Specific |  | Y |
| 1  | Web Order Lines | Description | String | 50 | Standard |  | Y |
| 1  | Web Order Lines | Unit of Measure Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Lines | Quantity | Decimal |  | Standard |  | Y |
| 1  | Web Order Lines | Unit Price | Decimal |  | Standard |  | Y |
| 1  | Web Order Lines | System Created At | DateTime |  |  |
| 1  | Web Order Lines | System Created By  | String |  |  |
| 1  | Web Order Lines | System Modified At | DateTime |  |  |
| 1  | Web Order Lines | System Modified By | String |  |  |


<!-- | 1..N  | Web Order Lines | Force Calculation Price | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Lot No. | String | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Negative | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Type | Option |  | Standard |  |  |
| 1..N  | Web Order Lines | No. | String | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Shipment Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Description | String | 50 | Standard |  | Y |
| 1..N  | Web Order Lines | Description 2 | String | 50 | Standard |  |  |
| 1..N  | Web Order Lines | VAT % | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Line Discount % | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Line Discount Amount | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Net Amount | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Amount Including VAT | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Shortcut Dimension 1 Code | String | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Shortcut Dimension 2 Code | String | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Gen. Bus. Posting Group | String | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Gen. Prod. Posting Group | String | 20 | Standard |  |  |
| 1..N  | Web Order Lines | VAT Bus. Posting Group | String | 20 | Standard |  |  |
| 1..N  | Web Order Lines | VAT Prod. Posting Group | String | 20 | Standard |  |  |
| 1..N  | Web Order Lines | VAT Base Amount | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Unit Cost | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | VAT Identifier | String | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Variant Code | String | 10 | Standard |  |  |
| 1..N  | Web Order Lines | Qty. per Unit of Measure | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Unit of Measure Code | String | 10 | Standard |  |  |
| 1..N  | Web Order Lines | Item Category Code | String | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Requested Delivery Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Promised Delivery Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Planned Delivery Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Planned Shipment Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Decimal 01 | Decimal |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Integer 01 | Integer |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Date 01 | Date |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Code 01 | String | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Time 01 | Time |  | Web Specific |  |  |
| 1..N  | Web Order Lines | DateTime 01 | DateTime |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Text 01 | String | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Boolean 01 | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Decimal 02 | Decimal |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Integer 02 | Integer |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Date 02 | Date |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Code 02 | String | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Time 02 | Time |  | Web Specific |  |  |
| 1..N  | Web Order Lines | DateTime 02 | DateTime |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Text 02 | String | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Boolean 02 | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Decimal 03 | Decimal |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Integer 03 | Integer |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Date 03 | Date |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Code 03 | String | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Time 03 | Time |  | Web Specific |  |  |
| 1..N  | Web Order Lines | DateTime 03 | DateTime |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Text 03 | String | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Boolean 03 | Boolean |  | Web Specific |  |  | -->
