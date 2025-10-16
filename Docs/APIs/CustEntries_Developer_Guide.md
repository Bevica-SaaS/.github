# Customer Ledger Entries API - Developer Guide

## Overview
The Customer Ledger Entries API provides read-only access to customer accounting entries for tracking accounts receivable, payments, invoices, and credit memos.

## API Endpoint Details
- **Endpoint**: `/custEntries`
- **Entity Name**: custEntry
- **Entity Set Name**: custEntries
- **Page ID**: 71990
- **Source Table**: Cust. Ledger Entry
- **API Group**: webbevica
- **Publisher**: tvisiontech
- **Version**: v2.0

## Permissions
- **Insert**: Not Allowed
- **Modify**: Not Allowed
- **Delete**: Not Allowed
- **Read**: Allowed

## Base URL
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/custEntries
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `documentType` | Enum | Payment, Invoice, Credit Memo, Finance Charge Memo, Reminder, Refund |
| `documentNo` | String | Document number |
| `documentDate` | Date | Document date |
| `dueDate` | Date | Payment due date |
| `externalDocumentNo` | String | External document reference |
| `entryNo` | Integer | Entry number |
| `description` | String | Entry description |
| `open` | Boolean | Entry is open (unpaid) |
| `positive` | Boolean | Entry is positive (debit) |
| `amountLCY` | Decimal | Amount in local currency |
| `currencyCode` | String | Currency code |
| `originalAmount` | Decimal | Original amount |
| `remainingAmount` | Decimal | Remaining amount to be paid |
| `remainingAmtLCY` | Decimal | Remaining amount in local currency |
| `customerNo` | String | Customer number |
| `customerName` | String | Customer name |
| `systemCreatedAt` | DateTime | Creation timestamp |
| `systemCreatedBy` | GUID | Created by user ID |
| `systemModifiedAt` | DateTime | Last modification timestamp |
| `systemModifiedBy` | GUID | Modified by user ID |

## Common Use Cases

### 1. Get All Open Entries for a Customer
```http
GET /custEntries?$filter=customerNo eq 'CUST001' and open eq true
```

### 2. Get Overdue Invoices
```http
GET /custEntries?$filter=dueDate lt 2025-10-14 and open eq true and documentType eq 'Invoice'
```

### 3. Get Entries by Document Number
```http
GET /custEntries?$filter=documentNo eq 'INV-12345'
```

### 4. Get Customer Balance Summary
```http
GET /custEntries?$filter=customerNo eq 'CUST001' and open eq true&$select=documentNo,documentDate,remainingAmount,dueDate
```

### 5. Get Recent Entries
```http
GET /custEntries?$filter=documentDate ge 2025-10-01&$orderby=documentDate desc
```

## Code Examples

### JavaScript
```javascript
async function getCustomerOpenEntries(customerNo) {
  const response = await fetch(
    `${baseUrl}/custEntries?$filter=customerNo eq '${customerNo}' and open eq true`,
    {
      headers: {
        'Authorization': `Bearer ${accessToken}`,
        'Content-Type': 'application/json'
      }
    }
  );
  
  const data = await response.json();
  return data.value;
}

async function getOverdueInvoices() {
  const today = new Date().toISOString().split('T')[0];
  const response = await fetch(
    `${baseUrl}/custEntries?$filter=dueDate lt ${today} and open eq true and documentType eq 'Invoice'&$orderby=dueDate asc`,
    {
      headers: {
        'Authorization': `Bearer ${accessToken}`,
        'Content-Type': 'application/json'
      }
    }
  );
  
  const data = await response.json();
  return data.value;
}
```

### Python
```python
def get_customer_ledger_entries(customer_no: str, open_only: bool = True):
    filter_query = f"customerNo eq '{customer_no}'"
    if open_only:
        filter_query += " and open eq true"
    
    response = requests.get(
        f'{base_url}/custEntries',
        headers=headers,
        params={'$filter': filter_query}
    )
    return response.json()['value']

def calculate_customer_balance(customer_no: str):
    entries = get_customer_ledger_entries(customer_no, open_only=True)
    return sum(entry['remainingAmtLCY'] for entry in entries)
```

### C#
```csharp
public async Task<List<CustLedgerEntry>> GetCustomerEntriesAsync(string customerNo, bool openOnly = true)
{
    var filter = $"customerNo eq '{customerNo}'";
    if (openOnly)
        filter += " and open eq true";
    
    var response = await _httpClient.GetAsync($"{_baseUrl}/custEntries?$filter={filter}");
    response.EnsureSuccessStatusCode();
    
    var json = await response.Content.ReadAsStringAsync();
    var result = JsonSerializer.Deserialize<ODataResponse<CustLedgerEntry>>(json);
    return result.Value;
}
```

## Business Logic Notes

- **Open Entries**: Entries with `open = true` have outstanding balances
- **Remaining Amounts**: Use `remainingAmtLCY` for accurate local currency balances
- **Document Types**: Different types indicate transaction purposes (Invoice, Payment, Credit Memo, etc.)
- **Positive Flag**: `true` indicates debit (customer owes), `false` indicates credit (customer paid/credit memo)

## Error Handling

This is a read-only API. Common errors:
- **401 Unauthorized**: Invalid or expired access token
- **404 Not Found**: Entry doesn't exist (when using specific SystemId)
- **400 Bad Request**: Invalid filter syntax

## Performance Tips

1. **Always filter by customer**: Reduces data transfer
2. **Use $select**: Only retrieve needed fields
3. **Filter on indexed fields**: `customerNo`, `entryNo`, `documentNo`
4. **Cache reference data**: Customer names don't change frequently
5. **Pagination**: Use `$top` and `$skip` for large datasets

## Related APIs
- **Customer API**: Get customer master data
- **Posted Sales Invoices**: Get invoice details
- **Web Payments**: Record payments

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
