## GET Ship To Address

Retrieve the properties and relationships of a customer object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/ShipToAddresses
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/ShipToAddresses",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzE1NDE5MTg2OTI5MjUxNDc5OTYzMTswMDsn\"",
            "systemId": "bfa77dc7-b6b6-ed11-9a88-000d3a86b91d",
            "customerNo": "21233572",
            "code": "DFREE",
            "name": "Somadis",
            "name2": "",
            "address": "37, Rue El Wahda",
            "address2": "",
            "city": "AGDAL-RABAT",
            "contact": "M. Syed ABBAS",
            "phoneNo": "",
            "shipmentMethodCode": "",
            "shippingAgentCode": "",
            "countryRegionCode": "MA",
            "postCode": "MA-10100",
            "county": "",
            "eMail": "",
            "shippingAgentServiceCode": "",
            "serviceZoneCode": "",
            "tvtDutyStatus": "DUTY FREE",
            "systemCreatedAt": "2023-02-27T15:52:47.587Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2023-02-27T15:53:10.883Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b"
        }
    ]
}    
```

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Ship-to Address | Customer No. | Code | 20 | |
| 1 | Ship-to Address | Code | Code | 10 | |
| 1 | Ship-to Address | Name | String | 100 | |
| 1 | Ship-to Address | Name 2 | String | 50 | |
| 1 | Ship-to Address | Address | String | 100 | |
| 1 | Ship-to Address | Address 2 | String | 50 | |
| 1 | Ship-to Address | City | String | 30 | |
| 1 | Ship-to Address | Contact | String | 100 | |
| 1 | Ship-to Address | Phone No. | String | 30 |  |
| 1 | Ship-to Address | Shipment Method Code | String | 10 |  |
| 1 | Ship-to Address | Shipping Agent Code | String | 10 |  |
| 1 | Ship-to Address | Country/Region Code | String | 10 |  |
| 1 | Ship-to Address | Post Code | String | 20 |  |
| 1 | Ship-to Address | County | String | 30 |  |
| 1 | Ship-to Address | E-Mail | String | 80 |  |
| 1 | Ship-to Address | Shipping Agent Service Code | String | 10 |  |
| 1 | Ship-to Address | Service Zone Code | String | 10 |  |
| 1 | Ship-to Address | TVT Duty Status | 10 |  |
| 1 | Ship-to Address | System Id | GUID |  |   |
| 1 | Ship-to Address | System Created At | DateTime |  |  |
| 1 | Ship-to Address | System Created By  | String |  |  |
| 1 | Ship-to Address | System Modified At | DateTime |  |  |
| 1 | Ship-to Address | System Modified By | String |  |  |

