## GET Posted Sales Credit Memos

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/PostedSalesCrMemoInvoices
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/PostedSalesCrMemoInvoices",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzEzMTUxNjQ3NjAxMDc3MzQ1Mzk4MTswMDsn\"",
            "systemId": "ec871204-5188-ed11-9989-6045bd0d024f",
            "sellToCustomerNo": "1010000",
            "sellToAddress": "Thatcham Business Village",
            "sellToAddress2": "Colthrop Way",
            "sellToCity": "Thatcham",
            "sellToPostCode": "RG19 4LW",
            "sellToCounty": "Surrey",
            "sellToCountryRegionCode": "GB",
            "billToCustomerNo": "1010000",
            "billToName": "Asado Bar & Grill",
            "billToName2": "",
            "billToAddress": "Thatcham Business Village",
            "billToAddress2": "Colthrop Way",
            "billToCity": "Thatcham",
            "billToPostCode": "RG19 4LW",
            "billToCounty": "Surrey",
            "billToCountryRegionCode": "GB",
            "no": "SCR000001",
            "yourReference": "",
            "shipToCode": "DUDLEY",
            "shipToName": "Blue Warehouse",
            "shipToName2": "",
            "shipToAddress": "South East Street, 3",
            "shipToAddress2": "",
            "shipToCity": "Birmingham",
            "shipToContact": "Jeff Smith",
            "postingDate": "2022-12-30",
            "shipmentDate": "0001-01-01",
            "shipmentMethodCode": "",
            "locationCode": "BLUE",
            "currencyCode": "",
            "salespersonCode": "ED",
            "amount": 11,
            "amountIncludingVAT": 13.2,
            "sellToCustomerName": "Asado Bar & Grill",
            "shipToPostCode": "B27 4KT",
            "shipToCounty": "",
            "shipToCountryRegionCode": "GB",
            "externalDocumentNo": "",
            "tvtDutyStatus": "DUTY PAID",
            "tvtSalesDocumentType": ""
        },
        {
            "@odata.etag": "W/\"JzE4OzQ5MTkyODEyNzkzMzAxNzQwMjE7MDA7Jw==\"",
            "systemId": "32a9647a-e297-ed11-bff5-0022481b46da",
            "sellToCustomerNo": "1010000",
            "sellToAddress": "Thatcham Business Village",
            "sellToAddress2": "Colthrop Way",
            "sellToCity": "Thatcham",
            "sellToPostCode": "RG19 4LW",
            "sellToCounty": "Surrey",
            "sellToCountryRegionCode": "GB",
            "billToCustomerNo": "1010000",
            "billToName": "Asado Bar & Grill",
            "billToName2": "",
            "billToAddress": "Thatcham Business Village",
            "billToAddress2": "Colthrop Way",
            "billToCity": "Thatcham",
            "billToPostCode": "RG19 4LW",
            "billToCounty": "Surrey",
            "billToCountryRegionCode": "GB",
            "no": "SCR000002",
            "yourReference": "",
            "shipToCode": "DUDLEY",
            "shipToName": "Blue Warehouse",
            "shipToName2": "",
            "shipToAddress": "South East Street, 3",
            "shipToAddress2": "",
            "shipToCity": "Birmingham",
            "shipToContact": "Jeff Smith",
            "postingDate": "2023-01-19",
            "shipmentDate": "0001-01-01",
            "shipmentMethodCode": "",
            "locationCode": "BLUE",
            "currencyCode": "",
            "salespersonCode": "ED",
            "amount": 100,
            "amountIncludingVAT": 120,
            "sellToCustomerName": "Asado Bar & Grill",
            "shipToPostCode": "B27 4KT",
            "shipToCounty": "",
            "shipToCountryRegionCode": "GB",
            "externalDocumentNo": "",
            "tvtDutyStatus": "DUTY PAID",
            "tvtSalesDocumentType": ""
        }
    ]
}

```

### Field Information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Sales Cr.Memo Header | System Id | GUID |  |  |
| 1 | Sales Cr.Memo Header | Sell-to Customer No. | String | 20 |  |
| 1 | Sales Cr.Memo Header | Sell-to Name | String | 35 |  |
| 1 | Sales Cr.Memo Header | Sell-to Name 2 | String | 50 |  |
| 1 | Sales Cr.Memo Header | Sell-to Address | String | 50  |   |
| 1 | Sales Cr.Memo Header | Sell-to Address 2 | String | 50 |  |
| 1 | Sales Cr.Memo Header | Sell-to City | String | 30 |  |
| 1 | Sales Cr.Memo Header | Sell-to Post Code | String | 20  |  |
| 1 | Sales Cr.Memo Header | Sell-to County | String | 30  |  |
| 1 | Sales Cr.Memo Header | Sell-to Country/Region Code | String | 30  |  |
| 1 | Sales Cr.Memo Header | Bill-to Customer No. | String | 20 |  |
| 1 | Sales Cr.Memo Header | Bill-to Name | String | 35 |  |
| 1 | Sales Cr.Memo Header | Bill-to Name 2 | String | 50 |  |
| 1 | Sales Cr.Memo Header | Bill-to Address | String | 50  |   |
| 1 | Sales Cr.Memo Header | Bill-to Address 2 | String | 50 |  |
| 1 | Sales Cr.Memo Header | Bill-to City | String | 30 |  |
| 1 | Sales Cr.Memo Header | Bill-to Post Code | String | 20  |  |
| 1 | Sales Cr.Memo Header | Bill-to County | String | 30  |  |
| 1 | Sales Cr.Memo Header | Bill-to Country/Region Code | String | 30  |  |
| 1 | Sales Cr.Memo Header | No. | String | 20 | |
| 1 | Sales Cr.Memo Header | Your Reference | 35 |  |  |
| 1 | Sales Cr.Memo Header | Ship-to Code | String |  |  |
| 1 | Sales Cr.Memo Header | Ship-to Name | String | 35 |  |
| 1 | Sales Cr.Memo Header | Ship-to Name 2 | String | 50 |  |
| 1 | Sales Cr.Memo Header | Ship-to Address | String | 50  |   |
| 1 | Sales Cr.Memo Header | Ship-to Address 2 | String | 50 |  |
| 1 | Sales Cr.Memo Header | Ship-to City | String | 30 |  |
| 1 | Sales Cr.Memo Header | Ship-to Contact | String | 20 |  |
| 1 | Sales Cr.Memo Header | Posting Date | Date |  |  |
| 1 | Sales Cr.Memo Header | Shipment Date | Date |  |  |
| 1 | Sales Cr.Memo Header | Shipment Method Code | String | 20 | |
| 1 | Sales Cr.Memo Header | Location Code | String | 10 |  |
| 1 | Sales Cr.Memo Header | Salesperson Code | String | 20 |  |
| 1 | Sales Cr.Memo Header | Amount | Decimal |   |  |
| 1 | Sales Cr.Memo Header | Amount Including VAT | Decimal | Boolean  |  |
| 1 | Sales Cr.Memo Header | Sell-to Customer Name | String | 100  |  |
| 1 | Sales Cr.Memo Header | Ship-to Post Code | String | 20  |  |
| 1 | Sales Cr.Memo Header | Ship-to County | String | 30  |  |
| 1 | Sales Cr.Memo Header | Ship-to Country/Region Code | String | 30 |  |
| 1 | Sales Cr.Memo Header | External Document No. | 35 |   |  
| 1 | Sales Cr.Memo Header | Duty Status | Code | 20 |  |
| 1 | Sales Cr.Memo Header | Sales Document Type| String | 20 |  |
