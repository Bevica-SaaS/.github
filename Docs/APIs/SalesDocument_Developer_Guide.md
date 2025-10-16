# Sales Documents API - Developer Guide

## Overview
The Sales Documents API provides access to sales order and quote headers, including customer information, addresses, amounts, and related lines.

## API Endpoint Details
- **Endpoint**: `/salesDocuments`
- **Entity Name**: salesDocument
- **Entity Set Name**: salesDocuments
- **Page ID**: 72204
- **Source Table**: Sales Header
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/salesDocuments
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `documentType` | Enum | Order, Quote, Invoice, Credit Memo, Blanket Order, Return Order |
| `no` | String | Document number |
| `sellToCustomerNo` | String | Sell-to customer number |
| `sellToCustomerName` | String | Sell-to customer name |
| `sellToAddress` | String | Sell-to address line 1 |
| `sellToCity` | String | Sell-to city |
| `billToCustomerNo` | String | Bill-to customer number |
| `billToName` | String | Bill-to name |
| `billToAddress` | String | Bill-to address |
| `shipToCode` | String | Ship-to address code |
| `shipToName` | String | Ship-to name |
| `shipToAddress` | String | Ship-to address |
| `shipToCity` | String | Ship-to city |
| `postingDate` | Date | Posting date |
| `shipmentDate` | Date | Requested shipment date |
| `requestedDeliveryDate` | Date | Requested delivery date |
| `dueDate` | Date | Payment due date |
| `amount` | Decimal | Total amount excl. VAT |
| `amountIncludingVAT` | Decimal | Total amount incl. VAT |
| `currencyCode` | String | Currency code |
| `paymentTermsCode` | String | Payment terms code |
| `shipmentMethodCode` | String | Shipment method |
| `locationCode` | String | Location code |
| `salespersonCode` | String | Salesperson code |
| `yourReference` | String | Customer reference |
| `externalDocumentNo` | String | External document number |
| `tvtDutyStatus` | Enum | Duty status (Duty Paid, Duty Free) |
| `tvtSalesDocumentType` | Enum | Sales document type |
| `tvtCreditStatus` | Enum | Credit check status |
| `tvtOrderSource` | String | Order source |
| `pricesIncludingVAT` | Boolean | Prices include VAT flag |

## Nested Entity
- **salesDocumentLines** - Sales document lines (see Sales Line API)

## Common Operations

### Create Sales Order
```http
POST /salesDocuments
Content-Type: application/json

{
  "documentType": "Order",
  "sellToCustomerNo": "CUST001",
  "postingDate": "2025-10-14",
  "shipmentDate": "2025-10-16",
  "shipToCode": "WAREHOUSE",
  "locationCode": "MAIN",
  "externalDocumentNo": "PO-12345",
  "yourReference": "Customer PO"
}
```

### Get Sales Orders
```http
GET /salesDocuments?$filter=documentType eq 'Order'&$expand=salesLines
```

### Get Customer Orders
```http
GET /salesDocuments?$filter=sellToCustomerNo eq 'CUST001' and documentType eq 'Order'
```

### Update Order
```http
PATCH /salesDocuments({systemId})
Content-Type: application/json
If-Match: *

{
  "shipmentDate": "2025-10-18",
  "yourReference": "Updated PO Reference"
}
```

## Code Examples

### JavaScript
```javascript
class SalesDocumentAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async createOrder(orderData) {
    const response = await fetch(`${this.baseUrl}/salesDocuments`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify({
        documentType: 'Order',
        ...orderData
      })
    });
    
    if (!response.ok) throw new Error(await response.text());
    return await response.json();
  }

  async getCustomerOrders(customerNo) {
    const filter = `sellToCustomerNo eq '${customerNo}' and documentType eq 'Order'`;
    const response = await fetch(
      `${this.baseUrl}/salesDocuments?$filter=${encodeURIComponent(filter)}&$expand=salesLines`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async updateOrder(systemId, updates) {
    const response = await fetch(`${this.baseUrl}/salesDocuments(${systemId})`, {
      method: 'PATCH',
      headers: { ...this.headers, 'If-Match': '*' },
      body: JSON.stringify(updates)
    });
    
    return await response.json();
  }
}

// Usage
const api = new SalesDocumentAPI(baseUrl, accessToken);

const order = await api.createOrder({
  sellToCustomerNo: 'CUST001',
  postingDate: '2025-10-14',
  shipmentDate: '2025-10-16',
  shipToCode: 'WAREHOUSE',
  externalDocumentNo: 'PO-12345'
});

console.log(`Order created: ${order.no}`);
```

### Python
```python
class SalesDocumentAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def create_order(self, order_data: dict) -> dict:
        response = requests.post(
            f'{self.base_url}/salesDocuments',
            headers=self.headers,
            json={'documentType': 'Order', **order_data}
        )
        response.raise_for_status()
        return response.json()
    
    def get_customer_orders(self, customer_no: str) -> list:
        params = {
            '$filter': f"sellToCustomerNo eq '{customer_no}' and documentType eq 'Order'",
            '$expand': 'salesLines'
        }
        response = requests.get(
            f'{self.base_url}/salesDocuments',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()['value']

# Usage
api = SalesDocumentAPI(base_url, access_token)

order = api.create_order({
    'sellToCustomerNo': 'CUST001',
    'postingDate': '2025-10-14',
    'shipmentDate': '2025-10-16',
    'shipToCode': 'WAREHOUSE'
})
```

### C#
```csharp
public class SalesDocumentApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public async Task<SalesDocument> CreateOrderAsync(SalesDocument order)
    {
        order.DocumentType = "Order";
        var json = JsonSerializer.Serialize(order);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/salesDocuments", content);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<SalesDocument>(responseJson);
    }
    
    public async Task<List<SalesDocument>> GetCustomerOrdersAsync(string customerNo)
    {
        var filter = $"sellToCustomerNo eq '{customerNo}' and documentType eq 'Order'";
        var response = await _httpClient.GetAsync(
            $"{_baseUrl}/salesDocuments?$filter={filter}&$expand=salesLines"
        );
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<SalesDocument>>(json);
        return result.Value;
    }
}

public class SalesDocument
{
    public Guid SystemId { get; set; }
    public string DocumentType { get; set; }
    public string No { get; set; }
    public string SellToCustomerNo { get; set; }
    public string SellToCustomerName { get; set; }
    public DateTime PostingDate { get; set; }
    public DateTime? ShipmentDate { get; set; }
    public decimal Amount { get; set; }
    public decimal AmountIncludingVAT { get; set; }
    public List<SalesLine> SalesLines { get; set; }
}
```

## Document Types

- **Order** - Sales order
- **Quote** - Sales quotation
- **Invoice** - Sales invoice
- **Credit Memo** - Credit memo
- **Blanket Order** - Blanket order
- **Return Order** - Return order

## Business Logic Notes

- **Delayed Insert**: Create header first, then add lines
- **Customer Validation**: Customer must exist in BC
- **Address Selection**: Use `shipToCode` for predefined addresses
- **Duty Status**: Wine-specific duty paid/free classification
- **Credit Check**: BC may perform credit limit checks
- **Lines via Subpage**: Access lines via `$expand=salesLines`

## Validation Rules

- `sellToCustomerNo` must exist
- `documentType` is required
- `postingDate` required
- `shipmentDate` should be >= postingDate
- Valid `shipToCode` if specified

## Related APIs
- **Sales Lines**: Document line items
- **Customers**: Customer data
- **Web Orders**: Web-originated orders
- **Sales Invoices**: Posted invoices

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
