## GET Sales Credit Memo Header

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

Coming soon
// "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies//(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/PostedSalesCrMemoInvoices",
//    "value": [
        {


//        },
//}
```

### Field Information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Sales Cr.Memo Header | System Id | GUID |  |  |
| 1 | Sales Cr.Memo Header | Sell-to Customer No. | String | 20 |  |
| 1 | Sales Cr.Memo Header | No. | String | 20 | |
| 1 | Sales Cr.Memo Header | Your Reference | 35 |  |  |
| 1 | Sales Cr.Memo Header | Ship-to Code | String |  |  |
| 1 | Sales Cr.Memo Header | Ship-to Name | String | 35 |  |
| 1 | Sales Cr.Memo Header | Ship-to Name 2 | String | 358 |  |
| 1 | Sales Cr.Memo Header | Ship-to Address | String | 50  |   |
| 1 | Sales Cr.Memo Header | Ship-to Address 2 | String | 50 |  |
| 1 | Sales Cr.Memo Header | Ship-to City | String | 30 |  |
| 1 | Sales Cr.Memo Header | Ship-to Contact | String | 20 |  |
| 1 | Sales Cr.Memo Header | Posting Date | Date |  |  |
| 1 | Sales Cr.Memo Header | Shipment Date | Date |  |  |
| 1 | Sales Cr.Memo Header | Shipment Method Code | String | 120 | |
| 1 | Sales Cr.Memo Header | Location Code | String |  |  |
| 1 | Sales Cr.Memo Header | Salesperson Code | String | 20 |  |
| 1 | Sales Cr.Memo Header | Amount | Decimal |   |  |
| 1 | Sales Cr.Memo Header | Amount Including VAT | Decimal |   |  |
| 1 | Sales Cr.Memo Header | Sell-to Customer Name | String |   |  |
| 1 | Sales Cr.Memo Header | Ship-to Post Code | String |   |  |
| 1 | Sales Cr.Memo Header | Ship-to County | String |   |  |
| 1 | Sales Cr.Memo Header | Ship-to Country/Region Code | String |   |  |
| 1 | Sales Cr.Memo Header | External Document No. | XX |   |  |
| 1 | Sales Cr.Memo Header | Duty Status | XX |   |  |
| 1 | Sales Cr.Memo Header | Sales Document Type| XX |   |  |
