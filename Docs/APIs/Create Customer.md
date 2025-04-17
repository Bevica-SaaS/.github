## Create Customer

Retrieve the properties and relationships of a Web Order object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
POST

businesscentralPrefix/customersEdit
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Here is an example of the request

```json

{
    "no": "",
    "name": "Postman Customer"    
}
```

### Response

Here is an example of the response

```json

{
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/customersEdit/$entity",
    "@odata.etag": "W/\"JzE5Ozc2Mzg5MzU4NjE1NTE1MTYyNzAxOzAwOyc=\"",
    "systemId": "dd03de29-711b-f011-9af4-002248432d30",
    "address": "",
    "address2": "",
    "applicationMethod": "Manual",
    "billToCustomerNo": "",
    "blocked": "_x0020_",
    "chainName": "",
    "city": "",
    "collectionMethod": "",
    "combineShipments": false,
    "contact": "",
    "contactType": "Company",
    "countryRegionCode": "",
    "county": "",
    "creditLimitLCY": 0,
    "currencyCode": "",
    "currencyId": "00000000-0000-0000-0000-000000000000",
    "customerDiscGroup": "",
    "customerPostingGroup": "",
    "customerPriceGroup": "",
    "eMail": "",
    "eoriNumber": "",
    "faxNo": "",
    "finChargeMemoAmountsLCY": 0,
    "finChargeTermsCode": "",
    "formatRegion": "",
    "gln": "",
    "genBusPostingGroup": "",
    "globalDimension1Code": "",
    "globalDimension2Code": "",
    "homePage": "",
    "icPartnerCode": "",
    "image": "00000000-0000-0000-0000-000000000000",
    "invoiceCopies": 0,
    "invoiceDiscCode": "C00150",
    "languageCode": "",
    "lastStatementNo": 0,
    "locationCode": "",
    "mobilePhoneNo": "",
    "name": "Postman Customer",
    "name2": "",
    "no": "C00150",
    "ourAccountNo": "",
    "partnerType": "_x0020_",
    "paymentMethodCode": "",
    "paymentMethodId": "00000000-0000-0000-0000-000000000000",
    "paymentTermsCode": "",
    "paymentTermsId": "00000000-0000-0000-0000-000000000000",
    "phoneNo": "",
    "placeOfExport": "",
    "postCode": "",
    "preferredBankAccountCode": "",
    "pricesIncludingVAT": false,
    "primaryContactNo": "",
    "printStatements": false,
    "privacyBlocked": false,
    "registrationNumber": "",
    "responsibilityCenter": "",
    "salespersonCode": "",
    "searchName": "POSTMAN CUSTOMER",
    "shipToCode": "",
    "shipmentMethodCode": "",
    "shipmentMethodId": "00000000-0000-0000-0000-000000000000",
    "shippingAdvice": "Partial",
    "shippingAgentCode": "",
    "shippingAgentServiceCode": "",
    "shippingTime": "",
    "systemCreatedAt": "2025-04-17T09:48:56.003Z",
    "systemCreatedBy": "fff77cf3-0f31-4147-b1ec-92eaa6f4782c",
    "systemModifiedAt": "2025-04-17T09:48:56.003Z",
    "systemModifiedBy": "fff77cf3-0f31-4147-b1ec-92eaa6f4782c",
    "tvtAWRSDate": "0001-01-01",
    "tvtAWRSURN": "",
    "tvtContraVendorNo": "",
    "tvtCreditStatus": "Open",
    "tvtwsWebId": "",
    "tvtwsWebLastModDateTime": "0001-01-01T00:00:00Z",
    "taxAreaCode": "",
    "taxAreaID": "00000000-0000-0000-0000-000000000000",
    "taxLiable": false,
    "telexAnswerBack": "",
    "telexNo": "",
    "territoryCode": "",
    "vatBusPostingGroup": "",
    "vatRegistrationNo": ""
}
```

### Field information
<details>
  <summary>Show</summary>


| Relation | Source Table | Field Caption | Field Type | Field Length | Note      | Mandatory | Required |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |--- |--- |
| 1  | Web Order Header | System ID | GUID |  |  |  |  |
| 1  | Web Order Header | Order Group | String | 50 | Key (Internal Use) |  |  |
| 1  | Web Order Header | Order Id | String | 50 | Key (Unique Web Reference) | Y | Y |
| 1  | Web Order Header | Order Type | String | 10 | Web Specific |  | Y |
| 1  | Web Order Header | Customer Email | String | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Sell-to Customer Name | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Customer Name 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Payment Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Pending Cart | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Shipping Agent Service Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Dispatched | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Paid | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Payment Terms Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Shipment Method Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Location Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 1 Code | String | 20 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 2 Code | String | 20 | Standard |  |  |
| 1  | Web Order Header | Prices Including VAT | Boolean |  | Standard |  |  |
| 1  | Web Order Header | Payment Method Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Shipping Agent Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer No. | String | 20 | Standard |  |  |
| 1  | Web Order Header | Sell-to City | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to County | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to E-Mail | String | 80 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Address | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Contact | String | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Address 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Phone No. | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Post Code | String | 20 | Standard |  | Y |
| 1  | Web Order Header | Order Date | Date |  | Standard |  | Y |
| 1  | Web Order Header | Shipment Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Currency Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Your Reference | String | 35 | Standard |  |  |
| 1  | Web Order Header | External Document No. | String | 35 | Standard |  |  |
| 1  | Web Order Header | Delivery Note Text 1 | String | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Delivery Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 1 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 1 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Ship-to Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Duty Free | Boolean | | Standard |  |  |
| 1  | Web Order Header | Ship-to Name | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Name 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to Address | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Address 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to City | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Contact | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Post Code | String | 20 | Standard |  | Y |
| 1  | Web Order Header | Ship-to County | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Country/Region Code | String | 10 | Standard |  | Y |
| 1  | Web Order Header | Order URL | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Total Order Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | System Created At | DateTime |  |  |
| 1  | Web Order Header | System Created By  | String |  |  |
| 1  | Web Order Header | System Modified At | DateTime |  |  |
| 1  | Web Order Header | System Modified By | String |  |  |


