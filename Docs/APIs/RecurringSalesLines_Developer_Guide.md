# Customer Recurring Sales Lines API - Developer Guide

## Overview
The Customer Recurring Sales Lines API provides read-only access to customer favorite items and frequently purchased products, supporting quick reordering.

## API Endpoint Details
- **Endpoint**: `/customerRecurringSalesLines`
- **Entity Name**: customerRecurringSalesLines
- **Entity Set Name**: customerRecurringSalesLines
- **Page ID**: 72200
- **Source Table**: TVTBE RecurrSLBuffer (Temporary)
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/customerRecurringSalesLines
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `stdSalesLineCode` | String | Standard sales line code |
| `customerNo` | String | Customer number |
| `itemNo` | String | Item number |
| `lineNo` | Integer | Line number |

## Common Use Cases

### Get Customer Favorites
```http
GET /customerRecurringSalesLines?$filter=customerNo eq 'CUST001'
```

### Get All Recurring Lines
```http
GET /customerRecurringSalesLines
```

## Code Examples

### JavaScript
```javascript
class RecurringSalesLineAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getCustomerFavorites(customerNo) {
    const response = await fetch(
      `${this.baseUrl}/customerRecurringSalesLines?$filter=customerNo eq '${customerNo}'`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getFavoriteItems(customerNo) {
    const favorites = await this.getCustomerFavorites(customerNo);
    // Get unique item numbers
    const itemNos = [...new Set(favorites.map(f => f.itemNo))];
    return itemNos;
  }

  buildQuickReorderList(favorites, itemAPI) {
    // Build a reorder list with item details
    return Promise.all(
      favorites.map(async (fav) => {
        const item = await itemAPI.getItem(fav.itemNo);
        return {
          itemNo: fav.itemNo,
          description: item?.description,
          stdSalesLineCode: fav.stdSalesLineCode,
          isFavorite: true
        };
      })
    );
  }
}

// Usage
const api = new RecurringSalesLineAPI(baseUrl, accessToken);

// Get customer favorites for "Quick Reorder" feature
const favorites = await api.getCustomerFavorites('CUST001');
console.log(`Customer has ${favorites.length} favorite items`);

// Display favorites
favorites.forEach(fav => {
  console.log(`Item: ${fav.itemNo} (Code: ${fav.stdSalesLineCode})`);
});

// Build quick reorder widget
const itemAPI = new ItemAPI(baseUrl, accessToken);
const reorderList = await api.buildQuickReorderList(favorites, itemAPI);
displayQuickReorder(reorderList);
```

### Python
```python
class RecurringSalesLineAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_customer_favorites(self, customer_no: str) -> list:
        response = requests.get(
            f'{self.base_url}/customerRecurringSalesLines',
            headers=self.headers,
            params={'$filter': f"customerNo eq '{customer_no}'"}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_favorite_items(self, customer_no: str) -> list:
        favorites = self.get_customer_favorites(customer_no)
        # Get unique item numbers
        item_nos = list(set(fav['itemNo'] for fav in favorites))
        return item_nos
    
    def build_quick_reorder_list(self, favorites: list, item_api) -> list:
        """Build reorder list with item details"""
        reorder_list = []
        for fav in favorites:
            item = item_api.get_item(fav['itemNo'])
            reorder_list.append({
                'itemNo': fav['itemNo'],
                'description': item.get('description') if item else None,
                'stdSalesLineCode': fav['stdSalesLineCode'],
                'isFavorite': True
            })
        return reorder_list

# Usage
api = RecurringSalesLineAPI(base_url, access_token)

# Get customer favorites
favorites = api.get_customer_favorites('CUST001')
print(f"Customer has {len(favorites)} favorite items")

# Display favorites
for fav in favorites:
    print(f"  {fav['itemNo']} - Line Code: {fav['stdSalesLineCode']}")

# Get unique item numbers for bulk operations
item_nos = api.get_favorite_items('CUST001')
print(f"Unique items: {len(item_nos)}")
```

### C#
```csharp
public class RecurringSalesLineApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public async Task<List<RecurringSalesLine>> GetCustomerFavoritesAsync(string customerNo)
    {
        var filter = $"customerNo eq '{customerNo}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/customerRecurringSalesLines?$filter={filter}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<RecurringSalesLine>>(json);
        return result.Value;
    }
    
    public async Task<List<string>> GetFavoriteItemsAsync(string customerNo)
    {
        var favorites = await GetCustomerFavoritesAsync(customerNo);
        return favorites.Select(f => f.ItemNo).Distinct().ToList();
    }
}

public class RecurringSalesLine
{
    public Guid SystemId { get; set; }
    public string StdSalesLineCode { get; set; }
    public string CustomerNo { get; set; }
    public string ItemNo { get; set; }
    public int LineNo { get; set; }
}
```

## Business Logic Notes

- **Read-Only**: Generated from standard sales lines
- **Customer Favorites**: Frequently ordered items
- **Quick Reorder**: Enables one-click reordering
- **Standard Lines**: Based on standard sales line templates
- **Temporary Table**: Data queried from underlying tables

## UI Implementation

### Quick Reorder Widget
```javascript
// Display favorite items for quick add to cart
function displayQuickReorder(favorites) {
  const container = document.getElementById('quick-reorder');
  
  favorites.forEach(item => {
    const button = document.createElement('button');
    button.className = 'quick-reorder-btn';
    button.innerHTML = `
      <i class="icon-favorite"></i>
      <span>${item.description}</span>
      <span class="add-icon">+</span>
    `;
    button.onclick = () => addFavoriteToCart(item.itemNo);
    container.appendChild(button);
  });
}

function addFavoriteToCart(itemNo) {
  // Add to cart with default quantity
  cart.addItem(itemNo, 6); // default case quantity
  showNotification(`Added ${itemNo} to cart`);
}
```

### Customer Dashboard
```html
<div class="favorites-section">
  <h3>Your Favorites - Quick Reorder</h3>
  <div id="quick-reorder" class="favorites-grid">
    <!-- Dynamically populated -->
  </div>
</div>
```

## Use Cases

1. **Quick Reorder**: One-click add to cart for favorites
2. **Customer Dashboard**: Display frequently purchased items
3. **Personalization**: Show recommended items based on history
4. **Mobile App**: Quick order feature
5. **Sales Suggestions**: Cross-sell related favorites

## Performance Tips

1. **Cache Favorites**: Cache per customer session
2. **Load on Login**: Prefetch when customer logs in
3. **Combine with Items**: Join with items API for details
4. **Icons**: Mark favorite items in catalog

## Related APIs
- **Items**: Item details and pricing
- **Web Orders**: Order creation
- **Customers**: Customer information

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
