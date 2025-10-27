# Web Orders API - Developer Guide

## Overview
The Web Orders API provides full create, read, and update access to web-originated orders with complete customer and shipping details.

## API Endpoint Details
- **Endpoint**: `/webOrders`
- **Entity Name**: webOder (note: typo in entity name)
- **Entity Set Name**: webOrders
- **Page ID**: 71977
- **Source Table**: TVTWS Web Order
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/webOrders
```

## Field Reference

| Field Name                     | Type         | Description                       |
|--------------------------------|--------------|-----------------------------------|
| systemId                       | Guid         | System field                      |
| orderGroup                     | Code[50]     | Key                               |
| orderId                        | Code[50]     | Key (Unique Web Reference)        |
| orderType                      | Code[10]     | Web Specific                      |
| customerId                     | Code[50]     | Web Specific                      |
| sellToCustomerNo               | Code[20]     | Standard                          |
| customerEmail                  | Text[80]     | Web Specific                      |
| sellToCustomerName             | Text[100]    | Standard                          |
| sellToCustomerName2            | Text[50]     | Standard                          |
| sellToCity                     | Text[30]     | Standard                          |
| sellToCounty                   | Text[30]     | Standard                          |
| sellToCountryRegionCode        | Code[10]     | Standard                          |
| sellToEMail                    | Text[80]     | Standard                          |
| sellToAddress                  | Text[100]    | Standard                          |
| sellToContactNo                | Code[20]     | Standard                          |
| sellToContact                  | Text[100]    | Standard                          |
| sellToAddress2                 | Text[50]     | Standard                          |
| sellToPhoneNo                  | Text[30]     | Standard                          |
| sellToPostCode                 | Code[20]     | Standard                          |
| customerPostingGroup           | Code[20]     | Standard                          |
| customerPriceGroup             | Code[10]     | Standard                          |
| customerDiscGroup              | Code[20]     | Standard                          |
| salespersonCode                | Code[20]     | Standard                          |
| vatBusPostingGroup             | Code[20]     | Standard                          |
| reasonCode                     | Code[10]     | Standard                          |
| genBusPostingGroup             | Code[20]     | Standard                          |
| vatRegistrationNo              | Text[20]     | Standard                          |
| documentDate                   | Date         | Standard                          |
| dueDate                        | Date         | Standard                          |
| orderDate                      | Date         | Standard                          |
| shipmentDate                   | Date         | Standard                          |
| locationCode                   | Code[10]     | Standard                          |
| currencyCode                   | Code[10]     | Standard                          |
| yourReference                  | Text[35]     | Standard                          |
| externalDocumentNo             | Code[35]     | Standard                          |
| deliveryNoteText1              | Text[80]     | Web Specific                      |
| deliveryNoteText2              | Text[80]     | Web Specific                      |
| giftNoteText1                  | Text[80]     | Web Specific                      |
| giftNoteText2                  | Text[80]     | Web Specific                      |
| noteText1                      | Text[80]     | Web Specific                      |
| noteText2                      | Text[80]     | Web Specific                      |
| shipToCode                     | Code[10]     | Standard                          |
| shipToName                     | Text[100]    | Standard                          |
| shipToCity                     | Text[30]     | Standard                          |
| shipToCounty                   | Text[30]     | Standard                          |
| shipToName2                    | Text[50]     | Standard                          |
| shipToAddress                  | Text[100]    | Standard                          |
| shipToContact                  | Text[100]    | Standard                          |
| shipToAddress2                 | Text[50]     | Standard                          |
| shipToPostCode                 | Code[20]     | Standard                          |
| shippingAgentCode              | Code[10]     | Standard                          |
| shipmentMethodCode             | Code[10]     | Standard                          |
| shipToCountryRegionCode        | Code[10]     | Standard                          |
| shippingAgentServiceCode       | Code[10]     | Standard                          |
| promisedDeliveryDate           | Date         | Standard                          |
| requestedDeliveryDate          | Date         | Standard                          |
| paymentId                      | Code[50]     | Web Specific                      |
| paymentMethodCode              | Code[10]     | Standard                          |
| paymentTermsCode               | Code[10]     | Standard                          |
| orderURL                       | Text[150]    | Web Specific                      |
| totalOrderAmount               | Decimal      | Web Specific                      |
| dutyFree                       | Boolean      | Web Specific                      |
| dispatched                     | Boolean      | Web Specific                      |
| pricesIncludingVAT             | Boolean      | Standard                          |
| shortcutDimension1Code         | Code[20]     | Standard                          |
| shortcutDimension2Code         | Code[20]     | Standard                          |
| decimal01                      | Decimal      | Web Specific                      |
| integer01                      | Integer      | Web Specific                      |
| date01                         | Date         | Web Specific                      |
| code01                         | Code[20]     | Web Specific                      |
| time01                         | Time         | Web Specific                      |
| dateTime01                     | DateTime     | Web Specific                      |
| text01                         | Text[100]    | Web Specific                      |
| boolean01                      | Boolean      | Web Specific                      |
| decimal02                      | Decimal      | Web Specific                      |
| integer02                      | Integer      | Web Specific                      |
| date02                         | Date         | Web Specific                      |
| code02                         | Code[20]     | Web Specific                      |
| time02                         | Time         | Web Specific                      |
| dateTime02                     | DateTime     | Web Specific                      |
| text02                         | Text[100]    | Web Specific                      |
| boolean02                      | Boolean      | Web Specific                      |
| systemModifiedBy               | Guid         | System field                      |
| systemCreatedAt                | DateTime     | System field                      |
| systemCreatedBy                | Guid         | System field                      |
| systemModifiedAt               | DateTime     | System field                      |


### Order Identification
- `systemId` - System identifier (OData key)
- `orderGroup` - Order group
- `orderId` - Order ID (web reference)
- `orderType` - Order type code

### Customer Information
- `sellToCustomerNo` - Customer number
- `sellToCustomerName`, `sellToCustomerName2` - Customer names
- `sellToAddress`, `sellToAddress2` - Customer address
- `sellToCity`, `sellToCounty`, `sellToPostCode` - Customer location
- `sellToCountryRegionCode` - Customer country
- `sellToContact`, `sellToPhoneNo`, `sellToEMail` - Contact info
- `customerEmail` - Additional email field

### Ship-To Address
- `shipToCode` - Ship-to address code
- `shipToName`, `shipToName2` - Shipping name
- `shipToAddress`, `shipToAddress2` - Shipping address
- `shipToCity`, `shipToCounty`, `shipToPostCode` - Shipping location
- `shipToCountryRegionCode` - Shipping country
- `shipToContact` - Shipping contact

### Order Details
- `orderDate` - Order date
- `shipmentDate` - Shipment date
- `locationCode` - Warehouse location
- `currencyCode` - Currency
- `yourReference`, `externalDocumentNo` - References
- `orderURL` - Web order URL

### Shipping
- `shipmentMethodCode` - Shipment method
- `shippingAgentCode` - Shipping agent
- `shippingAgentServiceCode` - Shipping service

### Payment
- `paymentId` - Payment ID
- `paymentMethodCode` - Payment method
- `paymentTermsCode` - Payment terms

### Amounts & Flags
- `totalOrderAmount` - Total order amount
- `paid` - Payment status flag
- `dutyFree` - Duty-free flag
- `dispatched` - Dispatch status
- `pendingCart` - Pending cart flag
- `pricesIncludingVAT` - Price includes VAT

### Notes
- `deliveryNoteText1`, `deliveryNoteText2` - Delivery notes
- `giftNoteText1`, `giftNoteText2` - Gift messages
- `noteText1`, `noteText2` - General notes

### Dimensions
- `shortcutDimension1Code`, `shortcutDimension2Code` - Dimensions

### System Fields
- `systemCreatedAt`, `systemCreatedBy`
- `systemModifiedAt`, `systemModifiedBy`

## Nested Data

### Web Order Lines (Subpage)
Access via `$expand=weborderLines`

## Common Operations

### Create New Web Order
```http
POST /webOrders
Content-Type: application/json

