# Manifest Lines API - Developer Guide

## Overview
The Manifest Lines API provides access to individual line items within shipping manifests.

## API Endpoint Details
- **Endpoint**: `/manifestLines`
- **Entity Name**: manifestLine
- **Entity Set Name**: manifestLines
- **Page ID**: 71984
- **Source Table**: TVT Manifest Line V2
- **API Group**: webbevica
- **Publisher**: tvisiontech
- **Version**: v2.0

## Permissions
- **Insert**: Allowed
- **Modify**: Allowed
- **Delete**: Allowed
- **Read**: Allowed

## Base URL
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/manifestLines
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `manifestNo` | String | Manifest header number |
| `lineNo` | Integer | Line number |
| `itemNo` | String | Item number |
| `description` | String | Item description |
| `quantity` | Decimal | Quantity |
| `unitOfMeasureCode` | String | Unit of measure |
| `locationCode` | String | Location code |
| `sourceType` | Enum | Source document type |
| `sourceNo` | String | Source document number |

## Common Operations

### Add Line to Manifest
```http
POST /manifestLines
Content-Type: application/json

{
  "manifestNo": "MAN-001",
  "lineNo": 10000,
  "itemNo": "WINE001",
  "quantity": 12,
  "unitOfMeasureCode": "CASE",
  "locationCode": "MAIN"
}
```

### Get Manifest Lines
```http
GET /manifestLines?$filter=manifestNo eq 'MAN-001'&$orderby=lineNo asc
```

## Code Examples

### JavaScript
```javascript
async function addManifestLine(lineData) {
  const response = await fetch(`${baseUrl}/manifestLines`, {
    method: 'POST',
    headers,
    body: JSON.stringify(lineData)
  });
  return await response.json();
}

async function getManifestLines(manifestNo) {
  const response = await fetch(
    `${baseUrl}/manifestLines?$filter=manifestNo eq '${manifestNo}'&$orderby=lineNo asc`,
    { headers }
  );
  return (await response.json()).value;
}
```

### Python
```python
def add_manifest_line(line_data: dict) -> dict:
    response = requests.post(
        f'{base_url}/manifestLines',
        headers=headers,
        json=line_data
    )
    return response.json()

def get_manifest_lines(manifest_no: str) -> list:
    response = requests.get(
        f'{base_url}/manifestLines',
        headers=headers,
        params={
            '$filter': f"manifestNo eq '{manifest_no}'",
            '$orderby': 'lineNo asc'
        }
    )
    return response.json()['value']
```

## Related APIs
- **Manifests**: Manifest headers
- **Items**: Item information

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
