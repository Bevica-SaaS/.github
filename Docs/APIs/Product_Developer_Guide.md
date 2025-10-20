# Web Product API - Developer Guide

## Overview
The Web Product API provides a marketing-focused view of products, including images, descriptions, brand information, and web-specific flags. This is ideal for e-commerce catalog display.

## API Endpoint Details
- **Endpoint**: `/webProducts`
- **Entity Name**: webProduct
- **Entity Set Name**: webProducts
- **Page ID**: 71968
- **Source Table**: TVTWS Web Item Product
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/webProducts
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `no` | String | Product number |
| `description` | String | Product description |
| `description2` | String | Extended description |
| `brand` | String | Brand name |
| `brandCode` | String | Brand code |
| `search` | String | Search keywords |
| `image` | String | Image URL |
| `imageBlob` | MediaSet | Image binary data |
| `unitPrice` | Decimal | Base unit price |
| `productGroup` | String | Product group |
| `itemCategoryCode` | String | Item category |
| `vintage` | Integer | Vintage year |
| `country` | String | Country of origin |
| `region` | String | Wine region |
| `subRegion` | String | Wine subregion |
| `varietals` | String | Grape varietals |
| `classification` | String | Wine classification |
| `alcoholContent` | Decimal | Alcohol % by volume |
| `bottleSize` | Decimal | Bottle size (ml) |
| `published` | Boolean | Published to web flag |
| `new` | Boolean | New product flag |
| `featured` | Boolean | Featured product flag |
| `onSale` | Boolean | On sale flag |
| `discontinued` | Boolean | Discontinued flag |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemCreatedBy` | GUID | Created by user ID |
| `systemModifiedAt` | DateTime | Last modification |
| `systemModifiedBy` | GUID | Modified by user ID |

## Common Use Cases

### 1. Get All Published Products
```http
GET /webProducts?$filter=published eq true and discontinued eq false
```

### 2. Get Featured Products
```http
GET /webProducts?$filter=featured eq true and published eq true&$top=10
```

### 3. Get Products by Brand
```http
GET /webProducts?$filter=brandCode eq 'CHATEAUNEUF' and published eq true
```

### 4. Search Products
```http
GET /webProducts?$filter=contains(tolower(search), 'cabernet sauvignon') and published eq true
```

### 5. Get New Arrivals
```http
GET /webProducts?$filter=new eq true and published eq true&$orderby=systemCreatedAt desc&$top=20
```

### 6. Get Products on Sale
```http
GET /webProducts?$filter=onSale eq true and published eq true
```

### 7. Get Products by Region
```http
GET /webProducts?$filter=region eq 'Bordeaux' and published eq true
```

## Code Examples

### JavaScript
```javascript
class WebProductAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getPublishedProducts(top = 100, skip = 0) {
    const params = new URLSearchParams({
      '$filter': 'published eq true and discontinued eq false',
      '$top': top,
      '$skip': skip,
      '$orderby': 'description asc'
    });
    