{
  "orderGroup": "WEB",
  "orderId": "WEB-2025-12345",
  "orderType": "STANDARD",
  "sellToCustomerNo": "CUST001",
  "sellToCustomerName": "John Smith",
  "sellToAddress": "123 Main Street",
  "sellToCity": "London",
  "sellToPostCode": "SW1A 1AA",
  "sellToCountryRegionCode": "GB",
  "sellToEMail": "john@example.com",
  "sellToPhoneNo": "+44 20 1234 5678",
  "shipToCode": "HOME",
  "orderDate": "2025-10-14",
  "shipmentDate": "2025-10-20",
  "locationCode": "MAIN",
  "currencyCode": "GBP",
  "paymentMethodCode": "CARD",
  "totalOrderAmount": 1500.00,
  "paid": false,
  "dutyFree": false,
  "pricesIncludingVAT": true
}
```

### Update Order Status
```http
PATCH /webOrders({systemId})
Content-Type: application/json
If-Match: *

{
  "paid": true,
  "paymentId": "PAY-123456"
}
```

### Get Order with Lines
```http
GET /webOrders?$filter=orderId eq 'WEB-2025-12345'&$expand=weborderLines
```

## Code Examples

### JavaScript
```javascript
class WebOrderAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async createOrder(orderData) {
    const response = await fetch(`${this.baseUrl}/webOrders`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify(orderData)
    });
    
    if (!response.ok) {
      throw new Error(`Failed to create order: ${await response.text()}`);
    }
    
    return await response.json();
  }

  async getOrder(orderId, includeLines = true) {
    const expand = includeLines ? '&$expand=weborderLines' : '';
    const response = await fetch(
      `${this.baseUrl}/webOrders?$filter=orderId eq '${orderId}'${expand}`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value[0];
  }

  async updateOrderPayment(systemId, paymentId) {
    const response = await fetch(`${this.baseUrl}/webOrders(${systemId})`, {
      method: 'PATCH',
      headers: {
        ...this.headers,
        'If-Match': '*'
      },
      body: JSON.stringify({
        paid: true,
        paymentId: paymentId
      })
    });
    
    return await response.json();
  }

  async getCustomerOrders(customerNo) {
    const response = await fetch(
      `${this.baseUrl}/webOrders?$filter=sellToCustomerNo eq '${customerNo}'&$orderby=orderDate desc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }
}

// Usage
const api = new WebOrderAPI(baseUrl, accessToken);

// Create order
const order = await api.createOrder({
  orderGroup: 'WEB',
  orderId: 'WEB-2025-12345',
  sellToCustomerNo: 'CUST001',
  sellToCustomerName: 'John Smith',
  sellToAddress: '123 Main St',
  sellToCity: 'London',
  sellToPostCode: 'SW1A 1AA',
  sellToCountryRegionCode: 'GB',
  orderDate: '2025-10-14',
  totalOrderAmount: 1500.00
});

console.log(`Order created: ${order.systemId}`);
```

### Python
```python
class WebOrderAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def create_order(self, order_data: dict) -> dict:
        response = requests.post(
            f'{self.base_url}/webOrders',
            headers=self.headers,
            json=order_data
        )
        response.raise_for_status()
        return response.json()
    
    def get_order(self, order_id: str, include_lines: bool = True) -> dict:
        params = {'$filter': f"orderId eq '{order_id}'"}
        if include_lines:
            params['$expand'] = 'weborderLines'
        
        response = requests.get(
            f'{self.base_url}/webOrders',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None
    
    def mark_as_paid(self, system_id: str, payment_id: str) -> dict:
        headers = self.headers.copy()
        headers['If-Match'] = '*'
        
        response = requests.patch(
            f'{self.base_url}/webOrders({system_id})',
            headers=headers,
            json={'paid': True, 'paymentId': payment_id}
        )
        response.raise_for_status()
        return response.json()
    
    def get_unpaid_orders(self) -> list:
        response = requests.get(
            f'{self.base_url}/webOrders',
            headers=self.headers,
            params={'$filter': 'paid eq false', '$orderby': 'orderDate desc'}
        )
        response.raise_for_status()
        return response.json()['value']

# Usage
api = WebOrderAPI(base_url, access_token)

# Create order
order = api.create_order({
    'orderGroup': 'WEB',
    'orderId': 'WEB-2025-12345',
    'sellToCustomerNo': 'CUST001',
    'orderDate': '2025-10-14',
    'totalOrderAmount': 1500.00
})

# Get order with lines
full_order = api.get_order('WEB-2025-12345', include_lines=True)
print(f"Order {full_order['orderId']} has {len(full_order.get('weborderLines', []))} lines")
```

### C#
```csharp
public class WebOrderApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public WebOrderApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<WebOrder> CreateOrderAsync(WebOrder order)
    {
        var json = JsonSerializer.Serialize(order);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/webOrders", content);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<WebOrder>(responseJson);
    }
    
    public async Task<WebOrder> GetOrderAsync(string orderId, bool includeLines = true)
    {
        var filter = $"orderId eq '{orderId}'";
        var expand = includeLines ? "&$expand=weborderLines" : "";
        
        var response = await _httpClient.GetAsync($"{_baseUrl}/webOrders?$filter={filter}{expand}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebOrder>>(json);
        return result.Value.FirstOrDefault();
    }
}
```

## Business Logic Notes

- **Order ID Uniqueness**: `orderId` should be unique within `orderGroup`
- **Delayed Insert**: Enabled - allows setting all fields before insert
- **Status Flags**: Use `paid`, `dispatched`, `pendingCart` for workflow
- **Nested Lines**: Order lines managed via webOrderLines subpage
- **Price Calculation**: `totalOrderAmount` should match sum of lines
- **Duty Handling**: `dutyFree` flag affects pricing and tax calculations

## Validation Rules

- `orderGroup` and `orderId` required
- `sellToCustomerNo` must exist
- `orderDate` required
- `totalOrderAmount` must be >= 0

## Related APIs
- **Web Order Lines**: Line items for orders
- **Web Order Status**: Processing status tracking
- **Web Payments**: Payment recording
- **Customers**: Customer master data

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
