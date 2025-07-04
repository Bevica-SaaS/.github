## GET Sales Documents

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/SalesDocuments
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/salesDocuments",
    "value": [
        {
            "@odata.etag": "W/\"JzE5Ozk5NTkxOTIyMTE0Njg3Mjg1MjQxOzAwOyc=\"",
            "systemId": "6b6a1e0a-a486-ed11-9989-6045bd0d0c6b",
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
            "documentType": "Quote",
            "no": "SQ000001",
            "yourReference": "",
            "shipToCode": "",
            "shipToName": "The Pickled Egg Pub",
            "shipToName2": "",
            "shipToAddress": "153 Thomas Drive",
            "shipToAddress2": "",
            "shipToCity": "",
            "shipToContact": "Mr. Mark McArthur",
            "postingDate": "2022-01-04",
            "shipmentDate": "2022-01-04",
            "shipmentMethodCode": "EXW",
            "locationCode": "BLUE",
            "currencyCode": "",
            "salespersonCode": "JR",
            "amount": 1230.84,
            "amountIncludingVAT": 1477.01,
            "sellToCustomerName": "The Pickled Egg Pub",
            "shipToPostCode": "KY16 1GY",
            "shipToCounty": "Fife",
            "shipToCountryRegionCode": "GB",
            "externalDocumentNo": "",
            "tvtDutyStatus": "DUTY PAID",
            "tvtSalesDocumentType": "NORMAL",
            "paymentTermsCode": "14 DAYS",
            "requestedDeliveryDate": "0001-01-01",
            "duedate": "2022-01-18",
            "tvtCreditStatus": "Open",
            "tvtOrderSource": "",
            "pricesIncludingVAT": false,
            "shippingAgentCode": "DHL",
            "shippingAgentServiceCode": "OVERNIGHT",
            "billtoContact": "Mr. Mark McArthur",
            "selltoContact": "Mr. Mark McArthur",
            "selltoPhoneNo": "",
            "shiptoPhoneNo": "",
            "selltoEmail": ""
        },
        {
            "@odata.etag": "W/\"JzIwOzE3ODkzMDM3NTM0MTI1Mzc3NjUzMTswMDsn\"",
            "systemId": "6d6a1e0a-a486-ed11-9989-6045bd0d0c6b",
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
            "documentType": "Quote",
            "no": "SQ000002",
            "yourReference": "",
            "shipToCode": "",
            "shipToName": "London Bar & Grill",
            "shipToName2": "",
            "shipToAddress": "100 Maidstone Ave.",
            "shipToAddress2": "",
            "shipToCity": "Maidstone",
            "shipToContact": "Mrs. Ariane Peeters",
            "postingDate": "2022-01-08",
            "shipmentDate": "2022-01-08",
            "shipmentMethodCode": "EXW",
            "locationCode": "BLUE",
            "currencyCode": "",
            "salespersonCode": "DC",
            "amount": 1749.12,
            "amountIncludingVAT": 2098.94,
            "sellToCustomerName": "London Bar & Grill",
            "shipToPostCode": "ME5 6RL",
            "shipToCounty": "",
            "shipToCountryRegionCode": "GB",
            "externalDocumentNo": "",
            "tvtDutyStatus": "DUTY PAID",
            "tvtSalesDocumentType": "NORMAL",
            "paymentTermsCode": "30 DAYS",
            "requestedDeliveryDate": "0001-01-01",
            "duedate": "2022-02-07",
            "tvtCreditStatus": "Open",
            "tvtOrderSource": "",
            "pricesIncludingVAT": false,
            "shippingAgentCode": "UPS",
            "shippingAgentServiceCode": "",
            "billtoContact": "Mrs. Ariane Peeters",
            "selltoContact": "Mrs. Ariane Peeters",
            "selltoPhoneNo": "",
            "shiptoPhoneNo": "",
            "selltoEmail": ""
        }
    ]
}

