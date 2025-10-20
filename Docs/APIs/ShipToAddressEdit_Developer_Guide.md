# Ship-To Address Edit API - Developer Guide

## Overview
The Ship-To Address Edit API provides full CRUD access for creating and managing customer delivery addresses.

## API Endpoint Details
- **Endpoint**: `/shipToAddressesEdit`
- **Entity Name**: shipToAddressEdit
- **Entity Set Name**: shipToAddressesEdit
- **Page ID**: 72202
- **Source Table**: Ship-to Address
- **API Group**: webbevica
- **Publisher**: tvisiontech
- **Version**: v2.0

## Permissions
- **Insert**: Allowed
- **Modify**: Allowed
- **Delete**: Not Allowed
- **Read**: Allowed

## Base URL
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/shipToAddressEdit
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `customerNo` | String | Customer number (required) |
| `code` | String | Ship-to address code (required) |
| `name` | String | Recipient name (required) |
| `name2` | String | Additional name field |
| `address` | String | Street address line 1 (required) |
| `address2` | String | Street address line 2 |
| `city` | String | City (required) |
| `contact` | String | Contact person |
| `phoneNo` | String | Phone number |
| `faxNo` | String | Fax number |
| `postCode` | String | Postal/ZIP code (required) |
| `county` | String | County/State |
| `countryRegionCode` | String | Country/region code (required) |
| `eMail` | String | Email address |
| `homePage` | String | Home page URL |
| `gln` | String | Global Location Number |
| `locationCode` | String | Location code |
| `salespersonCode` | String | Salesperson code |
| `shipmentMethodCode` | String | Shipment method code |
| `shippingAgentCode` | String | Shipping agent code |
| `shippingAgentServiceCode` | String | Shipping agent service code |
| `placeOfExport` | String | Place of export |
| `tvtDutyStatus` | Enum | Duty status |
| `tvtWarehouseKeeperNo` | String | Warehousekeeper number |
| `tvtWarehouseVATNo` | String | Warehouse VAT number |
| `tvthmHMRCDefAccount` | String | HMRC deferment account |
| `tvthmHMRCMovementType` | String | HMRC movement type |
| `tvtwsWebId` | String | Web ID |
| `taxAreaCode` | String | Tax area code |
| `taxLiable` | Boolean | Tax liable |
| `telexAnswerBack` | String | Telex answer back |
| `telexNo` | String | Telex number |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemCreatedBy` | GUID | Created by user ID |
| `systemModifiedAt` | DateTime | Last modification |
| `systemModifiedBy` | GUID | Modified by user ID |

## Common Operations

### Create New Ship-To Address
```http
POST /shipToAddressesEdit
Content-Type: application/json

{
  "customerNo": "CUST001",
  "code": "WAREHOUSE2",
  "name": "Customer Warehouse #2",
  "address": "456 Industrial Blvd",
  "city": "Boston",
  "county": "MA",
  "postCode": "02101",
  "countryRegionCode": "US",
  "contact": "Jane Smith",
  "phoneNo": "+1-617-555-0200",
  "eMail": "warehouse2@customer.com"
}
```

### Update Ship-To Address
```http
PATCH /shipToAddressesEdit({systemId})
Content-Type: application/json
If-Match: *

{
  "phoneNo": "+1-617-555-0299",
  "contact": "Jane Smith-Jones",
  "eMail": "jane.smith@customer.com"
}
```

### Note on Delete
Delete is not allowed on this API.
DELETE /shipToAddressEdit({systemId})
If-Match: *
```

## Code Examples

