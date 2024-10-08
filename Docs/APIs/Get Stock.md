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

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
|  1  | Web Stock| System ID | GUID |  |  |
|  1  | Web Stock| Item No.  |  String  | 20 | Primary Key Field SKU Code|
|  1  | Web Stock| Variant Code  |  String  | 10 | Primary Key Field Duty Status|
|  1  | Web Stock| Location Code  |  String  |  10 | Primary Key Field Location |
|  1  | Web Stock| Qty. per Unit of Measure  |  Decimal  | |
|  1  | Web Stock| Stock Available Base  |  Decimal  || Stock Available |
|  1  | Web Stock| Last Mod Date Time  |  Date Time  || Last Mod. Date Time|
|  1  | Web Stock| System Created At | DateTime |  |  |
|  1  | Web Stock| System Created By  | String |  |  |
|  1  | Web Stock| System Modified At | DateTime |  |  |
|  1  | Web Stock| System Modified By | String |  |  |
