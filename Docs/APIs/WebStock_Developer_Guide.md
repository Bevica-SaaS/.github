# Web Stock API - Developer Guide

## Overview
The Web Stock API provides real-time stock availability information for items across locations, essential for e-commerce inventory management.

## API Endpoint Details
- **Endpoint**: `/webStocks`
- **Entity Name**: webStock
- **Entity Set Name**: webStocks
- **Page ID**: 71986
- **Source Table**: TVTWS Web Stock
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/webStocks
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `locationCode` | String | Warehouse/location code |
| `itemNo` | String | Item number |
| `variantCode` | String | Variant code |
| `unitOfMeasureCode` | String | Unit of measure |
| `qtyPerUnitOfMeasure` | Decimal | Quantity per unit of measure |
| `stockAvailableBase` | Decimal | Stock available (base) |
| `lastModDateTime` | DateTime | Last modification date/time |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemCreatedBy` | GUID | Created by user ID |
| `systemModifiedAt` | DateTime | Last modification |
| `systemModifiedBy` | GUID | Modified by user ID |

## Common Use Cases

### 1. Get Stock for Item
```http
GET /webStocks?$filter=itemNo eq 'WINE001' and published eq true
```

### 2. Get Available Stock Only
```http
GET /webStocks?$filter=itemNo eq 'WINE001' and availableToPromise gt 0
```

### 3. Get Multi-Location Stock
```http
GET /webStocks?$filter=itemNo eq 'WINE001'&$select=locationCode,locationName,availableToPromise
```

### 4. Get Low Stock Items
```http
GET /webStocks?$filter=availableToPromise lt 12 and availableToPromise gt 0 and published eq true
```

### 5. Check Stock Availability
```http
GET /webStocks?$filter=itemNo eq 'WINE001'&$select=availableToPromise,nextReceiptDate,nextReceiptQty
```

## Code Examples

### JavaScript
```javascript
class WebStockAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getItemStock(itemNo) {
    const response = await fetch(
      `${this.baseUrl}/webStocks?$filter=itemNo eq '${itemNo}' and published eq true`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getTotalAvailableStock(itemNo) {
    const stockRecords = await this.getItemStock(itemNo);
    return stockRecords.reduce((total, record) => total + record.availableToPromise, 0);
  }

  async isInStock(itemNo, requiredQty = 1) {
    const totalStock = await this.getTotalAvailableStock(itemNo);
    return totalStock >= requiredQty;
  }

  async getStockByLocation(itemNo, locationCode) {
    const response = await fetch(
      `${this.baseUrl}/webStocks?$filter=itemNo eq '${itemNo}' and locationCode eq '${locationCode}'`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value[0];
  }

  async getLowStockItems(threshold = 12) {
    const response = await fetch(
      `${this.baseUrl}/webStocks?$filter=availableToPromise lt ${threshold} and availableToPromise gt 0 and published eq true`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getStockWithNextReceipt(itemNo) {
    const response = await fetch(
      `${this.baseUrl}/webStocks?$filter=itemNo eq '${itemNo}'&$select=locationCode,availableToPromise,nextReceiptDate,nextReceiptQty`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  getStockStatus(availableQty) {
    if (availableQty <= 0) return { status: 'out_of_stock', message: 'Out of Stock', class: 'danger' };
    if (availableQty < 6) return { status: 'low_stock', message: `Only ${availableQty} left`, class: 'warning' };
    if (availableQty < 24) return { status: 'limited', message: 'Limited Stock', class: 'info' };
    return { status: 'in_stock', message: 'In Stock', class: 'success' };
  }

  async checkMultipleItems(itemNos) {
    const results = await Promise.all(
      itemNos.map(async itemNo => ({
        itemNo,
        stock: await this.getTotalAvailableStock(itemNo),
        inStock: await this.isInStock(itemNo)
      }))
    );
    return results;
  }
}

// Usage
const api = new WebStockAPI(baseUrl, accessToken);

// Check single item
const stock = await api.getTotalAvailableStock('WINE001');
console.log(`Available: ${stock} units`);

// Check if can fulfill order
const canFulfill = await api.isInStock('WINE001', 6);
if (canFulfill) {
  console.log('Stock available for order');
} else {
  console.log('Insufficient stock');
}

// Get stock status for display
const totalStock = await api.getTotalAvailableStock('WINE001');
const status = api.getStockStatus(totalStock);
console.log(`Status: ${status.message}`);

// Check multiple items at once
const items = ['WINE001', 'WINE002', 'WINE003'];
const stockCheck = await api.checkMultipleItems(items);
stockCheck.forEach(item => {
  console.log(`${item.itemNo}: ${item.stock} (${item.inStock ? 'Available' : 'Out of Stock'})`);
});

// Get low stock alerts
const lowStock = await api.getLowStockItems(12);
console.log(`${lowStock.length} items low on stock`);
```

### Python
```python
from typing import List, Dict, Optional
from datetime import datetime

class WebStockAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_item_stock(self, item_no: str) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/webStocks',
            headers=self.headers,
            params={
                '$filter': f"itemNo eq '{item_no}' and published eq true"
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_total_available_stock(self, item_no: str) -> float:
        stock_records = self.get_item_stock(item_no)
        return sum(record['availableToPromise'] for record in stock_records)
    
    def is_in_stock(self, item_no: str, required_qty: float = 1) -> bool:
        total_stock = self.get_total_available_stock(item_no)
        return total_stock >= required_qty
    
    def get_stock_by_location(self, item_no: str, location_code: str) -> Optional[dict]:
        response = requests.get(
            f'{self.base_url}/webStocks',
            headers=self.headers,
            params={
                '$filter': f"itemNo eq '{item_no}' and locationCode eq '{location_code}'"
            }
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None
    
    def get_low_stock_items(self, threshold: int = 12) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/webStocks',
            headers=self.headers,
            params={
                '$filter': f'availableToPromise lt {threshold} and availableToPromise gt 0 and published eq true'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_stock_status(self, available_qty: float) -> dict:
        if available_qty <= 0:
            return {'status': 'out_of_stock', 'message': 'Out of Stock', 'class': 'danger'}
        elif available_qty < 6:
            return {'status': 'low_stock', 'message': f'Only {available_qty:.0f} left', 'class': 'warning'}
        elif available_qty < 24:
            return {'status': 'limited', 'message': 'Limited Stock', 'class': 'info'}
        return {'status': 'in_stock', 'message': 'In Stock', 'class': 'success'}
    
    def check_cart_availability(self, cart_items: List[Dict[str, any]]) -> Dict[str, any]:
        """Check if all cart items are available"""
        results = []
        all_available = True
        
        for item in cart_items:
            item_no = item['itemNo']
            quantity = item['quantity']
            available = self.get_total_available_stock(item_no)
            in_stock = available >= quantity
            
            results.append({
                'itemNo': item_no,
                'requested': quantity,
                'available': available,
                'inStock': in_stock
            })
            
            if not in_stock:
                all_available = False
        
        return {
            'allAvailable': all_available,
            'items': results
        }

# Usage
api = WebStockAPI(base_url, access_token)

# Product page stock display
item_no = 'WINE001'
stock = api.get_total_available_stock(item_no)
status = api.get_stock_status(stock)
print(f"Stock: {stock} - {status['message']}")

# Cart validation
cart = [
    {'itemNo': 'WINE001', 'quantity': 6},
    {'itemNo': 'WINE002', 'quantity': 12},
    {'itemNo': 'WINE003', 'quantity': 6}
]

availability = api.check_cart_availability(cart)
if availability['allAvailable']:
    print("All items available - proceed to checkout")
else:
    print("Some items unavailable:")
    for item in availability['items']:
        if not item['inStock']:
            print(f"  {item['itemNo']}: Need {item['requested']}, have {item['available']}")

# Low stock report
low_stock = api.get_low_stock_items(12)
print(f"\nLow Stock Alert: {len(low_stock)} items")
for item in low_stock:
    print(f"{item['itemNo']}: {item['availableToPromise']} units")
```

### C#
```csharp
public class WebStockApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public WebStockApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<List<WebStock>> GetItemStockAsync(string itemNo)
    {
        var filter = $"itemNo eq '{itemNo}' and published eq true";
        var response = await _httpClient.GetAsync($"{_baseUrl}/webStocks?$filter={filter}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebStock>>(json);
        return result.Value;
    }
    
    public async Task<decimal> GetTotalAvailableStockAsync(string itemNo)
    {
        var stockRecords = await GetItemStockAsync(itemNo);
        return stockRecords.Sum(s => s.AvailableToPromise);
    }
    
    public async Task<bool> IsInStockAsync(string itemNo, decimal requiredQty = 1)
    {
        var totalStock = await GetTotalAvailableStockAsync(itemNo);
        return totalStock >= requiredQty;
    }
    
    public async Task<List<WebStock>> GetLowStockItemsAsync(decimal threshold = 12)
    {
        var filter = $"availableToPromise lt {threshold} and availableToPromise gt 0 and published eq true";
        var response = await _httpClient.GetAsync($"{_baseUrl}/webStocks?$filter={filter}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebStock>>(json);
        return result.Value;
    }
    
    public StockStatus GetStockStatus(decimal availableQty)
    {
        if (availableQty <= 0)
            return new StockStatus { Status = "out_of_stock", Message = "Out of Stock", CssClass = "danger" };
        if (availableQty < 6)
            return new StockStatus { Status = "low_stock", Message = $"Only {availableQty} left", CssClass = "warning" };
        if (availableQty < 24)
            return new StockStatus { Status = "limited", Message = "Limited Stock", CssClass = "info" };
        
        return new StockStatus { Status = "in_stock", Message = "In Stock", CssClass = "success" };
    }
}

public class WebStock
{
    public Guid SystemId { get; set; }
    public string ItemNo { get; set; }
    public string Description { get; set; }
    public string LocationCode { get; set; }
    public string LocationName { get; set; }
    public string UnitOfMeasureCode { get; set; }
    public decimal Inventory { get; set; }
    public decimal QtyOnSalesOrder { get; set; }
    public decimal QtyOnPurchOrder { get; set; }
    public decimal ProjectedAvailable { get; set; }
    public decimal AvailableToPromise { get; set; }
    public DateTime? NextReceiptDate { get; set; }
    public decimal? NextReceiptQty { get; set; }
    public bool Published { get; set; }
    public bool Deleted { get; set; }
}

public class StockStatus
{
    public string Status { get; set; }
    public string Message { get; set; }
    public string CssClass { get; set; }
}
```

## Stock Calculations

- **Inventory**: Physical stock on hand
- **Available to Promise (ATP)**: Inventory - QtyOnSalesOrder
- **Projected Available**: Inventory + QtyOnPurchOrder - QtyOnSalesOrder

## Business Logic Notes

- **Multi-Location**: Items may have stock in multiple locations
- **ATP is Key**: Use `availableToPromise` for order fulfillment
- **Read-Only**: Stock updated by BC inventory transactions
- **Real-Time**: Stock reflects current BC inventory position
- **Published Filter**: Always filter by `published eq true`

## Display Recommendations

- **> 24 units**: "In Stock"
- **6-23 units**: "Limited Stock"
- **1-5 units**: "Only X left"
- **0 units**: "Out of Stock"
- **Next Receipt**: Show expected date if stock is low

## Performance Tips

1. **Cache Stock Data**: Cache for 5-15 minutes
2. **Aggregate ATP**: Sum `availableToPromise` across locations
3. **Batch Checks**: Check multiple items in parallel
4. **Select Fields**: Only request needed fields
5. **Filter Published**: Always include `published eq true`

## Related APIs
- **Items**: Item details
- **Web Products**: Marketing data
- **Web Orders**: Order placement

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
