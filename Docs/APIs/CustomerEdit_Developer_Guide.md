# Customer Edit API - Developer Guide

## Overview
The Customer Edit API provides full create and update capabilities for customer master data with extensive field access.

## API Endpoint Details
- **Endpoint**: `/customersEdit`
- **Entity Name**: customerEdit
- **Entity Set Name**: customersEdit
- **Page ID**: 72201
- **Source Table**: Customer
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/customersEdit
```

## Key Differences from Customer API

This API provides **write access** and exposes **100+ fields** including:
- Extended contact information (mobile, fax)
- Credit management fields
- Privacy and GDPR fields
- All setup and configuration fields
- Custom TVT fields

## Field Reference (Key Fields)

### Basic Information
- `no` - Customer number (required for creation)
- `name`, `name2` - Customer names
- `searchName` - Search name
- `blocked` - Block status
- `contactType`, `contact` - Contact details

### Address & Contact
- `address`, `address2` - Street address
- `city`, `county`, `postCode`, `countryRegionCode` - Location
- `phoneNo`, `mobilePhoneNo`, `faxNo` - Phone numbers
- `eMail`, `homePage` - Email and website

### Financial Settings
- `creditLimitLCY` - Credit limit
- `customerPostingGroup` - Posting group
- `customerPriceGroup`, `customerDiscGroup` - Price/discount groups
- `paymentTermsCode`, `paymentMethodCode` - Payment settings
- `currencyCode` - Default currency

### Tax & Legal
- `vatRegistrationNo` - VAT registration
- `vatBusPostingGroup` - VAT posting group
- `registrationNumber` - Company registration
- `eoriNumber` - EORI number for customs

### Shipping
- `locationCode` - Default location
- `shipmentMethodCode` - Shipment method
- `shippingAgentCode`, `shippingAgentServiceCode` - Shipping agent
- `shippingTime` - Shipping time
- `shippingAdvice` - Shipping advice

### Custom Fields
- `tvtAWRSURN`, `tvtAWRSDate` - UK alcohol licensing
- `tvtContraVendorNo` - Contra vendor
- `tvtCreditStatus` - Credit status
- `tvtwsWebId`, `tvtwsWebLastModDateTime` - Web integration

### Privacy & Compliance
- `privacyBlocked` - GDPR privacy block
- `formatRegion` - Format region

## Common Operations

### Create New Customer
```http
POST /customersEdit
Content-Type: application/json

{
  "no": "NEWCUST001",
  "name": "New Customer Ltd",
  "address": "123 High Street",
  "city": "London",
  "postCode": "SW1A 1AA",
  "countryRegionCode": "GB",
  "eMail": "info@newcustomer.com",
  "phoneNo": "+44 20 1234 5678",
  "paymentTermsCode": "30D",
  "currencyCode": "GBP"
}
```

### Update Customer
```http
PATCH /customersEdit({systemId})
Content-Type: application/json
If-Match: *

{
  "eMail": "newemail@customer.com",
  "phoneNo": "+44 20 9876 5432",
  "mobilePhoneNo": "+44 7700 900123"
}
```

### Update Credit Limit
```http
PATCH /customersEdit({systemId})
Content-Type: application/json
If-Match: *

{
  "creditLimitLCY": 50000.00,
  "tvtCreditStatus": "Approved"
}
```

## Code Examples

### JavaScript
```javascript
class CustomerEditAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async createCustomer(customerData) {
    const response = await fetch(`${this.baseUrl}/customersEdit`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify(customerData)
    });
    
    if (!response.ok) {
      const error = await response.json();
      throw new Error(`Failed to create customer: ${error.error.message}`);
    }
    
    return await response.json();
  }

  async updateCustomer(systemId, updates) {
    const response = await fetch(`${this.baseUrl}/customersEdit(${systemId})`, {
      method: 'PATCH',
      headers: {
        ...this.headers,
        'If-Match': '*'
      },
      body: JSON.stringify(updates)
    });
    
    if (!response.ok) {
      const error = await response.json();
      throw new Error(`Failed to update customer: ${error.error.message}`);
    }
    
    return await response.json();
  }

  async blockCustomer(systemId, blockType = 'All') {
    return await this.updateCustomer(systemId, { blocked: blockType });
  }
}

// Usage
const api = new CustomerEditAPI(baseUrl, accessToken);

