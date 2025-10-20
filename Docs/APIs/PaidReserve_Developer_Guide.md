# Paid Reserves API - Developer Guide

## Overview
The Paid Reserves API provides read-only access to paid reserve inventory allocations for wine storage and trading.

## API Endpoint Details
- **Endpoint**: `/PaidReserves`
- **Entity Name**: PaidReserve
- **Entity Set Name**: PaidReserves
- **Page ID**: 71976
- **Source Table**: TVT Paid Reserve Information
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/PaidReserves
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `no` | String | Reserve number |
| `sourceType` | Enum | Source type (Customer, Vendor) |
| `sourceNo` | String | Source number |
| `sourceName` | String | Source name |
| `itemNo` | String | Item number |
| `itemDescription` | String | Item description |
| `unitOfMeasureCode` | String | Unit of measure |
| `rotationNo` | String | Rotation number |
| `qtyPerUnitOfMeasure` | Decimal | Quantity per UOM |
| `origPaidReserveNo` | String | Original reserve number |
| `quantity` | Decimal | Total quantity |
| `remainingQuantity` | Decimal | Available quantity |
| `qtyBooked` | Decimal | Booked quantity |
| `qtyOnBroking` | Decimal | Quantity on broking |
| `unitPrice` | Decimal | Unit price |
| `unitCost` | Decimal | Unit cost |
| `withdrawalDutyAmtDP` | Decimal | Withdrawal duty amount |
| `withdrawalVATAmtDP` | Decimal | Withdrawal VAT amount |
| `withdrawalTotalAmtDP` | Decimal | Total withdrawal amount |
| `condition` | String | Wine condition |
| `provenanceSource` | String | Provenance/source |
| `contactNomineeNo` | String | Contact nominee number |
| `contactNomineeName` | String | Contact nominee name |
| `documentDate` | Date | Document date |
| `postingDate` | Date | Posting date |
| `documentNo` | String | Document number |
| `expDeliveryInstruction` | String | Export delivery instruction |
| `expDeliveryShipTo` | String | Export delivery ship-to |
| `internalInformation` | String | Internal notes |
| `externalDocumentNo` | String | External document number |

## Common Use Cases

### Get Customer Paid Reserves
```http
GET /PaidReserves?$filter=sourceType eq 'Customer' and sourceNo eq 'CUST001'
```

### Get Available Reserves
```http
GET /PaidReserves?$filter=remainingQuantity gt 0
```

### Get Reserves for Item
```http
GET /PaidReserves?$filter=itemNo eq 'WINE001'
```

### Get Reserve by Number
```http
GET /PaidReserves?$filter=no eq 'PR-001'
```

## Code Examples

### JavaScript
```javascript
class PaidReserveAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getCustomerReserves(customerNo) {
    const filter = `sourceType eq 'Customer' and sourceNo eq '${customerNo}'`;
    const response = await fetch(
      `${this.baseUrl}/PaidReserves?$filter=${encodeURIComponent(filter)}`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getAvailableReserves(itemNo = null) {
    let filter = 'remainingQuantity gt 0';
    if (itemNo) filter += ` and itemNo eq '${itemNo}'`;
    
    const response = await fetch(
      `${this.baseUrl}/PaidReserves?$filter=${encodeURIComponent(filter)}`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getReserve(reserveNo) {
    const response = await fetch(
      `${this.baseUrl}/PaidReserves?$filter=no eq '${reserveNo}'`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value[0];
  }
}

// Usage
const api = new PaidReserveAPI(baseUrl, accessToken);

// Get customer's paid reserves
const reserves = await api.getCustomerReserves('CUST001');
console.log(`Customer has ${reserves.length} paid reserves`);

reserves.forEach(reserve => {
  console.log(`${reserve.itemDescription}: ${reserve.remainingQuantity} available`);
});

// Check available reserves for item
const available = await api.getAvailableReserves('WINE001');
const totalAvailable = available.reduce((sum, r) => sum + r.remainingQuantity, 0);
console.log(`Total available for WINE001: ${totalAvailable}`);
```

### Python
```python
class PaidReserveAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_customer_reserves(self, customer_no: str) -> list:
        filter_query = f"sourceType eq 'Customer' and sourceNo eq '{customer_no}'"
        response = requests.get(
            f'{self.base_url}/PaidReserves',
            headers=self.headers,
            params={'$filter': filter_query}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_available_reserves(self, item_no: str = None) -> list:
        filter_query = 'remainingQuantity gt 0'
        if item_no:
            filter_query += f" and itemNo eq '{item_no}'"
        
        response = requests.get(
            f'{self.base_url}/PaidReserves',
            headers=self.headers,
            params={'$filter': filter_query}
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_reserve(self, reserve_no: str) -> dict:
        response = requests.get(
            f'{self.base_url}/PaidReserves',
            headers=self.headers,
            params={'$filter': f"no eq '{reserve_no}'"}
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None

# Usage
api = PaidReserveAPI(base_url, access_token)

# Get reserves with availability
reserves = api.get_available_reserves('WINE001')
for reserve in reserves:
    print(f"{reserve['no']}: {reserve['remainingQuantity']} available")
    print(f"  Price: ${reserve['unitPrice']:.2f}")
    print(f"  Rotation: {reserve['rotationNo']}")
```

### C#
```csharp
public class PaidReserveApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public async Task<List<PaidReserve>> GetCustomerReservesAsync(string customerNo)
    {
        var filter = $"sourceType eq 'Customer' and sourceNo eq '{customerNo}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/PaidReserves?$filter={Uri.EscapeDataString(filter)}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<PaidReserve>>(json);
        return result.Value;
    }
    
    public async Task<List<PaidReserve>> GetAvailableReservesAsync(string itemNo = null)
    {
        var filter = "remainingQuantity gt 0";
        if (!string.IsNullOrEmpty(itemNo))
            filter += $" and itemNo eq '{itemNo}'";
        
        var response = await _httpClient.GetAsync($"{_baseUrl}/PaidReserves?$filter={Uri.EscapeDataString(filter)}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<PaidReserve>>(json);
        return result.Value;
    }
}

public class PaidReserve
{
    public Guid SystemId { get; set; }
    public string No { get; set; }
    public string SourceType { get; set; }
    public string SourceNo { get; set; }
    public string ItemNo { get; set; }
    public string ItemDescription { get; set; }
    public decimal Quantity { get; set; }
    public decimal RemainingQuantity { get; set; }
    public decimal UnitPrice { get; set; }
    public string RotationNo { get; set; }
}
```

## Business Logic Notes

- **Read-Only**: Managed through BC inventory processes
- **Wine Storage**: Tracks allocated wine inventory
- **Remaining Quantity**: Available for orders
- **Rotation Tracking**: Wine rotation/lot numbers
- **Duty Calculations**: Withdrawal duty and VAT amounts
- **Provenance**: Source and condition tracking
- **Nominee**: Contact person for reserve

## Use Cases

1. **Customer Portal**: Show customer's stored wine
2. **Order Allocation**: Check available reserves for orders
3. **Inventory Tracking**: Monitor reserve quantities
4. **Duty Calculation**: Calculate withdrawal costs

## Performance Tips

1. **Filter by Customer**: Always filter by `sourceNo` for customer queries
2. **Check Availability**: Use `remainingQuantity gt 0` filter
3. **Cache Reserve Data**: Cache for session duration
4. **Index Fields**: Filter on `sourceNo`, `itemNo`, `no`

## Related APIs
- **Paid Reserve Entries**: Reserve transaction entries
- **Items**: Item information
- **Customers**: Customer data
- **Web Orders**: Order allocation

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
