# Web Order Lines API - Developer Guide

## Overview
The Web Order Lines API provides full access to line items within web orders, including product details, quantities, pricing, and special references like paid reserves.

## API Endpoint Details
- **Endpoint**: `/webOrderLines`
- **Entity Name**: webOrderLine
- **Entity Set Name**: webOrderLines
- **Page ID**: 71987
- **Source Table**: TVTWS Web Order Line
- **API Group**: webbevica
- **Publisher**: tvisiontech
- **Version**: v2.0

## Permissions
- **Insert**: Allowed
- **Modify**: Allowed
- **Delete**: Not Allowed
- **Read**: Allowed

## Base URL
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/webOrderLines
```

## Field Reference

| Field Name                     | Type         | Description                       |
|--------------------------------|--------------|-----------------------------------|
| orderGroup                     | Code[50]     | Key                               |
| orderId                        | Code[50]     | Key (Unique External Reference)   |
| lineId                         | Code[50]     | Key (Unique External Reference)   |
| type                           | Enum         | Standard                          |
| no                             | Code[20]     | Standard                          |
| productId                      | Code[50]     | Web Specific                      |
| transactionType                | Enum         | Bevica                            |
| unitOfMeasureId                | Code[50]     | Web Specific                      |
| unitOfMeasureCode              | Code[10]     | Standard                          |
| description                    | Text[50]     | Standard                          |
| description2                   | Text[50]     | Standard                          |
| quantity                       | Decimal      | Standard                          |
| unitPrice                      | Decimal      | Standard                          |
| lineDiscountAmount             | Decimal      | Standard                          |
| lineDiscountPercent            | Decimal      | Standard                          |
| shortcutDimension1Code         | Code[20]     | Standard                          |
| shortcutDimension2Code         | Code[20]     | Standard                          |
| unitCost                       | Decimal      | Standard                          |
| variantCode                    | Code[10]     | Standard                          |
| itemCategoryCode               | Code[20]     | Standard                          |
| requestedDeliveryDate          | Date         | Standard                          |
| purchasingCode                 | Code[20]     | Standard                          |
| paidReserveNo                  | Code[30]     | Bevica                            |
| unpaidReserves                 | Boolean      | Bevica                            |
| brokingPaidReserveNo           | Code[30]     | Bevica                            |
| decimal01                      | Decimal      | Web Specific                      |
| integer01                      | Integer      | Web Specific                      |
| date01                         | Date         | Web Specific                      |
| code01                         | Code[20]     | Web Specific                      |
| time01                         | Time         | Web Specific                      |
| dateTime01                     | DateTime     | Web Specific                      |
| text01                         | Text[50]     | Web Specific                      |
| boolean01                      | Boolean      | Web Specific                      |
| decimal02                      | Decimal      | Web Specific                      |
| integer02                      | Integer      | Web Specific                      |
| date02                         | Date         | Web Specific                      |
| code02                         | Code[20]     | Web Specific                      |
| time02                         | Time         | Web Specific                      |
| dateTime02                     | DateTime     | Web Specific                      |
| text02                         | Text[50]     | Web Specific                      |
| boolean02                      | Boolean      | Web Specific                      |
| systemId                       | Guid         | System field                      |
| systemCreatedAt                | DateTime     | System field                      |
| systemCreatedBy                | Guid         | System field                      |
| systemModifiedAt               | DateTime     | System field                      |
| systemModifiedBy               | Guid         | System field                      |


## Common Operations

### Create Order Line
```http
POST /webOrderLines
Content-Type: application/json

{
  "orderGroup": "WEB",
  "orderId": "WEB-2025-12345",
  "lineId": 10000,
  "productId": "ITEM001",
  "transactionType": "Sale",
  "unitOfMeasureId": "CASE",
  "description": "Premium Red Wine",
  "quantity": 6,
  "unitPrice": 45.00
}
```

### Update Order Line Quantity
```http
PATCH /webOrderLines({systemId})
Content-Type: application/json
If-Match: *

