# Brand API - Developer Guide

## Introduction
The Brand API provides access to brand information including contact details, address information, and geographical coordinates. This RESTful API follows OData v4 standards and is part of the Bevica Web Integration platform.

---

## API Endpoint

### Base URL
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/brands
```

### Authentication
This API requires OAuth 2.0 authentication. Include your access token in the Authorization header:
```
Authorization: Bearer {your_access_token}
```

---

## Operations

### 1. Get All Brands
Retrieve a list of all brands.

**Request:**
```http
GET /brands
```

**Response:** `200 OK`
```json
{
  "value": [
    {
      "code": "BRAND001",
      "name": "Example Brand",
      "address": "123 Main Street",
      "address2": "Suite 100",
      "city": "London",
      "countryRegionCode": "GB",
      "county": "Greater London",
      "postCode": "SW1A 1AA",
      "contact": "John Smith",
      "eMail": "contact@examplebrand.com",
      "faxNo": "+44 20 1234 5678",
      "homePage": "https://www.examplebrand.com",
      "latitude": 51.5074,
      "longitude": -0.1278,
      "noItems": 150,
      "phoneNo": "+44 20 7946 0958"
    }
  ]
}
```

---

### 2. Get a Single Brand
Retrieve details for a specific brand by code.

**Request:**
```http
GET /brands('{code}')
```

**Example:**
```http
GET /brands('BRAND001')
```

**Response:** `200 OK`
```json
{
  "code": "BRAND001",
  "name": "Example Brand",
  "address": "123 Main Street",
  "address2": "Suite 100",
  "city": "London",
  "countryRegionCode": "GB",
  "county": "Greater London",
  "postCode": "SW1A 1AA",
  "contact": "John Smith",
  "eMail": "contact@examplebrand.com",
  "faxNo": "+44 20 1234 5678",
  "homePage": "https://www.examplebrand.com",
  "latitude": 51.5074,
  "longitude": -0.1278,
  "noItems": 150,
  "phoneNo": "+44 20 7946 0958"
}
```

---

### 3. Create a New Brand
Create a new brand record.

**Request:**
```http
POST /brands
Content-Type: application/json
```

**Request Body:**
```json
{
  "code": "BRAND002",
  "name": "New Brand",
  "address": "456 High Street",
  "city": "Manchester",
  "countryRegionCode": "GB",
  "postCode": "M1 1AA",
  "contact": "Jane Doe",
  "eMail": "info@newbrand.com",
  "phoneNo": "+44 161 123 4567"
}
```

**Response:** `201 Created`
```json
{
  "code": "BRAND002",
  "name": "New Brand",
  "address": "456 High Street",
  "address2": "",
  "city": "Manchester",
  "countryRegionCode": "GB",
  "county": "",
  "postCode": "M1 1AA",
  "contact": "Jane Doe",
  "eMail": "info@newbrand.com",
  "faxNo": "",
  "homePage": "",
  "latitude": 0.0,
  "longitude": 0.0,
  "noItems": 0,
  "phoneNo": "+44 161 123 4567"
}
```

---

### 4. Update a Brand
Update an existing brand record using PATCH.

**Request:**
```http
PATCH /brands('{code}')
Content-Type: application/json
If-Match: *
```

**Request Body:**
```json
{
  "eMail": "newemail@examplebrand.com",
  "phoneNo": "+44 20 7946 1234",
  "homePage": "https://www.newsite.com"
}
```

**Response:** `200 OK`
Returns the updated brand object.

---

### 5. Delete a Brand
Delete a brand record.

**Request:**
```http
DELETE /brands('{code}')
If-Match: *
```

**Response:** `204 No Content`

---

## Field Reference

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `code` | String | Yes | Unique identifier for the brand. Primary key. |
| `name` | String | No | Brand display name |
| `address` | String | No | Primary street address |
| `address2` | String | No | Additional address information |
| `city` | String | No | City name |
| `countryRegionCode` | String | No | ISO country/region code (e.g., "GB", "US") |
| `county` | String | No | County or state |
| `postCode` | String | No | Postal or ZIP code |
| `contact` | String | No | Primary contact person name |
| `eMail` | String | No | Email address |
| `faxNo` | String | No | Fax number |
| `homePage` | String | No | Website URL |
| `latitude` | Decimal | No | Geographical latitude coordinate |
| `longitude` | Decimal | No | Geographical longitude coordinate |
| `noItems` | Integer | No | Count of items associated with this brand (read-only) |
| `phoneNo` | String | No | Primary contact phone number |

---

## Filtering and Querying

### Filter by Name
```http
GET /brands?$filter=name eq 'Example Brand'
```

### Filter by Country
```http
GET /brands?$filter=countryRegionCode eq 'GB'
```

### Search by City
```http
GET /brands?$filter=contains(city, 'London')
```

### Select Specific Fields
```http
GET /brands?$select=code,name,city,countryRegionCode
```

### Order Results
```http
GET /brands?$orderby=name asc
```

### Pagination
```http
GET /brands?$top=10&$skip=0
```

### Count Records
```http
GET /brands/$count
```

---

## Code Examples

### JavaScript (Fetch API)
```javascript
// Get all brands
async function getBrands() {
  const response = await fetch('https://api.businesscentral.dynamics.com/v2.0/production/api/tvisiontech/webbevica/v2.0/brands', {
    method: 'GET',
    headers: {
      'Authorization': 'Bearer ' + accessToken,
      'Content-Type': 'application/json'
    }
  });
  
  const data = await response.json();
  return data.value;
}

