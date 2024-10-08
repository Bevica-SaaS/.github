## GET Customers

Retrieve the properties and relationships of a customer object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/Customers
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/customers",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzE3ODg0MDY5ODgwMDI3NzE2MjgyMTswMDsn\"",
            "systemId": "0536ae7f-1f0f-ed11-90eb-0022480090f7",
            "no": "21233572",
            "name": "Somadis",
            "blocked": " ",
            "address": "37, Rue El Wahda",
            "address2": "",
            "city": "AGDAL-RABAT",
            "county": "",
            "countryRegionCode": "MA",
            "postCode": "MA-10100",
            "contact": "M. Syed ABBAS",
            "phoneNo": "",
            "eMail": "",
            "homePage": "",
            "languageCode": "",
            "currencyCode": "USD",
            "shipmentMethodCode": "EXW",
            "shippingAgentCode": "",
            "shippingAgentServiceCode": "",
            "locationCode": "BLUE",
            "paymentMethodCode": "",
            "paymentTermsCode": "30 DAYS",
            "vatRegistrationNo": "",
            "vatBusPostingGroup": "EXPORT",
            "genBusPostingGroup": "EXPORT",
            "customerPostingGroup": "FOREIGN",
            "customerPriceGroup": "",
            "customerDiscGroup": "",
            "salespersonCode": "JR",
            "territoryCode": "FOREIGN",
            "tvtAWRSURN": "",
            "gln": "",
            "balance": 0,
            "balanceLCY": 0,
            "balanceDue": 0,
            "balanceDueLCY": 0,
            "globalDimension1Code": "SALES",
            "globalDimension2Code": "",
            "tvtwsWebId": "",
            "tvtwsWebLastModDateTime": "2023-02-27T15:53:10.913Z",
            "systemCreatedAt": "2022-07-29T09:19:17.213Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2023-02-27T15:53:10.913Z",
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
| 1 | Customer | No. | String | 20 | Primary Key (Required for Update) |
| 1 | Customer | Web Id | String | 20 | Web Site Id |
| 1 | Customer | Web Last Mod Date Time | DateTime |  | Last Update Date Time  |
| 1 | Customer | Name | String | 100 |  |
| 1 | Customer | Blocked | option |  |  |
| 1 | Customer | Address | String | 100 |  |
| 1 | Customer | Address 2 | String | 50 |  |
| 1 | Customer | City | String | 30 |  |
| 1 | Customer | County | String | 30 |  |
| 1 | Customer | Post Code | String | 20 |  |
| 1 | Customer | Country/Region Code | String | 10 |  |
| 1 | Customer | Contact | String | 100 |  |
| 1 | Customer | Phone No. | String | 30 |  |
| 1 | Customer | E-Mail | String | 80 |  |
| 1 | Customer | Language Code | String | 10 |  |
| 1 | Customer | Currency Code | String | 10 |  |
| 1 | Customer | Shipment Method Code | String | 10 |  |
| 1 | Customer | Shipping Agent Code | String | 10 |  |
| 1 | Customer | Shipping Agent Service Code | String | 10 |  |
| 1 | Customer | Location Code | String | 10 |  |
| 1 | Customer | VAT Registration No. | String | 20 |  |
| 1 | Customer | Payment Terms Code | String | 10 |  |
| 1 | Customer | Payment Method Code | String | 10 |  |
| 1 | Customer | GLN | String | 13 |  |
| 1 | Customer | Gen. Bus. Posting Group | String | 20 |  |
| 1 | Customer | VAT Bus. Posting Group | String | 20 |  |
| 1 | Customer | Customer Posting Group | String | 20 |  |
| 1 | Customer | Customer Price Group | String | 20 |  |
| 1 | Customer | Customer Disc. Group | String | 20 |  |
| 1 | Customer | AWRS No. | String | 20 |  |
| 1 | Customer | Territory Code | String | 10 |  |
| 1 | Customer | Global Dimension 1 Code | String | 20 |  |
| 1 | Customer | Global Dimension 2 Code | String | 20 |  |
| 1 | Customer | Balance | Decimal |  |  |
| 1 | Customer | Balance_LCY | Decimal |  |  |
| 1 | Customer | Balance Due | Decimal |  |  |
| 1 | Customer | System Id | GUID |  |  (Required for Update) |
| 1 | Customer | System Created At | DateTime |  |  |
| 1 | Customer | System Created By  | String |  |  |
| 1 | Customer | System Modified At | DateTime |  |  |
| 1 | Customer | System Modified By | String |  |  |
