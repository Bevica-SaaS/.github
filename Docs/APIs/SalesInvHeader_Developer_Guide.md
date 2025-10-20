# Posted Sales Invoices API - Developer Guide

## Overview
The Posted Sales Invoices API provides read-only access to finalized sales invoices that have been posted in Business Central.

## API Endpoint Details
- **Endpoint**: `/PostedSalesInvoices`
- **Entity Name**: postedSalesInvoice
- **Entity Set Name**: PostedSalesInvoices
- **Page ID**: 72206
- **Source Table**: Sales Invoice Header
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/PostedSalesInvoices
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `no` | String | Invoice number |
| `sellToCustomerNo` | String | Customer number |
| `sellToCustomerName` | String | Customer name |
| `billToCustomerNo` | String | Bill-to customer |
| `billToName` | String | Bill-to name |
| `postingDate` | Date | Posting date |
| `documentDate` | Date | Document date |
| `dueDate` | Date | Payment due date |
| `amount` | Decimal | Total excl. VAT |
| `amountIncludingVAT` | Decimal | Total incl. VAT |
| `remainingAmount` | Decimal | Unpaid amount |
| `currencyCode` | String | Currency code |
| `externalDocumentNo` | String | External reference |
| `orderNo` | String | Source order number |
| `shipToCode` | String | Ship-to address code |
| `shipToName` | String | Ship-to name |
| `shipToAddress` | String | Ship-to address |
| `paymentTermsCode` | String | Payment terms |
| `salespersonCode` | String | Salesperson |

## Nested Entity
- **invoiceLines** - Invoice line details

## Common Use Cases

### Get Customer Invoices
```http
GET /PostedSalesInvoices?$filter=sellToCustomerNo eq 'CUST001'&$orderby=postingDate desc
```

### Get Recent Invoices
```http
GET /PostedSalesInvoices?$filter=postingDate ge 2025-10-01&$orderby=postingDate desc
```

### Get Invoice with Lines
```http
GET /PostedSalesInvoices?$filter=no eq 'INV-12345'&$expand=invoiceLines
```

### Get Unpaid Invoices
```http
GET /PostedSalesInvoices?$filter=remainingAmount gt 0
```

## Code Examples

### JavaScript
```javascript
class PostedInvoiceAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getCustomerInvoices(customerNo) {
    const response = await fetch(
      `${this.baseUrl}/PostedSalesInvoices?$filter=sellToCustomerNo eq '${customerNo}'&$orderby=postingDate desc`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getInvoice(invoiceNo) {
    const response = await fetch(
      `${this.baseUrl}/PostedSalesInvoices?$filter=no eq '${invoiceNo}'&$expand=invoiceLines`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value[0];
  }

  async getUnpaidInvoices(customerNo = null) {
    let filter = 'remainingAmount gt 0';
    if (customerNo) filter += ` and sellToCustomerNo eq '${customerNo}'`;
    
    const response = await fetch(
      `${this.baseUrl}/PostedSalesInvoices?$filter=${encodeURIComponent(filter)}`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }
}

// Usage
const api = new PostedInvoiceAPI(baseUrl, accessToken);

const invoices = await api.getCustomerInvoices('CUST001');
console.log(`Customer has ${invoices.length} invoices`);

const unpaid = await api.getUnpaidInvoices('CUST001');
const totalDue = unpaid.reduce((sum, inv) => sum + inv.remainingAmount, 0);
console.log(`Total due: $${totalDue.toFixed(2)}`);
```

### Python
```python
class PostedInvoiceAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_customer_invoices(self, customer_no: str) -> list:
        response = requests.get(
            f'{self.base_url}/PostedSalesInvoices',
            headers=self.headers,
            params={
                '$filter': f"sellToCustomerNo eq '{customer_no}'",
                '$orderby': 'postingDate desc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_invoice(self, invoice_no: str) -> dict:
        response = requests.get(
            f'{self.base_url}/PostedSalesInvoices',
            headers=self.headers,
            params={
                '$filter': f"no eq '{invoice_no}'",
                '$expand': 'invoiceLines'
            }
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None

# Usage
api = PostedInvoiceAPI(base_url, access_token)
invoices = api.get_customer_invoices('CUST001')
```

### C#
```csharp
public class PostedInvoiceApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public async Task<List<PostedSalesInvoice>> GetCustomerInvoicesAsync(string customerNo)
    {
        var filter = $"sellToCustomerNo eq '{customerNo}'";
        var response = await _httpClient.GetAsync(
            $"{_baseUrl}/PostedSalesInvoices?$filter={filter}&$orderby=postingDate desc"
        );
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<PostedSalesInvoice>>(json);
        return result.Value;
    }
}

public class PostedSalesInvoice
{
    public Guid SystemId { get; set; }
    public string No { get; set; }
    public string SellToCustomerNo { get; set; }
    public string SellToCustomerName { get; set; }
    public DateTime PostingDate { get; set; }
    public DateTime DueDate { get; set; }
    public decimal Amount { get; set; }
    public decimal AmountIncludingVAT { get; set; }
    public decimal RemainingAmount { get; set; }
}
```

## Business Logic Notes

- **Read-Only**: Posted documents cannot be modified
- **Remaining Amount**: Tracks unpaid balance
- **Order Link**: `orderNo` references source sales order
- **Payment Tracking**: Use Customer Ledger Entries for payment details

## Related APIs
- **Posted Invoice Lines**: Line item details
- **Customer Ledger Entries**: Payment tracking
- **Customers**: Customer information

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
