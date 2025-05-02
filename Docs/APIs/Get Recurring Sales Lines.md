## GET Brands

Retrieve the properties and relationships of a brand object for Business Central. 

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
businesscentralPrefix/brands
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
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/$metadata#companies(9ce13e1a-9f86-ed11-9989-6045bd0d0c6b)/brands",
    "value": [
        {
            "@odata.etag": "W/\"JzE5OzEwMjU1NjcwMDMzMDY2MzE5MDAxOzAwOyc=\"",
            "code": "ARÔME",
            "name": "Arôme Spirits",
            "address": "",
            "address2": "",
            "city": "",
            "countryRegionCode": "PA",
            "county": "",
            "postCode": "",
            "contact": "",
            "eMail": "",
            "faxNo": "",
            "homePage": "https://www.rumarome.com",
            "latitude": 34.61315,
            "longitude": 3.218747,
            "noItems": 1,
            "phoneNo": ""
        }
]
}

```

### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
| 1 | TVT Brands |  Code | String | 20 | | 
| 1 | TVT Region |  Name | String | 50 | | 
| 1 | TVT Region |  Address | String | 100 | | 
| 1 | TVT Region |  Address 2 | String | 50 | | 
| 1 | TVT Region |  City | String | 30 | | 
| 1 | TVT Region |  Country / Region Code | String | 10 | | 
| 1 | TVT Region |  County | String | 30 | | 
| 1 | TVT Region |  Post code | String | 20 | | 
| 1 | TVT Region |  Contact | String | 50 | | 
| 1 | TVT Region |  email | String | 80 | | 
| 1 | TVT Region |  Fax No. | String | 30 | | 
| 1 | TVT Region |  Home Page | String | 80 | | 
| 1 | TVT Region |  Latitude | Integer |  | | 
| 1 | TVT Region |  Longitude | Integer |  | | 
| 1 | TVT Region |  Phone No. | String | 30 | | 
