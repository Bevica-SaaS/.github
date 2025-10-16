# Web Payment API - Developer Guide

## Overview
The Web Payment API provides access to payment transaction entries linked to web orders, supporting payment recording and tracking.

## API Endpoint Details
- **Endpoint**: `/paymentEntries`
- **Entity Name**: paymentEntry
- **Entity Set Name**: paymentEntries
- **Page ID**: 71982
- **Source Table**: TVTWS Web Payment Entry
- **API Group**: webbevica
- **Publisher**: tvisiontech
- **Version**: v2.0

## Permissions
- **Insert**: Allowed
- **Modify**: Allowed
- **Delete**: Allowed
- **Read**: Allowed

## Base URL
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/paymentEntries
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `entryNo` | Integer | Entry number (ID) |
| `currencyCode` | String | Currency code |
| `customerId` | String | Customer ID |
| `customerNo` | String | Customer number |
| `documentNo` | String | Document number |
| `externalDocument` | String | External document reference |
| `paymentMethodCode` | String | Payment method code |
| `paymentReference` | String | Payment reference/transaction ID |
| `postingDate` | Date | Payment posting date |
| `amount` | Decimal | Payment amount |
| `dueDate` | Date | Due date |
| `refund` | Boolean | Refund flag |
| `appliesToDocType` | Enum | Applies to document type |
| `appliestoDocNo` | String | Applies to document number |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemCreatedBy` | GUID | Created by user ID |
| `systemModifiedAt` | DateTime | Last modification timestamp |
| `systemModifiedBy` | GUID | Modified by user ID |

## Common Operations

### Record Payment
```http
POST /paymentEntries
Content-Type: application/json

{
  "orderGroup": "WEB",
  "orderId": "WEB-2025-12345",
  "postingDate": "2025-10-14",
  "paymentMethod": "CREDIT_CARD",
  "paymentReference": "TXN-ABC123456",
  "amount": 450.00,
  "currencyCode": "USD",
  "customerNo": "CUST001",
  "description": "Online payment via Stripe"
}
```

### Get Order Payments
```http
GET /paymentEntries?$filter=orderId eq 'WEB-2025-12345'
```

### Get Unapplied Payments
```http
GET /paymentEntries?$filter=applied eq false
```

### Mark Payment as Applied
```http
PATCH /paymentEntries({systemId})
Content-Type: application/json
If-Match: *

{
  "applied": true,
  "appliedDocumentNo": "INV-2025-001"
}
```

## Code Examples

### JavaScript
```javascript
class WebPaymentAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async recordPayment(paymentData) {
    const response = await fetch(`${this.baseUrl}/paymentEntries`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify(paymentData)
    });
    
    if (!response.ok) {
      throw new Error(`Failed to record payment: ${await response.text()}`);
    }
    
    return await response.json();
  }

  async getOrderPayments(orderId) {
    const response = await fetch(
      `${this.baseUrl}/paymentEntries?$filter=orderId eq '${orderId}'&$orderby=postingDate desc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getOrderPaymentTotal(orderId) {
    const payments = await this.getOrderPayments(orderId);
    return payments.reduce((total, payment) => total + payment.amount, 0);
  }

  async markAsApplied(systemId, documentNo) {
    const response = await fetch(`${this.baseUrl}/paymentEntries(${systemId})`, {
      method: 'PATCH',
      headers: {
        ...this.headers,
        'If-Match': '*'
      },
      body: JSON.stringify({
        applied: true,
        appliedDocumentNo: documentNo
      })
    });
    
    return await response.json();
  }

  async getUnappliedPayments() {
    const response = await fetch(
      `${this.baseUrl}/paymentEntries?$filter=applied eq false&$orderby=postingDate asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }
}

// Usage
const api = new WebPaymentAPI(baseUrl, accessToken);

// Record credit card payment
const payment = await api.recordPayment({
  orderGroup: 'WEB',
  orderId: 'WEB-2025-12345',
  postingDate: new Date().toISOString().split('T')[0],
  paymentMethod: 'CREDIT_CARD',
  paymentReference: 'stripe_ch_3ABC123',
  amount: 450.00,
  currencyCode: 'USD',
  customerNo: 'CUST001',
  description: 'Stripe payment - Order WEB-2025-12345'
});

console.log(`Payment recorded: ${payment.entryNo}`);

// Get order payment total
const total = await api.getOrderPaymentTotal('WEB-2025-12345');
console.log(`Total payments: $${total.toFixed(2)}`);

// Process unapplied payments
const unapplied = await api.getUnappliedPayments();
console.log(`Unapplied payments: ${unapplied.length}`);
```

### Python
```python
from datetime import date
from typing import List, Dict

class WebPaymentAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def record_payment(self, payment_data: dict) -> dict:
        response = requests.post(
            f'{self.base_url}/paymentEntries',
            headers=self.headers,
            json=payment_data
        )
        response.raise_for_status()
        return response.json()
    
    def get_order_payments(self, order_id: str) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/paymentEntries',
            headers=self.headers,
            params={
                '$filter': f"orderId eq '{order_id}'",
                '$orderby': 'postingDate desc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_order_payment_total(self, order_id: str) -> float:
        payments = self.get_order_payments(order_id)
        return sum(p['amount'] for p in payments)
    
    def mark_as_applied(self, system_id: str, document_no: str) -> dict:
        headers = self.headers.copy()
        headers['If-Match'] = '*'
        
        response = requests.patch(
            f'{self.base_url}/paymentEntries({system_id})',
            headers=headers,
            json={
                'applied': True,
                'appliedDocumentNo': document_no
            }
        )
        response.raise_for_status()
        return response.json()
    
    def get_unapplied_payments(self) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/paymentEntries',
            headers=self.headers,
            params={
                '$filter': 'applied eq false',
                '$orderby': 'postingDate asc'
            }
        )
        response.raise_for_status()
        return response.json()['value']

# Usage
api = WebPaymentAPI(base_url, access_token)

# Record PayPal payment
payment = api.record_payment({
    'orderGroup': 'WEB',
    'orderId': 'WEB-2025-12345',
    'postingDate': date.today().isoformat(),
    'paymentMethod': 'PAYPAL',
    'paymentReference': 'PAYPAL-TXN-XYZ789',
    'amount': 450.00,
    'currencyCode': 'USD',
    'customerNo': 'CUST001',
    'description': 'PayPal payment'
})

# Check if order is fully paid
order_total = 450.00
payment_total = api.get_order_payment_total('WEB-2025-12345')
is_paid = payment_total >= order_total
print(f"Order fully paid: {is_paid}")
```

### C#
```csharp
public class WebPaymentApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public WebPaymentApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<WebPaymentEntry> RecordPaymentAsync(WebPaymentEntry payment)
    {
        var json = JsonSerializer.Serialize(payment);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/paymentEntries", content);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<WebPaymentEntry>(responseJson);
    }
    
    public async Task<List<WebPaymentEntry>> GetOrderPaymentsAsync(string orderId)
    {
        var filter = $"orderId eq '{orderId}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/paymentEntries?$filter={filter}&$orderby=postingDate desc");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebPaymentEntry>>(json);
        return result.Value;
    }
    
    public async Task<decimal> GetOrderPaymentTotalAsync(string orderId)
    {
        var payments = await GetOrderPaymentsAsync(orderId);
        return payments.Sum(p => p.Amount);
    }
    
    public async Task MarkAsAppliedAsync(Guid systemId, string documentNo)
    {
        var request = new HttpRequestMessage(HttpMethod.Patch, $"{_baseUrl}/paymentEntries({systemId})");
        request.Headers.Add("If-Match", "*");
        
        var update = new { applied = true, appliedDocumentNo = documentNo };
        request.Content = new StringContent(
            JsonSerializer.Serialize(update), 
            Encoding.UTF8, 
            "application/json"
        );
        
        var response = await _httpClient.SendAsync(request);
        response.EnsureSuccessStatusCode();
    }
}

public class WebPaymentEntry
{
    public Guid SystemId { get; set; }
    public int EntryNo { get; set; }
    public string OrderGroup { get; set; }
    public string OrderId { get; set; }
    public DateTime PostingDate { get; set; }
    public string PaymentMethod { get; set; }
    public string PaymentReference { get; set; }
    public decimal Amount { get; set; }
    public string CurrencyCode { get; set; }
    public string CustomerNo { get; set; }
    public string Description { get; set; }
    public bool Applied { get; set; }
    public string AppliedDocumentNo { get; set; }
}
```

## Payment Methods

Common payment method codes:
- `CREDIT_CARD` - Credit card payments
- `PAYPAL` - PayPal transactions
- `STRIPE` - Stripe payments
- `BANK_TRANSFER` - Wire transfers
- `CHECK` - Check payments
- `CASH` - Cash payments

## Business Logic Notes

- **Entry Numbers**: Auto-assigned by system
- **Payment Application**: Track which invoice payments are applied to
- **Multi-Currency**: Supports different currencies via `currencyCode`
- **Reference Tracking**: Store gateway transaction IDs in `paymentReference`
- **Order Linking**: Always link payments to orders via `orderId`

## Validation Rules

- `amount` must be > 0
- `postingDate` required
- `paymentMethod` must be valid code
- `orderId` must reference existing order
- `currencyCode` must be valid

## Error Handling

Common errors:
- **400**: Invalid payment data
- **404**: Order not found
- **409**: Duplicate payment reference
- **422**: Validation failure

## Performance Tips

1. **Batch Queries**: Query multiple order payments in single call
2. **Filter Applied**: Use `applied` filter to find unapplied payments
3. **Date Ranges**: Filter by `postingDate` for reporting
4. **Cache Methods**: Cache payment method list

## Related APIs
- **Web Orders**: Order information
- **Customers**: Customer data

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
