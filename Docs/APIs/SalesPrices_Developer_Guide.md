# Sales Prices API - Developer Guide

## Overview
The Sales Prices API provides access to legacy item pricing configured in Business Central, supporting customer-specific and general pricing.

## API Endpoint Details
- **Endpoint**: `/salesPrices`
- **Entity Name**: salesPrice
- **Entity Set Name**: salesPrices
- **Page ID**: 71984
- **Source Table**: Sales Price
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/salesPrices
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `itemNo` | String | Item number |
| `variantCode` | String | Item variant code |
| `salesType` | Enum | Sales type (Customer, Customer Price Group, All Customers) |
| `salesCode` | String | Customer/group code |
| `unitOfMeasureCode` | String | Unit of measure |
| `endingDate` | Date | Price effective end date |
| `currencyCode` | String | Currency code |
| `unitPrice` | Decimal | Unit price |
| `priceIncludesVAT` | Boolean | Price includes VAT flag |
| `minimumQuantity` | Decimal | Minimum quantity for price |
| `tvtwsWebLastModDateTime` | DateTime | Web last modified date/time |
| `tvtwsWebItemPublished` | Boolean | Web item published flag |
| `currencyCodeFilter` | String | Currency code filter |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemCreatedBy` | GUID | Created by user ID |
| `systemModifiedAt` | DateTime | Last modification |
| `systemModifiedBy` | GUID | Modified by user ID |

## Common Use Cases

### 1. Get Price for Item
```http
GET /salesPrices?$filter=itemNo eq 'WINE001' and salesType eq 'All Customers'
```

### 2. Get Customer-Specific Price
```http
GET /salesPrices?$filter=itemNo eq 'WINE001' and salesType eq 'Customer' and salesCode eq 'CUST001'
```

### 3. Get Active Prices
```http
GET /salesPrices?$filter=itemNo eq 'WINE001' and startingDate le 2025-10-14 and (endingDate eq null or endingDate ge 2025-10-14)
```

### 4. Get Quantity Break Prices
```http
GET /salesPrices?$filter=itemNo eq 'WINE001'&$orderby=minimumQuantity asc
```

## Code Examples

### JavaScript
```javascript
class SalesPriceAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getItemPrice(itemNo, customerNo = null, quantity = 1, date = null) {
    const today = date || new Date().toISOString().split('T')[0];
    
    // Build filter for customer-specific or general price
    let filter = `itemNo eq '${itemNo}' and minimumQuantity le ${quantity}`;
    filter += ` and startingDate le ${today}`;
    filter += ` and (endingDate eq null or endingDate ge ${today})`;
    
    if (customerNo) {
      filter += ` and ((salesType eq 'Customer' and salesCode eq '${customerNo}') or salesType eq 'All Customers')`;
    } else {
      filter += ` and salesType eq 'All Customers'`;
    }
    
    const response = await fetch(
      `${this.baseUrl}/salesPrices?$filter=${encodeURIComponent(filter)}&$orderby=salesType desc,minimumQuantity desc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    // Return most specific price (customer-specific > all customers, higher min qty > lower)
    return data.value[0];
  }

  async getQuantityBreakPrices(itemNo) {
    const response = await fetch(
      `${this.baseUrl}/salesPrices?$filter=itemNo eq '${itemNo}' and salesType eq 'All Customers'&$orderby=minimumQuantity asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getPriceForQuantity(itemNo, quantity, customerNo = null) {
    const priceRecord = await this.getItemPrice(itemNo, customerNo, quantity);
    return priceRecord ? priceRecord.unitPrice : null;
  }

  calculateLineTotal(unitPrice, quantity, allowLineDisc = false, lineDiscPct = 0) {
    let total = unitPrice * quantity;
    if (allowLineDisc && lineDiscPct > 0) {
      total *= (1 - lineDiscPct / 100);
    }
    return total;
  }
}

// Usage
const api = new SalesPriceAPI(baseUrl, accessToken);

// Get price for customer order
const price = await api.getItemPrice('WINE001', 'CUST001', 12);
console.log(`Price: $${price.unitPrice}`);
console.log(`Min Qty: ${price.minimumQuantity}`);

// Show quantity break pricing
const breaks = await api.getQuantityBreakPrices('WINE001');
breaks.forEach(priceBreak => {
  console.log(`${priceBreak.minimumQuantity}+ units: $${priceBreak.unitPrice}`);
});

// Calculate order line
const unitPrice = await api.getPriceForQuantity('WINE001', 24);
const lineTotal = api.calculateLineTotal(unitPrice, 24);
console.log(`Total: $${lineTotal.toFixed(2)}`);
```

### Python
```python
from datetime import date, datetime
from typing import Optional, List

class SalesPriceAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_item_price(self, item_no: str, customer_no: Optional[str] = None, 
                       quantity: float = 1, price_date: Optional[date] = None) -> Optional[dict]:
        today = (price_date or date.today()).isoformat()
        
        filter_parts = [
            f"itemNo eq '{item_no}'",
            f"minimumQuantity le {quantity}",
            f"startingDate le {today}",
            f"(endingDate eq null or endingDate ge {today})"
        ]
        
