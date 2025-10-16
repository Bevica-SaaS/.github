# Posted Sales Invoice Lines API - Developer Guide

## Overview
The Posted Sales Invoice Lines API provides read-only access to line items within posted sales invoices.

## API Endpoint Details
- **Endpoint**: `/PostedSalesInvoiceLines`
- **Entity Name**: postedSalesInvoiceLine
- **Entity Set Name**: PostedSalesInvoiceLines
- **Page ID**: 72207
- **Source Table**: Sales Invoice Line
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/PostedSalesInvoiceLines
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `documentNo` | String | Invoice number |
| `lineNo` | Integer | Line number |
| `type` | Enum | Item, Resource, G/L Account, etc. |
| `no` | String | Item/resource number |
| `description` | String | Line description |
| `quantity` | Decimal | Quantity |
| `unitOfMeasureCode` | String | Unit of measure |
| `unitPrice` | Decimal | Unit price |
| `lineAmount` | Decimal | Line amount excl. VAT |
| `amountIncludingVAT` | Decimal | Amount incl. VAT |
| `lineDiscountPercent` | Decimal | Discount percentage |
| `lineDiscountAmount` | Decimal | Discount amount |

## Common Use Cases

### Get Invoice Lines
```http
GET /PostedSalesInvoiceLines?$filter=documentNo eq 'INV-12345'&$orderby=lineNo asc
```

### Get Lines for Item
```http
GET /PostedSalesInvoiceLines?$filter=no eq 'WINE001' and type eq 'Item'
```

## Code Examples

### JavaScript
```javascript
async function getInvoiceLines(invoiceNo) {
  const response = await fetch(
    `${baseUrl}/PostedSalesInvoiceLines?$filter=documentNo eq '${invoiceNo}'&$orderby=lineNo asc`,
    { headers }
  );
  return (await response.json()).value;
}
```

### Python
```python
def get_invoice_lines(invoice_no: str) -> list:
    response = requests.get(
        f'{base_url}/PostedSalesInvoiceLines',
        headers=headers,
        params={
            '$filter': f"documentNo eq '{invoice_no}'",
            '$orderby': 'lineNo asc'
        }
    )
    return response.json()['value']
```

## Related APIs
- **Posted Sales Invoices**: Invoice headers
- **Items**: Product information

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
