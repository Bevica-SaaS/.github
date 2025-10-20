# Sub-Region Codes API - Developer Guide

## Overview
The Sub-Region Codes API provides read-only access to wine sub-region classifications, providing more granular geographic detail within wine regions.

## API Endpoint Details
- **Endpoint**: `/subRegions`
- **Entity Name**: subRegionCode
- **Entity Set Name**: subRegions
- **Page ID**: 71980
- **Source Table**: TVT Sub Region Code
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/subRegions
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `code` | String | Sub-region code |
| `description` | String | Sub-region description/name |
| `regionCode` | String | Parent region code |
| `countryRegionCode` | String | Country code |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemModifiedAt` | DateTime | Last modification |

## Common Use Cases

### 1. Get All Sub-Regions
```http
GET /subRegions
```

### 2. Get Sub-Regions for a Region
```http
GET /subRegions?$filter=regionCode eq 'BORDEAUX'
```

### 3. Get Sub-Regions by Country
```http
GET /subRegions?$filter=countryRegionCode eq 'FR'
```

### 4. Search Sub-Regions
```http
GET /subRegions?$filter=contains(tolower(description), 'medoc')
```

## Code Examples

### JavaScript
```javascript
class SubRegionCodeAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getAllSubRegions() {
    const response = await fetch(
      `${this.baseUrl}/subRegions?$orderby=description asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getSubRegionsByRegion(regionCode) {
    const response = await fetch(
      `${this.baseUrl}/subRegions?$filter=regionCode eq '${regionCode}'&$orderby=description asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getSubRegionsByCountry(countryCode) {
    const response = await fetch(
      `${this.baseUrl}/subRegions?$filter=countryRegionCode eq '${countryCode}'&$orderby=description asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async searchSubRegions(searchTerm) {
    const filter = `contains(tolower(description), '${searchTerm.toLowerCase()}')`;
    const response = await fetch(
      `${this.baseUrl}/subRegions?$filter=${encodeURIComponent(filter)}`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  groupByRegion(subRegions) {
    const grouped = {};
    subRegions.forEach(subRegion => {
      const region = subRegion.regionCode || 'Other';
      if (!grouped[region]) {
        grouped[region] = [];
      }
      grouped[region].push(subRegion);
    });
    return grouped;
  }

  async buildHierarchy(regionAPI) {
    const [regions, subRegions] = await Promise.all([
      regionAPI.getAllRegions(),
      this.getAllSubRegions()
    ]);
    
    const hierarchy = {};
    regions.forEach(region => {
      hierarchy[region.code] = {
        region: region,
        subRegions: subRegions.filter(sr => sr.regionCode === region.code)
      };
    });
    
    return hierarchy;
  }
}

// Usage
const subRegionAPI = new SubRegionCodeAPI(baseUrl, accessToken);
const regionAPI = new RegionCodeAPI(baseUrl, accessToken);

// Get sub-regions for Bordeaux
const bordeauxSubRegions = await subRegionAPI.getSubRegionsByRegion('BORDEAUX');
console.log('Bordeaux sub-regions:');
bordeauxSubRegions.forEach(sr => {
  console.log(`  ${sr.code}: ${sr.description}`);
});

// Build complete hierarchy for cascading dropdowns
const hierarchy = await subRegionAPI.buildHierarchy(regionAPI);

// Cascading dropdown: Region selected, load sub-regions
function onRegionChange(regionCode) {
  const subRegionSelect = document.getElementById('subRegion');
  subRegionSelect.innerHTML = '<option value="">Select Sub-Region...</option>';
  
  if (hierarchy[regionCode]) {
    hierarchy[regionCode].subRegions.forEach(sr => {
      const option = new Option(sr.description, sr.code);
      subRegionSelect.add(option);
    });
    subRegionSelect.disabled = false;
  } else {
    subRegionSelect.disabled = true;
  }
}

// Search across all sub-regions
const medocResults = await subRegionAPI.searchSubRegions('medoc');
console.log(`Found ${medocResults.length} Medoc sub-regions`);
```

### Python
```python
from typing import List, Dict, Any

class SubRegionCodeAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_all_subregions(self) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/subRegions',
            headers=self.headers,
            params={'$orderby': 'description asc'}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_subregions_by_region(self, region_code: str) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/subRegions',
            headers=self.headers,
            params={
                '$filter': f"regionCode eq '{region_code}'",
                '$orderby': 'description asc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_subregions_by_country(self, country_code: str) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/subRegions',
            headers=self.headers,
            params={
                '$filter': f"countryRegionCode eq '{country_code}'",
                '$orderby': 'description asc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def search_subregions(self, search_term: str) -> List[dict]:
        filter_query = f"contains(tolower(description), '{search_term.lower()}')"
        response = requests.get(
            f'{self.base_url}/subRegions',
            headers=self.headers,
            params={'$filter': filter_query}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def group_by_region(self, subregions: List[dict]) -> Dict[str, List[dict]]:
        grouped = {}
        for subregion in subregions:
            region = subregion.get('regionCode', 'Other')
            if region not in grouped:
                grouped[region] = []
            grouped[region].append(subregion)
        return grouped
    
    def build_hierarchy(self, region_api) -> Dict[str, Any]:
        regions = region_api.get_all_regions()
        subregions = self.get_all_subregions()
        
        hierarchy = {}
        for region in regions:
            hierarchy[region['code']] = {
                'region': region,
                'subRegions': [
                    sr for sr in subregions 
                    if sr.get('regionCode') == region['code']
                ]
            }
        
        return hierarchy

# Usage
subregion_api = SubRegionCodeAPI(base_url, access_token)
region_api = RegionCodeAPI(base_url, access_token)

# Get all French sub-regions
french_subregions = subregion_api.get_subregions_by_country('FR')
print(f"French sub-regions: {len(french_subregions)}")

# Group by region
grouped = subregion_api.group_by_region(french_subregions)
for region_code, subregions in grouped.items():
    print(f"\n{region_code}:")
    for sr in subregions:
        print(f"  - {sr['description']}")

# Build complete hierarchy
hierarchy = subregion_api.build_hierarchy(region_api)

# Example: Get Bordeaux structure
bordeaux = hierarchy.get('BORDEAUX')
if bordeaux:
    print(f"\nBordeaux region has {len(bordeaux['subRegions'])} sub-regions:")
    for sr in bordeaux['subRegions']:
        print(f"  {sr['code']}: {sr['description']}")
```

### C#
```csharp
public class SubRegionCodeApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public SubRegionCodeApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<List<SubRegionCode>> GetAllSubRegionsAsync()
    {
        var response = await _httpClient.GetAsync($"{_baseUrl}/subRegions?$orderby=description asc");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<SubRegionCode>>(json);
        return result.Value;
    }
    
    public async Task<List<SubRegionCode>> GetSubRegionsByRegionAsync(string regionCode)
    {
        var filter = $"regionCode eq '{regionCode}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/subRegions?$filter={filter}&$orderby=description asc");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<SubRegionCode>>(json);
        return result.Value;
    }
    
    public Dictionary<string, List<SubRegionCode>> GroupByRegion(List<SubRegionCode> subRegions)
    {
        return subRegions
            .GroupBy(sr => sr.RegionCode ?? "Other")
            .ToDictionary(g => g.Key, g => g.ToList());
    }
    
    public async Task<Dictionary<string, RegionHierarchy>> BuildHierarchyAsync(RegionCodeApiClient regionApi)
    {
        var regionsTask = regionApi.GetAllRegionsAsync();
        var subRegionsTask = GetAllSubRegionsAsync();
        
        await Task.WhenAll(regionsTask, subRegionsTask);
        
        var regions = await regionsTask;
        var subRegions = await subRegionsTask;
        
        return regions.ToDictionary(
            r => r.Code,
            r => new RegionHierarchy
            {
                Region = r,
                SubRegions = subRegions.Where(sr => sr.RegionCode == r.Code).ToList()
            }
        );
    }
}

public class SubRegionCode
{
    public Guid SystemId { get; set; }
    public string Code { get; set; }
    public string Description { get; set; }
    public string RegionCode { get; set; }
    public string CountryRegionCode { get; set; }
}

public class RegionHierarchy
{
    public RegionCode Region { get; set; }
    public List<SubRegionCode> SubRegions { get; set; }
}
```

## Business Logic Notes

- **Read-Only**: Reference data managed in BC
- **Hierarchical**: Sub-regions belong to regions
- **Wine Classification**: Provides detailed wine origin classification
- **Cascading**: Designed for cascading dropdown implementations
- **Caching**: Suitable for long-term caching

## Performance Tips

1. **Cache with Regions**: Load and cache with regions on startup
2. **Build Hierarchy Once**: Pre-build hierarchy for cascading dropdowns
3. **Client-Side Filter**: Filter cached data client-side
4. **Parallel Load**: Load regions and sub-regions in parallel

## UI Implementation

### Cascading Dropdowns
```javascript
// Load all data once
const [regions, subRegions] = await Promise.all([
  regionAPI.getAllRegions(),
  subRegionAPI.getAllSubRegions()
]);

// Build lookup
const subRegionsByRegion = {};
subRegions.forEach(sr => {
  if (!subRegionsByRegion[sr.regionCode]) {
    subRegionsByRegion[sr.regionCode] = [];
  }
  subRegionsByRegion[sr.regionCode].push(sr);
});

// Populate region dropdown
regions.forEach(region => {
  regionSelect.add(new Option(region.description, region.code));
});

// On region change, populate sub-region
regionSelect.addEventListener('change', (e) => {
  subRegionSelect.innerHTML = '<option>Select...</option>';
  const subs = subRegionsByRegion[e.target.value] || [];
  subs.forEach(sr => {
    subRegionSelect.add(new Option(sr.description, sr.code));
  });
});
```

## Related APIs
- **Region Codes**: Parent wine regions
- **Items**: Item sub-region classification
- **Web Products**: Product geographic display

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
