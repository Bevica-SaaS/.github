# Posted Sales Credit Memos API - Developer Guide

## Overview
The Posted Sales Credit Memos API provides read-only access to finalized credit memos that have been posted in Business Central.

## API Endpoint Details
- **Endpoint**: `/PostedSalesCrMemoInvoices`
- **Entity Name**: postedSalesCrMemo
- **Entity Set Name**: PostedSalesCrMemoInvoices
- **Page ID**: 72208
- **Source Table**: Sales Cr.Memo Header
- **API Group**: webbevica
- **Publisher**: tvisiontech
- **Version**: v2.0

## Permissions
- **Insert**: Not Allowed
- **Modify**: Not Allowed
- **Delete**: Not Allowed
- **Read**: Allowed (Read-Only)

## Base URL
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/PostedSalesCrMemoInvoices
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `no` | String | Credit memo number |
| `sellToCustomerNo` | String | Customer number |
| `sellToCustomerName` | String | Customer name |
| `billToCustomerNo` | String | Bill-to customer |
| `billToName` | String | Bill-to name |
| `postingDate` | Date | Posting date |
| `documentDate` | Date | Document date |
| `dueDate` | Date | Due date |
| `amount` | Decimal | Total excl. VAT |
| `amountIncludingVAT` | Decimal | Total incl. VAT |
| `remainingAmount` | Decimal | Unapplied amount |
| `currencyCode` | String | Currency code |
| `externalDocumentNo` | String | External reference |
| `returnOrderNo` | String | Source return order |

## Nested Entity
- **creditMemoLines** - Credit memo line details

## Common Use Cases

### Get Customer Credit Memos
```http
GET /PostedSalesCrMemoInvoices?$filter=sellToCustomerNo eq 'CUST001'&$orderby=postingDate desc
```

### Get Credit Memo with Lines
```http
GET /PostedSalesCrMemoInvoices?$filter=no eq 'CM-12345'&$expand=creditMemoLines
```

### Get Recent Credit Memos
```http
GET /PostedSalesCrMemoInvoices?$filter=postingDate ge 2025-10-01
```

## Code Examples

### JavaScript
```javascript
class CreditMemoAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getCustomerCreditMemos(customerNo) {
    const response = await fetch(
      `${this.baseUrl}/PostedSalesCrMemoInvoices?$filter=sellToCustomerNo eq '${customerNo}'&$orderby=postingDate desc`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getCreditMemo(creditMemoNo) {
    const response = await fetch(
      `${this.baseUrl}/PostedSalesCrMemoInvoices?$filter=no eq '${creditMemoNo}'&$expand=creditMemoLines`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value[0];
  }
}

// Usage
const api = new CreditMemoAPI(baseUrl, accessToken);
const memos = await api.getCustomerCreditMemos('CUST001');
console.log(`Customer has ${memos.length} credit memos`);
```

### Python
```python
class CreditMemoAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_customer_credit_memos(self, customer_no: str) -> list:
        response = requests.get(
            f'{self.base_url}/PostedSalesCrMemoInvoices',
            headers=self.headers,
            params={
                '$filter': f"sellToCustomerNo eq '{customer_no}'",
                '$orderby': 'postingDate desc'
            }
        )
        response.raise_for_status()
        return response.json()['value']

# Usage
api = CreditMemoAPI(base_url, access_token)
memos = api.get_customer_credit_memos('CUST001')
```

### C#
```csharp
public class CreditMemoApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public async Task<List<PostedCreditMemo>> GetCustomerCreditMemosAsync(string customerNo)
    {
        var filter = $"sellToCustomerNo eq '{customerNo}'";
        var response = await _httpClient.GetAsync(
            $"{_baseUrl}/PostedSalesCrMemoInvoices?$filter={filter}&$orderby=postingDate desc"
        );
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<PostedCreditMemo>>(json);
        return result.Value;
    }
}

public class PostedCreditMemo
{
    public Guid SystemId { get; set; }
    public string No { get; set; }
    public string SellToCustomerNo { get; set; }
    public string SellToCustomerName { get; set; }
    public DateTime PostingDate { get; set; }
    public decimal Amount { get; set; }
    public decimal AmountIncludingVAT { get; set; }
}
```

## Business Logic Notes

- **Read-Only**: Posted documents cannot be modified
- **Customer Credit**: Credits customer account
- **Return Link**: May reference return order
- **Application**: Applied against customer invoices

## Related APIs
- **Posted Credit Memo Lines**: Line details
- **Customer Ledger Entries**: Application tracking
- **Customers**: Customer information

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
