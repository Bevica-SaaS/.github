# Items API - Developer Guide

## Overview
The Items API provides comprehensive read-only access to item/product data including pricing, inventory, web-specific fields, and marketing content.

## API Endpoint Details
- **Endpoint**: `/items`
- **Entity Name**: item
- **Entity Set Name**: items  
- **Page ID**: 71989
- **Source Table**: TVTWS Web Item Product
- **API Group**: webbevica
- **Publisher**: tvisiontech
- **Version**: v2.0

## Permissions
- **Insert**: Not Allowed
- **Modify**: Not Allowed
- **Delete**: Not Allowed
- **Read**: Allowed

## Base URL
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/items
```

## Field Reference

### Identity & Status
- `systemId` - System identifier (OData key)
- `webItemId` - Web item ID
- `itemNo` - Item number
- `published` - Published to web status
- `deleted` - Deletion flag
- `webLastModDateTime` - Web last modified timestamp

### Basic Item Info
- `blocked` - Item blocked status
- `description` - Item description
- `baseUoMCode`, `baseUoMDescription` - Base unit of measure
- `salesUoMCode`, `salesUoMDescription`, `salesUoMQtyPer` - Sales UOM details
- `webUoMCode`, `webUoMDescription`, `webUoMQtyPer` - Web UOM details

### Pricing & Stock
- `unitPriceWithDuty` - Unit price including duty
- `unitPriceWithOutDuty` - Unit price excluding duty
- `stockQuantityBase` - Available stock (base UOM)

### Physical Attributes
- `unitVolume` - Unit volume
- `unitWeight` - Unit weight (base UOM)
- `salesUnitWeight` - Sales unit weight
- `bottlePerCase` - Bottles per case

### Wine-Specific Fields
- `drinkFrom`, `drinkTo` - Drinking window dates
- `appellation` - Appellation code
- `appellationDescription` - Appellation description
- `regionCode`, `regionDescription` - Region details
- `subRegionCode`, `subRegionDescription` - SubRegion details
- `classificationCode` - Classification
- `colourCode`, `colourDesc` - Wine color

### Web & Catalog
- `webSaleOnlyUnit` - Web sale only unit restriction
- `webCatalogue` - Web catalog assignments
- `purchasingCode` - Purchasing code

### Custom Fields
- `dutycontrolled` - Duty controlled flag
- `date1`, `date2`, `date3` - Custom dates
- `class1` through `class5` - Custom classification fields
- `number1` through `number5` - Custom number fields
- `option1` through `option5` - Custom option fields

### System Fields
- `systemCreatedAt`, `systemCreatedBy`
- `systemModifiedAt`, `systemModifiedBy`

## Nested Data

### Marketing Contents (Subpage)
Access via `$expand=marketingContents`

## Common Use Cases

### 1. Get All Published Items
```http
GET /items?$filter=published eq true and deleted eq false
```

### 2. Get Items with Stock
```http
GET /items?$filter=stockQuantityBase gt 0 and published eq true&$select=itemNo,description,stockQuantityBase,unitPriceWithDuty
```

### 3. Get Items with Marketing Content
```http
GET /items?$expand=marketingContents&$filter=published eq true
```

### 4. Search by Description
```http
GET /items?$filter=contains(description, 'Cabernet')
```

### 5. Get Items by Region
```http
GET /items?$filter=regionCode eq 'BORDEAUX'
```

### 6. Get Items by Catalog
```http
GET /items?$filter=contains(webCatalogue, 'PREMIUM')
```

## Code Examples

### JavaScript
```javascript
class ItemAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getPublishedItems(includeMarketing = false) {
    const expand = includeMarketing ? '&$expand=marketingContents' : '';
    const response = await fetch(
      `${this.baseUrl}/items?$filter=published eq true and deleted eq false${expand}`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getItemsWithStock() {
    const response = await fetch(
      `${this.baseUrl}/items?$filter=stockQuantityBase gt 0 and published eq true&$select=itemNo,description,stockQuantityBase,unitPriceWithDuty,webUoMQtyPer`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async searchItems(searchTerm) {
    const filter = `contains(description, '${searchTerm}') and published eq true`;
    const response = await fetch(
      `${this.baseUrl}/items?$filter=${encodeURIComponent(filter)}`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getItemsByRegion(regionCode) {
    const response = await fetch(
      `${this.baseUrl}/items?$filter=regionCode eq '${regionCode}' and published eq true`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }
}

// Usage
const api = new ItemAPI(baseUrl, accessToken);

// Get published items with marketing content
const items = await api.getPublishedItems(true);

// Display items
items.forEach(item => {
  console.log(`${item.itemNo}: ${item.description}`);
  console.log(`Price (duty-paid): ${item.unitPriceWithDuty}`);
  console.log(`Stock: ${item.stockQuantityBase}`);
  if (item.marketingContents) {
    console.log(`Marketing: ${item.marketingContents.length} entries`);
  }
});
```

### Python
```python
class ItemAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_published_items(self, include_marketing: bool = False) -> list:
        params = {
            '$filter': 'published eq true and deleted eq false'
        }
        if include_marketing:
            params['$expand'] = 'marketingContents'
        
        response = requests.get(
            f'{self.base_url}/items',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_items_in_stock(self) -> list:
        response = requests.get(
            f'{self.base_url}/items',
            headers=self.headers,
            params={
                '$filter': 'stockQuantityBase gt 0 and published eq true',
                '$select': 'itemNo,description,stockQuantityBase,unitPriceWithDuty'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def search_by_description(self, search_term: str) -> list:
        response = requests.get(
            f'{self.base_url}/items',
            headers=self.headers,
            params={
                '$filter': f"contains(description, '{search_term}') and published eq true"
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_wine_by_color(self, colour_code: str) -> list:
        response = requests.get(
            f'{self.base_url}/items',
            headers=self.headers,
            params={
                '$filter': f"colourCode eq '{colour_code}' and published eq true"
            }
        )
        response.raise_for_status()
        return response.json()['value']

# Usage
api = ItemAPI(base_url, access_token)

# Get items with marketing content
items = api.get_published_items(include_marketing=True)

# Get items in stock
in_stock = api.get_items_in_stock()
print(f"Items in stock: {len(in_stock)}")

# Search for Bordeaux wines
bordeaux = api.search_by_description('Bordeaux')
```

### C#
```csharp
public class ItemApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public ItemApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<List<Item>> GetPublishedItemsAsync(bool includeMarketing = false)
    {
        var filter = "published eq true and deleted eq false";
        var expand = includeMarketing ? "&$expand=marketingContents" : "";
        
        var response = await _httpClient.GetAsync($"{_baseUrl}/items?$filter={filter}{expand}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<Item>>(json);
        return result.Value;
    }
    
    public async Task<List<Item>> GetItemsWithStockAsync()
    {
        var filter = "stockQuantityBase gt 0 and published eq true";
        var select = "itemNo,description,stockQuantityBase,unitPriceWithDuty";
        
        var response = await _httpClient.GetAsync($"{_baseUrl}/items?$filter={filter}&$select={select}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<Item>>(json);
        return result.Value;
    }
}

public class Item
{
    public Guid SystemId { get; set; }
    public int WebItemId { get; set; }
    public string ItemNo { get; set; }
    public bool Published { get; set; }
    public bool Deleted { get; set; }
    public string Description { get; set; }
    public decimal UnitPriceWithDuty { get; set; }
    public decimal UnitPriceWithOutDuty { get; set; }
    public decimal StockQuantityBase { get; set; }
    public string RegionCode { get; set; }
    public string SubRegionCode { get; set; }
    public string ColourCode { get; set; }
    public List<MarketingContent> MarketingContents { get; set; }
}
```

## Business Logic Notes

- **Published Items**: Only items with `published=true` and `deleted=false` should be displayed
- **Stock Levels**: `stockQuantityBase` is in base UOM; convert using `salesUoMQtyPer` or `webUoMQtyPer`
- **Pricing**: Use `unitPriceWithDuty` for duty-paid, `unitPriceWithOutDuty` for duty-free
- **Web Catalogs**: Comma-separated list in `webCatalogue` field
- **Marketing Content**: Retrieved via expand, contains HTML/rich text
- **Wine Data**: Region, subregion, appellation provide geographic classification

## Performance Tips

1. **Always filter by published status**: Reduces data significantly
2. **Use $select**: Only retrieve needed fields to reduce payload
3. **Cache product data**: Changes infrequently, suitable for caching
4. **Expand sparingly**: Only expand marketing content when needed
5. **Pagination**: Use `$top` and `$skip` for large catalogs

## Related APIs
- **Web Products**: Aggregated product view with additional marketing fields
- **Web Stock**: Real-time stock by location
- **Sales Prices**: Pricing information
- **Marketing Content**: Detailed marketing information

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