// Create customer
const newCustomer = await api.createCustomer({
  no: 'CUST9999',
  name: 'Test Customer Ltd',
  address: '100 Test Street',
  city: 'London',
  postCode: 'E1 6AN',
  countryRegionCode: 'GB',
  eMail: 'test@example.com'
});

// Update customer
await api.updateCustomer(newCustomer.systemId, {
  phoneNo: '+44 20 1234 5678',
  creditLimitLCY: 10000.00
});
```

### Python
```python
class CustomerEditAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def create_customer(self, customer_data: dict) -> dict:
        response = requests.post(
            f'{self.base_url}/customersEdit',
            headers=self.headers,
            json=customer_data
        )
        response.raise_for_status()
        return response.json()
    
    def update_customer(self, system_id: str, updates: dict) -> dict:
        headers = self.headers.copy()
        headers['If-Match'] = '*'
        
        response = requests.patch(
            f'{self.base_url}/customersEdit({system_id})',
            headers=headers,
            json=updates
        )
        response.raise_for_status()
        return response.json()
    
    def update_contact_info(self, system_id: str, email: str = None, 
                           phone: str = None, mobile: str = None):
        updates = {}
        if email:
            updates['eMail'] = email
        if phone:
            updates['phoneNo'] = phone
        if mobile:
            updates['mobilePhoneNo'] = mobile
        
        return self.update_customer(system_id, updates)

# Usage
api = CustomerEditAPI(base_url, access_token)

# Create customer
customer = api.create_customer({
    'no': 'NEWCUST',
    'name': 'New Customer Ltd',
    'address': '123 Main St',
    'city': 'Manchester',
    'postCode': 'M1 1AA',
    'countryRegionCode': 'GB'
})

# Update contact info
api.update_contact_info(
    customer['systemId'],
    email='new@email.com',
    mobile='+44 7700 900123'
)
```

### C#
```csharp
public class CustomerEditApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public CustomerEditApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<CustomerEdit> CreateCustomerAsync(CustomerEdit customer)
    {
        var json = JsonSerializer.Serialize(customer);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/customersEdit", content);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<CustomerEdit>(responseJson);
    }
    
    public async Task<CustomerEdit> UpdateCustomerAsync(Guid systemId, object updates)
    {
        var json = JsonSerializer.Serialize(updates);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var request = new HttpRequestMessage(HttpMethod.Patch, $"{_baseUrl}/customersEdit({systemId})")
        {
            Content = content
        };
        request.Headers.Add("If-Match", "*");
        
        var response = await _httpClient.SendAsync(request);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<CustomerEdit>(responseJson);
    }
}
```

## Validation Rules

### Required Fields
- `no` - Customer number (when creating)

### Field Constraints
- `creditLimitLCY` must be >= 0
- `eMail` should be valid email format (client-side validation recommended)
- `blocked` values: blank, "Ship", "Invoice", "All"

## Business Logic Notes

- **Delayed Insert**: Set to true, allows setting key fields before insert
- **Customer Numbers**: Can be auto-generated or manually specified
- **Block Status**: Prevents transactions based on block type
- **Credit Limit**: 0 = unlimited, >0 = specific limit
- **Web Sync**: `tvtwsWebId` and `tvtwsWebLastModDateTime` manage web integration

## Error Handling

### Common Errors
- **400 Bad Request**: Missing required fields or validation failure
- **409 Conflict**: Duplicate customer number
- **412 Precondition Failed**: Missing If-Match header on PATCH
- **404 Not Found**: Customer doesn't exist (on PATCH)

### Example Error Response
```json
{
  "error": {
    "code": "ValidationError",
    "message": "The Customer already exists. Identification fields and values: No.='CUST001'"
  }
}
```

## Best Practices

1. **Always validate data client-side** before API calls
2. **Use If-Match: *** for updates to avoid concurrency issues
3. **Set reasonable credit limits** based on business rules
4. **Maintain web sync fields** when integrating with web platforms
5. **Handle privacy blocked customers** according to GDPR requirements
6. **Validate VAT numbers** before submission
7. **Use proper country codes** from ISO 3166-1 alpha-2

## Related APIs
- **Customer (Read-Only)**: For querying customer data
- **ShipToAddressesEdit**: For managing delivery addresses
- **CustEntries**: For viewing account activity

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
