## GET Sales Credit Memo Header

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/PostedSalesInvoices
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

Coming soon

```

### Field Information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Sales Invoice Header | System Id | GUID |  |  |
| 1 | Sales Invoice Header | Sell-to Customer No. | String | 20 |  |
| 1 | Sales Invoice Header | No. | String | 20 | |
| 1 | Sales Invoice Header | Your Reference | 35 |  |  |
| 1 | Sales Invoice Header | Ship-to Code | String |  |  |
| 1 | Sales Invoice Header | Ship-to Name | String | 35 |  |
| 1 | Sales Invoice Header | Ship-to Name 2 | String | 50 |  |
| 1 | Sales Invoice Header | Ship-to Address | String | 50  |   |
| 1 | Sales Invoice Header | Ship-to Address 2 | String | 50 |  |
| 1 | Sales Invoice Header | Ship-to City | String | 30 |  |
| 1 | Sales Invoice Header | Ship-to Contact | String | 20 |  |
| 1 | Sales Invoice Header | Posting Date | Date |  |  |
| 1 | Sales Invoice Header | Shipment Date | Date |  |  |
| 1 | Sales Invoice Header | Shipment Method Code | String | 20 | |
| 1 | Sales Invoice Header | Location Code | String | 10 |  |
| 1 | Sales Invoice Header | Salesperson Code | String | 20 |  |
| 1 | Sales Invoice Header | Order No. | String | 20 |  |
| 1 | Sales Invoice Header | Amount | Decimal |   |  |
| 1 | Sales Invoice Header | Amount Including VAT | Decimal |   |  
| 1 | Sales Invoice Header | Sell-to Customer Name | String | 100  |  |
| 1 | Sales Invoice Header | Ship-to Post Code | String | 20  |  |
| 1 | Sales Invoice Header | Ship-to County | String | 30  |  |
| 1 | Sales Invoice Header | Ship-to Country/Region Code | String | 30  |  |
| 1 | Sales Invoice Header | External Document No. | String | 35 |  |
| 1 | Sales Invoice Header | Duty Status | Code | 20  |  |
| 1 | Sales Invoice Header | Sales Document Type| String | 20 |  |
