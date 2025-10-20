# Customer API (Read-Only) - Developer Guide

## Overview
The Customer API provides read-only access to customer master data including contact information, balances, and web integration status.

## API Endpoint Details
- **Endpoint**: `/customers`
- **Entity Name**: customer
- **Entity Set Name**: customers
- **Page ID**: 71979
- **Source Table**: Customer
- **API Group**: webbevica
- **Publisher**: tvisiontech
- **Version**: v2.0

## Permissions
- **Insert**: Not Allowed
- **Modify**: Partially Allowed (use CustomersEdit for modifications)
- **Delete**: Not Allowed
- **Read**: Allowed

## Base URL
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/customers
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `no` | String | Customer number |
| `name` | String | Customer name |
| `blocked` | Enum | Block status (blank, Ship, Invoice, All) |
| `address` | String | Street address line 1 |
| `address2` | String | Street address line 2 |
| `city` | String | City |
| `county` | String | County/State |
| `countryRegionCode` | String | Country/region code |
| `postCode` | String | Postal/ZIP code |
| `contact` | String | Contact person name |
| `phoneNo` | String | Phone number |
| `eMail` | String | Email address |
| `homePage` | String | Website URL |
| `languageCode` | String | Language code |
| `currencyCode` | String | Default currency |
| `shipmentMethodCode` | String | Shipment method |
| `shippingAgentCode` | String | Shipping agent |
| `shippingAgentServiceCode` | String | Shipping service |
| `locationCode` | String | Default location |
| `paymentMethodCode` | String | Payment method |
| `paymentTermsCode` | String | Payment terms |
| `vatRegistrationNo` | String | VAT registration number |
| `vatBusPostingGroup` | String | VAT business posting group |
| `genBusPostingGroup` | String | General business posting group |
| `customerPostingGroup` | String | Customer posting group |
| `customerPriceGroup` | String | Customer price group |
| `customerDiscGroup` | String | Customer discount group |
| `salespersonCode` | String | Salesperson code |
| `territoryCode` | String | Territory code |
| `tvtAWRSURN` | String | AWRS URN (UK alcohol licensing) |
| `gln` | String | Global Location Number |
| `balance` | Decimal | Current balance |
| `balanceLCY` | Decimal | Balance in local currency |
| `balanceDue` | Decimal | Balance due |
| `balanceDueLCY` | Decimal | Balance due in local currency |
| `globalDimension1Code` | String | Global dimension 1 |
| `globalDimension2Code` | String | Global dimension 2 |
| `tvtwsWebId` | Integer | Web customer ID |
| `tvtwsWebLastModDateTime` | DateTime | Web last modified timestamp |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemCreatedBy` | GUID | Created by user ID |
| `systemModifiedAt` | DateTime | Last modification timestamp |
| `systemModifiedBy` | GUID | Modified by user ID |

## Common Use Cases

### 1. Get All Active Customers
```http
GET /customers?$filter=blocked eq ' '
```

### 2. Search Customers by Name
```http
GET /customers?$filter=contains(name, 'Limited')
```

### 3. Get Customer with Balance
```http
GET /customers?$filter=balanceLCY gt 0&$orderby=balanceLCY desc
```

### 4. Get Customer by Number
```http
GET /customers?$filter=no eq 'CUST001'
```

### 5. Get Web-Enabled Customers
```http
GET /customers?$filter=tvtwsWebId ne null
```

### 6. Get Customers by Email
```http
GET /customers?$filter=eMail eq 'customer@example.com'
```

## Code Examples

### JavaScript
```javascript
class CustomerAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getCustomer(customerNo) {
    const response = await fetch(
      `${this.baseUrl}/customers?$filter=no eq '${customerNo}'`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value[0];
  }

  async searchCustomers(searchTerm) {
    const response = await fetch(
      `${this.baseUrl}/customers?$filter=contains(name, '${searchTerm}') or contains(eMail, '${searchTerm}')`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getCustomerBalance(customerNo) {
    const customer = await this.getCustomer(customerNo);
    return {
      balance: customer.balanceLCY,
      balanceDue: customer.balanceDueLCY
    };
  }
}

// Usage
const api = new CustomerAPI(baseUrl, accessToken);
const customer = await api.getCustomer('CUST001');
console.log(`${customer.name}: Balance ${customer.balanceLCY}`);
```

### Python
```python
class CustomerAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_customer(self, customer_no: str) -> dict:
        response = requests.get(
            f'{self.base_url}/customers',
            headers=self.headers,
            params={'$filter': f"no eq '{customer_no}'"}
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None
    
    def get_customers_with_debt(self) -> list:
        response = requests.get(
            f'{self.base_url}/customers',
            headers=self.headers,
            params={'$filter': 'balanceDueLCY gt 0', '$orderby': 'balanceDueLCY desc'}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def search_by_email(self, email: str) -> dict:
        response = requests.get(
            f'{self.base_url}/customers',
            headers=self.headers,
            params={'$filter': f"eMail eq '{email}'"}
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None

# Usage
api = CustomerAPI(base_url, access_token)
customer = api.get_customer('CUST001')
print(f"Customer: {customer['name']}, Balance: {customer['balanceLCY']}")
```

### C#
```csharp
public class CustomerApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public CustomerApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<Customer> GetCustomerAsync(string customerNo)
    {
        var filter = $"no eq '{customerNo}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/customers?$filter={filter}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<Customer>>(json);
        return result.Value.FirstOrDefault();
    }
    
    public async Task<List<Customer>> SearchCustomersAsync(string searchTerm)
    {
        var filter = $"contains(name, '{searchTerm}')";
        var response = await _httpClient.GetAsync($"{_baseUrl}/customers?$filter={filter}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<Customer>>(json);
        return result.Value;
    }
}

public class Customer
{
    public Guid SystemId { get; set; }
    public string No { get; set; }
    public string Name { get; set; }
    public string Blocked { get; set; }
    public string EMail { get; set; }
    public string PhoneNo { get; set; }
    public decimal BalanceLCY { get; set; }
    public decimal BalanceDueLCY { get; set; }
    public int? TvtwsWebId { get; set; }
}
```

## Business Logic Notes

- **Blocked Status**: Empty string = active, "Ship" = cannot ship, "Invoice" = cannot invoice, "All" = completely blocked
- **Balance Fields**: Use `balanceLCY` and `balanceDueLCY` for accurate local currency values
- **Web Integration**: `tvtwsWebId` links to web platform customer records
- **Email Validation**: Email field is not validated; check format client-side
- **GLN**: Global Location Number for EDI integration

## Filtering Tips

```http
# Active customers only
$filter=blocked eq ' '

# Customers with email
$filter=eMail ne null and eMail ne ''

# Customers in specific territory
$filter=territoryCode eq 'SOUTH'

# Customers modified after date
$filter=systemModifiedAt gt 2025-10-01T00:00:00Z

# Web-enabled customers
$filter=tvtwsWebId ne null
```

## Error Handling

Common errors:
- **401 Unauthorized**: Invalid access token
- **404 Not Found**: Customer doesn't exist
- **400 Bad Request**: Invalid filter syntax

## Performance Tips

1. **Use $select**: Only retrieve needed fields
2. **Filter efficiently**: Use indexed fields (`no`, `systemId`)
3. **Cache data**: Customer master data changes infrequently
4. **Pagination**: Use `$top` and `$skip` for large lists
5. **Avoid wildcards**: Use exact matches when possible

## Related APIs
- **CustomersEdit**: For creating/updating customers
- **CustEntries**: For customer ledger entries
- **ShipToAddresses**: For alternative delivery addresses

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
