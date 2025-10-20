# Posted Sales Credit Memo Lines API - Developer Guide

## Overview
The Posted Sales Credit Memo Lines API provides read-only access to line items within posted credit memos.

## API Endpoint Details
- **Endpoint**: `/PostedSalesCrMemoLines`
- **Entity Name**: PostedSalesCrMemoLine
- **Entity Set Name**: PostedSalesCrMemoLines
- **Page ID**: 71995
- **Source Table**: Sales Cr.Memo Line
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/PostedSalesCrMemoLines
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `sellToCustomerNo` | String | Sell-to customer number |
| `documentNo` | String | Credit memo number |
| `lineNo` | Integer | Line number |
| `type` | Enum | Item, Resource, G/L Account, etc. |
| `no` | String | Item/resource number |
| `locationCode` | String | Location code |
| `shipmentDate` | Date | Shipment date |
| `description` | String | Line description |
| `unitOfMeasure` | String | Unit of measure |
| `quantity` | Decimal | Quantity |
| `unitPrice` | Decimal | Unit price |
| `lineDiscount` | Decimal | Line discount percentage |
| `lineDiscountAmount` | Decimal | Line discount amount |
| `amount` | Decimal | Line amount excl. VAT |
| `amountIncludingVAT` | Decimal | Amount incl. VAT |
| `variantCode` | String | Variant code |
| `unitOfMeasureCode` | String | Unit of measure code |
| `quantityBase` | Decimal | Quantity (Base) |

## Common Use Cases

### Get Credit Memo Lines
```http
GET /PostedSalesCrMemoLines?$filter=documentNo eq 'CM-12345'&$orderby=lineNo asc
```

## Code Examples

### JavaScript
```javascript
async function getCreditMemoLines(memoNo) {
  const response = await fetch(
    `${baseUrl}/PostedSalesCrMemoLines?$filter=documentNo eq '${memoNo}'&$orderby=lineNo asc`,
    { headers }
  );
  return (await response.json()).value;
}
```

### Python
```python
def get_credit_memo_lines(memo_no: str) -> list:
    response = requests.get(
        f'{base_url}/PostedSalesCrMemoLines',
        headers=headers,
        params={
            '$filter': f"documentNo eq '{memo_no}'",
            '$orderby': 'lineNo asc'
        }
    )
    return response.json()['value']
```

## Related APIs
- **Posted Credit Memos**: Credit memo headers
- **Items**: Product information

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
