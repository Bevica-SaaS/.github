# Web Order Status API - Developer Guide

## Overview
The Web Order Status API provides read-only access to order processing status and Business Central integration tracking.

## API Endpoint Details
- **Endpoint**: `/webOrderStatuses`
- **Entity Name**: webOrderStatus
- **Entity Set Name**: webOrderStatuses
- **Page ID**: 71978
- **Source Table**: TVTWS Web Order
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/webOrderStatuses
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `orderId` | String | Order ID |
| `orderDate` | Date | Order date |
| `bcStatus` | String | Business Central processing status |
| `bcErrorMessage` | String | Error message if processing failed |
| `bcCreationDateTime` | DateTime | BC record creation timestamp |
| `bcLastModDateTime` | DateTime | Last modification timestamp |
| `bcLastValidateDateTime` | DateTime | Last validation timestamp |
| `bcLastProcessDateTime` | DateTime | Last processing timestamp |
| `bcValidated` | Boolean | Validation completed flag |
| `bcProcessed` | Boolean | Processing completed flag |
| `bcDocumentType` | Enum | Created document type (Order, Invoice, etc.) |
| `bcDocumentNo` | String | Created document number |
| `systemCreatedAt` | DateTime | System creation timestamp |
| `systemCreatedBy` | GUID | Created by user ID |
| `systemModifiedAt` | DateTime | Last system modification |
| `systemModifiedBy` | GUID | Modified by user ID |

## Common Use Cases

### 1. Check Order Processing Status
```http
GET /webOrderStatuses?$filter=orderId eq 'WEB-2025-12345'
```

### 2. Get Failed Orders
```http
GET /webOrderStatuses?$filter=bcStatus eq 'Error'&$orderby=bcLastModDateTime desc
```

### 3. Get Unprocessed Orders
```http
GET /webOrderStatuses?$filter=bcProcessed eq false
```

### 4. Get Recently Processed Orders
```http
GET /webOrderStatuses?$filter=bcProcessed eq true and bcLastProcessDateTime ge 2025-10-14T00:00:00Z
```

### 5. Get Orders by Document Type
```http
GET /webOrderStatuses?$filter=bcDocumentType eq 'Order'
```

## Code Examples

### JavaScript
```javascript
class WebOrderStatusAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getOrderStatus(orderId) {
    const response = await fetch(
      `${this.baseUrl}/webOrderStatuses?$filter=orderId eq '${orderId}'`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value[0];
  }

  async getFailedOrders() {
    const response = await fetch(
      `${this.baseUrl}/webOrderStatuses?$filter=bcStatus eq 'Error'&$orderby=bcLastModDateTime desc`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    return data.value;
  }

  async waitForProcessing(orderId, maxWaitSeconds = 60, pollInterval = 5) {
    const startTime = Date.now();
    
    while ((Date.now() - startTime) / 1000 < maxWaitSeconds) {
      const status = await this.getOrderStatus(orderId);
      
      if (status.bcProcessed) {
        return status;
      }
      
      if (status.bcStatus === 'Error') {
        throw new Error(`Order processing failed: ${status.bcErrorMessage}`);
      }
      
      await new Promise(resolve => setTimeout(resolve, pollInterval * 1000));
    }
    
    throw new Error('Order processing timeout');
  }

  async getProcessingSummary() {
    const response = await fetch(
      `${this.baseUrl}/webOrderStatuses`,
      { headers: this.headers }
    );
    
    const data = await response.json();
    const orders = data.value;
    
    return {
      total: orders.length,
      processed: orders.filter(o => o.bcProcessed).length,
      validated: orders.filter(o => o.bcValidated).length,
      errors: orders.filter(o => o.bcStatus === 'Error').length,
      pending: orders.filter(o => !o.bcProcessed).length
    };
  }
}

// Usage
const api = new WebOrderStatusAPI(baseUrl, accessToken);

// Check order status
const status = await api.getOrderStatus('WEB-2025-12345');
console.log(`Status: ${status.bcStatus}`);
console.log(`Processed: ${status.bcProcessed}`);
console.log(`Document: ${status.bcDocumentType} ${status.bcDocumentNo}`);

// Wait for order to process
try {
  const result = await api.waitForProcessing('WEB-2025-12345', 60, 5);
  console.log(`Order processed successfully: ${result.bcDocumentNo}`);
} catch (error) {
  console.error(`Processing failed: ${error.message}`);
}

// Get failed orders
const failed = await api.getFailedOrders();
failed.forEach(order => {
  console.log(`Order ${order.orderId}: ${order.bcErrorMessage}`);
});
```

