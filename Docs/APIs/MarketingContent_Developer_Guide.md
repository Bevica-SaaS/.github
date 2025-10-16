# Marketing Content API - Developer Guide

## Overview
The Marketing Content API provides access to marketing content and descriptions for items, supporting rich text content for web display.

## API Endpoint Details
- **Endpoint**: `/marketingContents`
- **Entity Name**: marketingContent
- **Entity Set Name**: marketingContents
- **Page ID**: 71991
- **Source Table**: TVT Marketing Content
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
https://api.businesscentral.dynamics.com/v2.0/{environment}/api/tvisiontech/webbevica/v2.0/marketingContents
```

## Field Reference

| Field Name | Type | Description |
|------------|------|-------------|
| `systemId` | GUID | System identifier (OData key) |
| `marketingGroupCode` | String | Marketing group code (typically item number) |
| `date` | Date | Content effective date |
| `description` | String | Content description |
| `contentExist` | Boolean | Content exists flag |
| `contentdata` | Text | Marketing content (HTML/text) |

## Common Use Cases

### Get Item Marketing Content
```http
GET /marketingContents?$filter=marketingGroupCode eq 'WINE001'
```

### Get Latest Content for Item
```http
GET /marketingContents?$filter=marketingGroupCode eq 'WINE001'&$orderby=date desc&$top=1
```

### Create Marketing Content
```http
POST /marketingContents
Content-Type: application/json

{
  "marketingGroupCode": "WINE001",
  "date": "2025-10-14",
  "description": "Product Description",
  "contentdata": "<h2>Premium Red Wine</h2><p>A rich, full-bodied wine with notes of cherry and oak...</p>"
}
```

### Update Content
```http
PATCH /marketingContents({systemId})
Content-Type: application/json
If-Match: *

{
  "contentdata": "<h2>Updated Description</h2><p>New marketing text...</p>"
}
```

## Code Examples

### JavaScript
```javascript
class MarketingContentAPI {
  constructor(baseUrl, accessToken) {
    this.baseUrl = baseUrl;
    this.headers = {
      'Authorization': `Bearer ${accessToken}`,
      'Content-Type': 'application/json'
    };
  }

  async getItemContent(itemNo) {
    const response = await fetch(
      `${this.baseUrl}/marketingContents?$filter=marketingGroupCode eq '${itemNo}'&$orderby=date desc`,
      { headers: this.headers }
    );
    const data = await response.json();
    return data.value;
  }

  async getLatestContent(itemNo) {
    const contents = await this.getItemContent(itemNo);
    return contents[0];
  }

  async createContent(contentData) {
    const response = await fetch(`${this.baseUrl}/marketingContents`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify(contentData)
    });
    
    if (!response.ok) throw new Error(await response.text());
    return await response.json();
  }

  async updateContent(systemId, newContent) {
    const response = await fetch(`${this.baseUrl}/marketingContents(${systemId})`, {
      method: 'PATCH',
      headers: { ...this.headers, 'If-Match': '*' },
      body: JSON.stringify({ contentdata: newContent })
    });
    return await response.json();
  }

  renderContent(content) {
    // Safely render HTML content
    const container = document.createElement('div');
    container.className = 'marketing-content';
    container.innerHTML = content.contentdata || '';
    return container;
  }
}

// Usage
const api = new MarketingContentAPI(baseUrl, accessToken);

// Get latest marketing content for product page
const content = await api.getLatestContent('WINE001');
if (content && content.contentExist) {
  const contentDiv = api.renderContent(content);
  document.getElementById('product-description').appendChild(contentDiv);
}

// Create new marketing content
await api.createContent({
  marketingGroupCode: 'WINE001',
  date: '2025-10-14',
  description: 'Product Marketing',
  contentdata: '<h2>Premium Selection</h2><p>Exceptional quality...</p>'
});
```

### Python
```python
from datetime import date

