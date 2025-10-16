# Paid Reserve Entries API - Developer Guide

## Overview
The Paid Reserve Entries API provides read-only access to transaction entries related to paid reserve inventory movements.

## API Endpoint Details
- **Endpoint**: `/PaidReserveEntries`
- **Entity Name**: PaidReserveEntry
- **Entity Set Name**: PaidReserveEntries
- **Page ID**: 71977
- **Source Table**: TVT Paid Reserve Entry
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/PaidReserveEntries
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `entryNo` | Integer | Entry number |
| `paidReserveNo` | String | Paid reserve number |
| `itemNo` | String | Item number |
| `itemDescription` | String | Item description |
| `postingDate` | Date | Posting date |
| `entryType` | Enum | Entry type (Purchase, Sale, Transfer, etc.) |
| `documentNo` | String | Document number |
| `documentType` | Enum | Document type |
| `quantity` | Decimal | Transaction quantity |
| `remainingQuantity` | Decimal | Remaining quantity after transaction |
| `sourceType` | Enum | Source type |
| `sourceNo` | String | Source number |
| `locationCode` | String | Location code |
| `unitOfMeasureCode` | String | Unit of measure |

## Common Use Cases

### Get Entries for Reserve
```http
GET /PaidReserveEntries?$filter=paidReserveNo eq 'PR-001'&$orderby=postingDate desc
```

### Get Recent Entries
```http
GET /PaidReserveEntries?$filter=postingDate ge 2025-10-01&$orderby=postingDate desc
```

### Get Entries by Item
```http
GET /PaidReserveEntries?$filter=itemNo eq 'WINE001'
```

## Code Examples

### JavaScript
```javascript
class PaidReserveEntryAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getReserveEntries(reserveNo) {
    const response = await fetch(
      `${this.baseUrl}/PaidReserveEntries?$filter=paidReserveNo eq '${reserveNo}'&$orderby=postingDate desc`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getRecentEntries(fromDate) {
    const response = await fetch(
      `${this.baseUrl}/PaidReserveEntries?$filter=postingDate ge ${fromDate}&$orderby=postingDate desc`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }
}

// Usage
const api = new PaidReserveEntryAPI(baseUrl, accessToken);

const entries = await api.getReserveEntries('PR-001');
console.log(`Reserve has ${entries.length} transactions`);

entries.forEach(entry => {
  console.log(`${entry.postingDate}: ${entry.entryType} ${entry.quantity} ${entry.itemDescription}`);
});
```

### Python
```python
class PaidReserveEntryAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_reserve_entries(self, reserve_no: str) -> list:
        response = requests.get(
            f'{self.base_url}/PaidReserveEntries',
            headers=self.headers,
            params={
                '$filter': f"paidReserveNo eq '{reserve_no}'",
                '$orderby': 'postingDate desc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_recent_entries(self, from_date: str) -> list:
        response = requests.get(
            f'{self.base_url}/PaidReserveEntries',
            headers=self.headers,
            params={
                '$filter': f"postingDate ge {from_date}",
                '$orderby': 'postingDate desc'
            }
        )
        response.raise_for_status()
        return response.json()['value']

# Usage
api = PaidReserveEntryAPI(base_url, access_token)
entries = api.get_reserve_entries('PR-001')

for entry in entries:
    print(f"{entry['entryNo']}: {entry['entryType']} - {entry['quantity']}")
```

### C#
```csharp
public class PaidReserveEntryApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public async Task<List<PaidReserveEntry>> GetReserveEntriesAsync(string reserveNo)
    {
        var filter = $"paidReserveNo eq '{reserveNo}'";
        var response = await _httpClient.GetAsync(
            $"{_baseUrl}/PaidReserveEntries?$filter={filter}&$orderby=postingDate desc"
        );
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<PaidReserveEntry>>(json);
        return result.Value;
    }
}

public class PaidReserveEntry
{
    public Guid SystemId { get; set; }
    public int EntryNo { get; set; }
    public string PaidReserveNo { get; set; }
    public string ItemNo { get; set; }
    public DateTime PostingDate { get; set; }
    public string EntryType { get; set; }
    public string DocumentNo { get; set; }
    public decimal Quantity { get; set; }
    public decimal RemainingQuantity { get; set; }
}
```

## Entry Types

- **Purchase** - Reserve purchase
- **Sale** - Reserve sale/withdrawal
- **Transfer** - Reserve transfer
- **Adjustment** - Quantity adjustment

## Business Logic Notes

- **Read-Only**: Transaction history
- **Chronological**: Track reserve movements over time
- **Remaining Qty**: Shows balance after each transaction
- **Audit Trail**: Complete transaction history

## Related APIs
- **Paid Reserves**: Reserve headers
- **Items**: Item information

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