<!--
| Relation | Source Table | Field Caption | Field Type | Field Length | Note      | Mandatory | Required |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |--- |--- |
| 1  | Web Order Header | System ID | GUID |  |  |  |  |
| 1  | Web Order Header | Order Group | String | 50 | Key (Internal Use) |  |  |
| 1  | Web Order Header | Order Id | String | 50 | Key (Unique Web Reference) | Y | Y |
| 1  | Web Order Header | Order Type | String | 10 | Web Specific |  | Y |
| 1  | Web Order Header | sellToCustomerNo | String | 50 | Web Specific |  | Y |
| 1  | Web Order Header | Customer Email | String | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Sell-to Customer Name | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Customer Name 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship Address Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Payment Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Ship Method Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Pending Cart | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Payment Method Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Shipping Agent Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Shipping Agent Service Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Dispatched | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Paid | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Posting Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Posting Description | String | 50 | Standard |  |  |
| 1  | Web Order Header | Payment Terms Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Due Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Shipment Method Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Location Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 1 Code | String | 20 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 2 Code | String | 20 | Standard |  |  |
| 1  | Web Order Header | Customer Posting Group | String | 20 | Standard |  |  |
| 1  | Web Order Header | Currency Factor | Decimal |  | Standard |  |  |
| 1  | Web Order Header | Customer Price Group | String | 10 | Standard |  |  |
| 1  | Web Order Header | Prices Including VAT | Boolean |  | Standard |  |  |
| 1  | Web Order Header | Customer Disc. Group | String | 20 | Standard |  |  |
| 1  | Web Order Header | Language Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Salesperson Code | String | 20 | Standard |  |  |
| 1  | Web Order Header | Package Tracking No. | String | 30 | Standard |  |  |
| 1  | Web Order Header | VAT Bus. Posting Group | String | 20 | Standard |  |  |
| 1  | Web Order Header | VAT Registration No. | String | 20 | Standard |  |  |
| 1  | Web Order Header | Reason Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Gen. Bus. Posting Group | String | 20 | Standard |  |  |
| 1  | Web Order Header | Payment Method Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Shipping Agent Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | VAT Country/Region Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Document Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer No. | String | 20 | Standard |  |  |
| 1  | Web Order Header | Sell-to City | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to County | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to E-Mail | String | 80 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Address | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Contact | String | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Address 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Phone No. | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Post Code | String | 20 | Standard |  | Y |
| 1  | Web Order Header | Order Date | Date |  | Standard |  | Y |
| 1  | Web Order Header | Shipment Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Location Id | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Currency Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Your Reference | String | 35 | Standard |  |  |
| 1  | Web Order Header | External Document No. | String | 35 | Standard |  |  |
| 1  | Web Order Header | Delivery Note Text 1 | String | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Delivery Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 1 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 1 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Sell-to Country/Region Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer Template Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Contact No. | String | 20 | Standard |  |  |
| 1  | Web Order Header | Ship-to Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Ship-to Name | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Name 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to Address | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Address 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to City | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Contact | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Post Code | String | 20 | Standard |  | Y |
| 1  | Web Order Header | Ship-to County | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Country/Region Code | String | 10 | Standard |  | Y |
| 1  | Web Order Header | Order URL | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Total Order Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | System Created At | DateTime |  |  |
| 1  | Web Order Header | System Created By  | String |  |  |
| 1  | Web Order Header | System Modified At | DateTime |  |  |
| 1  | Web Order Header | System Modified By | String |  |  |-->

<!-- | 1  | Web Order Header | Total Tax Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Requested Delivery Date | Date |  | Standard |  | Y |
| 1  | Web Order Header | Promised Delivery Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Shipping Agent Service Code | String | 10 | Standard |  |  |
| 1  | Web Order Header | Decimal 01 | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Integer 01 | Integer |  | Web Specific |  |  |
| 1  | Web Order Header | Date 01 | Date |  | Web Specific |  |  |
| 1  | Web Order Header | Code 01 | String | 20 | Web Specific |  |  |
| 1  | Web Order Header | Time 01 | Time |  | Web Specific |  |  |
| 1  | Web Order Header | DateTime 01 | DateTime |  | Web Specific |  |  |
| 1  | Web Order Header | Text 01 | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Boolean 01 | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Decimal 02 | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Integer 02 | Integer |  | Web Specific |  |  |
| 1  | Web Order Header | Date 02 | Date |  | Web Specific |  |  |
| 1  | Web Order Header | Code 02 | String | 20 | Web Specific |  |  |
| 1  | Web Order Header | Time 02 | Time |  | Web Specific |  |  |
| 1  | Web Order Header | DateTime 02 | DateTime |  | Web Specific |  |  |
| 1  | Web Order Header | Text 02 | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Boolean 02 | Boolean |  | Web Specific |  |  | -->
