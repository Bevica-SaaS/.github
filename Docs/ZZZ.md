# Bevica Web Integration API Documentation

## Documentation Overview

This folder contains comprehensive API documentation for the Bevica Web Integration v2.0 platform.

## Quick Start

**New to the API?** Start here:
1. Check **API_Documentation_Status.md** - Documentation coverage status
2. Browse individual API guides for detailed deep-dives

## Authentication

All APIs require OAuth 2.0 authentication:

```http
Authorization: Bearer {your_access_token}
Content-Type: application/json
```

**Base URL:**
```
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/
```

## Common Patterns

### Filtering
```http
GET /customers?$filter=balance gt 0
GET /items?$filter=published eq true and deleted eq false
```

### Selecting Fields
```http
GET /customers?$select=no,name,balance,eMail
```

### Sorting
```http
GET /items?$orderby=description asc
```

### Pagination
```http
GET /customers?$top=50&$skip=0
```

### Expanding Related Data
```http
GET /webOrders?$expand=weborderLines
GET /items?$expand=marketingContents
```

## Code Examples

Each individual guide includes production-ready code examples in:
- **JavaScript/TypeScript** (Fetch API)
- **Python** (requests library)
- **C# .NET** (HttpClient)

## Important Notes

- **Read vs Write**: Some APIs are read-only (Items, Products, Regions)
- **Delayed Insert**: Many APIs support delayed insert for better data integrity
- **OData Keys**: Most APIs use `systemId` as the OData key
- **If-Match Header**: Required for PATCH and DELETE operations
- **Rate Limiting**: Implement retry logic with exponential backoff

## Related Resources

- **OData v4 Specification**: [odata.org](https://www.odata.org/)
- **Business Central API**: [Microsoft Docs](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/api-reference/v2.0/)

## Support

For API support or questions:
- Check the status document for coverage details
- Contact tvisiontech support team

## Version Information

- **API Version**: v2.0
- **API Group**: webbevica
- **Publisher**: tvisiontech
- **Protocol**: OData v4.0
- **Documentation Last Updated**: October 14, 2025

---

## Document Structure

Each individual API guide follows this format:
1. **Overview** - API purpose and capabilities
2. **Endpoint Details** - Technical specifications
3. **Permissions** - Available operations
4. **Field Reference** - Complete field documentation
5. **Common Use Cases** - Practical examples
6. **Code Examples** - JavaScript, Python, C#
7. **Business Logic** - Important behavior notes
8. **Performance Tips** - Optimization guidance
9. **Related APIs** - Connected endpoints

---

**Status**: Core documentation complete  
**Coverage**: All APIs documented in master guide  
**Individual Guides**: 6 of 29 deep-dive guides available
