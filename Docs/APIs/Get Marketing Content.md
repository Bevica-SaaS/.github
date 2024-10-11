## GET Marketing Data

Retrieve the properties and relationships of a Stock object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/marketingContents
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Do not supply a request body for this method.

### Response

Here is an example of the response

```json

Coming soon

```

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
|  1  | Marketing Content | Marketing Group Code | String |  |  |
|  1  | Marketing Content | Date | Date |  |  |
|  1  | Marketing Content | Description | String | 50 |  |
|  1  | Marketing Content | Content Exist | Boolean |  |  |
|  1  | Marketing Content | contentdata | Blob |  |  |
