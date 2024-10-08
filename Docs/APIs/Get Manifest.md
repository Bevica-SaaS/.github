## GET Manifest

Retrieve the properties and relationships of a Manifest object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/manifests
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/manifests",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzExMzM2NDcyMjcxNjA4NTMxNTM3MTswMDsn\"",
            "systemId": "4879745a-20ca-ed11-a7c9-00224800e466",
            "no": "DMAN000001",
            "address": "",
            "address2": "",
            "addressCode": "",
            "city": "",
            "contact": "",
            "countryRegionCode": "",
            "totalNetWeight": 0,
            "totalGrossWeight": 0,
            "totalEqCasesToMove": 0.5,
            "status": "Open",
            "shippingAgentCode": "DHL",
            "shipmentMethodCode": "CIF",
            "manifestType": "Purchase",
            "description": "Test ",
            "county": "",
            "documentDate": "2023-03-15",
            "finalDeliveryType": "Order Address",
            "locationCode": "BLUE",
            "logisticsDate": "0001-01-01",
            "logisticsReference": "",
            "logisticsStatus": "",
            "noLines": 1,
            "postCode": "",
            "primaryVendorNo": "",
            "primaryVendorName": "",
            "shippingAgentServiceCode": "",
            "type": "Inbound",
            "systemCreatedAt": "2023-03-24T08:46:32.963Z",
            "systemCreatedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00",
            "systemModifiedAt": "2023-03-24T08:47:11.863Z",
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
|  1          | TVT Manifest Header V2    | System Id | GUID |  |  |
|  1          | TVT Manifest Header V2    | No.         |  Code    | 20           | |
|  1          | TVT Manifest Header V2    | Address         |  String    | 100           | |
|  1          | TVT Manifest Header V2    | Address 2         |  String    | 50           | |
|  1          | TVT Manifest Header V2    | Address Code         |  Code    | 10            | |
|  1          | TVT Manifest Header V2    | City         |  String    | 30           | |
|  1          | TVT Manifest Header V2    | Contact         |  String    | 100            | |
|  1          | TVT Manifest Header V2    | Post Code         |  String    | 20            | |
|  1          | TVT Manifest Header V2    | Country/Region Code         |  Date    |            | |
|  1          | TVT Manifest Header V2    | Status         |  Code | 20            | |
|  1          | TVT Manifest Header V2    | Total Net Weight         |  Decimal    |            | |
|  1          | TVT Manifest Header V2    | Total Gross Weight         |  Decimal    |            | |
|  1          | TVT Manifest Header V2    | Total Eq. Cases to Move      |  Decimal    |            | |
|  1          | TVT Manifest Header V2    | Shipping Agent Code      |  Code    | 10            | |
|  1          | TVT Manifest Header V2    | Shipment Method Code        |  String    | 30           | |
|  1          | TVT Manifest Header V2    | Manifest Type         |   Enum  |             | |
|  1          | TVT Manifest Header V2    | Description         |  String    |  100         | |
|  1          | TVT Manifest Header V2    | County       |  String    | 30           | |
|  1          | TVT Manifest Header V2    | Document Date         |  Date    |            | |
|  1          | TVT Manifest Header V2    | Final Delivery Type        |  Enum    | 50           | |
|  1          | TVT Manifest Header V2    | Location Code      |  Code    | 20            | |
|  1          | TVT Manifest Header V2    | Logistics Date         |  Date    | 30           | |
|  1          | TVT Manifest Header V2    | Logistics Reference         |  String    | 100            | |
|  1          | TVT Manifest Header V2    | Logistics Status        |  Code    |   10         | |
|  1          | TVT Manifest Header V2    | No. Lines         |  Integer    |            | |
|  1          | TVT Manifest Header V2    | Primary Vendor No.         |  Code    | 20           | |
|  1          | TVT Manifest Header V2    | Primary Vendor Name        |  String    | 50           | |
|  1          | TVT Manifest Header V2    | Shipping Agent Service Code'        |  Code    | 10            | |
|  1          | TVT Manifest Header V2    | Type         |  Option    | 30           | |
|  1          | TVT Manifest Header V2    | System Created At | DateTime |  |  |
|  1          | TVT Manifest Header V2    | System Created By  | String |  |  |
|  1          | TVT Manifest Header V2    | System Modified At | DateTime |  |  |
|  1          | TVT Manifest Header V2    | System Modified By | String |  |  |