// Create a new brand
async function createBrand(brandData) {
  const response = await fetch('https://api.businesscentral.dynamics.com/v2.0/production/api/tvisiontech/webbevica/v2.0/brands', {
    method: 'POST',
    headers: {
      'Authorization': 'Bearer ' + accessToken,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(brandData)
  });
  
  return await response.json();
}

// Update a brand
async function updateBrand(code, updates) {
  const response = await fetch(`https://api.businesscentral.dynamics.com/v2.0/production/api/tvisiontech/webbevica/v2.0/brands('${code}')`, {
    method: 'PATCH',
    headers: {
      'Authorization': 'Bearer ' + accessToken,
      'Content-Type': 'application/json',
      'If-Match': '*'
    },
    body: JSON.stringify(updates)
  });
  
  return await response.json();
}
```

### Python
```python
import requests

class BrandAPI:
    def __init__(self, base_url, access_token):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_all_brands(self):
        response = requests.get(
            f'{self.base_url}/brands',
            headers=self.headers
        )
        return response.json()['value']
    
    def get_brand(self, code):
        response = requests.get(
            f'{self.base_url}/brands(\'{code}\')',
            headers=self.headers
        )
        return response.json()
    
    def create_brand(self, brand_data):
        response = requests.post(
            f'{self.base_url}/brands',
            headers=self.headers,
            json=brand_data
        )
        return response.json()
    
    def update_brand(self, code, updates):
        headers = self.headers.copy()
        headers['If-Match'] = '*'
        response = requests.patch(
            f'{self.base_url}/brands(\'{code}\')',
            headers=headers,
            json=updates
        )
        return response.json()

# Usage
api = BrandAPI('https://api.businesscentral.dynamics.com/v2.0/production/api/tvisiontech/webbevica/v2.0', 'your_token')
brands = api.get_all_brands()
```

### C# (.NET)
```csharp
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text.Json;

public class BrandApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public BrandApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<List<Brand>> GetAllBrandsAsync()
    {
        var response = await _httpClient.GetAsync($"{_baseUrl}/brands");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<Brand>>(json);
        return result.Value;
    }
    
    public async Task<Brand> GetBrandAsync(string code)
    {
        var response = await _httpClient.GetAsync($"{_baseUrl}/brands('{code}')");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<Brand>(json);
    }
    
    public async Task<Brand> CreateBrandAsync(Brand brand)
    {
        var content = new StringContent(
            JsonSerializer.Serialize(brand),
            System.Text.Encoding.UTF8,
            "application/json"
        );
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/brands", content);
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<Brand>(json);
    }
}

public class Brand
{
    public string Code { get; set; }
    public string Name { get; set; }
    public string Address { get; set; }
    public string Address2 { get; set; }
    public string City { get; set; }
    public string CountryRegionCode { get; set; }
    public string County { get; set; }
    public string PostCode { get; set; }
    public string Contact { get; set; }
    public string EMail { get; set; }
    public string FaxNo { get; set; }
    public string HomePage { get; set; }
    public decimal Latitude { get; set; }
    public decimal Longitude { get; set; }
    public int NoItems { get; set; }
    public string PhoneNo { get; set; }
}
```

---

## Error Handling

### Common Error Codes

| Status Code | Description | Solution |
|-------------|-------------|----------|
| 400 Bad Request | Invalid request format or missing required fields | Verify JSON structure and required fields |
| 401 Unauthorized | Missing or invalid authentication token | Check your access token |
| 404 Not Found | Brand code does not exist | Verify the brand code exists |
| 409 Conflict | Brand code already exists | Use a unique brand code or update existing brand |
| 412 Precondition Failed | If-Match header required or etag mismatch | Include If-Match: * header in PATCH/DELETE requests |
| 500 Internal Server Error | Server error | Contact support with request details |

### Error Response Format
```json
{
  "error": {
    "code": "ValidationError",
    "message": "The field 'code' is required."
  }
}
```

---

## Best Practices

1. **Rate Limiting**: Implement retry logic with exponential backoff
2. **Caching**: Cache brand data locally and refresh periodically
3. **Batch Operations**: Use `$batch` endpoint for multiple operations
4. **Field Selection**: Use `$select` to retrieve only needed fields
5. **Error Handling**: Always implement comprehensive error handling
6. **Webhooks**: Consider implementing webhooks for real-time updates (if available)
7. **Validation**: Validate data client-side before sending requests

---

## Common Use Cases

### 1. Brand Directory Display
Retrieve and display all brands with their contact information:
```javascript
const brands = await getBrands();
brands.forEach(brand => {
  console.log(`${brand.name} - ${brand.city}, ${brand.countryRegionCode}`);
});
```

### 2. Brand Location Mapping
Get brands with geographical coordinates for map display:
```http
GET /brands?$filter=latitude ne 0 and longitude ne 0&$select=code,name,latitude,longitude,address,city
```

### 3. Search by Location
Find brands in a specific region:
```http
GET /brands?$filter=countryRegionCode eq 'GB' and contains(city, 'London')
```

### 4. Brand Inventory Count
Get brands with their item counts:
```http
GET /brands?$select=code,name,noItems&$orderby=noItems desc
```

---

## Technical Specifications

- **Page ID**: 71998
- **Page Name**: TVTWS Brand
- **API Group**: webbevica
- **API Publisher**: tvisiontech
- **API Version**: v2.0
- **Entity Name**: brand
- **Entity Set Name**: brands
- **Source Table**: TVT Brand
- **OData Version**: 4.0
- **Delayed Insert**: Enabled

---

## Support and Resources

For additional support or questions, please contact the technical support team.

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0