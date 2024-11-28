## GET Regions

Retrieve the properties and relationships of a region object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/regionCodes
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/regionCodes",
    "value": [
        {
            "@odata.etag": "W/\"JzIwOzExMjQwMTM0MDY5NDk5NzQ2OTkwMTswMDsn\"",
            "code": "ABRUZZO",
            "countryRegionCode": "IT",
            "name": "Abruzzo",
            "noSubregions": 0,
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
| 1 | Region |  Code | String | 20 | | 
| 1 | Region |  CountryRegionCode | xx |  | | 
| 1 | Region |  Name | xx |  | | 
| 1 | Region |  NoSubregions | xx |  | | 
| 1 | Region |  NoItem | xx |  | | 

