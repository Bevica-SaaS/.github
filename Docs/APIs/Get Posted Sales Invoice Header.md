## GET Posted Sales Invoices

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/PostedSalesInvoices
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/PostedSalesInvoices",
    "value": [
        {
            "@odata.etag": "W/\"JzE5OzgzMzg2MTE5Njg1ODY5MzMwNjIxOzAwOyc=\"",
            "systemId": "667fdb40-a686-ed11-9989-6045bd0d0c6b",
            "sellToCustomerNo": "1020000",
            "sellToAddress": "153 Thomas Drive",
            "sellToAddress2": "",
            "sellToCity": "",
            "sellToPostCode": "KY16 1GY",
            "sellToCounty": "Fife",
            "sellToCountryRegionCode": "GB",
            "billToCustomerNo": "1020000",
            "billToName": "The Pickled Egg Pub",
            "billToName2": "",
            "billToAddress": "153 Thomas Drive",
            "billToAddress2": "",
            "billToCity": "",
            "billToPostCode": "KY16 1GY",
            "billToCounty": "Fife",
            "billToCountryRegionCode": "GB",
            "no": "SI000001",
            "yourReference": "BJSSWKAC",
            "shipToCode": "",
            "shipToName": "The Pickled Egg Pub",
            "shipToName2": "",
            "shipToAddress": "153 Thomas Drive",
            "shipToAddress2": "",
            "shipToCity": "",
            "shipToContact": "Mr. Mark McArthur",
            "postingDate": "2021-01-04",
            "shipmentDate": "2021-01-04",
            "shipmentMethodCode": "EXW",
            "locationCode": "BLUE",
            "currencyCode": "",
            "salespersonCode": "JR",
            "orderNo": "SO000001",
            "amount": 6980.04,
            "amountIncludingVAT": 8376.05,
            "sellToCustomerName": "The Pickled Egg Pub",
            "shipToPostCode": "KY16 1GY",
            "shipToCounty": "Fife",
            "shipToCountryRegionCode": "GB",
            "externalDocumentNo": "BJSSWKAC",
            "tvtDutyStatus": "DUTY PAID",
            "tvtSalesDocumentType": "NORMAL",
            "paymentTermsCode": "30D",
            "custLedgerEntryNo": 2514,
            "closed": false
        },
        {
            "@odata.etag": "W/\"JzE3Ozg4NjQzNzkzNjg3NjcwMzU5MTswMDsn\"",
            "systemId": "2e84e446-a686-ed11-9989-6045bd0d0c6b",
            "sellToCustomerNo": "1044180220",
            "sellToAddress": "100 Maidstone Ave.",
            "sellToAddress2": "",
            "sellToCity": "Maidstone",
            "sellToPostCode": "ME5 6RL",
            "sellToCounty": "",
            "sellToCountryRegionCode": "GB",
            "billToCustomerNo": "1044180220",
            "billToName": "London Bar & Grill",
            "billToName2": "",
            "billToAddress": "100 Maidstone Ave.",
            "billToAddress2": "",
            "billToCity": "Maidstone",
            "billToPostCode": "ME5 6RL",
            "billToCounty": "",
            "billToCountryRegionCode": "GB",
            "no": "SI000002",
            "yourReference": "KZ92D6W3",
            "shipToCode": "",
            "shipToName": "London Bar & Grill",
            "shipToName2": "",
            "shipToAddress": "100 Maidstone Ave.",
            "shipToAddress2": "",
            "shipToCity": "Maidstone",
            "shipToContact": "Mrs. Ariane Peeters",
            "postingDate": "2020-01-08",
            "shipmentDate": "2020-01-08",
            "shipmentMethodCode": "EXW",
            "locationCode": "BLUE",
            "currencyCode": "",
            "salespersonCode": "DC",
            "orderNo": "SO000002",
            "amount": 8262.42,
            "amountIncludingVAT": 9914.9,
            "sellToCustomerName": "London Bar & Grill",
            "shipToPostCode": "ME5 6RL",
            "shipToCounty": "",
            "shipToCountryRegionCode": "GB",
            "externalDocumentNo": "KZ92D6W3",
            "tvtDutyStatus": "DUTY PAID",
            "tvtSalesDocumentType": "NORMAL"
        }
   ]
}