### JavaScript
```javascript
class ShipToAddressEditAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async createAddress(addressData) {
    const response = await fetch(`${this.baseUrl}/shipToAddressEdit`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify(addressData)
    });
    
    if (!response.ok) {
      const error = await response.text();
      throw new Error(`Failed to create address: ${error}`);
    }
    
    return await response.json();
  }

  async updateAddress(systemId, updates) {
    const response = await fetch(`${this.baseUrl}/shipToAddressEdit(${systemId})`, {
      method: 'PATCH',
      headers: {
        ...this.headers,
        'If-Match': '*'
      },
      body: JSON.stringify(updates)
    });
    
    if (!response.ok) {
      throw new Error(`Failed to update address: ${await response.text()}`);
    }
    
    return await response.json();
  }

  async deleteAddress(systemId) {
    const response = await fetch(`${this.baseUrl}/shipToAddressEdit(${systemId})`, {
      method: 'DELETE',
      headers: {
        ...this.headers,
        'If-Match': '*'
      }
    });
    
    if (!response.ok) {
      throw new Error(`Failed to delete address: ${await response.text()}`);
    }
  }

  async getAddress(customerNo, code) {
    const response = await fetch(
      `${this.baseUrl}/shipToAddressEdit?$filter=customerNo eq '${customerNo}' and code eq '${code}'`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value[0];
  }

  validateAddress(address) {
    const errors = [];
    
    if (!address.customerNo) errors.push('Customer number is required');
    if (!address.code) errors.push('Address code is required');
    if (!address.name) errors.push('Name is required');
    if (!address.address) errors.push('Street address is required');
    if (!address.city) errors.push('City is required');
    if (!address.postCode) errors.push('Postal code is required');
    if (!address.countryRegionCode) errors.push('Country is required');
    
    return errors;
  }
}

// Usage
const api = new ShipToAddressEditAPI(baseUrl, accessToken);

// Create new address from form
const newAddress = {
  customerNo: 'CUST001',
  code: 'OFFICE',
  name: 'Corporate Office',
  address: '100 Main Street',
  address2: 'Suite 500',
  city: 'New York',
  county: 'NY',
  postCode: '10001',
  countryRegionCode: 'US',
  contact: 'John Doe',
  phoneNo: '+1-212-555-0100',
  eMail: 'john.doe@company.com'
};

// Validate before creating
const errors = api.validateAddress(newAddress);
if (errors.length > 0) {
  console.error('Validation errors:', errors);
} else {
  const created = await api.createAddress(newAddress);
  console.log(`Address created: ${created.code}`);
}

// Update address
await api.updateAddress(created.systemId, {
  phoneNo: '+1-212-555-0199',
  contact: 'John Doe (Manager)'
});

console.log('Address updated successfully');
```

### Python
```python
from typing import Dict, List, Optional
import re

class ShipToAddressEditAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def create_address(self, address_data: dict) -> dict:
        response = requests.post(
            f'{self.base_url}/shipToAddressEdit',
            headers=self.headers,
            json=address_data
        )
        response.raise_for_status()
        return response.json()
    
    def update_address(self, system_id: str, updates: dict) -> dict:
        headers = self.headers.copy()
        headers['If-Match'] = '*'
        
        response = requests.patch(
            f'{self.base_url}/shipToAddressEdit({system_id})',
            headers=headers,
            json=updates
        )
        response.raise_for_status()
        return response.json()
    
    def delete_address(self, system_id: str) -> None:
        headers = self.headers.copy()
        headers['If-Match'] = '*'
        
        response = requests.delete(
            f'{self.base_url}/shipToAddressEdit({system_id})',
            headers=headers
        )
        response.raise_for_status()
    
    def get_address(self, customer_no: str, code: str) -> Optional[dict]:
        response = requests.get(
            f'{self.base_url}/shipToAddressEdit',
            headers=self.headers,
            params={
                '$filter': f"customerNo eq '{customer_no}' and code eq '{code}'"
            }
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None
    
    def validate_address(self, address: dict) -> List[str]:
        errors = []
        
        required_fields = {
            'customerNo': 'Customer number',
            'code': 'Address code',
            'name': 'Name',
            'address': 'Street address',
            'city': 'City',
            'postCode': 'Postal code',
            'countryRegionCode': 'Country'
        }
        
        for field, label in required_fields.items():
            if not address.get(field):
                errors.append(f'{label} is required')
        
        # Validate email format if provided
        if address.get('eMail') and not re.match(r'^[\w\.-]+@[\w\.-]+\.\w+$', address['eMail']):
            errors.append('Invalid email format')
        
        return errors

# Usage
api = ShipToAddressEditAPI(base_url, access_token)

# Create address from user input
new_address = {
    'customerNo': 'CUST001',
    'code': 'HOME',
    'name': 'Residential Address',
    'address': '123 Oak Street',
    'city': 'San Francisco',
    'county': 'CA',
    'postCode': '94102',
    'countryRegionCode': 'US',
    'contact': 'Jane Customer',
    'phoneNo': '+1-415-555-0100',
    'eMail': 'jane@example.com'
}

# Validate
errors = api.validate_address(new_address)
if errors:
    print("Validation errors:")
    for error in errors:
        print(f"  - {error}")
else:
    # Create
    created = api.create_address(new_address)
    print(f"Address created: {created['code']}")
    
    # Update
    api.update_address(created['systemId'], {
        'phoneNo': '+1-415-555-0199'
    })
    print("Address updated")
```

