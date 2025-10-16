-# Manifests API - Developer Guide

## Overview
The Manifests API provides access to shipping manifest headers for tracking consolidated shipments and logistics.

## API Endpoint Details
- **Endpoint**: `/manifests`
- **Entity Name**: manifest
- **Entity Set Name**: manifests
- **Page ID**: 71981
- **Source Table**: TVT Manifest Header V2
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/manifests
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `no` | String | Manifest number |
| `manifestType` | Enum | Manifest type |
| `type` | Enum | Type classification |
| `description` | String | Manifest description |
| `status` | Enum | Status (Open, Released, etc.) |
| `documentDate` | Date | Document date |
| `logisticsDate` | Date | Logistics date |
| `logisticsReference` | String | Logistics reference |
| `logisticsStatus` | Enum | Logistics status |
| `addressCode` | String | Destination address code |
| `address` | String | To address line 1 |
| `address2` | String | To address line 2 |
| `city` | String | To city |
| `postCode` | String | To postal code |
| `county` | String | To county/state |
| `countryRegionCode` | String | To country code |
| `contact` | String | Contact person |
| `locationCode` | String | Source location |
| `primaryVendorNo` | String | Primary vendor number |
| `primaryVendorName` | String | Primary vendor name |
| `shippingAgentCode` | String | Shipping agent |
| `shippingAgentServiceCode` | String | Shipping service |
| `shipmentMethodCode` | String | Shipment method |
| `finalDeliveryType` | Enum | Final delivery type |
| `totalNetWeight` | Decimal | Total net weight |
| `totalGrossWeight` | Decimal | Total gross weight |
| `totalEqCasesToMove` | Decimal | Total equivalent cases |
| `noLines` | Integer | Number of lines |

## Common Operations

### Create Manifest
```http
POST /manifests
Content-Type: application/json

{
  "manifestType": "Customer",
  "description": "Customer Shipment - Oct 2025",
  "documentDate": "2025-10-14",
  "locationCode": "MAIN",
  "addressCode": "WAREHOUSE",
  "shippingAgentCode": "DHL"
}
```

### Get Active Manifests
```http
GET /manifests?$filter=status eq 'Open'
```

### Get Manifests by Date
```http
GET /manifests?$filter=documentDate ge 2025-10-01&$orderby=documentDate desc
```

### Update Manifest
```http
PATCH /manifests({systemId})
Content-Type: application/json
If-Match: *

{
  "status": "Released",
  "logisticsReference": "SHIP-12345"
}
```

## Code Examples

### JavaScript
```javascript
class ManifestAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async createManifest(manifestData) {
    const response = await fetch(`${this.baseUrl}/manifests`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify(manifestData)
    });
    
    if (!response.ok) throw new Error(await response.text());
    return await response.json();
  }

  async getActiveManifests() {
    const response = await fetch(
      `${this.baseUrl}/manifests?$filter=status eq 'Open'`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async updateManifest(systemId, updates) {
    const response = await fetch(`${this.baseUrl}/manifests(${systemId})`, {
      method: 'PATCH',
      headers: { ...this.headers, 'If-Match': '*' },
      body: JSON.stringify(updates)
    });
    return await response.json();
  }
}

// Usage
const api = new ManifestAPI(baseUrl, accessToken);

const manifest = await api.createManifest({
  manifestType: 'Customer',
  description: 'Daily Shipment',
  documentDate: '2025-10-14',
  locationCode: 'MAIN',
  shippingAgentCode: 'FEDEX'
});

console.log(`Manifest created: ${manifest.no}`);
```

### Python
```python
class ManifestAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def create_manifest(self, manifest_data: dict) -> dict:
        response = requests.post(
            f'{self.base_url}/manifests',
            headers=self.headers,
            json=manifest_data
        )
        response.raise_for_status()
        return response.json()
    
    def get_active_manifests(self) -> list:
        response = requests.get(
            f'{self.base_url}/manifests',
            headers=self.headers,
            params={'$filter': "status eq 'Open'"}
        )
        response.raise_for_status()
        return response.json()['value']

# Usage
api = ManifestAPI(base_url, access_token)
manifest = api.create_manifest({
    'manifestType': 'Customer',
    'description': 'Daily Shipment',
    'documentDate': '2025-10-14'
})
```

### C#
```csharp
public class ManifestApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public async Task<Manifest> CreateManifestAsync(Manifest manifest)
    {
        var json = JsonSerializer.Serialize(manifest);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/manifests", content);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<Manifest>(responseJson);
    }
    
    public async Task<List<Manifest>> GetActiveManifestsAsync()
    {
        var response = await _httpClient.GetAsync($"{_baseUrl}/manifests?$filter=status eq 'Open'");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<Manifest>>(json);
        return result.Value;
    }
}

public class Manifest
{
    public Guid SystemId { get; set; }
    public string No { get; set; }
    public string ManifestType { get; set; }
    public string Description { get; set; }
    public string Status { get; set; }
    public DateTime DocumentDate { get; set; }
    public string LocationCode { get; set; }
}
```

## Status Values

- **Open** - In progress
- **Released** - Released for shipping
- **Shipped** - Shipped
- **Received** - Received at destination

## Business Logic Notes

- **Consolidation**: Groups multiple shipments
- **Weight Tracking**: Tracks net and gross weights
- **Logistics Integration**: Links to logistics providers
- **Vendor Link**: Primary vendor for manifest
- **Address Management**: Destination address details

## Related APIs
- **Manifest Lines**: Line item details
- **Sales Documents**: Source orders

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
