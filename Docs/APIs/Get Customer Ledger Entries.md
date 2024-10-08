## GET Customer Ledger Entries

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/CustEntries
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

### Field Information
<details>
  <summary>Show</summary>

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
