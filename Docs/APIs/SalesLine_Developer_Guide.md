# Sales Lines API - Developer Guide

## Overview
The Sales Lines API provides access to line items within sales documents, including products, quantities, prices, and discounts.

## API Endpoint Details
- **Endpoint**: `/salesDocumentLines`
- **Entity Name**: salesDocumentLine
- **Entity Set Name**: salesDocumentLines
- **Page ID**: 72205
- **Source Table**: Sales Line
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/salesDocumentLines
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `documentType` | Enum | Document type |
| `documentNo` | String | Document number |
| `lineNo` | Integer | Line number |
| `type` | Enum | Item, Resource, G/L Account, Fixed Asset, Charge (Item) |
| `no` | String | Item/resource number |
| `description` | String | Line description |
| `description2` | String | Extended description |
| `quantity` | Decimal | Quantity |
| `unitOfMeasureCode` | String | Unit of measure |
| `unitPrice` | Decimal | Unit price |
| `lineAmount` | Decimal | Line amount excl. VAT |
| `lineDiscountPercent` | Decimal | Line discount % |
| `lineDiscountAmount` | Decimal | Line discount amount |
| `amountIncludingVAT` | Decimal | Amount incl. VAT |
| `locationCode` | String | Location code |
| `shipmentDate` | Date | Planned shipment date |
| `qtyToShip` | Decimal | Quantity to ship |
| `quantityShipped` | Decimal | Quantity shipped |
| `quantityInvoiced` | Decimal | Quantity invoiced |
| `outstandingQuantity` | Decimal | Outstanding quantity |
| `tvtRotationNo` | String | Rotation number |

## Common Operations

### Add Line to Order
```http
POST /salesDocumentLines
Content-Type: application/json

{
  "documentType": "Order",
  "documentNo": "SO-12345",
  "lineNo": 10000,
  "type": "Item",
  "no": "WINE001",
  "description": "Premium Red Wine",
  "quantity": 12,
  "unitPrice": 45.00
}
```

### Get Lines for Document
```http
GET /salesDocumentLines?$filter=documentNo eq 'SO-12345'&$orderby=lineNo asc
```

### Update Line Quantity
```http
PATCH /salesDocumentLines({systemId})
Content-Type: application/json
If-Match: *

{
  "quantity": 24,
  "lineDiscountPercent": 10
}
```

### Delete Line
```http
DELETE /salesDocumentLines({systemId})
If-Match: *
```

## Code Examples

### JavaScript
```javascript
class SalesLineAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async addLine(lineData) {
    const response = await fetch(`${this.baseUrl}/salesDocumentLines`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify(lineData)
    });
    
    if (!response.ok) throw new Error(await response.text());
    return await response.json();
  }

  async getDocumentLines(documentNo) {
    const response = await fetch(
      `${this.baseUrl}/salesDocumentLines?$filter=documentNo eq '${documentNo}'&$orderby=lineNo asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async updateLine(systemId, updates) {
    const response = await fetch(`${this.baseUrl}/salesDocumentLines(${systemId})`, {
      method: 'PATCH',
      headers: { ...this.headers, 'If-Match': '*' },
      body: JSON.stringify(updates)
    });
    
    return await response.json();
  }

  async deleteLine(systemId) {
    await fetch(`${this.baseUrl}/salesDocumentLines(${systemId})`, {
      method: 'DELETE',
      headers: { ...this.headers, 'If-Match': '*' }
    });
  }

  calculateLineTotal(lines) {
    return lines.reduce((total, line) => total + line.lineAmount, 0);
  }
}

// Usage
const api = new SalesLineAPI(baseUrl, accessToken);

// Add multiple lines
const items = [
  { no: 'WINE001', quantity: 12, unitPrice: 45.00 },
  { no: 'WINE002', quantity: 6, unitPrice: 65.00 }
];

let lineNo = 10000;
for (const item of items) {
  await api.addLine({
    documentType: 'Order',
    documentNo: 'SO-12345',
    lineNo: lineNo,
    type: 'Item',
    ...item
  });
  lineNo += 10000;
}

// Get order total
const lines = await api.getDocumentLines('SO-12345');
const total = api.calculateLineTotal(lines);
console.log(`Order total: $${total.toFixed(2)}`);
```

### Python
```python
class SalesLineAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def add_line(self, line_data: dict) -> dict:
        response = requests.post(
            f'{self.base_url}/salesDocumentLines',
            headers=self.headers,
            json=line_data
        )
        response.raise_for_status()
        return response.json()
    
    def get_document_lines(self, document_no: str) -> list:
        response = requests.get(
            f'{self.base_url}/salesDocumentLines',
            headers=self.headers,
            params={
                '$filter': f"documentNo eq '{document_no}'",
                '$orderby': 'lineNo asc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def update_line(self, system_id: str, updates: dict) -> dict:
        headers = self.headers.copy()
        headers['If-Match'] = '*'
        
        response = requests.patch(
            f'{self.base_url}/salesDocumentLines({system_id})',
            headers=headers,
            json=updates
        )
        response.raise_for_status()
        return response.json()

# Usage
api = SalesLineAPI(base_url, access_token)

# Add lines to order
lines_to_add = [
    {'no': 'WINE001', 'quantity': 12, 'unitPrice': 45.00},
    {'no': 'WINE002', 'quantity': 6, 'unitPrice': 65.00}
]

line_no = 10000
for item in lines_to_add:
    api.add_line({
        'documentType': 'Order',
        'documentNo': 'SO-12345',
        'lineNo': line_no,
        'type': 'Item',
        **item
    })
    line_no += 10000
```

### C#
```csharp
public class SalesLineApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public async Task<SalesLine> AddLineAsync(SalesLine line)
    {
        var json = JsonSerializer.Serialize(line);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/salesDocumentLines", content);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<SalesLine>(responseJson);
    }
    
    public async Task<List<SalesLine>> GetDocumentLinesAsync(string documentNo)
    {
        var filter = $"documentNo eq '{documentNo}'";
        var response = await _httpClient.GetAsync(
            $"{_baseUrl}/salesDocumentLines?$filter={filter}&$orderby=lineNo asc"
        );
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<SalesLine>>(json);
        return result.Value;
    }
}

public class SalesLine
{
    public Guid SystemId { get; set; }
    public string DocumentType { get; set; }
    public string DocumentNo { get; set; }
    public int LineNo { get; set; }
    public string Type { get; set; }
    public string No { get; set; }
    public string Description { get; set; }
    public decimal Quantity { get; set; }
    public string UnitOfMeasureCode { get; set; }
    public decimal UnitPrice { get; set; }
    public decimal LineAmount { get; set; }
    public decimal LineDiscountPercent { get; set; }
}
```

## Line Types

- **Item** - Inventory item
- **Resource** - Resource/service
- **G/L Account** - General ledger account
- **Fixed Asset** - Fixed asset
- **Charge (Item)** - Item charge

## Business Logic Notes

- **Line Numbers**: Increment by 10000 (10000, 20000, 30000)
- **Pricing**: BC may apply customer-specific pricing
- **Discounts**: Line and invoice discounts may apply
- **Outstanding Qty**: Quantity - (Shipped + Invoiced)
- **Rotation Numbers**: Wine-specific tracking

## Validation Rules

- `documentType` and `documentNo` must reference existing document
- `lineNo` must be unique within document
- `type` and `no` required
- `quantity` must be > 0
- Item must be in stock (if inventory item)

## Related APIs
- **Sales Documents**: Parent document headers
- **Items**: Product information
- **Customers**: Pricing and discounts

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
