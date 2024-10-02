# Bevica Web Integration

## Main Entities

| Name | Description | Data Flow | Operations | Note|
| ----------- | ----------- | ----------- | -------- | ---------- |
| [Customer](#get-customers) | Customer Info and Ship Addresses | BC -> Web | Read | |
| [Product](#get-products) | Items and Attributes | BC -> Web | Read | |
| [Stock](#get-stock) | Stock Available  | BC -> Web | Read | |
| [Web Order](#create-web-order) | Create Web Order and Lines in BC | Web->BC    | Read Create | |
| [Payments](#create-payment) | Create Payment on Paym. Journal in BC | Web->BC | Create | |
| [Manifest](#get-manifest) | Shipping Manifest Status | BC -> Web | Read | |
| [Orders Status](#get-orders-status) | List of Orders with Tracking updates | BC -> Web | Read | |
| [Sales Prices](#get-sales-prices) | Plain List of Sales Prices| BC -> Web | Read | |
| SOAP Real Time Functions| Library of function to consume with SOAP Calls | BC -> Web | Read | |

## Endpoints businesscentralodataV4Prefix structure

Common endpoint service

~~~ api
https://api.businesscentral.dynamics.com/<API Version>/<user domain name>/<Enviroment Name>/ODataV4/Company('<Company Namme>')
~~~

Sample

~~~ api
https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/Production/ODataV4/Company('Bevica%20Web%20Integration')
~~~

## Endpoints businesscentralodataV4Prefix structure



## GET Customers

Retrieve the properties and relationships of a customer object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralodatav4prefix-structure).

~~~ api
businesscentralodataV4Prefix/WS_Customer_V3
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
"value": [
        {
            "@odata.etag": "W/\"JzQ0OzMwdHIvR0xYVndidXFwVVBiaGcvS1g0NVFpQWtyNytMYW5ZV2VyVnJxRjg9MTswMDsn\"",
            "No": "1010000",
            "Web_Id": "",
            "Web_Last_Mod_Date_Time": "2022-06-28T15:10:41.603Z",
            "Name": "Asado Bar & Grill",
            "Blocked": " ",
            "Address": "Thatcham Business Village",
            "Address_2": "Colthrop Way",
            "City": "Thatcham",
            "County": "Surrey",
            "Post_Code": "RG19 4LW",
            "Country_Region_Code": "GB",
            "Primary_Contact_No": "CT100292",
            "Contact_Name": "Greg Chapman",
            "Phone_No": "",
            "E_Mail": "greg@contoso.com",
            "Home_Page": "www.Bevica.co.uk",
            "Language_Code": "ENG",
            "Currency_Code": "",
            "Shipment_Method_Code": "EXW",
            "Shipping_Agent_Code": "DHL",
            "Shipping_Agent_Service_Code": "OVERNIGHT",
            "Location_Code": "BLUE",
            "VAT_Registration_No": "",
            "Payment_Terms_Code": "30 DAYS",
            "Payment_Method_Code": "",
            "GLN": "8712345000004",
            "Gen_Bus_Posting_Group": "DOMESTIC",
            "VAT_Bus_Posting_Group": "DOMESTIC",
            "Customer_Posting_Group": "DOMESTIC",
            "Customer_Price_Group": "BARS",
            "Customer_Disc_Group": "",
            "AWRS_URN": "",
            "Territory_Code": "MID",
            "Partner_Type": " ",
            "Privacy_Blocked": false,
            "Salesperson_Code": "ED",
            "Responsibility_Center": "",
            "Global_Dimension_1_Code": "SALES",
            "Global_Dimension_2_Code": "",
            "Balance": 0,
            "Balance_LCY": 0,
            "Balance_Due": 0,
            "Global_Dimension_1_Filter": "",
            "Global_Dimension_2_Filter": "",
            "Currency_Filter": "",
            "Date_Filter": "..06/28/22"
        },
        {
            "@odata.etag": "W/\"JzQ0O0pnMGoxR3pLTTQ1ZFNHME1Gb1BwSUtmc0FKU09ieGxPY0NYSkhJTlpOZ3c9MTswMDsn\"",
            "No": "1020000",
            "Web_Id": "",
            "Web_Last_Mod_Date_Time": "2022-06-28T15:10:41.697Z",
            "Name": "The Pickled Egg Pub",
            "Blocked": " ",
            "Address": "153 Thomas Drive",
            "Address_2": "",
            "City": "",
            "County": "Fife",
            "Post_Code": "KY16 1GY",
            "Country_Region_Code": "GB",
            "Primary_Contact_No": "",
            "Contact_Name": "Mr. Mark McArthur",
            "Phone_No": "",
            "E_Mail": "",
            "Home_Page": "",
            "Language_Code": "ENG",
            "Currency_Code": "",
            "Shipment_Method_Code": "EXW",
            "Shipping_Agent_Code": "DHL",
            "Shipping_Agent_Service_Code": "",
            "Location_Code": "BLUE",
            "VAT_Registration_No": "",
            "Payment_Terms_Code": "14 DAYS",
            "Payment_Method_Code": "",
            "GLN": "8712345000011",
            "Gen_Bus_Posting_Group": "DOMESTIC",
            "VAT_Bus_Posting_Group": "DOMESTIC",
            "Customer_Posting_Group": "DOMESTIC",
            "Customer_Price_Group": "LND GRP",
            "Customer_Disc_Group": "",
            "AWRS_URN": "",
            "Territory_Code": "MID",
            "Partner_Type": " ",
            "Privacy_Blocked": false,
            "Salesperson_Code": "JR",
            "Responsibility_Center": "",
            "Global_Dimension_1_Code": "SALES",
            "Global_Dimension_2_Code": "",
            "Balance": 0,
            "Balance_LCY": 0,
            "Balance_Due": 0,
            "Global_Dimension_1_Filter": "",
            "Global_Dimension_2_Filter": "",
            "Currency_Filter": "",
            "Date_Filter": "..06/28/22"
        }
    ]
}
```

### Customer Fields

| Relation | Source Table | Field Caption | Field Type | Field Lenght | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
| 1 | Customer | No. | string | 20 | Primaty Key (Required for Update) |
| 1 | Customer | Web Id | string | 20 | Web Site Id |
| 1 | Customer | Web Last Mod Date Time | datetime |  | Last Update Date Time  |
| 1 | Customer | Name | string | 100 |  |
| 1 | Customer | Name 2 | string | 50 |  |
| 1 | Customer | Blocked | option |  |  |
| 1 | Customer | Address | string | 100 |  |
| 1 | Customer | Address 2 | string | 50 |  |
| 1 | Customer | City | string | 30 |  |
| 1 | Customer | County | string | 30 |  |
| 1 | Customer | Post Code | string | 20 |  |
| 1 | Customer | Country/Region Code | string | 10 |  |
| 1 | Customer | Primary Contact No. | string | 20 |  |
| 1 | Customer | Contact | string | 100 |  |
| 1 | Customer | Phone No. | string | 30 |  |
| 1 | Customer | E-Mail | string | 80 |  |
| 1 | Customer | Home Page | string | 80 |  |
| 1 | Customer | Language Code | string | 10 |  |
| 1 | Customer | Currency Code | string | 10 |  |
| 1 | Customer | Shipment Method Code | string | 10 |  |
| 1 | Customer | Shipping Agent Code | string | 10 |  |
| 1 | Customer | Shipping Agent Service Code | string | 19 |  |
| 1 | Customer | Location Code | string | 10 |  |
| 1 | Customer | VAT Registration No. | string | 20 |  |
| 1 | Customer | Payment Terms Code | string | 10 |  |
| 1 | Customer | Payment Method Code | string | 10 |  |
| 1 | Customer | GLN | string | 13 |  |
| 1 | Customer | Gen. Bus. Posting Group | string | 20 |  |
| 1 | Customer | VAT Bus. Posting Group | string | 20 |  |
| 1 | Customer | Customer Posting Group | string | 20 |  |
| 1 | Customer | Customer Price Group | string | 20 |  |
| 1 | Customer | Customer Disc. Group | string | 20 |  |
| 1 | Customer | AWRS No. | string | 20 |  |
| 1 | Customer | Territory Code | string | 10 |  |
| 1 | Customer | Partner Type | enum |  |  |
| 1 | Customer | Privacy Blocked | bool |  |  |
| 1 | Customer | Salesperson Code | string | 20 |  |
| 1 | Customer | Responsibility Center | string | 10 |  |
| 1 | Customer | Global Dimension 1 Code | string | 20 |  |
| 1 | Customer | Global Dimension 2 Code | string | 20 |  |
| 1 | Customer | Balance | decimal |  |  |
| 1 | Customer | Balance_LCY | decimal |  |  |
| 1 | Customer | Balance Due | decimal |  |  |
| 1..N | Ship-to Address | Customer No. | string | 20 | PK Key (Required for Update) |
| 1..N | Ship-to Address | Code | string | 20 | PK Key (Required for Update)|
| 1..N | Ship-to Address | Name | string | 100 |  |
| 1..N | Ship-to Address | Name 2 | string | 50 |  |
| 1..N | Ship-to Address | Address | string | 100 |  |
| 1..N | Ship-to Address | Address 2 | string | 50 |  |
| 1..N | Ship-to Address | City | string | 30 |  |
| 1..N | Ship-to Address | Contact | string |  |  |
| 1..N | Ship-to Address | Phone No. | string | 100 |  |
| 1..N | Ship-to Address | Shipment Method Code | string | 10 |  |
| 1..N | Ship-to Address | Shipping Agent Code | string | 10 |  |
| 1..N | Ship-to Address | Country/Region Code | string | 10 |  |
| 1..N | Ship-to Address | Post Code | string | 20 |  |
| 1..N | Ship-to Address | County | string | 30 |  |
| 1..N | Ship-to Address | E-Mail | string | 80 |  |
| 1..N | Ship-to Address | Shipping Agent Service Code | string | 10 |  |
| 1..N | Ship-to Address | Service Zone Code | string | 10 |  |
| 1..N | Ship-to Address | Duty Type | string | 10 |  |

## GET Products

Retrieve the properties and relationships of a Item object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralodatav4prefix-structure).

~~~ api
businesscentralodataV4Prefix/WS_Product_V3
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

"value": [
        {
            "@odata.etag": "W/\"JzQ0O0U5ZXp6Vm9ISEVhakh4QSthNk1MeVhKUU9qZXArMTFVSG5ua0F4ZHZPWDQ9MTswMDsn\"",
            "Code": "B12147",
            "Web_Product_ID": "{73C93262-09B9-464F-9673-2CC0B707DEC4}",
            "Web_Last_Mod_Date_Time": "2022-06-28T15:14:23.827Z",
            "Published": 1,
            "Marketing_Description": "Barolo Riserva DOCG, Vigna Colonello, Marchese Antinori, Prunotto",
            "Category_Code": "STILL RED",
            "Category_Description": "Red Still",
            "Country_Code": "IT",
            "Country_Description": "Italy",
            "Region_Code": "",
            "Region_Description": "",
            "SubRegion_Code": "",
            "SubRegion_Description": "",
            "Producer_Code": "PRUNOTTO",
            "Producer_Name": "Prunotto",
            "Item_Classification": "DOCG",
            "Alcool_Percent": "14%",
            "Vintage": "2010",
            "Grapes": "",
            "Attributes": "Vegan=Yes,Sulphites=Yes",
            "Tags": "IT,,,Yes,Yes,2010,Prunotto,DOCG,14%,Red Still,"
        },
        {
            "@odata.etag": "W/\"JzQ0O3lsQlhaM2xjSU5KaEo4UFZFR3FkdEplRWZieEdWWHdRdGpBMFlJY2xmY0k9MTswMDsn\"",
            "Code": "B12148",
            "Web_Product_ID": "{07119AA4-7F12-484A-ADA1-8F3B82BFCE25}",
            "Web_Last_Mod_Date_Time": "2022-06-28T15:14:32.153Z",
            "Published": 1,
            "Marketing_Description": "Barolo Riserva DOCG, Vigna Colonello, Marchese Antinori, Prunotto",
            "Category_Code": "STILL RED",
            "Category_Description": "Red Still",
            "Country_Code": "IT",
            "Country_Description": "Italy",
            "Region_Code": "",
            "Region_Description": "",
            "SubRegion_Code": "",
            "SubRegion_Description": "",
            "Producer_Code": "PRUNOTTO",
            "Producer_Name": "Prunotto",
            "Item_Classification": "DOCG",
            "Alcool_Percent": "14%",
            "Vintage": "2009",
            "Grapes": "",
            "Attributes": "",
            "Tags": "IT,,,,2009,Prunotto,DOCG,14%,Red Still,"
        },
        {
            "@odata.etag": "W/\"JzQ0O1Naa0dERkxpMW1iQzRERExQTFB3NWRjUFUvMnhRcU94Tng5bjgyNDRDWkk9MTswMDsn\"",
            "Code": "B12154",
            "Web_Product_ID": "{708E3384-FCC5-4AF6-B69B-9E8840573AB5}",
            "Web_Last_Mod_Date_Time": "2022-06-28T15:14:42.053Z",
            "Published": 1,
            "Marketing_Description": "Barolo Riserva DOCG, Vigna Colonello, Marchese Antinori, Prunotto",
            "Category_Code": "STILL RED",
            "Category_Description": "Red Still",
            "Country_Code": "IT",
            "Country_Description": "Italy",
            "Region_Code": "",
            "Region_Description": "",
            "SubRegion_Code": "",
            "SubRegion_Description": "",
            "Producer_Code": "PRUNOTTO",
            "Producer_Name": "Prunotto",
            "Item_Classification": "DOCG",
            "Alcool_Percent": "14%",
            "Vintage": "2012",
            "Grapes": "",
            "Attributes": "",
            "Tags": "IT,,,,2012,Prunotto,DOCG,14%,Red Still,"
        
    ]
}
```

### Product Fields

| Relation | Source Table | Field Caption | Field Type | Field Lenght | Note |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1       |  Product      |  Code        | Code       |  20          |           |
|  1       |  Product      |  Web Product Id  | Code       |  20      |           |
|  1       |  Product      |  Web Last Md. Date Time  | Date Time     |           |
|  1       |  Product      |  Published  | Boolean    |               ||
|  1       |  Product      |  Last Modification  | Date Time          ||
|  1       |  Product      |  Marketing Description  |String ||
|  1       |  Product      |  Category Code  | String ||
|  1       |  Product      |  Category Description  | String ||
|  1       |  Product      |  Country Code  | String ||
|  1       |  Product      |  Country Description  |  String ||
|  1       |  Product      |  Region Code  | String ||
|  1       |  Product      |  Region Description  |String ||
|  1       |  Product      |  SubRegion Code  |String ||
|  1       |  Product      |  SubRegion Description  |String ||
|  1       |  Product      |  Producer  |String ||
|  1       |  Product      |  Item Classification  |String ||
|  1       |  Product      |  Alcool Percent  |Decimal ||
|  1       |  Product      |  Vintage  |String ||
|  1       |  Product      |  Grapes  |String ||
|  1       |  Product      |  Attributes  |String ||
|  1       |  Product      |  Tags  |String ||
|  1..1    |  SKU\Variant  |  Web Item Id  |String ||
|  1..1    |  SKU\Variant  |  Published  |Boolean ||
|  1..1    |  SKU\Variant  |  Deleted  |Boolean ||
|  1..1    |  SKU\Variant  |  Web Last Mod. Date Time  | Date Time ||
|  1..1    |  SKU\Variant  |  Item No  | String ||
|  1..1    |  SKU\Variant  |  Blocked  | Boolean ||
|  1..1    |  SKU\Variant  |  Last Modification  | Date Time ||
|  1..1    |  SKU\Variant  |  Description  | String ||
|  1..1    |  SKU\Variant  |  Base UoM Code  | String ||
|  1..1    |  SKU\Variant  |  Base UoM Description  | String ||
|  1..1    |  SKU\Variant  |  Sales UoM Code  | String ||
|  1..1    |  SKU\Variant  |  Sales UoM Description  | String ||
|  1..1    |  SKU\Variant  |  Sales UoM Qty Per  | Decimal ||
|  1..1    |  SKU\Variant  |  Unit Volume  | Decimal ||
|  1..1    |  SKU\Variant  |  Unit Price With Duty  |Decimal ||
|  1..1    |  SKU\Variant  |  Unit Price WithOut Duty  |Decimal ||
|  1..1    |  SKU\Variant  |  Stock Quantity Base  |Decimal ||
|  1..1    |  SKU\Variant  |  Bottles Per Case | Deciaml||
|  1..1    |  SKU\Variant  |  Purchasing Code | String||
|  1..1    |  SKU\Variant  |  Unit Weight | Decimal||
|  1..1    |  SKU\Variant  |  Sales Unit Weight | Decimal||
|  1..1    |  SKU\Variant  |  Web UoM Code | String||
|  1..1    |  SKU\Variant  |  Web UoM Description | String||
|  1..1    |  SKU\Variant  |  Web Sale Only Unit | Decimal||
|  1..1    |  SKU\Variant  |  Web Catalogue  | String||

## GET Stock

Retrieve the properties and relationships of a Stock object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralodatav4prefix-structure).

~~~ api
businesscentralodataV4Prefix/WS_Stock_V3
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

"value": [
        {
            "@odata.etag": "W/\"JzQ0OzZuUmRLaHlpY1lIbkcxVWEvaGxDOW1tdzdaR2dLdVp3d2J4S1g4NGU1UHc9MTswMDsn\"",
            "Group_Code": "",
            "Item_No": "B12147",
            "Variant_Code": "",
            "Unit_of_Measure_Code": "75CL",
            "Location_Code": "BLUE",
            "Qty_per_Unit_of_Measure": 1,
            "Stock_Available_Base": 1320,
            "Last_Mod_Date_Time": "2022-06-28T16:01:26.077Z"
        },
        {
            "@odata.etag": "W/\"JzQ0OzNwbWNwTHlmOURUSHhkWFpTK1VGTWVzVExiNlpDRS9rVzExdSt0YVMwSlU9MTswMDsn\"",
            "Group_Code": "",
            "Item_No": "B12148",
            "Variant_Code": "",
            "Unit_of_Measure_Code": "75CL",
            "Location_Code": "BLUE",
            "Qty_per_Unit_of_Measure": 1,
            "Stock_Available_Base": 0,
            "Last_Mod_Date_Time": "2022-06-28T16:01:26.107Z"
        },
        {
            "@odata.etag": "W/\"JzQ0O1U0b1dOb25wQnFWUkFWNXBkbXEvVDZBQnhRRldNeFBSeXMzNmUvOGh5WGc9MTswMDsn\"",
            "Group_Code": "",
            "Item_No": "B12154",
            "Variant_Code": "",
            "Unit_of_Measure_Code": "75CL",
            "Location_Code": "BLUE",
            "Qty_per_Unit_of_Measure": 1,
            "Stock_Available_Base": 6000,
            "Last_Mod_Date_Time": "2022-06-28T16:01:26.12Z"
        },
        {
            "@odata.etag": "W/\"JzQ0O0t1SEFTQzFPUXRmaXpxL0RNMHUxeTVxZFlxcXczdmZnUU5RU3BYV3hQVTg9MTswMDsn\"",
            "Group_Code": "",
            "Item_No": "B12161",
            "Variant_Code": "",
            "Unit_of_Measure_Code": "37.5CL",
            "Location_Code": "BLUE",
            "Qty_per_Unit_of_Measure": 1,
            "Stock_Available_Base": 0,
            "Last_Mod_Date_Time": "2022-06-28T16:01:26.137Z"
        },
        {
            "@odata.etag": "W/\"JzQ0O3ZwSzErUG1BRmRiZFJ0amZyU3llWUlvUEUvM1VXQnU4eVdibTg5TUZLRjg9MTswMDsn\"",
            "Group_Code": "",
            "Item_No": "B12168",
            "Variant_Code": "",
            "Unit_of_Measure_Code": "37.5CL",
            "Location_Code": "BLUE",
            "Qty_per_Unit_of_Measure": 1,
            "Stock_Available_Base": 0,
            "Last_Mod_Date_Time": "2022-06-28T16:01:26.153Z"
        },
        {
            "@odata.etag": "W/\"JzQ0O0dCbVViY1dOSStUMDlIMi9PdmY0YStuWnJ2RHNHaHEvMnNJVENpRVpYeUk9MTswMDsn\"",
            "Group_Code": "",
            "Item_No": "B62470",
            "Variant_Code": "",
            "Unit_of_Measure_Code": "75CL",
            "Location_Code": "BLUE",
            "Qty_per_Unit_of_Measure": 1,
            "Stock_Available_Base": 0,
            "Last_Mod_Date_Time": "2022-06-28T16:01:26.153Z"
        }
    ]
}
```

### Stock Fields

| Relation | Source Table | Field Caption | Field Type | Field Lenght | Note |
| ----------- | ----------- | ----------- | -------- | ---------- |---------- |
|  1  | Web Stock| Item_No  |  String  | 20 | Primary Key Field SKU Code|
|  1  | Web Stock| Variant_Code  |  String  | 10 | Primary Key Field Duty Status|
|  1  | Web Stock| Unit_of_Measure_Code  |  String  | 10 | Primary Key Field UoM|
|  1  | Web Stock| Location_Code  |  String  |  10 | Primary Key Field Location |
|  1  | Web Stock| Group_Code  |  String  | 50 | Primary Key Field (Not Used)|
|  1  | Web Stock| Qty_per_Unit_of_Measure  |  Decimal  | |
|  1  | Web Stock| Stock_Available_Base  |  Decimal  | Stock Available |
|  1  | Web Stock| Last_Mod_Date_Time  |  Date Time  || Last Mod. Date Time|



## Create Web Order

Retrieve the properties and relationships of a Web Order object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralodatav4prefix-structure).

~~~ api
businesscentralodataV4Prefix/WS_Order_V3
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Here is an example of the request

```json
{
    
        {
            "Order_Type": "WEB",
            "Order_Id": "WEB04",
            "Total_Order_Amount": 238.95,
            "Your_Reference": "2000000020",
            "External_Document_No": "2000000020",
            "Sell_to_Customer_No": "C00001",
            "Sell_to_Customer_Name": "Black and White Ltd",
            "Sell_to_Customer_Name_2": "",
            "Sell_to_Address": "16 Hyde Park Gate",
            "Sell_to_Address_2": "",
            "Sell_to_City": "London",
            "Sell_to_Contact": "Mr. John Black",
            "Sell_to_Post_Code": "SW7 9DG",
            "Sell_to_County": "",
            "Sell_to_Country_Region_Code": "GB",
            "Sell_to_Phone_No": "07110221662",
            "Sell_to_E_Mail": "black&whiteltd@gmail.com",
            "Sell_to_Customer_Template_Code": "",
            "Sell_to_Contact_No": "",
            "Ship_to_Code": "",
            "Ship_to_Name": "Camden Shop 1",
            "Ship_to_Name_2": "",
            "Ship_to_Address": "211 Camden High St",
            "Ship_to_Address_2": "",
            "Ship_to_City": "London",
            "Ship_to_Contact": "Mr. Sam White",
            "Ship_to_Post_Code": "NW1 7BT",
            "Ship_to_County": "",
            "Ship_to_Country_Region_Code": "GB",

            "WS_Order_V3Lines": [
               {
                "Order_Group": "GROUP_A",
                "Order_Id": "WEB04",
                "Line_Id": "1",
                "Type": "Item",
                "No": "B12147",
                "Description": "First Line",
                "Description_2": "",
                "Quantity": 1
               }
            ]
           
        }
}
```

### Response

Here is an example of the response

```json
{
    "value": [
        {
            "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/Production/ODataV4/$metadata#Company('Bevica%20Web%20Integration')/WS_Order_V3/$entity",
            "@odata.etag": "W/\"JzQ0O2xEZXoxOE96dnlCQUwvUDlPUkl6YWtES3l2Umx5ZEVrSDd1YnFRaHhkWDg9MTswMDsn\"",
            "Order_Group": "GROUP_A",
            "Order_Id": "WEB04",
            "Order_Type": "WEB",
            "Customer_Id": "",
            "Customer_Email": "",
            "Location_Id": "",
            "Ship_Address_Id": "",
            "Ship_Method_Id": "",
            "Shipping_Agent_Id": "",
            "Shipping_Agent_Service_Id": "",
            "Payment_Method_Id": "",
            "Payment_Id": "",
            "Pending_Cart": false,
            "Dispatched": false,
            "Paid": false,
            "Total_Tax_Amount": 0,
            "Total_Order_Amount": 238.95,
            "Total_Discount_Amount": 0,
            "Total_Voucher_Amount": 0,
            "Total_Ship_Cost_Amount": 0,
            "Order_URL": "",
            "Delivery_Note_Text_1": "",
            "Delivery_Note_Text_2": "",
            "Gift_Note_Text_1": "",
            "Gift_Note_Text_2": "",
            "Note_Text_1": "",
            "Note_Text_2": "",
            "Order_Date": "0001-01-01",
            "Posting_Date": "0001-01-01",
            "Shipment_Date": "0001-01-01",
            "Posting_Description": "",
            "Payment_Terms_Code": "",
            "Due_Date": "0001-01-01",
            "Shipment_Method_Code": "",
            "Location_Code": "",
            "Shortcut_Dimension_1_Code": "",
            "Shortcut_Dimension_2_Code": "",
            "Customer_Posting_Group": "",
            "Currency_Code": "",
            "Currency_Factor": 0,
            "Customer_Price_Group": "",
            "Prices_Including_VAT": false,
            "Customer_Disc_Group": "",
            "Language_Code": "",
            "Salesperson_Code": "",
            "Package_Tracking_No": "",
            "VAT_Bus_Posting_Group": "",
            "Your_Reference": "2000000020",
            "VAT_Registration_No": "",
            "Reason_Code": "",
            "Gen_Bus_Posting_Group": "",
            "External_Document_No": "2000000020",
            "Payment_Method_Code": "",
            "Shipping_Agent_Code": "",
            "VAT_Country_Region_Code": "",
            "Document_Date": "0001-01-01",
            "Sell_to_Customer_No": "C00001",
            "Sell_to_Customer_Name": "Black and White Ltd",
            "Sell_to_Customer_Name_2": "",
            "Sell_to_Address": "16 Hyde Park Gate",
            "Sell_to_Address_2": "",
            "Sell_to_City": "London",
            "Sell_to_Contact": "Mr. John Black",
            "Sell_to_Post_Code": "SW7 9DG",
            "Sell_to_County": "",
            "Sell_to_Country_Region_Code": "GB",
            "Sell_to_Phone_No": "07110221662",
            "Sell_to_E_Mail": "black&whiteltd@gmail.com",
            "Sell_to_Customer_Template_Code": "",
            "Sell_to_Contact_No": "",
            "Ship_to_Code": "",
            "Ship_to_Name": "Camden Shop 1",
            "Ship_to_Name_2": "",
            "Ship_to_Address": "211 Camden High St",
            "Ship_to_Address_2": "",
            "Ship_to_City": "London",
            "Ship_to_Contact": "Mr. Sam White",
            "Ship_to_Post_Code": "NW1 7BT",
            "Ship_to_County": "",
            "Ship_to_Country_Region_Code": "GB",
            "Requested_Delivery_Date": "0001-01-01",
            "Promised_Delivery_Date": "0001-01-01",
            "Shipping_Agent_Service_Code": ""
        }
   
    ]
}
```

### Web Order Fields

| Relation | Source Table | Field Caption | Field Type | Field Lenght | Note      | Mandatory | Required |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |--- |--- |
| 1  | Web Order Header | Order Group | Code | 50 | Key (Internal Use) |  |  |
| 1  | Web Order Header | Order Id | Code | 50 | Key (Unique Web Reference) | Y | Y |
| 1  | Web Order Header | Order Type | Code | 10 | Web Specific |  | Y |
| 1  | Web Order Header | Customer Id | Code | 50 | Web Specific |  | Y |
| 1  | Web Order Header | Customer Email | Text | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Location Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Ship Address Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Payment Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Ship Method Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Pending Cart | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Payment Method Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Shpping Agent Id | code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Shipping Agent Service Id | Code | 50 | Web Specific |  |  |
| 1  | Web Order Header | Dispatched | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Paid | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Order Date | Date |  | Standard |  | Y |
| 1  | Web Order Header | Posting Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Shipment Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Posting Description | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Payment Terms Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Due Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Shipment Method Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Location Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 1 Code | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Shortcut Dimension 2 Code | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Customer Posting Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Currency Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Currency Factor | Decimal |  | Standard |  |  |
| 1  | Web Order Header | Customer Price Group | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Prices Including VAT | Boolean |  | Standard |  |  |
| 1  | Web Order Header | Customer Disc. Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Language Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Salesperson Code | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Package Tracking No. | Text | 30 | Standard |  |  |
| 1  | Web Order Header | VAT Bus. Posting Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Your Reference | Text | 35 | Standard |  |  |
| 1  | Web Order Header | VAT Registration No. | Text | 20 | Standard |  |  |
| 1  | Web Order Header | Reason Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Gen. Bus. Posting Group | Code | 20 | Standard |  |  |
| 1  | Web Order Header | External Document No. | Code | 35 | Standard |  |  |
| 1  | Web Order Header | Payment Method Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Shipping Agent Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | VAT Country/Region Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Document Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer No. | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Sell-to Customer Name | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Customer Name 2 | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Address | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Address 2 | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to City | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Contact | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Sell-to Post Code | Code | 20 | Standard |  | Y |
| 1  | Web Order Header | Sell-to County | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Country/Region Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Phone No. | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Sell-to E-Mail | Text | 80 | Standard |  | Y |
| 1  | Web Order Header | Sell-to Customer Template Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Sell-to Contact No. | Code | 20 | Standard |  |  |
| 1  | Web Order Header | Ship-to Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Ship-to Name | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Name 2 | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to Address | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Address 2 | Text | 50 | Standard |  |  |
| 1  | Web Order Header | Ship-to City | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Contact | Text | 50 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Post Code | Code | 20 | Standard |  | Y |
| 1  | Web Order Header | Ship-to County | Text | 30 | Standard |  | Y |
| 1  | Web Order Header | Ship-to Country/Region Code | Code | 10 | Standard |  | Y |
| 1  | Web Order Header | Order URL | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Total Ship Cost Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Total Voucher Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Total Discount Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Total Order Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Total Tax Amount | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Delivery Note Text 1 | Text | 80 | Web Specific |  | Y |
| 1  | Web Order Header | Delivery Note Text 2 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 1 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Gift Note Text 2 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 1 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Note Text 2 | Text | 80 | Web Specific |  |  |
| 1  | Web Order Header | Requested Delivery Date | Date |  | Standard |  | Y |
| 1  | Web Order Header | Promised Delivery Date | Date |  | Standard |  |  |
| 1  | Web Order Header | Shipping Agent Service Code | Code | 10 | Standard |  |  |
| 1  | Web Order Header | Decimal 01 | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Integer 01 | Integer |  | Web Specific |  |  |
| 1  | Web Order Header | Date 01 | Date |  | Web Specific |  |  |
| 1  | Web Order Header | Code 01 | Code | 20 | Web Specific |  |  |
| 1  | Web Order Header | Time 01 | Time |  | Web Specific |  |  |
| 1  | Web Order Header | DateTime 01 | DateTime |  | Web Specific |  |  |
| 1  | Web Order Header | Text 01 | Text | 50 | Web Specific |  |  |
| 1  | Web Order Header | Boolean 01 | Boolean |  | Web Specific |  |  |
| 1  | Web Order Header | Decimal 02 | Decimal |  | Web Specific |  |  |
| 1  | Web Order Header | Integer 02 | Integer |  | Web Specific |  |  |
| 1  | Web Order Header | Date 02 | Date |  | Web Specific |  |  |
| 1  | Web Order Header | Code 02 | Code | 20 | Web Specific |  |  |
| 1  | Web Order Header | Time 02 | Time |  | Web Specific |  |  |
| 1  | Web Order Header | DateTime 02 | DateTime |  | Web Specific |  |  |
| 1  | Web Order Header | Text 02 | Text | 50 | Web Specific |  |  |
| 1  | Web Order Header | Boolean 02 | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Order Group | Code | 50 | Key |  |  |
| 1..N  | Web Order Lines | Order Id | Code | 50 | Key (Unique External Reference) | Y | Y |
| 1..N  | Web Order Lines | Line Id | Code | 50 | Key (Unique External Reference) | Y | Y |
| 1..N  | Web Order Lines | Product Id | Code | 50 | Web Specific |  | Y |
| 1..N  | Web Order Lines | Unit of Measure Id | Code | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Force Calculation Price | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Lot No. | Code | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Negative | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Type | Option |  | Standard |  |  |
| 1..N  | Web Order Lines | No. | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Shipment Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Description | Text | 50 | Standard |  | Y |
| 1..N  | Web Order Lines | Description 2 | Text | 50 | Standard |  |  |
| 1..N  | Web Order Lines | Quantity | Decimal |  | Standard |  | Y |
| 1..N  | Web Order Lines | Unit Price | Decimal |  | Standard |  | Y |
| 1..N  | Web Order Lines | VAT % | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Line Discount % | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Line Discount Amount | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Net Amount | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Amount Including VAT | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Shortcut Dimension 1 Code | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Shortcut Dimension 2 Code | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Gen. Bus. Posting Group | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Gen. Prod. Posting Group | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | VAT Bus. Posting Group | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | VAT Prod. Posting Group | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | VAT Base Amount | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Unit Cost | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | VAT Identifier | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Variant Code | Code | 10 | Standard |  |  |
| 1..N  | Web Order Lines | Qty. per Unit of Measure | Decimal |  | Standard |  |  |
| 1..N  | Web Order Lines | Unit of Measure Code | Code | 10 | Standard |  |  |
| 1..N  | Web Order Lines | Item Category Code | Code | 20 | Standard |  |  |
| 1..N  | Web Order Lines | Requested Delivery Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Promised Delivery Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Planned Delivery Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Planned Shipment Date | Date |  | Standard |  |  |
| 1..N  | Web Order Lines | Decimal 01 | Decimal |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Integer 01 | Integer |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Date 01 | Date |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Code 01 | Code | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Time 01 | Time |  | Web Specific |  |  |
| 1..N  | Web Order Lines | DateTime 01 | DateTime |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Text 01 | Text | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Boolean 01 | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Decimal 02 | Decimal |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Integer 02 | Integer |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Date 02 | Date |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Code 02 | Code | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Time 02 | Time |  | Web Specific |  |  |
| 1..N  | Web Order Lines | DateTime 02 | DateTime |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Text 02 | Text | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Boolean 02 | Boolean |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Decimal 03 | Decimal |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Integer 03 | Integer |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Date 03 | Date |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Code 03 | Code | 20 | Web Specific |  |  |
| 1..N  | Web Order Lines | Time 03 | Time |  | Web Specific |  |  |
| 1..N  | Web Order Lines | DateTime 03 | DateTime |  | Web Specific |  |  |
| 1..N  | Web Order Lines | Text 03 | Text | 50 | Web Specific |  |  |
| 1..N  | Web Order Lines | Boolean 03 | Boolean |  | Web Specific |  |  |

## Create Payment

Retrieve the properties and relationships of a Payment Journal object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralodatav4prefix-structure).

~~~ api
POST

businesscentralodataV4Prefix/WS_Payment_V3
~~~

### Request Headers

Header | Value |
--- | --- |
Authorization | Bearer {token}. Required.|

### Request Body

Here is an example of the request

```json
{
   
    "External_Document": "TEST001",
    "Currency_Code": "GBP",
    "Customer_No": "C001",
    "Payment_Reference": "TPAYTESTEST",
    "Amount": 70.7

}
```
### Response

Here is an example of the response

```json
{
    "value": [
        {
            "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/Production/ODataV4/$metadata#Company('Bevica%20Web%20Integration')/WS_Payment_V3/$entity",
            "@odata.etag": "W/\"JzQ0OytoRXh1REljR1habHMyNHFvZ0F2QVFUd1I1RGk0WXd6L2ZCSlo1RCtUK2M9MTswMDsn\"",
            "Entry_No": 2,
            "Currency_Code": "GBP",
            "Customer_Id": "",
            "Customer_No": "C001",
            "Document_No": "",
            "External_Document": "TEST001",
            "Payment_Method_Code": "",
            "Payment_Reference": "TPAYTESTEST",
            "Posting_Date": "0001-01-01",
            "Amount": 70.7,
            "Due_Date": "0001-01-01",
            "Refund": false
        }
    ]
}
```

### Payment Fields

| Relation | Source Table | Field Caption | Field Type | Field Lenght | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1          | Payment         | External_Document         |  String    | 80           | |
|  1          | Payment         | Currency_Code         |  String    | 10           | |
|  1          | Payment         | Payment_Reference         |  String    | 50           | |
|  1          | Payment         | Amount         |  Decimal    |            | |
|  1          | Payment         | Payment_Method_Code         |  String    | 10           | |
|  1          | Payment         | Posting_Date         |  Date    |            | |
|  1          | Payment         | Due_Date         |  Date    |            | |


## GET Manifest

Retrieve the properties and relationships of a Manifest object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralodatav4prefix-structure).

~~~ api
businesscentralodataV4Prefix/WS_Manifest_V3
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


## GET Orders Status

Retrieve the properties and relationships of a Web Order object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralodatav4prefix-structure).

~~~ api
businesscentralodataV4Prefix/WS_OrderStatus_V3
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
        {
    "@odata.context": "https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/Production/ODataV4/$metadata#Company('Bevica%20Web%20Integration')/WS_OrderStatus_V3",
    "value": [
        {
            "@odata.etag": "W/\"JzQ0O0hFMHVLcEwrclZreUdPeHYrcWVCRG9ORHpFeHg5UjZHZjFDOWhlUnFER3c9MTswMDsn\"",
            "Order_Group": "GROUP_A",
            "Order_Id": "WEB04",
            "Order_Date": "0001-01-01",
            "BC_Status": "Created",
            "BC_Error_Message": "",
            "BC_Creation_Date_Time": "2022-06-29T15:50:26.81Z",
            "BC_Last_Mod_Date_Time": "2022-06-29T15:50:26.81Z",
            "BC_Last_Validate_Date_Time": "0001-01-01T00:00:00Z",
            "BC_Last_Process_Date_Time": "0001-01-01T00:00:00Z",
            "BC_Validated": false,
            "BC_Processed": false,
            "BC_Errored": false,
            "BC_Document_Type": " ",
            "BC_Document_No": ""
        },
        {
            "@odata.etag": "W/\"JzQ0OzE2bzRXUTVoVDBwOFcwdDc0ZzlFUnNlRlAzc3BPeC9LMkxiTkY0K1hBS0k9MTswMDsn\"",
            "Order_Group": "GROUP_A",
            "Order_Id": "WEBORDER00001",
            "Order_Date": "0001-01-01",
            "BC_Status": "Created",
            "BC_Error_Message": "",
            "BC_Creation_Date_Time": "2022-06-29T14:25:19.313Z",
            "BC_Last_Mod_Date_Time": "2022-06-29T14:25:19.327Z",
            "BC_Last_Validate_Date_Time": "0001-01-01T00:00:00Z",
            "BC_Last_Process_Date_Time": "0001-01-01T00:00:00Z",
            "BC_Validated": false,
            "BC_Processed": false,
            "BC_Errored": false,
            "BC_Document_Type": " ",
            "BC_Document_No": ""
        }
    ]
}
   
    ]
}
```

### Order Status Fields

| Relation | Source Table | Field Caption | Field Type | Field Lenght | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|  1          | Web Order         | BC_Status         |  Enum    | Created,Validated,Processed,Posted           | |
|  1          | Web Order         | BC_Error_Message         |  Text    | 250  | Error On Validation |
|  1          | Web Order         | BC_Document_No         |  Text    | 20  | Sales Order No. on BC |

## GET Sales Prices

Retrieve the properties and relationships of a Sales Prices object for Business Central.

### Http Request

Replace the URL endpoint for Dynamics 365 Business Central depending on environment following the [guideline](#endpoints-businesscentralodatav4prefix-structure).

~~~ api
GET 

businesscentralodataV4Prefix/WS_SalesPrices_V3
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
### Sales Prices Fields

| Relation | Source Table | Field Caption | Field Type | Field Lenght | Note      |
| ----------- | ----------- | ----------- | ---------- | ------------ |---------- |
|	1	|	Sales Prices	|	Item No	|	string	|	20	|
|	1	|	Sales Prices	|	Variant Code	|	string	|	10	|
|	1	|	Sales Prices	|	Sales Type	|	Type	|		|
|	1	|	Sales Prices	|	Sales Code	|	string	|	10	|
|	1	|	Sales Prices	|	Unit of Measure Code	|	string	|	10	|
|	1	|	Sales Prices	|	Starting Date	|	date	|		|
|	1	|	Sales Prices	|	Ending Date	|	date	|		|
|	1	|	Sales Prices	|	Unit Price	|	decimal	|		|
|	1	|	Sales Prices	|	Price Includes VAT	|	boolean	|		|
|	1	|	Sales Prices	|	Minimum Quantity	|	decimal	|		|


### Recommended Content

[Business Central Standard Web Service ](BC/Readme.md)

[Get Companies](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/api-reference/v2.0/api/dynamics_company_get)
