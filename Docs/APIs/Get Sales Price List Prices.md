## GET Sales Price List Prices

Retrieve the properties and relationships of a (Sales) Price List Line object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralPrefix-structure).

~~~ api
GET 

businesscentralPrefix/SalesListPrices
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
    "value": [
   
    ]
}
```
### Field information
<details>
  <summary>Show</summary>

| Relation | Source Table | Field Caption | Field Type | Field Length | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|	1	|	Price List Line	|	Item No	|	string	|	20	|
|	1	|	Price List Line	|	Variant Code	|	string	|	10	|
|	1	|	Price List Line	|	Sales Type	|	Type	|		|
|	1	|	Price List Line	|	Sales Code	|	string	|	10	|
|	1	|	Price List Line	|	Unit of Measure Code	|	string	|	10	|
|	1	|	Price List Line	|	Starting Date	|	date	|		|
|	1	|	Price List Line	|	Ending Date	|	date	|		|
|	1	|	Price List Line	|	Unit Price	|	decimal	|		|
|	1	|	Price List Line	|	Price Includes VAT	|	boolean	|		|
|	1	|	Price List Line	|	Minimum Quantity	|	decimal	|		|
