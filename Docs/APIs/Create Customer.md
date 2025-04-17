## Create Customer

Retrieve the properties and relationships of a Customer object for Business Central.

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


