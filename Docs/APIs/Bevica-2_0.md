# Bevica Web Integration 2.0 (Rest APIs)


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


[Read More here](/Docs/README.md)

## Main Entities

| Name | Description | Data Flow | Operations | Note|
| ----------- | ----------- | ----------- | -------- | ---------- |
| [Create Payments](/Docs/APIs/Create%20Payment.md) | Create payment on Payment Journal in BC | Web->BC | Create | |
| [Create Web Order Lines](/Docs/APIs/Create%20Web%20Order%20Lines.md) | Create Web Order Lines in BC | Web->BC    | Read Create | |
| [Create Web Order](/Docs/APIs/Create%20Web%20Order.md) | Create Web Order BC | Web->BC    | Read Create | |
| [Get Customer Ledger Entries](/Docs/APIs/Get%20Customer%20Ledger%20Entries.md) | Customer Ledger Entries | BC -> Web | Read | | 
| [Get Customer](/Docs/APIs/Get%20Customer.md) | Customer information| BC -> Web | Read | |
| [Get Item](/Docs/APIs/Get%20Item.md) | Customer information| BC -> Web | Read | |
| [Get Manifest Lines](/Docs/APIs/Get%20Manifest%20Lines.md) | List of Manifest Lines | BC -> Web | Read | |
| [Get Manifest](/Docs/APIs/Get%20Manifest.md) | Shipping Manifest Status | BC -> Web | Read | |
| [Get Customer](/Docs/APIs/Get%20Marketing%20Content.md) | Customer information| BC -> Web | Read | |
| [Get Orders Status](/Docs/APIs/Get%20Order%20Status.md) | List of Orders with Tracking updates | BC -> Web | Read | |
| [Get Paid Reserve Entries](/Docs/APIs/Get%20Paid%20Reserve%20Entries.md) | List of all Paid Reserve Entries| BC -> Web | Read | |
| [Get Paid Reserve](/Docs/APIs/Get%20Paid%20Reserve.md) | List of Paid Reserve Information| BC -> Web | Read | |
| [Get Sales Credit Memo Header](/Docs/APIs/Get%20Sales%20Credit%20Memo%20Header.md) | List of Paid Reserve Information| BC -> Web | Read | |
| [Get Sales Credit Memo Line](/Docs/APIs/Get%20Sales%20Credit%20Memo%20Line.md) | List of Paid Reserve Information| BC -> Web | Read | |
| [Get Sales Invoice Header](/Docs/APIs/Get%20Sales%20Invoice%20Header.md) | List of Paid Reserve Information| BC -> Web | Read | |
| [Get Sales Invoice Line](/Docs/APIs/Get%20Sales%20Invoice%20Line.md) | List of Paid Reserve Information| BC -> Web | Read | |
| [Get Sales Price List Prices](/Docs/APIs/Get%20Sales%20Price%20List%20Prices.md) | Plain List of Sales Price List prices| BC -> Web | Read | |
| [Get Sales Prices](/Docs/APIs/Get%20Sales%20Prices.md) | Plain List of Sales Prices| BC -> Web | Read | |
| [Get Ship-to Address](/Docs/APIs/Get%20Ship-to%20Address.md) | Customer Ship to Addresses | BC -> Web | Read | |
| [Get Stock](/Docs/APIs/Get%20Stock.md) | Stock Available  | BC -> Web | Read | |
| [Get Web Product](/Docs/APIs/Get%20Web%20Product.md) | Web product details and attributes | BC -> Web | Read | |

## Endpoints businesscentralPrefix structure

Common endpoint service

~~~ api
https://api.businesscentral.dynamics.com/v2.0/<user domain name>/api/<API publisher>/<API group>/<API version>/companies(<company id>)/Customer
~~~

Sample

~~~ api
https://api.businesscentral.dynamics.com/v2.0/bevicasaas.onmicrosoft.com/tvt_develop/api/tvisiontech/webbevica/v2.0/companies(08f3eaa4-1d0f-ed11-90eb-0022480090f7)/Customer
~~~