{
  "quantity": 12,
  "unitPrice": 42.00
}
```

### Get Lines for an Order
```http
GET /webOrderLines?$filter=orderId eq 'WEB-2025-12345'
```

## Code Examples

### JavaScript
```javascript
class WebOrderLineAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async addLine(lineData) {
    const response = await fetch(`${this.baseUrl}/webOrderLines`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify(lineData)
    });
    
    if (!response.ok) {
      throw new Error(`Failed to add line: ${await response.text()}`);
    }
    
    return await response.json();
  }

  async getOrderLines(orderId) {
    const response = await fetch(
      `${this.baseUrl}/webOrderLines?$filter=orderId eq '${orderId}'&$orderby=lineId asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async updateLine(systemId, updates) {
    const response = await fetch(`${this.baseUrl}/webOrderLines(${systemId})`, {
      method: 'PATCH',
      headers: {
        ...this.headers,
        'If-Match': '*'
      },
      body: JSON.stringify(updates)
    });
    
    return await response.json();
  }

  async calculateOrderTotal(orderId) {
    const lines = await this.getOrderLines(orderId);
    return lines.reduce((total, line) => total + (line.quantity * line.unitPrice), 0);
  }
}

// Usage
const api = new WebOrderLineAPI(baseUrl, accessToken);

// Add line
await api.addLine({
  orderGroup: 'WEB',
  orderId: 'WEB-2025-12345',
  lineId: 10000,
  productId: 'WINE001',
  quantity: 6,
  unitPrice: 45.00
});

// Get order total
const total = await api.calculateOrderTotal('WEB-2025-12345');
console.log(`Order total: ${total}`);
```

### Python
```python
class WebOrderLineAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def add_line(self, line_data: dict) -> dict:
        response = requests.post(
            f'{self.base_url}/webOrderLines',
            headers=self.headers,
            json=line_data
        )
        response.raise_for_status()
        return response.json()
    
    def get_order_lines(self, order_id: str) -> list:
        response = requests.get(
            f'{self.base_url}/webOrderLines',
            headers=self.headers,
            params={
                '$filter': f"orderId eq '{order_id}'",
                '$orderby': 'lineId asc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def update_line(self, system_id: str, updates: dict) -> dict:
        headers = self.headers.copy()
        headers['If-Match'] = '*'
        
        response = requests.patch(
            f'{self.base_url}/webOrderLines({system_id})',
            headers=headers,
            json=updates
        )
        response.raise_for_status()
        return response.json()
    
    def calculate_order_total(self, order_id: str) -> float:
        lines = self.get_order_lines(order_id)
        return sum(line['quantity'] * line['unitPrice'] for line in lines)

# Usage
api = WebOrderLineAPI(base_url, access_token)

# Add multiple lines
lines = [
    {'productId': 'WINE001', 'quantity': 6, 'unitPrice': 45.00},
    {'productId': 'WINE002', 'quantity': 12, 'unitPrice': 35.00}
]

for idx, line in enumerate(lines, start=1):
    api.add_line({
        'orderGroup': 'WEB',
        'orderId': 'WEB-2025-12345',
        'lineId': idx * 10000,
        **line
    })
```

### C#
```csharp
public class WebOrderLineApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public WebOrderLineApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<WebOrderLine> AddLineAsync(WebOrderLine line)
    {
        var json = JsonSerializer.Serialize(line);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/webOrderLines", content);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<WebOrderLine>(responseJson);
    }
    
    public async Task<List<WebOrderLine>> GetOrderLinesAsync(string orderId)
    {
        var filter = $"orderId eq '{orderId}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/webOrderLines?$filter={filter}&$orderby=lineId asc");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebOrderLine>>(json);
        return result.Value;
    }
    
    public async Task<decimal> CalculateOrderTotalAsync(string orderId)
    {
        var lines = await GetOrderLinesAsync(orderId);
        return lines.Sum(l => l.Quantity * l.UnitPrice);
    }
}

public class WebOrderLine
{
    public Guid SystemId { get; set; }
    public string OrderGroup { get; set; }
    public string OrderId { get; set; }
    public int LineId { get; set; }
    public string ProductId { get; set; }
    public string TransactionType { get; set; }
    public string UnitOfMeasureId { get; set; }
    public string Description { get; set; }
    public decimal Quantity { get; set; }
    public decimal UnitPrice { get; set; }
    public string PaidReserveNo { get; set; }
    public bool UnpaidReserves { get; set; }
}
```

## Business Logic Notes

- **Line IDs**: Typically incremented by 10000 (10000, 20000, 30000)
- **Order Reference**: Lines linked to order via `orderGroup` and `orderId`
- **Paid Reserves**: `paidReserveNo` references allocated inventory
- **Transaction Types**: Defines the nature of the transaction (Sale, Return, etc.)
- **Pricing**: Line total = quantity × unitPrice

## Validation Rules

- `orderGroup` and `orderId` must reference existing order
- `lineId` must be unique within order
- `quantity` must be > 0
- `unitPrice` must be >= 0

## Related APIs
- **Web Orders**: Parent order headers
- **Items**: Product information
- **Paid Reserves**: Inventory allocation
- **Web Stock**: Stock availability

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
