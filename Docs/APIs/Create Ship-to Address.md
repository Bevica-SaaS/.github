## Create Customer

Retrieve the properties and relationships of a Ship-to Address object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
POST

businesscentralPrefix/shipToAddressesEdit
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Here is an example of the request

```json

{
    "customerNo": "C00140",
    "code": "LONDON",
    "name": "Postman customer",
    "name2": "",
    "address": "55 Cross Court",
    "address2": "Premier House"
}

```

### Response

Here is an example of the response

```json

{
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/shipToAddressesEdit/$entity",
    "@odata.etag": "W/\"JzE5OzMzNjAxMzc0NzcyNjUyNjk5MTMxOzAwOyc=\"",
    "systemId": "a733c276-721b-f011-9af4-000d3ad65798",
    "address": "55 Cross Court",
    "address2": "Premier House",
    "city": "",
    "code": "LONDON",
    "contact": "",
    "countryRegionCode": "",
    "county": "",
    "customerNo": "C00140",
    "eMail": "",
    "faxNo": "",
    "gln": "",
    "homePage": "",
    "locationCode": "",
    "name": "Postman Customer",
    "name2": "",
    "phoneNo": "",
    "placeOfExport": "",
    "postCode": "",
    "salespersonCode": "",
    "shipmentMethodCode": "",
    "shippingAgentCode": "",
    "shippingAgentServiceCode": "",
    "systemCreatedAt": "2025-04-17T09:58:09.123Z",
    "systemCreatedBy": "fff77cf3-0f31-4147-b1ec-92eaa6f4782c",
    "systemModifiedAt": "2025-04-17T09:58:09.123Z",
    "systemModifiedBy": "fff77cf3-0f31-4147-b1ec-92eaa6f4782c",
    "tvtDutyStatus": "DUTY PAID",
    "tvtWarehouseKeeperNo": "",
    "tvtWarehouseVATNo": "",
    "tvthmHMRCDefAccount": "",
    "tvthmHMRCMovementType": "_x0020_",
    "tvtwsWebId": "",
    "taxAreaCode": "",
    "taxLiable": false,
    "telexAnswerBack": "",
    "telexNo": ""
}
```


### Field information
<details>
  <summary>Show</summary>


