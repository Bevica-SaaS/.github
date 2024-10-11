## GET Manifest Lines

Retrieve the properties and relationships of a Manifest object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/manifestsLines
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/manifestLines",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzE2NDk0NTc5NDI1NTYyMzA3MTExMTswMDsn\"",
            "systemId": "8b67e47c-20ca-ed11-a7c9-00224800e466",
            "documentNo": "SO001049",
            "manifestNo": "DMAN000001",
            "lineNo": 10000,
            "dutyStatus": "DUTY PAID",
            "sourceNo": "1010000",
            "totalEqCases": 0.5,
            "shippingAgentCode": "OWN LOG.",
            "shippingAgentServiceCode": "NEXT DAY",
            "noOfItemLines": 1,
            "grossWeight": 0,
            "netWeight": 0,
            "postedDocumentNo": "",
            "finalDeliveryType": "Order Address",
            "toAddress": "2 Lewes Road",
            "toAddress2": "",
            "toAddressCode": "DUDLEY",
            "toCity": "Dudley",
            "toContact": "Bryn Paul Dunton",
            "toCountryRegionCode": "GB",
            "toCounty": "",
            "fromAddress": "South East Street, 3",
            "fromAddress2": "",
            "fromAddressCode": "BLUE",
            "fromCity": "Birmingham",
            "fromContact": "Jeff Smith",
            "fromCountryRegionCode": "GB",
            "fromCounty": "",
            "fromName": "Blue Warehouse",
            "fromName2": "",
            "fromPostCode": "B27 4KT",
            "systemCreatedAt": "2023-03-24T08:47:21.193Z",
            "systemCreatedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00",
            "systemModifiedAt": "2023-03-24T08:47:21.193Z",
            "systemModifiedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00"
        }
    ]
}
```
### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1          | TVT Manifest Line V2    | System Id | GUID |  |  |
|  1          | TVT Manifest Line V2    | Document No. | String | 20 |  |
|  1          | TVT Manifest Line V2    | Manifest No. | String | 20 |  |
|  1          | TVT Manifest Line V2    | Line No. | Integer |  |  |
|  1          | TVT Manifest Line V2    | Duty Status | String | 10 |  |
|  1          | TVT Manifest Line V2    | Source No. | String | 20 |  |
|  1          | TVT Manifest Line V2    | Total Eq. Cases | Decimal | 20 |  |
|  1          | TVT Manifest Line V2    | Shipping Agent Code      |  Code    | 10            | |
|  1          | TVT Manifest Line V2    | Shipping Agent Service Code      |  Code    | 10            | |
|  1          | TVT Manifest Line V2    | No. of Item Lines      |  Integer    |   | |
|  1          | TVT Manifest Line V2    | Gross Weight     |  Decimal    |   | |
|  1          | TVT Manifest Line V2    | Net Weight     |  Decimal    |   | |
|  1          | TVT Manifest Line V2    |  Posted Document No. | String | 20 |  |
|  1          | TVT Manifest Line V2    |  Final Delivery Type| Enum |Order Address,Manifest To Address,Manifest From Address |  |
|  1          | TVT Manifest Line V2    | To Address         |  String    | 100           | |
|  1          | TVT Manifest Line V2    | To Address 2         |  String    | 50           | |
|  1          | TVT Manifest Line V2    | To Address Code         |  Code    | 10            | |
|  1          | TVT Manifest Line V2    | To City         |  String    | 30           | |
|  1          | TVT Manifest Line V2    | To Contact         |  String    | 100            | |
|  1          | TVT Manifest Line V2    | To Country/Region Code         |  Code    |   10         | |
|  1          | TVT Manifest Line V2    | To County         |  String    | 100            | |
|  1          | TVT Manifest Line V2    | From Address         |  String    | 100           | |
|  1          | TVT Manifest Line V2    | From Address 2         |  String    | 50           | |
|  1          | TVT Manifest Line V2    | From Address Code         |  Code    | 10            | |
|  1          | TVT Manifest Line V2    | From City         |  String    | 30           | |
|  1          | TVT Manifest Line V2    | From Contact         |  String    | 100            | |
|  1          | TVT Manifest Line V2    | From Country/Region Code         |  Code    |   10         | |
|  1          | TVT Manifest Line V2    | From County         |  String    | 100            | |
|  1          | TVT Manifest Line V2    | Name        |  String    | 100            | |
|  1          | TVT Manifest Line V2    | Name 2       |  String    | 50            | |
|  1          | TVT Manifest Line V2    | From Post Code         |  Code    | 20            | |
|  1          | TVT Manifest Line V2    | System Created At | DateTime |  |  |
|  1          | TVT Manifest Line V2    | System Created By  | String |  |  |
|  1          | TVT Manifest Line V2    | System Modified At | DateTime |  |  |
|  1          | TVT Manifest Line V2    | System Modified By | String |  |  |

