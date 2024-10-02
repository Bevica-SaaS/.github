# Bevica Web Integration 2.0 (Rest APIs)


## Introduction

The Bevica APIs documented below outline the interactions available to a third party to integrate a Bevica into their platform.
 The  request can be used independently of one another or together to create a complete workflow.

All of our endpoints are secured so before you can begin to make calls to the API you will first need to obtain an access token.

For more information on the business workflows that the APIs support, head to the [Guides](https://tvisiontech.freshdesk.com/) section.

If you have any questions or feedback on the API reference, please reach out to our support.

## APIs

RESTful web services are typically created to interchange data between Business Central and external systems. The acronym REST stands for REpresentational State Transfer. Any coding language capable of calling REST APIs can be used to use this feature. The Business Central API stack have been optimized for performance and is the preferred way to integrate with Business Central.

Business Central comes with an extensive list of built-in APIs that requires no code and minimal setup to use. When using the built-in APIs, please choose the highest API version available. You can also develop your own custom APIs using the AL object types API pages and API queries.

The articles in this section describe the key concepts and techniques for using APIs with Business Central.

[API(v2.0) MS Docs](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/api-reference/v2.0/)

## Main Entities

| Name | Description | Data Flow | Operations | Note|
| ----------- | ----------- | ----------- | -------- | ---------- |
| [Customer](#get-customers) | Customer Info| BC -> Web | Read | |
| [Ship To Address](#get-Ship-To-Address) | List of Customers Ship to Addresses | BC -> Web | Read | |
| [Customer Ledger Entries](#get-customer-ledger-entries) | Customer Ledger Entries | BC -> Web | Read | | 
| [Product](#get-products) | Items and Attributes | BC -> Web | Read | |
| [Stock](#get-stock) | Stock Available  | BC -> Web | Read | |
| [Web Order](#create-web-order) | Create Web Order BC | Web->BC    | Read Create | |
| [Web Order Lines](#create-web-order-lines) | Create Web Order Lines in BC | Web->BC    | Read Create | |
| [Payments](#create-payment) | Create Payment on Paym. Journal in BC | Web->BC | Create | |
| [Manifest](#get-manifest) | Shipping Manifest Status | BC -> Web | Read | |
| [Manifest Lines](#get-manifest-lines) | List of Manifest Lines | BC -> Web | Read | |
| [Orders Status](#get-orders-status) | List of Orders with Tracking updates | BC -> Web | Read | |
| [Sales Prices](#get-sales-prices) | Plain List of Sales Prices| BC -> Web | Read | |
| [Paid Reserve](#get-paid-reserve) | List of Paid Reserve Information| BC -> Web | Read | |
| [Paid Reserve Entries](#get-paid-reserve-entries) | List of all Paid Reserve Entries| BC -> Web | Read | |

## Endpoints businesscentralPrefix structure

Common endpoint service

~~~ api
https://api.businesscentral.dynamics.com/v2.0/<user domain name>/api/<API publisher>/<API group>/<API version>/companies(<company id>)/Customer
~~~

Sample

~~~ api
https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/Customer
~~~

## Endpoints businesscentralPrefix structure



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
| 1 | Customer | No. | string | 20 | Primaty Key (Required for Update) |
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



## GET Ship To Address

Retrieve the properties and relationships of a customer object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/shiptoAddresses
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/shiptoAddresses",
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

### Ship to Address Fields

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
| 1 | Ship-to Address | Phone No. | string | 30 |  |
| 1 | Ship-to Address | Shipment Method Code | string | 10 |  |
| 1 | Ship-to Address | Shipping Agent Code | string | 10 |  |
| 1 | Ship-to Address | Country/Region Code | string | 10 |  |
| 1 | Ship-to Address | Post Code | string | 20 |  |
| 1 | Ship-to Address | County | string | 30 |  |
| 1 | Ship-to Address | E-Mail | string | 80 |  |
| 1 | Ship-to Address | Shipping Agent Service Code | string | 10 |  |
| 1 | Ship-to Address | Service Zone Code | string | 10 |  |
| 1 | Ship-to Address | Shipping Agent Service Code | TVT Duty Status | 10 |  |
| 1 | Ship-to Address | System Id | GUID |  |   |
| 1 | Ship-to Address | System Created At | DateTime |  |  |
| 1 | Ship-to Address | System Created By  | String |  |  |
| 1 | Ship-to Address | System Modified At | DateTime |  |  |
| 1 | Ship-to Address | System Modified By | String |  |  |


## GET Customer Ledger Entries

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/custEntries
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

 "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/custEntries",
    "value": [
        {
            "@odata.etag": "W/\"JzE5OzQ3OTMzNjQ4MDI3MDkxMjY3MjMxOzAwOyc=\"",
            "systemId": "c9c0ed7c-f1c3-ed11-9a88-000d3a86b26a",
            "documentType": "Invoice",
            "documentNo": "SI100010",
            "documentDate": "2022-01-09",
            "dueDate": "2022-01-23",
            "externalDocumentNo": "HPGH92MD",
            "entryNo": 8066,
            "description": "Order SO001006",
            "open": true,
            "positive": true,
            "amountLCY": 6044.05,
            "currencyCode": "EUR",
            "originalAmount": 6708.9,
            "remainingAmount": 6708.9,
            "remainingAmtLCY": 6044.05,
            "customerNo": "1050000",
            "customerName": "Caves Des Sommelier",
            "systemCreatedAt": "2023-03-16T11:55:49.68Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2023-03-16T11:55:49.68Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b"
        },
}
```

### Fields Information

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Customer Ledger Entry | System Id | GUID |  |  (Required for Update) |
| 1 | Customer Ledger Entry | Document Type | string | 20 |  |
| 1 | Customer Ledger Entry | Document No. | Code |  | |
| 1 | Customer Ledger Entry | Due Date | Date |  |  |
| 1 | Customer Ledger Entry | External Document No. | string | 35 |  |
| 1 | Customer Ledger Entry | Entry No | Integer |  |  |
| 1 | Customer Ledger Entry | Description | String | 100  |   |
| 1 | Customer Ledger Entry | Open | Boolean |  |  |
| 1 | Customer Ledger Entry | Positive | Boolean |  |  |
| 1 | Customer Ledger Entry | Amount (LCY) | Decimal |  |  |
| 1 | Customer Ledger Entry | Currency Code | Code | 10 |  |
| 1 | Customer Ledger Entry | Original Amount | Decimal |  |  |
| 1 | Customer Ledger Entry | Remaining Amount | Decimal |  | |
| 1 | Customer Ledger Entry | Remaining Amount LCY | Decimal |  |  |
| 1 | Customer Ledger Entry | Customer No | code | 20 |  |
| 1 | Customer Ledger Entry | Customer Name | string | 100  |  |
| 1 | Customer Ledger Entry | System Created At | DateTime |  |  |
| 1 | Customer Ledger Entry | System Created By  | String |  |  |
| 1 | Customer Ledger Entry | System Modified At | DateTime |  |  |
| 1 | Customer Ledger Entry | System Modified By | String |  |  |



## GET Products

Retrieve the properties and relationships of a Item object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/webProducts
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/webProducts",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzE3MTA5ODI1MzE5NDM5NTUzMDUxMTswMDsn\"",
            "systemId": "5abce6cd-9c7f-ed11-9989-002248004f60",
            "code": "1",
            "webProductID": "{60E1BEFE-C317-4FFB-ABB6-787DAA87FAF0}",
            "lastModification": "2022-12-19T13:00:32.203Z",
            "published": 0,
            "marketingDescription": "test 1 ",
            "categoryDescription": "White Sparkling",
            "countryCode": "FR",
            "countryDescription": "France",
            "regionCode": "",
            "egionDescription": "",
            "subRegionCode": "",
            "subRegionDescription": "",
            "producerCode": "AGRAPART",
            "producerName": "",
            "itemClassification": "",
            "alcoolPercent": "12.3%",
            "vintage": "2005",
            "grapes": "",
            "attributes": "",
            "tags": "FR,,,,2005,,,12.3%,White Sparkling,",
            "systemCreatedAt": "2022-12-19T12:58:17.473Z",
            "systemCreatedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00",
            "systemModifiedAt": "2022-12-19T13:00:32.203Z",
            "systemModifiedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00"
        }
    ]
}
```

### Product Fields

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1       |  Product      |  Code        | Code       |  20          |           |
|  1       |  Product      |  Web Product Id  | Code       |  20      |           |
|  1       |  Product      |  Web Last Md. Date Time  | Date Time     |           |
|  1       |  Product      |  Published  | Boolean    |               ||
|  1       |  Product      |  Last Modification  | Date Time          ||
|  1       |  Product      |  Marketing Description  |String ||
|  1       |  Product      |  Category Code  | String ||
|  1       |  Product      |  Category Description  | String ||
|  1       |  Product      |  Country Code  | String ||
|  1       |  Product      |  Country Description  |  String ||
|  1       |  Product      |  Region Code  | String ||
|  1       |  Product      |  Region Description  |String ||
|  1       |  Product      |  SubRegion Code  |String ||
|  1       |  Product      |  SubRegion Description  |String ||
|  1       |  Product      |  Producer  |String ||
|  1       |  Product      |  Item Classification  |String ||
|  1       |  Product      |  Alcool Percent  |Decimal ||
|  1       |  Product      |  Vintage  |String ||
|  1       |  Product      |  Grapes  |String ||
|  1       |  Product      |  Attributes  |String ||
|  1       |  Product      |  Tags  |String ||
|  1       |  Product      | System Id | GUID |  |  |
|  1       |  Product      | System Created At | DateTime |  |  |
|  1       |  Product      | System Created By  | String |  |  |
|  1       |  Product      | System Modified At | DateTime |  |  |
|  1       |  Product      | System Modified By | String |  |  |
<!-- |  1..1    |  SKU\Variant  |  Web Item Id  |String ||
|  1..1    |  SKU\Variant  |  Published  |Boolean ||
|  1..1    |  SKU\Variant  |  Deleted  |Boolean ||
|  1..1    |  SKU\Variant  |  Web Last Mod. Date Time  | Date Time ||
|  1..1    |  SKU\Variant  |  Item No  | String ||
|  1..1    |  SKU\Variant  |  Blocked  | Boolean ||
|  1..1    |  SKU\Variant  |  Last Modification  | Date Time ||
|  1..1    |  SKU\Variant  |  Description  | String ||
|  1..1    |  SKU\Variant  |  Base UoM Code  | String ||
|  1..1    |  SKU\Variant  |  Base UoM Description  | String ||
|  1..1    |  SKU\Variant  |  Sales UoM Code  | String ||
|  1..1    |  SKU\Variant  |  Sales UoM Description  | String ||
|  1..1    |  SKU\Variant  |  Sales UoM Qty Per  | Decimal ||
|  1..1    |  SKU\Variant  |  Unit Volume  | Decimal ||
|  1..1    |  SKU\Variant  |  Unit Price With Duty  |Decimal ||
|  1..1    |  SKU\Variant  |  Unit Price WithOut Duty  |Decimal ||
|  1..1    |  SKU\Variant  |  Stock Quantity Base  |Decimal ||
|  1..1    |  SKU\Variant  |  Bottles Per Case | Deciaml||
|  1..1    |  SKU\Variant  |  Purchasing Code | String||
|  1..1    |  SKU\Variant  |  Unit Weight | Decimal||
|  1..1    |  SKU\Variant  |  Sales Unit Weight | Decimal||
|  1..1    |  SKU\Variant  |  Web UoM Code | String||
|  1..1    |  SKU\Variant  |  Web UoM Description | String||
|  1..1    |  SKU\Variant  |  Web Sale Only Unit | Decimal||
|  1..1    |  SKU\Variant  |  Web Catalogue  | String|| -->

## GET Stock

Retrieve the properties and relationships of a Stock object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/webStocks
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/webStocks",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzE2Njc2Mzg3NDU3MTI3MzQwMTg4MTswMDsn\"",
            "systemId": "a94ce3d8-18ca-ed11-a7c9-00224800e466",
            "locationCode": "BLUE",
            "itemNo": "AGRA26205A",
            "variantCode": "",
            "qtyPerUnitOfMeasure": 0,
            "stockAvailableBase": 0,
            "lastModDateTime": "2023-03-24T07:52:40.64Z",
            "systemCreatedAt": "2023-03-24T07:52:40.657Z",
            "systemCreatedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00",
            "systemModifiedAt": "2023-03-24T07:52:40.657Z",
            "systemModifiedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00"
        }
    ]
}
```

### Stock Fields

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
|  1  | Web Stock| System ID | GUID |  |  |
|  1  | Web Stock| Item_No  |  String  | 20 | Primary Key Field SKU Code|
|  1  | Web Stock| Variant_Code  |  String  | 10 | Primary Key Field Duty Status|
|  1  | Web Stock| Unit_of_Measure_Code  |  String  | 10 | Primary Key Field UoM|
|  1  | Web Stock| Location_Code  |  String  |  10 | Primary Key Field Location |
|  1  | Web Stock| Group_Code  |  String  | 50 | Primary Key Field (Not Used)|
|  1  | Web Stock| Qty_per_Unit_of_Measure  |  Decimal  | |
|  1  | Web Stock| Stock_Available_Base  |  Decimal  | Stock Available |
|  1  | Web Stock| Last_Mod_Date_Time  |  Date Time  || Last Mod. Date Time|
|  1  | Web Stock| System Created At | DateTime |  |  |
|  1  | Web Stock| System Created By  | String |  |  |
|  1  | Web Stock| System Modified At | DateTime |  |  |
|  1  | Web Stock| System Modified By | String |  |  |




## Create Web Order

Retrieve the properties and relationships of a Web Order object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
POST

businesscentralPrefix/webOrders
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Here is an example of the request

```json

{
    "orderGroup": "GROUP_A",
    "orderId": "PFLOW997",
    "orderType": "WEB",
    "sellToCustomerNo": "1020000",
    "customerEmail": "Test@tvisiontech.co.uk",
    "sellToCustomerName": "",
    "sellToCustomerName2": "",
    "sellToCity": "",
    "sellToCounty": "",
    "sellToEMail": "",
    "sellToAddress": "",
    "sellToContact": "",
    "sellToAddress2": "",
    "sellToPhoneNo": "",
    "sellToPostCode": "",
    "orderDate": "0001-01-01",
    "shipmentDate": "0001-01-01",
    "currencyCode": "",
    "yourReference": "",
    "externalDocumentNo": "",
    "deliveryNoteText1": "",
    "deliveryNoteText2": "",
    "giftNoteText1": "",
    "giftNoteText2": "",
    "noteText1": "",
    "noteText2": "",
    "shipToCode": "",
    "shipToName": "",
    "shipToCity": "",
    "shipToCounty": "",
    "shipToName2": "",
    "shipToAddress": "",
    "shipToContact": "",
    "shipToAddress2": "",
    "shipToPostCode": "",
    "shippingAgentCode": "",
    "shipmentMethodCode": "",
    "shipToCountryRegionCode": "",
    "shippingAgentServiceCode": "",
    "paymentMethodCode": "",
    "paymentTermsCode": "",
    "orderURL": "",
    "totalOrderAmount": 0,
    "paid": false,
    "dispatched": false,
    "pendingCart": false,
    "pricesIncludingVAT": false,
    "shortcutDimension1Code": "",
    "shortcutDimension2Code": "",
}

```

### Response

Here is an example of the response

```json
{
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/webOrders",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzE1MjA3OTY5Mzc4NjU4ODEzMTI5MTswMDsn\"",
            "systemId": "81b0bab8-54bf-ed11-9a88-000d3a86ba5f",
            "orderGroup": "GROUP_A",
            "orderId": "PFLOW997",
            "orderType": "WEB",
            "sellToCustomerNo": "1020000",
            "customerEmail": "",
            "sellToCustomerName": "",
            "sellToCustomerName2": "",
            "sellToCity": "",
            "sellToCounty": "",
            "sellToEMail": "",
            "sellToAddress": "",
            "sellToContact": "",
            "sellToAddress2": "",
            "sellToPhoneNo": "",
            "sellToPostCode": "",
            "orderDate": "0001-01-01",
            "shipmentDate": "0001-01-01",
            "locationCode": "BLUE",
            "currencyCode": "",
            "yourReference": "",
            "externalDocumentNo": "",
            "deliveryNoteText1": "",
            "deliveryNoteText2": "",
            "giftNoteText1": "",
            "giftNoteText2": "",
            "noteText1": "",
            "noteText2": "",
            "shipToCode": "",
            "shipToName": "",
            "shipToCity": "",
            "shipToCounty": "",
            "shipToName2": "",
            "shipToAddress": "",
            "shipToContact": "",
            "shipToAddress2": "",
            "shipToPostCode": "",
            "shippingAgentCode": "",
            "shipmentMethodCode": "",
            "shipToCountryRegionCode": "",
            "shippingAgentServiceCode": "",
            "paymentMethodCode": "",
            "paymentTermsCode": "",
            "orderURL": "",
            "totalOrderAmount": 0,
            "paid": false,
            "dispatched": false,
            "pendingCart": false,
            "pricesIncludingVAT": false,
            "shortcutDimension1Code": "",
            "shortcutDimension2Code": "",
            "systemModifiedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00",
            "systemCreatedAt": "2023-03-10T15:03:32.59Z",
            "systemCreatedBy": "ce53a24b-ca42-4195-af5e-f3027962c9ec",
            "systemModifiedAt": "2023-03-10T15:14:33.127Z"
        }
    ]
}
```
### Web Order Fields

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      | Mandatory | Required |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |--- |--- |
| 1  | Web Order Header | System ID | GUID |  |  |  |  |
| 1  | Web Order Header | Order Group | Code | 50 | Key (Internal Use) |  |  |
| 1  | Web Order Header | Order Id | Code | 50 | Key (Unique Web Reference) | Y | Y |
| 1  | Web Order Header | Order Type | Code | 10 | Web Specific |  | Y |
| 1  | Web Order Header | sellToCustomerNo | Code | 50 | Web Specific |  | Y |
| 1  | Web Order Header | Customer Email | Text | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Sell-to Customer Name | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Customer Name 2 | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Ship Address Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Payment Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Ship Method Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Pending Cart | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Payment Method Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Shpping Agent Id | code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Shipping Agent Service Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Dispatched | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Paid | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Posting Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Posting Description | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Payment Terms Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Due Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Shipment Method Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Location Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 1 Code | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 2 Code | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Customer Posting Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Currency Factor | Decimal |  | Standard |  |  |
| 1  | Web Order Header | Customer Price Group | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Prices Including VAT | Boolean |  | Standard |  |  |
| 1  | Web Order Header | Customer Disc. Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Language Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Salesperson Code | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Package Tracking No. | Text | 30 | Standard |  |  |
| 1  | Web Order Header | VAT Bus. Posting Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | VAT Registration No. | Text | 20 | Standard |  |  |
| 1  | Web Order Header | Reason Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Gen. Bus. Posting Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Payment Method Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Shipping Agent Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | VAT Country/Region Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Document Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer No. | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Sell-to City | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to County | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to E-Mail | Text | 80 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Address | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Contact | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Address 2 | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Phone No. | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Post Code | Code | 20 | Standard |  | Y |
| 1  | Web Order Header | Order Date | Date |  | Standard |  | Y |
| 1  | Web Order Header | Shipment Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Location Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Currency Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Your Reference | Text | 35 | Standard |  |  |
| 1  | Web Order Header | External Document No. | Code | 35 | Standard |  |  |
| 1  | Web Order Header | Delivery Note Text 1 | Text | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Delivery Note Text 2 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 1 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 2 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 1 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 2 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Sell-to Country/Region Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer Template Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Contact No. | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Ship-to Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Ship-to Name | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Name 2 | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to Address | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Address 2 | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to City | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Contact | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Post Code | Code | 20 | Standard |  | Y |
| 1  | Web Order Header | Ship-to County | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Country/Region Code | Code | 10 | Standard |  | Y |
| 1  | Web Order Header | Order URL | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Total Order Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | System Created At | DateTime |  |  |
| 1  | Web Order Header | System Created By  | String |  |  |
| 1  | Web Order Header | System Modified At | DateTime |  |  |
| 1  | Web Order Header | System Modified By | String |  |  |

<!-- | 1  | Web Order Header | Total Tax Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Requested Delivery Date | Date |  | Standard |  | Y |
| 1  | Web Order Header | Promised Delivery Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Shipping Agent Service Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Decimal 01 | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Integer 01 | Integer |  | Web Specific |  |  |
| 1  | Web Order Header | Date 01 | Date |  | Web Specific |  |  |
| 1  | Web Order Header | Code 01 | Code | 20 | Web Specific |  |  |
| 1  | Web Order Header | Time 01 | Time |  | Web Specific |  |  |
| 1  | Web Order Header | DateTime 01 | DateTime |  | Web Specific |  |  |
| 1  | Web Order Header | Text 01 | Text | 50 | Web Specific |  |  |
| 1  | Web Order Header | Boolean 01 | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Decimal 02 | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Integer 02 | Integer |  | Web Specific |  |  |
| 1  | Web Order Header | Date 02 | Date |  | Web Specific |  |  |
| 1  | Web Order Header | Code 02 | Code | 20 | Web Specific |  |  |
| 1  | Web Order Header | Time 02 | Time |  | Web Specific |  |  |
| 1  | Web Order Header | DateTime 02 | DateTime |  | Web Specific |  |  |
| 1  | Web Order Header | Text 02 | Text | 50 | Web Specific |  |  |
| 1  | Web Order Header | Boolean 02 | Boolean |  | Web Specific |  |  | -->

## Create Web Order Lines

Retrieve the properties and relationships of a Web Lines object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
POST

businesscentralPrefix/webOrderLines
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Here is an example of the request

```json
   
{

    "orderGroup": "GROUP_A",
    "orderId": "PFLOW997",
    "lineId": "1",
    "productId": "B12141",
    "unitOfMeasureId": "6X75CL",
    "description": "Barolo Colonello, Prunotto 2009 6x75",
    "quantity": 40,
    "unitPrice": 0,
}

```


### Response

Here is an example of the response

```json
{
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/webOrderLines",
    "value": [
        {
            "@odata.etag": "W/\"JzE5OzEyNjA1MTc0NDE5MzU2ODQzODYxOzAwOyc=\"",
            "systemId": "82b0bab8-54bf-ed11-9a88-000d3a86ba5f",
            "orderGroup": "GROUP_A",
            "orderId": "PFLOW997",
            "lineId": "1",
            "productId": "B12141",
            "unitOfMeasureId": "6X75CL",
            "description": "Barolo Colonello, Prunotto 2009 6x75",
            "quantity": 40,
            "unitPrice": 0,
            "systemCreatedAt": "2023-03-10T15:03:32.95Z",
            "systemCreatedBy": "ce53a24b-ca42-4195-af5e-f3027962c9ec",
            "systemModifiedAt": "2023-03-10T15:14:32.5Z",
            "systemModifiedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00"
        }
}
```

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      | Mandatory | Required |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |--- |--- |
| 1  | Web Order Lines | System Id | GUID |  |  |
| 1  | Web Order Lines | Order Group | Code | 50 | Key |  |  |
| 1  | Web Order Lines | Order Id | Code | 50 | Key (Unique External Reference) | Y | Y |
| 1  | Web Order Lines | Line Id | Code | 50 | Key (Unique External Reference) | Y | Y |
| 1  | Web Order Lines | Product Id | Code | 50 | Web Specific |  | Y |
| 1  | Web Order Lines | Description | Text | 50 | Standard |  | Y |
| 1  | Web Order Lines | Unit of Measure Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Lines | Quantity | Decimal |  | Standard |  | Y |
| 1  | Web Order Lines | Unit Price | Decimal |  | Standard |  | Y |
| 1  | Web Order Lines | System Created At | DateTime |  |  |
| 1  | Web Order Lines | System Created By  | String |  |  |
| 1  | Web Order Lines | System Modified At | DateTime |  |  |
| 1  | Web Order Lines | System Modified By | String |  |  |


<!-- | 1..N  | Web Order Lines | Force Calculation Price | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Lot No. | Code | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Negative | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Type | Option |  | Standard |  |  |
| 1..N  | Web Order Lines | No. | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Shipment Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Description | Text | 50 | Standard |  | Y |
| 1..N  | Web Order Lines | Description 2 | Text | 50 | Standard |  |  |
| 1..N  | Web Order Lines | VAT % | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Line Discount % | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Line Discount Amount | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Net Amount | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Amount Including VAT | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Shortcut Dimension 1 Code | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Shortcut Dimension 2 Code | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Gen. Bus. Posting Group | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Gen. Prod. Posting Group | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | VAT Bus. Posting Group | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | VAT Prod. Posting Group | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | VAT Base Amount | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Unit Cost | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | VAT Identifier | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Variant Code | Code | 10 | Standard |  |  |
| 1..N  | Web Order Lines | Qty. per Unit of Measure | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Unit of Measure Code | Code | 10 | Standard |  |  |
| 1..N  | Web Order Lines | Item Category Code | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Requested Delivery Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Promised Delivery Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Planned Delivery Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Planned Shipment Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Decimal 01 | Decimal |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Integer 01 | Integer |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Date 01 | Date |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Code 01 | Code | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Time 01 | Time |  | Web Specific |  |  |
| 1..N  | Web Order Lines | DateTime 01 | DateTime |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Text 01 | Text | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Boolean 01 | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Decimal 02 | Decimal |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Integer 02 | Integer |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Date 02 | Date |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Code 02 | Code | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Time 02 | Time |  | Web Specific |  |  |
| 1..N  | Web Order Lines | DateTime 02 | DateTime |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Text 02 | Text | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Boolean 02 | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Decimal 03 | Decimal |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Integer 03 | Integer |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Date 03 | Date |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Code 03 | Code | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Time 03 | Time |  | Web Specific |  |  |
| 1..N  | Web Order Lines | DateTime 03 | DateTime |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Text 03 | Text | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Boolean 03 | Boolean |  | Web Specific |  |  | -->

## Create Payment

Retrieve the properties and relationships of a Payment Journal object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
POST

businesscentralPrefix/paymentEntries
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Here is an example of the request

```json
{
   
    "externalDocument": "TEST001",
    "currencyCode": "GBP",
    "customerNo": "C001",
    "paymentReference": "TPAYTESTEST",
    "Amount": 70.7

}
```
### Response

Here is an example of the response

```json
{
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/paymentEntries/$entity",
    "@odata.etag": "W/\"JzE5Ozk5OTUyMDQ3NTg3MzgxODIyMDYxOzAwOyc=\"",
    "systemId": "522a4c25-1eca-ed11-a7c9-00224800e466",
    "currencyCode": "GBP",
    "customerId": "",
    "customerNo": "C001",
    "documentNo": "",
    "externalDocument": "TEST001",
    "paymentMethodCode": "",
    "paymentReference": "TPAYTESTEST",
    "postingDate": "0001-01-01",
    "amount": 70.7,
    "entryNo": 1,
    "dueDate": "0001-01-01",
    "refund": false,
    "systemCreatedAt": "2023-03-24T08:30:42.367Z",
    "systemCreatedBy": "fff77cf3-0f31-4147-b1ec-92eaa6f4782c",
    "systemModifiedAt": "2023-03-24T08:30:42.367Z",
    "systemModifiedBy": "fff77cf3-0f31-4147-b1ec-92eaa6f4782c"
}
```

### Payment Fields

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1          | Payment         | System Id | GUID |  |  |
|  1          | Payment         | External_Document         |  String    | 80           | |
|  1          | Payment         | Currency_Code         |  String    | 10           | |
|  1          | Payment         | Payment_Reference         |  String    | 50           | |
|  1          | Payment         | Amount         |  Decimal    |            | |
|  1          | Payment         | Payment_Method_Code         |  String    | 10           | |
|  1          | Payment         | Posting_Date         |  Date    |            | |
|  1          | Payment         | Due_Date         |  Date    |            | |
|  1          | Payment         | System Created At | DateTime |  |  |
|  1          | Payment         | System Created By  | String |  |  |
|  1          | Payment         | System Modified At | DateTime |  |  |
|  1          | Payment         | System Modified By | String |  |  |



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
### Manifest Fields

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1          | TVT Manifest Header V2    | System Id | GUID |  |  |
|  1          | TVT Manifest Header V2    | No.         |  Code    | 20           | |
|  1          | TVT Manifest Header V2    | Address         |  String    | 100           | |
|  1          | TVT Manifest Header V2    | Address 2         |  String    | 50           | |
|  1          | TVT Manifest Header V2    | Address Code         |  Code    | 10            | |
|  1          | TVT Manifest Header V2    | City         |  String    | 30           | |
|  1          | TVT Manifest Header V2    | Contact         |  String    | 100            | |
|  1          | TVT Manifest Header V2    | Country/Region Code         |  Date    |            | |
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
### Manifest Line Fields
| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1          | TVT Manifest Line V2    | System Id | GUID |  |  |
|  1          | TVT Manifest Line V2    | Document No. | Code | 20 |  |
|  1          | TVT Manifest Line V2    | Manifest No. | Code | 20 |  |
|  1          | TVT Manifest Line V2    | Line No. | Integer |  |  |
|  1          | TVT Manifest Line V2    | Duty Status | Code | 10 |  |
|  1          | TVT Manifest Line V2    | Source No. | Code | 20 |  |
|  1          | TVT Manifest Line V2    | Total Eq. Cases | Decimal | 20 |  |
|  1          | TVT Manifest Line V2    | Document No. | Code | 20 |  |
|  1          | TVT Manifest Line V2    | Manifest No.. | Code | 20 |  |
|  1          | TVT Manifest Line V2    | Document No. | Code | 20 |  |
|  1          | TVT Manifest Line V2    | Manifest No.. | Code | 20 |  |
|  1          | TVT Manifest Line V2    | Shipping Agent Code      |  Code    | 10            | |
|  1          | TVT Manifest Line V2    | Shipping Agent Service Code      |  Code    | 10            | |
|  1          | TVT Manifest Line V2    | No. of Item Lines      |  Integer    |   | |
|  1          | TVT Manifest Line V2    | Gross Weight     |  Decimal    |   | |
|  1          | TVT Manifest Line V2    | Net Weight     |  Decimal    |   | |
|  1          | TVT Manifest Line V2    |  Posted Document No. | Code | 20 |  |
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


## GET Orders Status

Retrieve the properties and relationships of a Web Order object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/webOrderStatuses
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/webOrderStatuses",
    "value": [
        {
            "@odata.etag": "W/\"JzE5OzUzNDY3NjI2Nzg5OTExOTI2OTgxOzAwOyc=\"",
            "systemId": "eb502159-9fb0-ed11-9a88-000d3a86ba5f",
            "orderId": "",
            "orderDate": "0001-01-01",
            "bcStatus": "Created",
            "bcErrorMessage": "",
            "bcCreationDateTime": "2023-02-19T21:49:57.093Z",
            "bcLastModDateTime": "0001-01-01T00:00:00Z",
            "bcLastValidateDateTime": "0001-01-01T00:00:00Z",
            "bcLastProcessDateTime": "0001-01-01T00:00:00Z",
            "bcValidated": false,
            "bcProcessed": false,
            "bcDocumentType": " ",
            "bcDocumentNo": "",
            "systemCreatedAt": "2023-02-19T21:49:57.093Z",
            "systemCreatedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00",
            "systemModifiedAt": "2023-02-19T21:49:57.093Z",
            "systemModifiedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00"
        }
    ]
}   
```

### Order Status Fields

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1          | TVTWS Web Order | Order Id         |  Code    |   50         | |
|  1          | TVTWS Web Order | Order Date       |  Text    | 250  |  |
|  1          | TVTWS Web Order | BC Status        |  Enum    | 20  | Created,Validated,Processed,Posted |
|  1          | TVTWS Web Order | BC Error Message        |  Text    | 250       | |
|  1          | TVTWS Web Order | BC Creation DateTime         |  DateTime    |   |  |
|  1          | TVTWS Web Order | BC Last Validate Date Time         |  DateTime    |   |  |
|  1          | TVTWS Web Order | BC Last Process Date Time      |  DateTime    |       | |
|  1          | TVTWS Web Order | BC Validated        |  Boolean    |   |  |
|  1          | TVTWS Web Order | BC Processed       |  Boolean    |   |  |
|  1          | TVTWS Web Order | Document Type       |  Enum    | '',Sales Order,Sales Return        | |
|  1          | TVTWS Web Order | Document No        |  Code    | 20  |  |
|  1          | TVTWS Web Order | System Id | GUID |  |  |
|  1          | TVTWS Web Order | System Created At | DateTime |  |  |
|  1          | TVTWS Web Order | System Created By  | String |  |  |
|  1          | TVTWS Web Order | System Modified At | DateTime |  |  |
|  1          | TVTWS Web Order | System Modified By | String |  |  |

## GET Sales Prices

Retrieve the properties and relationships of a Sales Prices object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
GET 

businesscentralPrefix/salesPrices
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

    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/salesPrices",
    "value": [
        {
            "@odata.etag": "W/\"JzE5Ozc3NDU3MTMwNTk2MTQzMDgxODMxOzAwOyc=\"",
            "systemId": "a2b0fad7-b5b6-ed11-9a88-000d3a86b91d",
            "itemNo": "B12141",
            "variantCode": "DUTY FREE",
            "salesType": "Campaign",
            "salesCode": "CP1001",
            "unitOfMeasureCode": "",
            "endingDate": "0001-01-01",
            "currencyCode": "£",
            "unitPrice": 10,
            "priceIncludesVAT": false,
            "minimumQuantity": 0,
            "systemCreatedAt": "2023-02-27T15:46:15.657Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2023-02-27T15:47:35.56Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "tvtwsWebLastModDateTime": "2023-02-27T15:47:35.56Z",
            "tvtwsWebItemPublished": false
        }
    ]
}
```
### Sales Prices Fields

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|	1	|	Sales Prices	|	Item No	|	string	|	20	|
|	1	|	Sales Prices	|	Variant Code	|	string	|	10	|
|	1	|	Sales Prices	|	Sales Type	|	Type	|		|
|	1	|	Sales Prices	|	Sales Code	|	string	|	10	|
|	1	|	Sales Prices	|	Unit of Measure Code	|	string	|	10	|
|	1	|	Sales Prices	|	Starting Date	|	date	|		|
|	1	|	Sales Prices	|	Ending Date	|	date	|		|
|	1	|	Sales Prices	|	Unit Price	|	decimal	|		|
|	1	|	Sales Prices	|	Price Includes VAT	|	boolean	|		|
|	1	|	Sales Prices	|	Minimum Quantity	|	decimal	|		|
|   1   |   Sales Prices      | System Id | GUID |  |  |
|  1    |   Sales Prices      | System Created At | DateTime |  |  |
|  1    |   Sales Prices      | System Created By  | String |  |  |
|  1    |   Sales Prices      | System Modified At | DateTime |  |  |
|  1    |   Sales Prices      | System Modified By | String |  |  |



## GET Paid Reserve

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/PaidReserves
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/PaidReserves",
    "value": [
        {
            "@odata.etag": "W/\"JzE5Ozc3MTI4MzgxNzQzNDAwNzY3NzYxOzAwOyc=\"",
            "systemId": "0efb92e7-5b75-ed11-9989-000d3a0cd6a6",
            "no": "PRES0010087",
            "systemCreatedAt": "2022-12-06T11:48:38.35Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2022-12-06T11:48:38.35Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "sourceType": "Customer",
            "sourceNo": "1010000XXXXXXXXXXXXX",
            "sourceName": "Asado Bar & Grill",
            "itemNo": "B12141",
            "itemDescription": "Barolo Colonello Prunotto 2009 6x75",
            "unitOfMeasureCode": "75CL",
            "rotationNo": "",
            "qtyPerUnitOfMeasure": 1,
            "origPaidReserveNo": "",
            "quantity": 15,
            "remainingQuantity": 15,
            "qtyBooked": 0,
            "qtyOnBroking": 0,
            "unitPrice": 11,
            "unitCost": 0,
            "condition": "",
            "provenanceSource": "1",
            "contactNomineeNo": "",
            "contactNomineeName": "",
            "documentDate": "2022-08-10",
            "postingDate": "2022-08-10",
            "documentNo": "Q001",
            "expDeliveryInstruction": " ",
            "expDeliveryShipTo": "",
            "internalInformation": "",
            "externalDocumentNo": "",
            "dutyStatusFilter": "",
            "locationFilter": ""
        }
    ]
}
```

### Paid Reserve

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
|  1  | TVT Paid Reserve Information | No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Source Type  |  Enum  | '',Customer,Vendor |  |
|  1  | TVT Paid Reserve Information | Source No |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Source Name  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Item No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Item Description  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Unit of Measure Code  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Information | Rotation No. |  Code  | 50 |  |
|  1  | TVT Paid Reserve Information | Qty. per Unit of Measure  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Original Paid Reserve No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Quantity  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Remaining Quantity  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Qty. Booked  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Qty. on Broking  |  IntegerDecimal  |  |  |
|  1  | TVT Paid Reserve Information | Unit Price  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Unit Cost  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Information | Condition  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Provenance/Source  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Contact Nominee No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Contact Nominee Name  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | Document Date  |  Date  |  |  |
|  1  | TVT Paid Reserve Information | Posting Date  |  Date  |  |  |
|  1  | TVT Paid Reserve Information | Document No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Information | Exp. Delivery Instruction  |  Enum  | '',Intro Storage,Deliver to Ship-to |  |
|  1  | TVT Paid Reserve Information | Exp. Delivery Ship-to  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Information | Internal Information  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Information | External Document No.  |  Code  | 35 |  |
|  1  | TVT Paid Reserve Information | Duty Status Filter  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Information | Location Filter  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Information | System Id | GUID |  |  |
|  1  | TVT Paid Reserve Information | System Created At | DateTime |  |  |
|  1  | TVT Paid Reserve Information | System Created By  | String |  |  |
|  1  | TVT Paid Reserve Information | System Modified At | DateTime |  |  |
|  1  | TVT Paid Reserve Information | System Modified By | String |  |  |




## GET Paid Reserve Entries

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/PaidReserveEntries
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/PaidReserveEntries",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzExNjkzNjY4Nzk4MDM3NTc3MDAzMTswMDsn\"",
            "systemId": "9e1702f4-5b75-ed11-9989-000d3a0cd6a6",
            "entryNo": 106,
            "itemNo": "B12141",
            "postingDate": "2022-08-10",
            "entryType": "Stock into Paid Reserve",
            "paidReserveNo": "PRES0010087",
            "documentNo": "Q001",
            "description": "Barolo Colonello Prunotto 2009 6x75",
            "locationCode": "BLUE",
            "quantity": 15,
            "open": true,
            "quantityBase": 15,
            "remQuantityBase": 15,
            "unitCost": 0,
            "totalCost": 0,
            "unitPrice": 11,
            "totalPrice": 165,
            "sourceName": "Asado Bar & Grill",
            "reasonCode": "",
            "sourceType": "Customer",
            "sourceNo": "1010000XXXXXXXXXXXXX",
            "provenanceSource": "1",
            "condition": "",
            "origPaidReserveNo": "",
            "rotationNo": "",
            "bestBeforeDate": "0001-01-01",
            "rotationRef": "",
            "qtyBooked": 0,
            "qtyResBooked": 0,
            "reservedQuantity": 15,
            "variantCode": "DUTY FREE",
            "qtyPerUnitOfMeasure": 1,
            "unitOfMeasureCode": "75CL",
            "systemCreatedAt": "2022-12-06T11:48:53.757Z",
            "systemCreatedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "systemModifiedAt": "2022-12-06T11:48:53.757Z",
            "systemModifiedBy": "b6188cb8-d398-4a1c-8ec3-87ce63665e0b",
            "documentDate": "2022-08-10",
            "externalDocumentNo": "",
            "documentType": " ",
            "documentLineNo": 10000,
            "internalInformation": "",
            "itemLedgerEntryNo": 2205,
            "expDeliveryInstruction": " ",
            "expDeliveryShipTo": "",
            "contactNomineeNo": "",
            "contactNomineeName": "",
            "applyToILENo": 0
        },
    ]
}
```

### Fields Information

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
|  1  | TVT Paid Reserve Led. Entry | Entry No.  |  Integer  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Item No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Posting Date  |  Date  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Entry Type  |  Enum  | Stock Into,Withdrawal Stock,Transfer Stock,Cancel,Split,Purchase|  |
|  1  | TVT Paid Reserve Led. Entry | Paid Reserve No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Document No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Document No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Location Code  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Quantity  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Open  |  Boolean  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Quantity (Base)  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Rem. Quantity (Base)  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Unit Cost  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Total Unit Cost  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Unit Price  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Total Unit Price  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Source Name  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Led. Entry | Reason Code  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Led. Entry | Source Type  |  Enum  | '',Customer,Vendor |  |
|  1  | TVT Paid Reserve Led. Entry | Provenance/Source  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Led. Entry | Condition  |  Text  | 100 |  |
|  1  | TVT Paid Reserve Led. Entry | Original Paid Reserve No.  |  Code  | 20 |  |
|  1  | TVT Paid Reserve Led. Entry | Best Before Date  |  Date  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Rotation Ref.  |  Code  | 50  |  |
|  1  | TVT Paid Reserve Led. Entry | Qty. Booked  |  Decimal  |   |  |
|  1  | TVT Paid Reserve Led. Entry | Qty. Res. (Booked)  |  Decimal  |   |  |
|  1  | TVT Paid Reserve Led. Entry | Reserved Quantity |  Decimal  |   |  |
|  1  | TVT Paid Reserve Led. Entry | Variant Code |  Code  | 10  |  |
|  1  | TVT Paid Reserve Led. Entry | Qty. per Unit of Measure  |  Decimal  |  |  |
|  1  | TVT Paid Reserve Led. Entry | Unit of Measure Code  |  Code  | 10 |  |
|  1  | TVT Paid Reserve Led. Entry | System Id | GUID |  |  |
|  1  | TVT Paid Reserve Led. Entry | System Created At | DateTime |  |  |
|  1  | TVT Paid Reserve Led. Entry | System Created By  | String |  |  |
|  1  | TVT Paid Reserve Led. Entry | System Modified At | DateTime |  |  |
|  1  | TVT Paid Reserve Led. Entry | System Modified By | String |  |  |


### Recommended Content

[Business Central Standard Web Service ](BC/Readme.md)

[Get Companies](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/api-reference/v2.0/api/dynamics_company_get)