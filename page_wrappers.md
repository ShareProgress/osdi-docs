---
layout: default
title: PageWrapper
---
 
# PageWrapper

This document defines the PageWrapper resource.

### Sections
	
* [Endpoints and URL structures](#endpoints-and-url-structures)
* [Fields](#fields)
* [Scenarios](#scenarios)
    * [Scenario: Retrieving a list of PageWrappers (GET)](#scenario-retrieving-a-list-of-page-wrappers-get)
    * [Scenario: Retrieving a PageWrapper for a SharePage (GET)](#scenario-retrieving-a-page-wrapper-for-a-share-page-get)
    * [Scenario: Creating a new PageWrapper (POST)](#scenario-creating-a-new-page-wrapper-post)
    * [Scenario: Modifying a PageWrapper (PUT)](#scenario-modifying-a-page-wrapper-put)
    * [Scenario: Deleting a PageWrapper (DELETE)](#scenario-deleting-a-page-wrapper-delete)

{% include endpoints_and_url_structures.md %}

## Fields

|Name|Type |Description|
|---|---|---|
|default| boolean|If defined as true - will override the current default wrapper. |
|name|string| Name of the wrapper |
|html|string| Content of the wrapper |
|success|boolean| true if wrapper is created |


## Scenarios

{% include scenarios_intro.md %}

### Scenario: Retrieving a list of PageWrappers (GET)

### Scenario: Retrieving a PageWrapper for a SharePage (GET)

#### Request

```javascript

```
### Scenario: Creating a new PageWrapper (POST)

Creates or updates a wrapper - validates presence of the {SHAREACTION} in the HTML block.
If 'default' is defined as true, this will override the current default wrapper.

#### Request

```javascript
POST https://osdi-sample-system.org/api/v1/wrappers/update 

Header:
OSDI-API-Token:[your api key here]

{
     "name": "Default Wrapper",
     "default": false,
     "html": "<!doctype html>\r\n<html lang=\"en\">\r\n<head>\r\n\r\n  <meta charset=\"utf-8\">\r\n\r\n  <title>PAGE_TITLE</title> <!-- this will be replaced automatically -->\r\n\r\n  <meta http-equiv=\"X-UA-Compatible\" content=\"IE=edge;chrome=1\">\r\n  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1, maximum-scale=1\">\r\n  \r\n  <link href=\"/basic.css\" media=\"all\" rel=\"stylesheet\" type=\"text/css\" />\r\n</head>\r\n\r\n<body>\r\n  <iframe src=\"http://localhost:3000\"></iframe>\r\n\r\n  <div id=\"header\">\r\n    <div id=\"header_content\">\r\n      <h1>new org</h1>\r\n    </div> <!-- #header_content -->\r\n  </div> <!-- #header -->\r\n\r\n  <div class=\"content\">\r\n  {ShareAction}\r\n  </div> <!-- .content -->\r\n\r\n  <div id=\"footer\">\r\n    <div id=\"footer_content\">\r\n      Page Disclaimer\r\n    </div> <!-- #footer_content -->\r\n  </div> <!-- #footer -->\r\n\r\n</body>\r\n</html>\r\n"
}
```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: ?

{
  "success": true
  "response": [
    {
      "id": 48,
      "name": "Default Wrapper"
    }
  ]
}
```

### Scenario: Modifying a PageWrapper (PUT)

### Scenario: Deleting a PageWrapper (DELETE)