```

### Field Information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Sales Invoice Header | System Id | GUID |  |  |
| 1 | Sales Invoice Header | Sell-to Customer No. | String | 20 |  |
| 1 | Sales Invoice Header | Sell-to Name | String | 35 |  |
| 1 | Sales Invoice Header | Sell-to Name 2 | String | 50 |  |
| 1 | Sales Invoice Header | Sell-to Address | String | 50  |   |
| 1 | Sales Invoice Header | Sell-to Address 2 | String | 50 |  |
| 1 | Sales Invoice Header | Sell-to City | String | 30 |  |
| 1 | Sales Invoice Header | Sell-to Post Code | String | 20  |  |
| 1 | Sales Invoice Header | Sell-to County | String | 30  |  |
| 1 | Sales Invoice Header | Sell-to Country/Region Code | String | 30  |  |
| 1 | Sales Invoice Header | No. | String | 20 | |
| 1 | Sales Invoice Header | Bill-to Customer No. | String | 20 |  |
| 1 | Sales Invoice Header | Bill-to Name | String | 35 |  |
| 1 | Sales Invoice Header | Bill-to Name 2 | String | 50 |  |
| 1 | Sales Invoice Header | Bill-to Address | String | 50  |   |
| 1 | Sales Invoice Header | Bill-to Address 2 | String | 50 |  |
| 1 | Sales Invoice Header | Bill-to City | String | 30 |  |
| 1 | Sales Invoice Header | Bill-to Post Code | String | 20  |  |
| 1 | Sales Invoice Header | Bill-to County | String | 30  |  |
| 1 | Sales Invoice Header | Bill-to Country/Region Code | String | 30  |  |
| 1 | Sales Invoice Header | Your Reference | 35 |  |  |
| 1 | Sales Invoice Header | Ship-to Code | String |  |  |
| 1 | Sales Invoice Header | Ship-to Name | String | 35 |  |
| 1 | Sales Invoice Header | Ship-to Name 2 | String | 50 |  |
| 1 | Sales Invoice Header | Ship-to Address | String | 50  |   |
| 1 | Sales Invoice Header | Ship-to Address 2 | String | 50 |  |
| 1 | Sales Invoice Header | Ship-to City | String | 30 |  |
| 1 | Sales Invoice Header | Ship-to Contact | String | 20 |  |
| 1 | Sales Invoice Header | Posting Date | Date |  |  |
| 1 | Sales Invoice Header | Shipment Date | Date |  |  |
| 1 | Sales Invoice Header | Shipment Method Code | String | 20 | |
| 1 | Sales Invoice Header | Location Code | String | 10 |  |
| 1 | Sales Invoice Header | Salesperson Code | String | 20 |  |
| 1 | Sales Invoice Header | Order No. | String | 20 |  |
| 1 | Sales Invoice Header | Amount | Decimal |   |  |
| 1 | Sales Invoice Header | Amount Including VAT | Decimal |   |  
| 1 | Sales Invoice Header | Sell-to Customer Name | String | 100  |  |
| 1 | Sales Invoice Header | Ship-to Post Code | String | 20  |  |
| 1 | Sales Invoice Header | Ship-to County | String | 30  |  |
| 1 | Sales Invoice Header | Ship-to Country/Region Code | String | 30  |  |
| 1 | Sales Invoice Header | External Document No. | String | 35 |  |
| 1 | Sales Invoice Header | Duty Status | Code | 20  |  |
| 1 | Sales Invoice Header | Sales Document Type| String | 20 |  |
| 1 | Sales Invoice Header | Payment Terms| String | 20 |  |
| 1 | Sales Invoice Header | Customer Ledger Entry No. | Integer | 20 |  |
| 1 | Sales Invoice Header | Closed| Boolean | |  |

