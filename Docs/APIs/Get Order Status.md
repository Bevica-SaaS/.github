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

### Field information
<details>
  <summary>Show</summary>

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
