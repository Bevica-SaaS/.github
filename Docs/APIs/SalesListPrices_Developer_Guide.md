# Sales List Prices API - Developer Guide

## Overview
The Sales List Prices API provides access to the modern price list system in Business Central, supporting complex pricing scenarios with price lists, customer groups, and campaigns.

## API Endpoint Details
- **Endpoint**: `/salesListPrices`
- **Entity Name**: salesListPrice
- **Entity Set Name**: salesListPrices
- **Page ID**: 71996
- **Source Table**: Price list line
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/salesListPrices
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `itemNo` | String | Item number (Asset No.) |
| `variantCode` | String | Item variant code |
| `salesType` | Enum | Sales type (Asset Type) |
| `assignToType` | Enum | Assign-to type (Source Type) |
| `assignToNo` | String | Assign-to number (Source No.) |
| `salesCode` | String | Sales code (Price List Code) |
| `unitOfMeasureCode` | String | Unit of measure |
| `startingDate` | Date | Effective start date |
| `endingDate` | Date | Effective end date |
| `currencyCode` | String | Currency code |
| `unitPrice` | Decimal | Unit price |
| `priceIncludesVAT` | Boolean | Price includes VAT |
| `minimumQuantity` | Decimal | Minimum quantity |
| `lineDiscountPercen` | Decimal | Line discount percentage |
| `tvtwsWebLastModDateTime` | DateTime | Web last modified date/time |
| `tvtwsWebItemPublished` | Boolean | Web item published flag |
| `currencyCodeFilter` | String | Currency code filter |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemCreatedBy` | GUID | Created by user ID |
| `systemModifiedAt` | DateTime | Last modification |
| `systemModifiedBy` | GUID | Modified by user ID |

## Common Use Cases

### 1. Get Active Prices for Item
```http
GET /salesListPrices?$filter=assetNo eq 'WINE001' and status eq 'Active' and assetType eq 'Item'
```

### 2. Get Customer-Specific Price List
```http
GET /salesListPrices?$filter=sourceType eq 'Customer' and sourceNo eq 'CUST001' and status eq 'Active'
```

### 3. Get Campaign Prices
```http
GET /salesListPrices?$filter=sourceType eq 'Campaign' and status eq 'Active'
```

### 4. Get Prices from Specific Price List
```http
GET /salesListPrices?$filter=priceListCode eq 'AUTUMN2025' and status eq 'Active'
```

## Code Examples

### JavaScript
```javascript
class SalesListPriceAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getItemPrices(itemNo, customerNo = null, quantity = 1, date = null) {
    const today = date || new Date().toISOString().split('T')[0];
    
    let filter = `assetNo eq '${itemNo}' and assetType eq 'Item' and status eq 'Active'`;
    filter += ` and minimumQuantity le ${quantity}`;
    filter += ` and (startingDate eq null or startingDate le ${today})`;
    filter += ` and (endingDate eq null or endingDate ge ${today})`;
    
    if (customerNo) {
      filter += ` and (sourceType eq 'All Customers' or (sourceType eq 'Customer' and sourceNo eq '${customerNo}'))`;
    } else {
      filter += ` and sourceType eq 'All Customers'`;
    }
    
    const response = await fetch(
      `${this.baseUrl}/salesListPrices?$filter=${encodeURIComponent(filter)}&$orderby=sourceType desc,minimumQuantity desc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getBestPrice(itemNo, customerNo = null, quantity = 1) {
    const prices = await this.getItemPrices(itemNo, customerNo, quantity);
    
    // Priority: Customer-specific > All Customers, higher min qty > lower
    const bestPrice = prices[0];
    return bestPrice ? bestPrice.unitPrice : null;
  }

  async getPriceListDetails(priceListCode) {
    const response = await fetch(
      `${this.baseUrl}/salesListPrices?$filter=priceListCode eq '${priceListCode}' and status eq 'Active'`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getCampaignPrices() {
    const today = new Date().toISOString().split('T')[0];
    const filter = `sourceType eq 'Campaign' and status eq 'Active' and (startingDate eq null or startingDate le ${today}) and (endingDate eq null or endingDate ge ${today})`;
    
    const response = await fetch(
      `${this.baseUrl}/salesListPrices?$filter=${encodeURIComponent(filter)}`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getQuantityBreakPrices(itemNo) {
    const filter = `assetNo eq '${itemNo}' and status eq 'Active' and sourceType eq 'All Customers'`;
    
    const response = await fetch(
      `${this.baseUrl}/salesListPrices?$filter=${encodeURIComponent(filter)}&$orderby=minimumQuantity asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }
}