    const response = await fetch(
      `${this.baseUrl}/webProducts?${params}`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getFeaturedProducts(limit = 10) {
    const response = await fetch(
      `${this.baseUrl}/webProducts?$filter=featured eq true and published eq true&$top=${limit}`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async searchProducts(searchTerm) {
    const filter = `contains(tolower(search), '${searchTerm.toLowerCase()}') and published eq true`;
    const response = await fetch(
      `${this.baseUrl}/webProducts?$filter=${encodeURIComponent(filter)}`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getProductsByBrand(brandCode) {
    const response = await fetch(
      `${this.baseUrl}/webProducts?$filter=brandCode eq '${brandCode}' and published eq true`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getProductsByRegion(region) {
    const response = await fetch(
      `${this.baseUrl}/webProducts?$filter=region eq '${region}' and published eq true`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getNewArrivals(limit = 20) {
    const response = await fetch(
      `${this.baseUrl}/webProducts?$filter=new eq true and published eq true&$orderby=systemCreatedAt desc&$top=${limit}`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getProductsOnSale() {
    const response = await fetch(
      `${this.baseUrl}/webProducts?$filter=onSale eq true and published eq true`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getProduct(productNo) {
    const response = await fetch(
      `${this.baseUrl}/webProducts?$filter=no eq '${productNo}'`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value[0];
  }
}

// Usage
const api = new WebProductAPI(baseUrl, accessToken);

// Get featured products for homepage
const featured = await api.getFeaturedProducts(6);
featured.forEach(product => {
  console.log(`${product.description} - ${product.brand}`);
  console.log(`Price: $${product.unitPrice}`);
  console.log(`Image: ${product.image}`);
});

// Search for products
const results = await api.searchProducts('pinot noir');
console.log(`Found ${results.length} products`);

// Get new arrivals
const newProducts = await api.getNewArrivals(10);
console.log(`New arrivals: ${newProducts.length}`);
```

### Python
```python
from typing import List, Optional
from urllib.parse import quote

class WebProductAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_published_products(self, top: int = 100, skip: int = 0) -> List[dict]:
        params = {
            '$filter': 'published eq true and discontinued eq false',
            '$top': top,
            '$skip': skip,
            '$orderby': 'description asc'
        }
        
        response = requests.get(
            f'{self.base_url}/webProducts',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_featured_products(self, limit: int = 10) -> List[dict]:
        params = {
            '$filter': 'featured eq true and published eq true',
            '$top': limit
        }
        
        response = requests.get(
            f'{self.base_url}/webProducts',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()['value']
    
    def search_products(self, search_term: str) -> List[dict]:
        filter_query = f"contains(tolower(search), '{search_term.lower()}') and published eq true"
        
        response = requests.get(
            f'{self.base_url}/webProducts',
            headers=self.headers,
            params={'$filter': filter_query}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_products_by_brand(self, brand_code: str) -> List[dict]:
        params = {
            '$filter': f"brandCode eq '{brand_code}' and published eq true"
        }
        
        response = requests.get(
            f'{self.base_url}/webProducts',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_products_by_region(self, region: str) -> List[dict]:
        params = {
            '$filter': f"region eq '{region}' and published eq true"
        }
        
        response = requests.get(
            f'{self.base_url}/webProducts',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_new_arrivals(self, limit: int = 20) -> List[dict]:
        params = {
            '$filter': 'new eq true and published eq true',
            '$orderby': 'systemCreatedAt desc',
            '$top': limit
        }
        
        response = requests.get(
            f'{self.base_url}/webProducts',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_products_on_sale(self) -> List[dict]:
        params = {
            '$filter': 'onSale eq true and published eq true'
        }
        
        response = requests.get(
            f'{self.base_url}/webProducts',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()['value']

# Usage
api = WebProductAPI(base_url, access_token)

# Build product catalog page
products = api.get_published_products(top=50, skip=0)
for product in products:
    print(f"{product['no']}: {product['description']}")
    print(f"Brand: {product['brand']}")
    print(f"Price: ${product['unitPrice']:.2f}")
    print(f"Region: {product['region']}")
    print()

# Get featured products
featured = api.get_featured_products(6)
print(f"Featured products: {len(featured)}")

# Search functionality
results = api.search_products('merlot')
print(f"Search results: {len(results)}")
```

### C#
```csharp
public class WebProductApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public WebProductApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<List<WebProduct>> GetPublishedProductsAsync(int top = 100, int skip = 0)
    {
        var filter = "published eq true and discontinued eq false";
        var url = $"{_baseUrl}/webProducts?$filter={filter}&$top={top}&$skip={skip}&$orderby=description asc";
        
        var response = await _httpClient.GetAsync(url);
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebProduct>>(json);
        return result.Value;
    }
    
    public async Task<List<WebProduct>> GetFeaturedProductsAsync(int limit = 10)
    {
        var filter = "featured eq true and published eq true";
        var response = await _httpClient.GetAsync($"{_baseUrl}/webProducts?$filter={filter}&$top={limit}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebProduct>>(json);
        return result.Value;
    }
    
    public async Task<List<WebProduct>> SearchProductsAsync(string searchTerm)
    {
        var filter = $"contains(tolower(search), '{searchTerm.ToLower()}') and published eq true";
        var encodedFilter = Uri.EscapeDataString(filter);
        
        var response = await _httpClient.GetAsync($"{_baseUrl}/webProducts?$filter={encodedFilter}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebProduct>>(json);
        return result.Value;
    }
    
    public async Task<List<WebProduct>> GetProductsByBrandAsync(string brandCode)
    {
        var filter = $"brandCode eq '{brandCode}' and published eq true";
        var response = await _httpClient.GetAsync($"{_baseUrl}/webProducts?$filter={filter}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebProduct>>(json);
        return result.Value;
    }
}

public class WebProduct
{
    public Guid SystemId { get; set; }
    public string No { get; set; }
    public string Description { get; set; }
    public string Description2 { get; set; }
    public string Brand { get; set; }
    public string BrandCode { get; set; }
    public string Search { get; set; }
    public string Image { get; set; }
    public decimal UnitPrice { get; set; }
    public string ProductGroup { get; set; }
    public string ItemCategoryCode { get; set; }
    public int? Vintage { get; set; }
    public string Country { get; set; }
    public string Region { get; set; }
    public string SubRegion { get; set; }
    public string Varietals { get; set; }
    public string Classification { get; set; }
    public decimal? AlcoholContent { get; set; }
    public decimal? BottleSize { get; set; }
    public bool Published { get; set; }
    public bool New { get; set; }
    public bool Featured { get; set; }
    public bool OnSale { get; set; }
    public bool Discontinued { get; set; }
}
```

## Filter Flags

Key boolean filters for product selection:
- `published` - Show on website
- `new` - New arrival
- `featured` - Featured/highlighted
- `onSale` - On sale/promotion
- `discontinued` - Discontinued (exclude)

## Business Logic Notes

- **Read-Only**: Product data managed in BC, API is for display only
- **Image Handling**: Use `image` URL or `imageBlob` for binary data
- **Search Field**: Pre-built search keywords for efficient searching
- **Wine-Specific**: Rich wine data (vintage, region, varietals, etc.)
- **Marketing Flags**: Control product visibility and promotion

## Performance Tips

1. **Always Filter Published**: `published eq true` is essential
2. **Exclude Discontinued**: Add `discontinued eq false` to filters
3. **Pagination**: Use `$top` and `$skip` for large catalogs
4. **Select Fields**: Use `$select` to reduce payload size
5. **Cache Heavily**: Product data changes infrequently
6. **Index Search**: Use `search` field for full-text search

## Related APIs
- **Items**: Complete item data including stock
- **Web Stock**: Stock availability
- **Brands**: Brand information
- **Sales Prices**: Pricing data

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
