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

### Customer Fields

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Customer | No. | string | 20 | Primary Key (Required for Update) |
| 1 | Customer | Web Id | string | 20 | Web Site Id |
| 1 | Customer | Web Last Mod Date Time | datetime |  | Last Update Date Time  |
| 1 | Customer | Name | string | 100 |  |
| 1 | Customer | Blocked | option |  |  |
| 1 | Customer | Address | string | 100 |  |
| 1 | Customer | Address 2 | string | 50 |  |
| 1 | Customer | City | string | 30 |  |
| 1 | Customer | County | string | 30 |  |
| 1 | Customer | Post Code | string | 20 |  |
| 1 | Customer | Country/Region Code | string | 10 |  |
| 1 | Customer | Contact | string | 100 |  |
| 1 | Customer | Phone No. | string | 30 |  |
| 1 | Customer | E-Mail | string | 80 |  |
| 1 | Customer | Language Code | string | 10 |  |
| 1 | Customer | Currency Code | string | 10 |  |
| 1 | Customer | Shipment Method Code | string | 10 |  |
| 1 | Customer | Shipping Agent Code | string | 10 |  |
| 1 | Customer | Shipping Agent Service Code | string | 10 |  |
| 1 | Customer | Location Code | string | 10 |  |
| 1 | Customer | VAT Registration No. | string | 20 |  |
| 1 | Customer | Payment Terms Code | string | 10 |  |
| 1 | Customer | Payment Method Code | string | 10 |  |
| 1 | Customer | GLN | string | 13 |  |
| 1 | Customer | Gen. Bus. Posting Group | string | 20 |  |
| 1 | Customer | VAT Bus. Posting Group | string | 20 |  |
| 1 | Customer | Customer Posting Group | string | 20 |  |
| 1 | Customer | Customer Price Group | string | 20 |  |
| 1 | Customer | Customer Disc. Group | string | 20 |  |
| 1 | Customer | AWRS No. | string | 20 |  |
| 1 | Customer | Territory Code | string | 10 |  |
| 1 | Customer | Global Dimension 1 Code | string | 20 |  |
| 1 | Customer | Global Dimension 2 Code | string | 20 |  |
| 1 | Customer | Balance | decimal |  |  |
| 1 | Customer | Balance_LCY | decimal |  |  |
| 1 | Customer | Balance Due | decimal |  |  |
| 1 | Customer | System Id | GUID |  |  (Required for Update) |
| 1 | Customer | System Created At | DateTime |  |  |
| 1 | Customer | System Created By  | String |  |  |
| 1 | Customer | System Modified At | DateTime |  |  |
| 1 | Customer | System Modified By | String |  |  |
