# Bevica 2.0 API Documentation Status

## Introduction 

The Bevica APIs documented below outline the interactions available to a third party to integrate a Bevica into their platform.
 The  request can be used independently of one another or together to create a complete workflow.

All of our endpoints are secured so before you can begin to make calls to the API you will first need to obtain an access token.

For more information on the business workflows that the APIs support, head to the [Guides](https://tvisiontech.freshdesk.com/) section.

If you have any questions or feedback on the API reference, please reach out to our support.

## APIs

RESTful web services are typically created to interchange data between Business Central and external systems. The acronym REST stands for REpresentational State Transfer. Any coding language capable of calling REST APIs can be used to use this feature. The Business Central API stack have been optimized for performance and is the preferred way to integrate with Business Central.

Business Central comes with an extensive list of built-in APIs that requires no code and minimal setup to use. When using the built-in APIs, please choose the highest API version available. You can also develop your own custom APIs using the AL object types API pages and API queries.

The articles in this section describe the key concepts and techniques for using APIs with Business Central.

[API(v2.0) MS Docs](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/api-reference/v2.0/)

## Master Documentation

### Customer (5)
- Customer_Developer_Guide.md - Customer API (Read-Only)
- CustomerEdit_Developer_Guide.md - Customer Edit API
- CustEntries_Developer_Guide.md - Customer Entries API
- ShipToAddr_Developer_Guide.md - Ship-To Addresses API
- ShipToAddressEdit_Developer_Guide.md - Ship-To Address Edit API

### Product & Inventory (7)
- Item_Developer_Guide.md - Items API
- Product_Developer_Guide.md - Web Products API
- Brand_Developer_Guide.md - Brand API (existing)
- Regions_Developer_Guide.md - Region Codes API
- SubRegionCodes_Developer_Guide.md - SubRegion Codes API
- WebStock_Developer_Guide.md - Web Stock API
- MarketingContent_Developer_Guide.md - Marketing Content API

### Orders & Shipping (6)
- WebOrder_Developer_Guide.md - Web Orders API
- WebOrderLines_Developer_Guide.md - Web Order Lines API
- WebOrderStatus_Developer_Guide.md - Web Order Status API
- WebPayment_Developer_Guide.md - Web Payments API
- Manifest_Developer_Guide.md - Manifest Headers API
- ManifestLine_Developer_Guide.md - Manifest Lines API
- RecurringSalesLines_Developer_Guide.md - Recurring Sales Lines API

### Sales Documents (6)
- SalesDocument_Developer_Guide.md - Sales Documents API
- SalesLine_Developer_Guide.md - Sales Lines API
- SalesInvHeader_Developer_Guide.md - Posted Sales Invoices API
- SalesInvLine_Developer_Guide.md - Posted Sales Invoice Lines API
- SalesCrMemoHeader_Developer_Guide.md - Posted Credit Memos API
- SalesCrMemoLine_Developer_Guide.md - Posted Credit Memo Lines API

### Pricing (2)
- SalesPrices_Developer_Guide.md - Sales Prices API (Legacy)
- SalesListPrices_Developer_Guide.md - Sales List Prices API (Modern)

### Paid Reserve (2)
- PaidReserve_Developer_Guide.md - Paid Reserves API
- PaidReserveEntries_Developer_Guide.md - Paid Reserve Entries API

## Documentation Standards

Each individual guide may include these sections:
- **Overview** - Purpose and description
- **API Endpoint Details** - Technical specifications
- **Permissions** - CRUD operations allowed
- **Base URL** - Complete endpoint URL
- **Field Reference** - Comprehensive field list with descriptions
- **Common Use Cases** - Practical examples with HTTP requests
- **Code Examples** - JavaScript, Python, and C# implementations
- **Business Logic Notes** - Important behavioral notes
- **Validation Rules** - Field requirements and constraints
- **Error Handling** - Common errors and solutions
- **Performance Tips** - Optimization recommendations
- **Related APIs** - Connected endpoints

## Quick Reference Matrix

| API Name | Endpoint | Operations | Key Use Case |
|----------|----------|------------|--------------|
| Brand | /brands | GET, POST, PATCH | Brand management |
| Customer | /customers | GET | Customer lookup (read-only) |
| CustomerEdit | /customersEdit | GET, POST, PATCH | Customer maintenance |
| CustEntries | /custEntries | GET | AR tracking |
| Item | /items | GET | Product catalog |
| WebOrder | /webOrders | GET, POST, PATCH | Order management |
| WebOrderLines | /webOrderLines | GET, POST, PATCH | Order line items |
| WebOrderStatus | /webOrderStatuses | GET | Order processing status |
| WebPayment | /paymentEntries | GET, POST, PATCH | Payment tracking |
| WebProduct | /webProducts | GET | Marketing product view |
| WebStock | /webStocks | GET, POST, PATCH | Stock availability |
| SalesDocument | /salesDocuments | GET | Sales orders/quotes |
| SalesLine | /salesDocumentLines | GET | Sales document lines |
| PostedSalesInvoice | /PostedSalesInvoices | GET | Historical invoices |
| PostedSalesInvoiceLine | /PostedSalesInvoiceLines | GET | Invoice line details |
| PostedSalesCrMemo | /PostedSalesCrMemoInvoices | GET | Credit memos |
| PostedSalesCrMemoLine | /PostedSalesCrMemoLines | GET | Credit memo lines |
| SalesPrice | /salesPrices | GET | Legacy pricing |
| SalesListPrice | /salesListPrices | GET | Modern pricing |
| ShipToAddr | /shiptoAddresses | GET, POST, PATCH | Delivery addresses |
| ShipToEdit | /shipToAddressesEdit | GET, POST, PATCH | Address maintenance |
| Manifest | /manifests | GET, POST, PATCH | Shipping manifests |
| ManifestLine | /manifestLines | GET, POST, PATCH | Manifest line items |
| PaidReserve | /PaidReserves | GET | Reserve inventory |
| PaidReserveEntry | /PaidReserveEntries | GET | Reserve movements |
| Region | /regionCodes | GET | Geographic regions |
| SubRegion | /subRegions | GET | Geographic subregions |
| MarketingContent | /marketingContents | GET, POST, PATCH | Marketing text/HTML |
| RecurringSalesLines | /customerRecurringSalesLines | GET, PATCH | Customer favorites |

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
