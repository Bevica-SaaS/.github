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
            "@odata.etag": "W/\"JzIwOzE1OTQyMzk0MzIxNjcxNTA0NzM2MTswMDsn\"",
            "systemId": "ec871204-5188-ed11-9989-6045bd0d024f",
            "sellToCustomerNo": "1010000",
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
        }
    ]
}
