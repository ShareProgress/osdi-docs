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

### Scenario: Creating a new PageWrapper (POST)

### Scenario: Modifying a PageWrapper (PUT)

### Scenario: Deleting a PageWrapper (DELETE)
