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

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1          | Payment         | System Id | GUID |  |  |
|  1          | Payment         | Currency_Code         |  String    | 10           | |
|  1          | Payment         | CustomerID         |  String    | 20           | |
|  1          | Payment         | Customer_No.         |  String    | 20           | |
|  1          | Payment         | Document_No.         |  String    | 20           | |
|  1          | Payment         | External_Document         |  String    | 80           | |
|  1          | Payment         | Payment_Reference         |  String    | 50           | |
|  1          | Payment         | Amount         |  Decimal    |            | |
|  1          | Payment         | Entry_No.         |  Integer    |            | |
|  1          | Payment         | Payment_Method_Code         |  String    | 10           | |
|  1          | Payment         | Posting_Date         |  Date    |            | |
|  1          | Payment         | Due_Date         |  Date    |            | |
|  1          | Payment         | Refund         |  Boolean    |            | |
|  1          | Payment         | System Created At | DateTime |  |  |
|  1          | Payment         | System Created By  | String |  |  |
|  1          | Payment         | System Modified At | DateTime |  |  |
|  1          | Payment         | System Modified By | String |  |  |

