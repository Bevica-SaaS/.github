# Ship-To Addresses API - Developer Guide

## Overview
The Ship-To Addresses API provides read-only access to customer delivery addresses configured in Business Central.

## API Endpoint Details
- **Endpoint**: `/shiptoAddresses`
- **Entity Name**: shipToAddress
- **Entity Set Name**: shiptoAddresses
- **Page ID**: 71971
- **Source Table**: Ship-to Address
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/shiptoAddresses
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `customerNo` | String | Customer number |
| `code` | String | Ship-to address code |
| `name` | String | Recipient name |
| `name2` | String | Additional name field |
| `address` | String | Street address line 1 |
| `address2` | String | Street address line 2 |
| `city` | String | City |
| `contact` | String | Contact person |
| `phoneNo` | String | Phone number |
| `postCode` | String | Postal/ZIP code |
| `county` | String | County/State |
| `countryRegionCode` | String | Country/region code |
| `eMail` | String | Email address |
| `lastDateModified` | Date | Last modification date |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemModifiedAt` | DateTime | Last modification |

## Common Use Cases

### 1. Get Customer Ship-To Addresses
```http
GET /shiptoAddresses?$filter=customerNo eq 'CUST001'
```

### 2. Get Specific Ship-To Address
```http
GET /shiptoAddresses?$filter=customerNo eq 'CUST001' and code eq 'WAREHOUSE'
```

### 3. Search by City
```http
GET /shiptoAddresses?$filter=customerNo eq 'CUST001' and contains(tolower(city), 'boston')
```

## Code Examples

### JavaScript
```javascript
class ShipToAddressAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getCustomerAddresses(customerNo) {
    const response = await fetch(
      `${this.baseUrl}/shiptoAddresses?$filter=customerNo eq '${customerNo}'&$orderby=code asc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async getAddress(customerNo, addressCode) {
    const response = await fetch(
      `${this.baseUrl}/shiptoAddresses?$filter=customerNo eq '${customerNo}' and code eq '${addressCode}'`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value[0];
  }

  formatAddress(address) {
    const lines = [
      address.name,
      address.name2,
      address.address,
      address.address2,
      `${address.city}, ${address.county} ${address.postCode}`,
      address.countryRegionCode
    ].filter(line => line && line.trim());
    
    return lines.join('\n');
  }

  formatAddressForLabel(address) {
    return {
      recipient: address.name,
      line1: address.address,
      line2: address.address2 || '',
      cityStateZip: `${address.city}, ${address.county} ${address.postCode}`,
      country: address.countryRegionCode,
      contact: address.contact,
      phone: address.phoneNo
    };
  }
}

// Usage
const api = new ShipToAddressAPI(baseUrl, accessToken);

// Get all addresses for customer
const addresses = await api.getCustomerAddresses('CUST001');
console.log(`Customer has ${addresses.length} delivery addresses`);

// Display addresses for selection
addresses.forEach(addr => {
  console.log(`\n[${addr.code}] ${addr.name}`);
  console.log(api.formatAddress(addr));
});

// Get specific address for order
const shipTo = await api.getAddress('CUST001', 'WAREHOUSE');
const label = api.formatAddressForLabel(shipTo);
console.log('\nShipping Label:');
console.log(label.recipient);
console.log(label.line1);
if (label.line2) console.log(label.line2);
console.log(label.cityStateZip);
console.log(label.country);
```

### Python
```python
from typing import List, Optional, Dict

class ShipToAddressAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_customer_addresses(self, customer_no: str) -> List[dict]:
        response = requests.get(
            f'{self.base_url}/shiptoAddresses',
            headers=self.headers,
            params={
                '$filter': f"customerNo eq '{customer_no}'",
                '$orderby': 'code asc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_address(self, customer_no: str, address_code: str) -> Optional[dict]:
        response = requests.get(
            f'{self.base_url}/shiptoAddresses',
            headers=self.headers,
            params={
                '$filter': f"customerNo eq '{customer_no}' and code eq '{address_code}'"
            }
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None
    
    def format_address(self, address: dict) -> str:
        lines = [
            address.get('name'),
            address.get('name2'),
            address.get('address'),
            address.get('address2'),
            f"{address.get('city')}, {address.get('county')} {address.get('postCode')}",
            address.get('countryRegionCode')
        ]
        return '\n'.join(line for line in lines if line and line.strip())
    
    def format_address_for_label(self, address: dict) -> Dict[str, str]:
        return {
            'recipient': address.get('name', ''),
            'line1': address.get('address', ''),
            'line2': address.get('address2', ''),
            'cityStateZip': f"{address.get('city')}, {address.get('county')} {address.get('postCode')}",
            'country': address.get('countryRegionCode', ''),
            'contact': address.get('contact', ''),
            'phone': address.get('phoneNo', '')
        }

# Usage
api = ShipToAddressAPI(base_url, access_token)

# Get addresses for dropdown
addresses = api.get_customer_addresses('CUST001')
print(f"Available delivery addresses: {len(addresses)}")

for addr in addresses:
    print(f"\n{addr['code']}: {addr['name']}")
    print(api.format_address(addr))

# Get address for order processing
ship_to = api.get_address('CUST001', 'WAREHOUSE')
if ship_to:
    label = api.format_address_for_label(ship_to)
    print("\nShipping Label Data:")
    print(f"To: {label['recipient']}")
    print(f"Address: {label['line1']}")
    print(f"City/State/ZIP: {label['cityStateZip']}")
    print(f"Country: {label['country']}")
```

### C#
```csharp
public class ShipToAddressApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public ShipToAddressApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<List<ShipToAddress>> GetCustomerAddressesAsync(string customerNo)
    {
        var filter = $"customerNo eq '{customerNo}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/shiptoAddresses?$filter={filter}&$orderby=code asc");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<ShipToAddress>>(json);
        return result.Value;
    }
    
    public async Task<ShipToAddress> GetAddressAsync(string customerNo, string addressCode)
    {
        var filter = $"customerNo eq '{customerNo}' and code eq '{addressCode}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/shiptoAddresses?$filter={filter}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<ShipToAddress>>(json);
        return result.Value.FirstOrDefault();
    }
    
    public string FormatAddress(ShipToAddress address)
    {
        var lines = new List<string>
        {
            address.Name,
            address.Name2,
            address.Address,
            address.Address2,
            $"{address.City}, {address.County} {address.PostCode}",
            address.CountryRegionCode
        }.Where(line => !string.IsNullOrWhiteSpace(line));
        
        return string.Join(Environment.NewLine, lines);
    }
}

public class ShipToAddress
{
    public Guid SystemId { get; set; }
    public string CustomerNo { get; set; }
    public string Code { get; set; }
    public string Name { get; set; }
    public string Name2 { get; set; }
    public string Address { get; set; }
    public string Address2 { get; set; }
    public string City { get; set; }
    public string Contact { get; set; }
    public string PhoneNo { get; set; }
    public string PostCode { get; set; }
    public string County { get; set; }
    public string CountryRegionCode { get; set; }
    public string EMail { get; set; }
    public DateTime? LastDateModified { get; set; }
}
```

## Business Logic Notes

- **Read-Only**: Addresses managed in BC, API for display/selection
- **Customer-Specific**: Addresses linked to customer records
- **Code as Key**: Address code uniquely identifies address for customer
- **Address Formatting**: Build multi-line addresses for display
- **Contact Info**: Includes contact person, phone, email

## UI Implementation

### Address Selector
```javascript
// Build address dropdown
addresses.forEach(addr => {
  const option = new Option(
    `${addr.code} - ${addr.name} (${addr.city})`,
    addr.code
  );
  selectElement.add(option);
});
```

### Address Display Card
```html
<div class="address-card">
  <h4>${address.name}</h4>
  <p>${address.address}</p>
  <p>${address.city}, ${address.county} ${address.postCode}</p>
  <p>${address.countryRegionCode}</p>
  <p>Contact: ${address.contact}</p>
  <p>Phone: ${address.phoneNo}</p>
</div>
```

## Performance Tips

1. **Cache Addresses**: Cache per customer session
2. **Filter Early**: Always filter by `customerNo`
3. **Minimal Fields**: Use `$select` for dropdown lists
4. **Prefetch**: Load addresses when customer logs in

## Related APIs
- **Ship-To Address Edit**: Editable version for address management
- **Customers**: Customer information
- **Web Orders**: Order shipping address selection

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
