---
layout: default
title: Account
---

# Account

This document defines the Account resource.

### Sections

* [Endpoints and URL structures](#endpoints-and-url-structures)
* [Fields](#fields)
    * [Related Objects](#related-objects)
* [Scenarios](#scenarios)
    * [Scenario: Retrieving an Account resource (GET)](#scenario-retrieving-an-account-resource-get)

{% include endpoints_and_url_structures.md %}

## Fields

|Name|Type|Description|
|---|---|---|
|name|string|Name of organization|
|billing_start|date||
|billing_end|date||
|shares_this_cycle|integer||
|share_budget|integer||
|plan|string||
|monthly_cost|string||

## Scenarios

{% include scenarios_intro.md %}

### Scenario: Retrieving an Account resource (GET)