class MarketingContentAPI:
    def __init__(self, base_url: str, access_token: str):
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {access_token}',
            'Content-Type': 'application/json'
        }
    
    def get_item_content(self, item_no: str) -> list:
        response = requests.get(
            f'{self.base_url}/marketingContents',
            headers=self.headers,
            params={
                '$filter': f"marketingGroupCode eq '{item_no}'",
                '$orderby': 'date desc'
            }
        )
        response.raise_for_status()
        return response.json()['value']
    
    def get_latest_content(self, item_no: str) -> dict:
        contents = self.get_item_content(item_no)
        return contents[0] if contents else None
    
    def create_content(self, content_data: dict) -> dict:
        response = requests.post(
            f'{self.base_url}/marketingContents',
            headers=self.headers,
            json=content_data
        )
        response.raise_for_status()
        return response.json()
    
    def update_content(self, system_id: str, new_content: str) -> dict:
        headers = self.headers.copy()
        headers['If-Match'] = '*'
        
        response = requests.patch(
            f'{self.base_url}/marketingContents({system_id})',
            headers=headers,
            json={'contentdata': new_content}
        )
        response.raise_for_status()
        return response.json()

# Usage
api = MarketingContentAPI(base_url, access_token)

# Get content for product page
content = api.get_latest_content('WINE001')
if content and content['contentExist']:
    print(f"Marketing content: {content['contentdata']}")

# Create new content
api.create_content({
    'marketingGroupCode': 'WINE001',
    'date': date.today().isoformat(),
    'description': 'Product Marketing',
    'contentdata': '<h2>Premium Wine</h2><p>Rich and complex...</p>'
})
```

### C#
```csharp
public class MarketingContentApiClient
{
    private readonly HttpClient _httpClient;
    private readonly string _baseUrl;
    
    public async Task<List<MarketingContent>> GetItemContentAsync(string itemNo)
    {
        var filter = $"marketingGroupCode eq '{itemNo}'";
        var response = await _httpClient.GetAsync(
            $"{_baseUrl}/marketingContents?$filter={filter}&$orderby=date desc"
        );
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        var result = JsonSerializer.Deserialize<ODataResponse<MarketingContent>>(json);
        return result.Value;
    }
    
    public async Task<MarketingContent> GetLatestContentAsync(string itemNo)
    {
        var contents = await GetItemContentAsync(itemNo);
        return contents.FirstOrDefault();
    }
    
    public async Task<MarketingContent> CreateContentAsync(MarketingContent content)
    {
        var json = JsonSerializer.Serialize(content);
        var httpContent = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await _httpClient.PostAsync($"{_baseUrl}/marketingContents", httpContent);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonSerializer.Deserialize<MarketingContent>(responseJson);
    }
}

public class MarketingContent
{
    public Guid SystemId { get; set; }
    public string MarketingGroupCode { get; set; }
    public DateTime Date { get; set; }
    public string Description { get; set; }
    public bool ContentExist { get; set; }
    public string Contentdata { get; set; }
}
```

## Business Logic Notes

- **Item-Specific**: Linked via `marketingGroupCode` (item number)
- **Date-Based**: Multiple versions with different dates
- **Rich Content**: Supports HTML for web display
- **Latest Content**: Use most recent date for current marketing
- **Content Storage**: Text stored in `contentdata` field

## Content Guidelines

1. **HTML Support**: Use HTML for formatting
2. **Sanitization**: Sanitize HTML before rendering
3. **Version Control**: Use date field for versions
4. **SEO Optimization**: Include relevant keywords
5. **Mobile-Friendly**: Keep content responsive

## Use Cases

- **Product Descriptions**: Rich product details for web
- **Marketing Copy**: Promotional content
- **Vintage Notes**: Wine tasting notes
- **Origin Stories**: Producer and vineyard information
- **Food Pairing**: Serving suggestions

## Performance Tips

1. **Cache Content**: Cache for product page loads
2. **Latest Only**: Query for most recent date
3. **Lazy Load**: Load content after initial page render
4. **CDN Delivery**: Consider CDN for static content

## Related APIs
- **Items**: Item information
- **Web Products**: Product catalog

---

**Last Updated**: October 14, 2025  
**API Version**: 2.0