        if customer_no:
            filter_parts.append(
                f"((salesType eq 'Customer' and salesCode eq '{customer_no}') or salesType eq 'All Customers')"
            )
        else:
            filter_parts.append("salesType eq 'All Customers'")
        
        filter_query = ' and '.join(filter_parts)
        
        response = requests.get(
            f'{self.base_url}/salesPrices',
            headers=self.headers,
            params={
                '$filter': filter_query,
                '$orderby': 'salesType desc,minimumQuantity desc'
            }
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None
    
    def get_quantity_break_prices(self, item_no: str) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/salesPrices',
            headers=self.headers,
            params={
                '$filter': f"itemNo eq '{item_no}' and salesType eq 'All Customers'",
                '$orderby': 'minimumQuantity asc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_price_for_quantity(self, item_no: str, quantity: float, 
                               customer_no: Optional[str] = None) -> Optional[float]:
        price_record = self.get_item_price(item_no, customer_no, quantity)
        return price_record['unitPrice'] if price_record else None
    
    def calculate_line_total(self, unit_price: float, quantity: float, 
                            allow_line_disc: bool = False, line_disc_pct: float = 0) -> float:
        total = unit_price * quantity
        if allow_line_disc and line_disc_pct > 0:
            total *= (1 - line_disc_pct / 100)
        return total

# Usage
api = SalesPriceAPI(base_url, access_token)

# Get best price for customer and quantity
price = api.get_item_price('WINE001', customer_no='CUST001', quantity=24)
if price:
    print(f"Price: ${price['unitPrice']:.2f}")
    print(f"Min Qty: {price['minimumQuantity']}")
    print(f"Allows Line Discount: {price['allowLineDisc']}")

# Display quantity break pricing table
breaks = api.get_quantity_break_prices('WINE001')
print("\nQuantity Break Pricing:")
for price_break in breaks:
    print(f"{price_break['minimumQuantity']:>3.0f}+ units: ${price_break['unitPrice']:>6.2f}")
```

### C#
```csharp
public class SalesPriceApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public SalesPriceApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<SalesPrice> GetItemPriceAsync(string itemNo, string customerNo = null, 
        decimal quantity = 1, DateTime? priceDate = null)
    {
        var today = (priceDate ?? DateTime.Today).ToString("yyyy-MM-dd");
        
        var filter = $"itemNo eq '{itemNo}' and minimumQuantity le {quantity} " +
                     $"and startingDate le {today} " +
                     $"and (endingDate eq null or endingDate ge {today})";
        
        if (!string.IsNullOrEmpty(customerNo))
        {
            filter += $" and ((salesType eq 'Customer' and salesCode eq '{customerNo}') or salesType eq 'All Customers')";
        }
        else
        {
            filter += " and salesType eq 'All Customers'";
        }
        
        var url = $"{_baseUrl}/salesPrices?$filter={Uri.EscapeDataString(filter)}&$orderby=salesType desc,minimumQuantity desc";
        var response = await _httpClient.GetAsync(url);
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<SalesPrice>>(json);
        return result.Value.FirstOrDefault();
    }
    
    public async Task<List<SalesPrice>> GetQuantityBreakPricesAsync(string itemNo)
    {
        var filter = $"itemNo eq '{itemNo}' and salesType eq 'All Customers'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/salesPrices?$filter={filter}&$orderby=minimumQuantity asc");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<SalesPrice>>(json);
        return result.Value;
    }
}

public class SalesPrice
{
    public Guid SystemId { get; set; }
    public string ItemNo { get; set; }
    public string SalesType { get; set; }
    public string SalesCode { get; set; }
    public DateTime StartingDate { get; set; }
    public string CurrencyCode { get; set; }
    public string VariantCode { get; set; }
    public string UnitOfMeasureCode { get; set; }
    public decimal MinimumQuantity { get; set; }
    public decimal UnitPrice { get; set; }
    public bool PriceIncludesVAT { get; set; }
    public bool AllowInvoiceDisc { get; set; }
    public bool AllowLineDisc { get; set; }
    public DateTime? EndingDate { get; set; }
}
```

## Sales Type Values

- `All Customers` - General pricing for all customers
- `Customer` - Customer-specific pricing
- `Customer Price Group` - Pricing by customer group

## Business Logic Notes

- **Price Priority**: Customer-specific > Customer Price Group > All Customers
- **Quantity Breaks**: Higher minimum quantity prices take precedence
- **Date Effective**: Check `startingDate` and `endingDate`
- **Legacy System**: This is the old pricing system (see Sales List Prices for modern pricing)
- **VAT Handling**: Check `priceIncludesVAT` flag for tax calculations

## Performance Tips

1. **Filter by Date**: Always include date range filters
2. **Order Results**: Use `$orderby` to get best price first
3. **Cache Prices**: Cache for session or short period
4. **Batch Lookups**: Look up multiple items in parallel

## Related APIs
- **Sales List Prices**: Modern price list system
- **Items**: Item information
- **Web Products**: Product catalog

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