### Python
```python
import time
from datetime import datetime, timedelta

class WebOrderStatusAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_order_status(self, order_id: str) -> dict:
        response = requests.get(
            f'{self.base_url}/webOrderStatuses',
            headers=self.headers,
            params={'$filter': f"orderId eq '{order_id}'"}
        )
        response.raise_for_status()
        data = response.json()['value']
        return data[0] if data else None
    
    def get_failed_orders(self) -> list:
        response = requests.get(
            f'{self.base_url}/webOrderStatuses',
            headers=self.headers,
            params={
                '$filter': "bcStatus eq 'Error'",
                '$orderby': 'bcLastModDateTime desc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def wait_for_processing(self, order_id: str, max_wait_seconds: int = 60, 
                           poll_interval: int = 5) -> dict:
        start_time = time.time()
        
        while (time.time() - start_time) < max_wait_seconds:
            status = self.get_order_status(order_id)
            
            if status['bcProcessed']:
                return status
            
            if status['bcStatus'] == 'Error':
                raise Exception(f"Order processing failed: {status['bcErrorMessage']}")
            
            time.sleep(poll_interval)
        
        raise TimeoutError('Order processing timeout')
    
    def get_processing_summary(self) -> dict:
        response = requests.get(
            f'{self.base_url}/webOrderStatuses',
            headers=self.headers
        )
        response.raise_for_status()
        orders = response.json()['value']
        
        return {
            'total': len(orders),
            'processed': sum(1 for o in orders if o['bcProcessed']),
            'validated': sum(1 for o in orders if o['bcValidated']),
            'errors': sum(1 for o in orders if o['bcStatus'] == 'Error'),
            'pending': sum(1 for o in orders if not o['bcProcessed'])
        }

# Usage
api = WebOrderStatusAPI(base_url, access_token)

# Check status
status = api.get_order_status('WEB-2025-12345')
if status:
    print(f"Status: {status['bcStatus']}")
    print(f"Document: {status['bcDocumentType']} {status['bcDocumentNo']}")

# Get summary
summary = api.get_processing_summary()
print(f"Total: {summary['total']}, Processed: {summary['processed']}, Errors: {summary['errors']}")
```

### C#
```csharp
public class WebOrderStatusApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public WebOrderStatusApiClient(string baseUrl, string accessToken)
    {
        _baseUrl = baseUrl;
        _httpClient = new HttpClient();
        _httpClient.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
    }
    
    public async Task<WebOrderStatus> GetOrderStatusAsync(string orderId)
    {
        var filter = $"orderId eq '{orderId}'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/webOrderStatuses?$filter={filter}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebOrderStatus>>(json);
        return result.Value.FirstOrDefault();
    }
    
    public async Task<List<WebOrderStatus>> GetFailedOrdersAsync()
    {
        var filter = "bcStatus eq 'Error'";
        var response = await _httpClient.GetAsync($"{_baseUrl}/webOrderStatuses?$filter={filter}&$orderby=bcLastModDateTime desc");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<WebOrderStatus>>(json);
        return result.Value;
    }
    
    public async Task<WebOrderStatus> WaitForProcessingAsync(string orderId, 
        int maxWaitSeconds = 60, int pollInterval = 5)
    {
        var startTime = DateTime.Now;
        
        while ((DateTime.Now - startTime).TotalSeconds < maxWaitSeconds)
        {
            var status = await GetOrderStatusAsync(orderId);
            
            if (status.BcProcessed)
                return status;
            
            if (status.BcStatus == "Error")
                throw new Exception($"Order processing failed: {status.BcErrorMessage}");
            
            await Task.Delay(pollInterval * 1000);
        }
        
        throw new TimeoutException("Order processing timeout");
    }
}

public class WebOrderStatus
{
    public Guid SystemId { get; set; }
    public string OrderId { get; set; }
    public DateTime OrderDate { get; set; }
    public string BcStatus { get; set; }
    public string BcErrorMessage { get; set; }
    public DateTime? BcCreationDateTime { get; set; }
    public DateTime? BcLastModDateTime { get; set; }
    public DateTime? BcLastValidateDateTime { get; set; }
    public DateTime? BcLastProcessDateTime { get; set; }
    public bool BcValidated { get; set; }
    public bool BcProcessed { get; set; }
    public string BcDocumentType { get; set; }
    public string BcDocumentNo { get; set; }
}
```

## Status Values

### BC Status
- `Pending` - Awaiting processing
- `Validating` - Validation in progress
- `Processing` - Processing in progress
- `Completed` - Successfully processed
- `Error` - Processing failed

## Business Logic Notes

- **Read-Only**: Status is updated by BC processing engine
- **Polling**: Use polling pattern to monitor order processing
- **Error Handling**: Check `bcErrorMessage` for failure details
- **Document Reference**: `bcDocumentNo` links to created BC document
- **Timestamps**: Track processing progress via timestamps

## Performance Tips

1. **Poll Interval**: Use 5-10 second intervals for status checking
2. **Filter by Date**: Limit queries to recent orders
3. **Cache Status**: Cache processed order status to reduce API calls
4. **Batch Monitoring**: Check multiple orders in single filtered query

## Related APIs
- **Web Orders**: Order header data
- **Sales Documents**: Created BC documents

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
