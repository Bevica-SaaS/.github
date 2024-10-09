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
    "systemId": "c9c0ed7c-f1c3-ed11-9a88-001d3a86b26a",
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
    "locationcode": "BLUE",
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
    "paymentId": "",
    "paymentMethodCode": "",
    "paymentTermsCode": "",
    "orderURL": "",
    "totalOrderAmount": 0,
    "paid": false,
    "dutyFree": "true",
    "dispatched": false,
    "pendingCart": false,
    "pricesIncludingVAT": false,
    "shortcutDimension1Code": "",
    "shortcutDimension2Code": "",
    "systemCreatedAt": "2023-03-10T15:03:32.95Z",
    "systemCreatedBy": "ce53a24b-ca42-4195-af5e-f3027962c9ec",
    "systemModifiedAt": "2023-03-10T15:14:32.5Z",
    "systemModifiedBy": "691db9f1-24f4-48ca-a179-a41eb57d7c00"
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
            "paymentId": "",
            "paymentMethodCode": "",
            "paymentTermsCode": "",
            "orderURL": "",
            "totalOrderAmount": 0,
            "paid": false,
            "dutyFree": "false",
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

### Field information
<details>
  <summary>Show</summary>


| Relation | Source Table | Field Caption | Field Type | Field Length | Note      | Mandatory | Required |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |--- |--- |
| 1  | Web Order Header | System ID | GUID |  |  |  |  |
| 1  | Web Order Header | Order Group | Code | 50 | Key (Internal Use) |  |  |
| 1  | Web Order Header | Order Id | Code | 50 | Key (Unique Web Reference) | Y | Y |
| 1  | Web Order Header | Order Type | Code | 10 | Web Specific |  | Y |
| 1  | Web Order Header | Customer Email | String | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Sell-to Customer Name | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Customer Name 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Payment Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Pending Cart | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Shipping Agent Service Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Dispatched | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Paid | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Payment Terms Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Shipment Method Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Location Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 1 Code | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 2 Code | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Prices Including VAT | Boolean |  | Standard |  |  |
| 1  | Web Order Header | Payment Method Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Shipping Agent Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer No. | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Sell-to City | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to County | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to E-Mail | String | 80 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Address | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Contact | String | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Address 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Phone No. | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Post Code | Code | 20 | Standard |  | Y |
| 1  | Web Order Header | Order Date | Date |  | Standard |  | Y |
| 1  | Web Order Header | Shipment Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Currency Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Your Reference | String | 35 | Standard |  |  |
| 1  | Web Order Header | External Document No. | Code | 35 | Standard |  |  |
| 1  | Web Order Header | Delivery Note Text 1 | String | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Delivery Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 1 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 1 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Ship-to Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Duty Free | Boolean | | Standard |  |  |
| 1  | Web Order Header | Ship-to Name | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Name 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to Address | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Address 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to City | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Contact | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Post Code | Code | 20 | Standard |  | Y |
| 1  | Web Order Header | Ship-to County | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Country/Region Code | Code | 10 | Standard |  | Y |
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
| 1  | Web Order Header | Order Group | Code | 50 | Key (Internal Use) |  |  |
| 1  | Web Order Header | Order Id | Code | 50 | Key (Unique Web Reference) | Y | Y |
| 1  | Web Order Header | Order Type | Code | 10 | Web Specific |  | Y |
| 1  | Web Order Header | sellToCustomerNo | Code | 50 | Web Specific |  | Y |
| 1  | Web Order Header | Customer Email | String | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Sell-to Customer Name | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Customer Name 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship Address Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Payment Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Ship Method Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Pending Cart | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Payment Method Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Shipping Agent Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Shipping Agent Service Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Dispatched | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Paid | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Posting Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Posting Description | String | 50 | Standard |  |  |
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
| 1  | Web Order Header | Package Tracking No. | String | 30 | Standard |  |  |
| 1  | Web Order Header | VAT Bus. Posting Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | VAT Registration No. | String | 20 | Standard |  |  |
| 1  | Web Order Header | Reason Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Gen. Bus. Posting Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Payment Method Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Shipping Agent Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | VAT Country/Region Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Document Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer No. | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Sell-to City | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to County | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to E-Mail | String | 80 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Address | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Contact | String | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Address 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Phone No. | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Post Code | Code | 20 | Standard |  | Y |
| 1  | Web Order Header | Order Date | Date |  | Standard |  | Y |
| 1  | Web Order Header | Shipment Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Location Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Currency Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Your Reference | String | 35 | Standard |  |  |
| 1  | Web Order Header | External Document No. | Code | 35 | Standard |  |  |
| 1  | Web Order Header | Delivery Note Text 1 | String | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Delivery Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 1 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 1 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 2 | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Sell-to Country/Region Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer Template Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Contact No. | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Ship-to Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Ship-to Name | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Name 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to Address | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Address 2 | String | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to City | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Contact | String | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Post Code | Code | 20 | Standard |  | Y |
| 1  | Web Order Header | Ship-to County | String | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Country/Region Code | Code | 10 | Standard |  | Y |
| 1  | Web Order Header | Order URL | String | 80 | Web Specific |  |  |
| 1  | Web Order Header | Total Order Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | System Created At | DateTime |  |  |
| 1  | Web Order Header | System Created By  | String |  |  |
| 1  | Web Order Header | System Modified At | DateTime |  |  |
| 1  | Web Order Header | System Modified By | String |  |  |-->

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
| 1  | Web Order Header | Text 01 | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Boolean 01 | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Decimal 02 | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Integer 02 | Integer |  | Web Specific |  |  |
| 1  | Web Order Header | Date 02 | Date |  | Web Specific |  |  |
| 1  | Web Order Header | Code 02 | Code | 20 | Web Specific |  |  |
| 1  | Web Order Header | Time 02 | Time |  | Web Specific |  |  |
| 1  | Web Order Header | DateTime 02 | DateTime |  | Web Specific |  |  |
| 1  | Web Order Header | Text 02 | String | 50 | Web Specific |  |  |
| 1  | Web Order Header | Boolean 02 | Boolean |  | Web Specific |  |  | -->