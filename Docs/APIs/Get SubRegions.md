## GET Regions

Retrieve the properties and relationships of a region object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/SubRegions
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
{
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/subRegions",
    "value": [
        {
            "@odata.etag": "W/\"JzE5OzM1ODgyNTk4MzM4MzI4ODk3NDcxOzAwOyc=\"",
            "regionCode": "BEAUJOLAIS",
            "code": "BEAUJOLAIS CRUS",
            "countryRegionCode": "FR",
            "name": "Beaujolais Crus",
            "noItems": 0
        }
]
}


```

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
| 1 | Region |  Region Code | String | 20 | | 
| 1 | Region |  Code | String | 20 | | 
| 1 | Region |  Country / Region Code | String | 20 | | 
| 1 | Region |  Name | String | 50 | | 
| 1 | Region |  No. Item | Integer |  | | 