```

### Field information
<details>
  <summary>Show</summary>


| Field Name                | Caption                     | Source Field                  |
|-------------------------- |----------------------------|-------------------------------|
| systemId                  | SystemId                    | SystemId                      |
| sellToCustomerNo          | Sell-to Customer No.        | Sell-to Customer No.          |
| sellToAddress             | Sell-to Address             | Sell-to Address               |
| sellToAddress2            | Sell-to Address 2           | Sell-to Address 2             |
| sellToCity                | Sell-to City                | Sell-to City                  |
| sellToPostCode            | Sell-to Post Code           | Sell-to Post Code             |
| sellToCounty              | Sell-to County              | Sell-to County                |
| sellToCountryRegionCode   | Sell-to Country/Region Code | Sell-to Country/Region Code   |
| billToCustomerNo          | Bill-to Customer No.        | Bill-to Customer No.          |
| billToName                | Bill-to Name                | Bill-to Name                  |
| billToName2               | Bill-to Name 2              | Bill-to Name 2                |
| billToAddress             | Bill-to Address             | Bill-to Address               |
| billToAddress2            | Bill-to Address 2           | Bill-to Address 2             |
| billToCity                | Bill-to City                | Bill-to City                  |
| billToPostCode            | Bill-to Post Code           | Bill-to Post Code             |
| billToCounty              | Bill-to County              | Bill-to County                |
| billToCountryRegionCode   | Bill-to Country/Region Code | Bill-to Country/Region Code   |
| documentType              | Document Type               | Document Type                 |
| no                        | No.                         | No.                           |
| yourReference             | Your Reference              | Your Reference                |
| shipToCode                | Ship-to Code                | Ship-to Code                  |
| shipToName                | Ship-to Name                | Ship-to Name                  |
| shipToName2               | Ship-to Name 2              | Ship-to Name 2                |
| shipToAddress             | Ship-to Address             | Ship-to Address               |
| shipToAddress2            | Ship-to Address 2           | Ship-to Address 2             |
| shipToCity                | Ship-to City                | Ship-to City                  |
| shipToContact             | Ship-to Contact             | Ship-to Contact               |
| postingDate               | Posting Date                | Posting Date                  |
| shipmentDate              | Shipment Date               | Shipment Date                 |
| shipmentMethodCode        | Shipment Method Code        | Shipment Method Code          |
| locationCode              | Location Code               | Location Code                 |
| currencyCode              | Currency Code               | Currency Code                 |
| salespersonCode           | Salesperson Code            | Salesperson Code              |
| amount                    | Amount                      | Amount                        |
| amountIncludingVAT        | Amount Including VAT        | Amount Including VAT          |
| sellToCustomerName        | Sell-to Customer Name       | Sell-to Customer Name         |
| shipToPostCode            | Ship-to Post Code           | Ship-to Post Code             |
| shipToCounty              | Ship-to County              | Ship-to County                |
| shipToCountryRegionCode   | Ship-to Country/Region Code | Ship-to Country/Region Code   |
| externalDocumentNo        | External Document No.       | External Document No.         |
| tvtDutyStatus             | Duty Status                 | TVT Duty Status               |
| tvtSalesDocumentType      | Sales Document Type         | TVT Sales Document Type       |
| paymentTermsCode          | Payment Terms Code          | Payment Terms Code            |
| requestedDeliveryDate     | Requested Delivery Date     | Requested Delivery Date       |
| duedate                   | Due Date                    | Due Date                      |
| tvtCreditStatus           | CreditStatus                | TVT Credit Status             |
| tvtOrderSource            | Order Source                | TVT Order Source              |
| pricesIncludingVAT        | Prices Including VATe       | Prices Including VAT          |
| shippingAgentCode         | Shipping Agent Code         | Shipping Agent Code           |
| shippingAgentServiceCode  | Shipping Agent Service Code | Shipping Agent Service Code   |
| billtoContact             | Bill-to Contact             | Bill-to Contact               |
| selltoContact             | Sell-to Contact             | Sell-to Contact               |
| selltoPhoneNo             | Sell-to Phone No.           | Sell-to Phone No.             |
| shiptoPhoneNo             | Ship-to Phone No.           | Ship-to Phone No.             |
| selltoEmail               | Sell-to E-Mail              | Sell-to E-Mail                |


## Subpages

- **salesLines**: [TVTWS API Sales Lines](#)  
  - Entity Name: salesDocumentLine  
  - Entity Set Name: salesDocumentLines  
  - Multiplicity: Many  
  - SubPageLink: "Document Type" = field("Document Type"), "Document No." = field("No.")

---

**Source:** [`src/API/v2.0/APISalesDocument.Page.al`](src/API/v2.0/APISalesDocument.Page.al)
