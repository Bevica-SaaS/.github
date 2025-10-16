# Region Codes API - Developer Guide

## Overview
The Region Codes API provides read-only access to wine region classifications used for geographic categorization of wine products.

## API Endpoint Details
- **Endpoint**: `/regionCodes`
- **Entity Name**: regionCode
- **Entity Set Name**: regionCodes
- **Page ID**: 71979
- **Source Table**: TVT Region Code
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/regionCodes
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `code` | String | Region code |
| `description` | String | Region description/name |
| `countryRegionCode` | String | Country code |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemModifiedAt` | DateTime | Last modification |

## Common Use Cases

### 1. Get All Regions
```http
GET /regionCodes
```

### 2. Get Regions by Country
```http
GET /regionCodes?$filter=countryRegionCode eq 'FR'
```

### 3. Search Regions
```http
GET /regionCodes?$filter=contains(tolower(description), 'bordeaux')
```

### 4. Get Specific Region
```http
GET /regionCodes?$filter=code eq 'BORDEAUX'
```

## Code Examples

### JavaScript
```javascript
class RegionCodeAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getAllRegions() {
    const response = await fetch(
      `${this.baseUrl}/regionCodes?$orderby=description asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getRegionsByCountry(countryCode) {
    const response = await fetch(
      `${this.baseUrl}/regionCodes?$filter=countryRegionCode eq '${countryCode}'&$orderby=description asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async searchRegions(searchTerm) {
    const filter = `contains(tolower(description), '${searchTerm.toLowerCase()}')`;
    const response = await fetch(
      `${this.baseUrl}/regionCodes?$filter=${encodeURIComponent(filter)}`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getRegion(code) {
    const response = await fetch(
      `${this.baseUrl}/regionCodes?$filter=code eq '${code}'`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value[0];
  }

  groupByCountry(regions) {
    const grouped = {};
    regions.forEach(region => {
      const country = region.countryRegionCode || 'Other';
      if (!grouped[country]) {
        grouped[country] = [];
      }
      grouped[country].push(region);
    });
    return grouped;
  }
}

// Usage
const api = new RegionCodeAPI(baseUrl, accessToken);

// Load regions for dropdown
const regions = await api.getAllRegions();
const regionSelect = document.getElementById('region');
regions.forEach(region => {
  const option = new Option(region.description, region.code);
  regionSelect.add(option);
});

// Group regions by country
const grouped = api.groupByCountry(regions);
console.log('French Regions:', grouped['FR'].length);

// Search for Bordeaux regions
const bordeaux = await api.searchRegions('bordeaux');
console.log(`Found ${bordeaux.length} Bordeaux regions`);
```

### Python
```python
from typing import List, Dict

class RegionCodeAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_all_regions(self) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/regionCodes',
            headers=self.headers,
            params={'$orderby': 'description asc'}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_regions_by_country(self, country_code: str) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/regionCodes',
            headers=self.headers,
            params={
                '$filter': f"countryRegionCode eq '{country_code}'",
                '$orderby': 'description asc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def search_regions(self, search_term: str) -> List[dict]:
        filter_query = f"contains(tolower(description), '{search_term.lower()}')"
        response = requests.get(
            f'{self.base_url}/regionCodes',
            headers=self.headers,
            params={'$filter': filter_query}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def group_by_country(self, regions: List[dict]) -> Dict[str, List[dict]]:
        grouped = {}
        for region in regions:
            country = region.get('countryRegionCode', 'Other')
            if country not in grouped:
                grouped[country] = []
            grouped[country].append(region)
        return grouped

# Usage
api = RegionCodeAPI(base_url, access_token)

# Get all regions and cache
regions = api.get_all_regions()
print(f"Total regions: {len(regions)}")

# French wine regions
french_regions = api.get_regions_by_country('FR')
print(f"\nFrench wine regions: {len(french_regions)}")
for region in french_regions:
    print(f"  {region['code']}: {region['description']}")

# Group by country
grouped = api.group_by_country(regions)
print(f"\nRegions by country:")
for country, country_regions in grouped.items():
    print(f"  {country}: {len(country_regions)} regions")
```

### C#
```csharp
public class RegionCodeApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public RegionCodeApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<List<RegionCode>> GetAllRegionsAsync()
    {
        var response = await _httpClient.GetAsync($"{_baseUrl}/regionCodes?$orderby=description asc");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<RegionCode>>(json);
        return result.Value;
    }
    
    public async Task<List<RegionCode>> GetRegionsByCountryAsync(string countryCode)
    {
        var filter = $"countryRegionCode eq '{countryCode}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/regionCodes?$filter={filter}&$orderby=description asc");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<RegionCode>>(json);
        return result.Value;
    }
    
    public Dictionary<string, List<RegionCode>> GroupByCountry(List<RegionCode> regions)
    {
        return regions
            .GroupBy(r => r.CountryRegionCode ?? "Other")
            .ToDictionary(g => g.Key, g => g.ToList());
    }
}

public class RegionCode
{
    public Guid SystemId { get; set; }
    public string Code { get; set; }
    public string Description { get; set; }
    public string CountryRegionCode { get; set; }
}
```

## Business Logic Notes

- **Read-Only**: Reference data managed in BC
- **Wine-Specific**: Geographic classifications for wine products
- **Hierarchical**: Regions may have sub-regions (see SubRegionCodes API)
- **Country Link**: Linked to country/region master data
- **Caching**: Suitable for long-term caching (rarely changes)

## Performance Tips

1. **Cache Aggressively**: Region data rarely changes - cache for hours/days
2. **Load Once**: Load all regions on app startup
3. **Client-Side Filtering**: Filter cached data client-side for search
4. **Group for Display**: Pre-group by country for hierarchical dropdowns

## UI Implementation

### Grouped Dropdown
```javascript
const grouped = api.groupByCountry(regions);
Object.keys(grouped).sort().forEach(country => {
  const optgroup = document.createElement('optgroup');
  optgroup.label = country;
  grouped[country].forEach(region => {
    const option = new Option(region.description, region.code);
    optgroup.appendChild(option);
  });
  selectElement.appendChild(optgroup);
});
```

## Related APIs
- **Sub-Region Codes**: Wine sub-regions within regions
- **Items**: Item region classification
- **Web Products**: Product region display

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