// Usage
const api = new SalesListPriceAPI(baseUrl, accessToken);

// Get best price for customer
const price = await api.getBestPrice('WINE001', 'CUST001', 12);
console.log(`Best price: $${price}`);

// Show quantity breaks
const breaks = await api.getQuantityBreakPrices('WINE001');
console.log('\nQuantity Break Pricing:');
breaks.forEach(priceBreak => {
  console.log(`${priceBreak.minimumQuantity}+ @ $${priceBreak.unitPrice} (${priceBreak.priceListCode})`);
});

// Get campaign prices
const campaigns = await api.getCampaignPrices();
console.log(`\nActive campaign prices: ${campaigns.length}`);
campaigns.forEach(item => {
  console.log(`${item.assetNo}: $${item.unitPrice} (${item.priceListCode})`);
});
```

### Python
```python
from datetime import date
from typing import Optional, List

class SalesListPriceAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_item_prices(self, item_no: str, customer_no: Optional[str] = None,
                       quantity: float = 1, price_date: Optional[date] = None) -> List[dict]:
        today = (price_date or date.today()).isoformat()
        
        filter_parts = [
            f"assetNo eq '{item_no}'",
            "assetType eq 'Item'",
            "status eq 'Active'",
            f"minimumQuantity le {quantity}",
            f"(startingDate eq null or startingDate le {today})",
            f"(endingDate eq null or endingDate ge {today})"
        ]
        
        if customer_no:
            filter_parts.append(
                f"(sourceType eq 'All Customers' or (sourceType eq 'Customer' and sourceNo eq '{customer_no}'))"
            )
        else:
            filter_parts.append("sourceType eq 'All Customers'")
        
        filter_query = ' and '.join(filter_parts)
        
        response = requests.get(
            f'{self.base_url}/salesListPrices',
            headers=self.headers,
            params={
                '$filter': filter_query,
                '$orderby': 'sourceType desc,minimumQuantity desc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_best_price(self, item_no: str, customer_no: Optional[str] = None,
                      quantity: float = 1) -> Optional[float]:
        prices = self.get_item_prices(item_no, customer_no, quantity)
        return prices[0]['unitPrice'] if prices else None
    
    def get_campaign_prices(self) -> List[dict]:
        today = date.today().isoformat()
        filter_query = (
            f"sourceType eq 'Campaign' and status eq 'Active' "
            f"and (startingDate eq null or startingDate le {today}) "
            f"and (endingDate eq null or endingDate ge {today})"
        )
        
        response = requests.get(
            f'{self.base_url}/salesListPrices',
            headers=self.headers,
            params={'$filter': filter_query}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_quantity_break_prices(self, item_no: str) -> List[dict]:
        filter_query = f"assetNo eq '{item_no}' and status eq 'Active' and sourceType eq 'All Customers'"
        
        response = requests.get(
            f'{self.base_url}/salesListPrices',
            headers=self.headers,
            params={
                '$filter': filter_query,
                '$orderby': 'minimumQuantity asc'
            }
        )
        response.raise_for_status()
        return response.json()['value']

# Usage
api = SalesListPriceAPI(base_url, access_token)

# Get best price
price = api.get_best_price('WINE001', customer_no='CUST001', quantity=24)
print(f"Best price: ${price:.2f}")

# Display quantity breaks
breaks = api.get_quantity_break_prices('WINE001')
print("\nQuantity Breaks:")
for pb in breaks:
    print(f"{pb['minimumQuantity']:>3.0f}+ @ ${pb['unitPrice']:>6.2f} ({pb['priceListCode']})")

# Show active campaigns
campaigns = api.get_campaign_prices()
print(f"\nActive Campaigns: {len(campaigns)} special prices")
```

### C#
```csharp
public class SalesListPriceApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public SalesListPriceApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<List<SalesListPrice>> GetItemPricesAsync(string itemNo, 
        string customerNo = null, decimal quantity = 1, DateTime? priceDate = null)
    {
        var today = (priceDate ?? DateTime.Today).ToString("yyyy-MM-dd");
        
        var filter = $"assetNo eq '{itemNo}' and assetType eq 'Item' and status eq 'Active' " +
                     $"and minimumQuantity le {quantity} " +
                     $"and (startingDate eq null or startingDate le {today}) " +
                     $"and (endingDate eq null or endingDate ge {today})";
        
        if (!string.IsNullOrEmpty(customerNo))
        {
            filter += $" and (sourceType eq 'All Customers' or (sourceType eq 'Customer' and sourceNo eq '{customerNo}'))";
        }
        else
        {
            filter += " and sourceType eq 'All Customers'";
        }
        
        var url = $"{_baseUrl}/salesListPrices?$filter={Uri.EscapeDataString(filter)}&$orderby=sourceType desc,minimumQuantity desc";
        var response = await _httpClient.GetAsync(url);
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<SalesListPrice>>(json);
        return result.Value;
    }
    
    public async Task<decimal?> GetBestPriceAsync(string itemNo, string customerNo = null, decimal quantity = 1)
    {
        var prices = await GetItemPricesAsync(itemNo, customerNo, quantity);
        return prices.FirstOrDefault()?.UnitPrice;
    }
}

public class SalesListPrice
{
    public Guid SystemId { get; set; }
    public string PriceListCode { get; set; }
    public int LineNo { get; set; }
    public string SourceType { get; set; }
    public string SourceNo { get; set; }
    public string AssetType { get; set; }
    public string AssetNo { get; set; }
    public string VariantCode { get; set; }
    public string UnitOfMeasureCode { get; set; }
    public decimal MinimumQuantity { get; set; }
    public string AmountType { get; set; }
    public decimal UnitPrice { get; set; }
    public decimal DirectUnitPrice { get; set; }
    public bool AllowInvoiceDisc { get; set; }
    public bool AllowLineDisc { get; set; }
    public DateTime? StartingDate { get; set; }
    public DateTime? EndingDate { get; set; }
    public string Status { get; set; }
    public bool PriceIncludesVAT { get; set; }
}
```

## Source Type Priority

1. **Customer** - Highest priority
2. **Customer Price Group** - Mid priority
3. **Campaign** - Campaign-specific
4. **All Customers** - Lowest priority (default)

## Status Values

- `Draft` - Not yet active
- `Active` - Currently active
- `Inactive` - Deactivated

## Business Logic Notes

- **Modern System**: Replaces legacy sales prices with more flexible pricing
- **Price Lists**: Supports multiple price lists (campaigns, seasons, etc.)
- **Date Ranges**: Automatic activation/deactivation based on dates
- **Priority**: Most specific source type wins
- **Quantity Breaks**: Higher minimum quantity = priority

## Performance Tips

1. **Filter by Status**: Always include `status eq 'Active'`
2. **Filter by Date**: Include date range checks
3. **Order Results**: Order by priority fields
4. **Cache Prices**: Cache price lookups
5. **Batch Queries**: Query multiple items in parallel

## Related APIs
- **Sales Prices**: Legacy pricing system
- **Items**: Item catalog
- **Customers**: Customer data

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
