# Standard Microsoft Business Central Web Service

Business Central supports three types of web services: API, SOAP, and OData. Web services are a lightweight, industry-standard way to make application functionality available to various external systems and users. Developers can create and publish functionality as web services, where they expose pages, codeunits, or queries, and even enhance a page web service by using an extension codeunit. When Business Central objects are published as web services, they're immediately available on the network.

## Authentication

Business Central supports the OAuth authorization protocol for SOAP and OData web services. This article describes some basics behind the use and configuration of OAuth authentication in Business Central. It describes the general aspects of the OAuth authorization protocol, including how to set it up for Business Central. The article also provides a guide on how to create a custom .NET application that connects to Business Central web services and authenticates by using OAuth.

[Using OAuth MS Docs](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/webservices/authenticate-web-services-using-oauth)

---
## APIs

RESTful web services are typically created to interchange data between Business Central and external systems. The acronym REST stands for REpresentational State Transfer. Any coding language capable of calling REST APIs can be used to use this feature. The Business Central API stack have been optimized for performance and is the preferred way to integrate with Business Central.

Business Central comes with an extensive list of built-in APIs that requires no code and minimal setup to use. When using the built-in APIs, please choose the highest API version available. You can also develop your own custom APIs using the AL object types API pages and API queries.

The articles in this section describe the key concepts and techniques for using APIs with Business Central.

[API(v2.0) MS Docs](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/api-reference/v2.0/)

---
## ODATA

The Open Data Protocol (OData) is a web protocol that is designed for querying tabular data and provides you with an alternative to SOAP-based web services. OData builds on web technologies such as HTTP and JavaScript Object Notation (JSON) to provide access to information from different applications, services, and stores. OData uses URIs for resource identification and commits to an HTTP-based, uniform interface for interacting with resources. This commitment to core Web principles allows for OData to enable a new level of data integration and interoperability across a broad range of clients, servers, services, and tools.

### $Expand statement
~~~ api
https://api.businesscentral.dynamics.com/<API Version>/<user domain name>/<Enviroment Name>/ODataV4/Company('<Company Namme>')
~~~

[OData Web Services MS Docs](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/webservices/odata-web-services)

[OData Filter expressions MS Docs](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/webservices/use-filter-expressions-in-odata-uris)

--
## SOAP

SOAP web services enable full flexibility for building operation-centric services. They provide industry-standard interoperability and channel and host pluggability.

You can use SOAP to interact with page or codeunit web services in Business Central.

[SOAP Web Services MS Docs](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/webservices/soap-web-services)