### C#
```csharp
public class ShipToAddressEditApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public ShipToAddressEditApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<ShipToAddressEdit> CreateAddressAsync(ShipToAddressEdit address)
    {
        var json = JsonSerializer.Serialize(address);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/shipToAddressEdit", content);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<ShipToAddressEdit>(responseJson);
    }
    
    public async Task<ShipToAddressEdit> UpdateAddressAsync(Guid systemId, ShipToAddressEdit updates)
    {
        var request = new HttpRequestMessage(HttpMethod.Patch, $"{_baseUrl}/shipToAddressEdit({systemId})");
        request.Headers.Add("If-Match", "*");
        request.Content = new StringContent(
            JsonSerializer.Serialize(updates),
            Encoding.UTF8,
            "application/json"
        );
        
        var response = await _httpClient.SendAsync(request);
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<ShipToAddressEdit>(json);
    }
    
    public async Task DeleteAddressAsync(Guid systemId)
    {
        var request = new HttpRequestMessage(HttpMethod.Delete, $"{_baseUrl}/shipToAddressEdit({systemId})");
        request.Headers.Add("If-Match", "*");
        
        var response = await _httpClient.SendAsync(request);
        response.EnsureSuccessStatusCode();
    }
    
    public List<string> ValidateAddress(ShipToAddressEdit address)
    {
        var errors = new List<string>();
        
        if (string.IsNullOrWhiteSpace(address.CustomerNo))
            errors.Add("Customer number is required");
        if (string.IsNullOrWhiteSpace(address.Code))
            errors.Add("Address code is required");
        if (string.IsNullOrWhiteSpace(address.Name))
            errors.Add("Name is required");
        if (string.IsNullOrWhiteSpace(address.Address))
            errors.Add("Street address is required");
        if (string.IsNullOrWhiteSpace(address.City))
            errors.Add("City is required");
        if (string.IsNullOrWhiteSpace(address.PostCode))
            errors.Add("Postal code is required");
        if (string.IsNullOrWhiteSpace(address.CountryRegionCode))
            errors.Add("Country is required");
        
        return errors;
    }
}

public class ShipToAddressEdit
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
}
```

## Required Fields

- `customerNo` - Customer the address belongs to
- `code` - Unique address code for customer
- `name` - Recipient/location name
- `address` - Street address
- `city` - City name
- `postCode` - Postal/ZIP code
- `countryRegionCode` - Country code (US, CA, UK, etc.)

## Business Logic Notes

- **Code Uniqueness**: Address code must be unique per customer
- **Customer Link**: Address must be linked to existing customer
- **Default Address**: First address may become default
- **Address Validation**: Consider using address validation service
- **Character Limits**: Check BC field lengths before submission

## Validation Rules

- All required fields must have values
- Email must be valid format (if provided)
- Phone number format varies by country
- Country code must exist in BC
- Address code: alphanumeric, typically 10-20 characters

## Error Handling

Common errors:
- **400**: Validation failure (missing required fields)
- **404**: Customer not found
- **409**: Duplicate address code for customer
- **422**: Invalid country code or data format

## Performance Tips

1. **Validate Client-Side**: Validate before API call
2. **Batch Creates**: Create multiple addresses in parallel
3. **Check Existence**: Verify address doesn't exist before creating
4. **Handle Duplicates**: Provide clear error messages for duplicate codes

## Related APIs
- **Ship-To Addresses**: Read-only address list
- **Customers**: Customer management
- **Web Orders**: Address selection for orders

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
