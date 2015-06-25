---
layout: default
title: AccountInfo
---

# AccountInfo

This document defines the AccountInfo resource.

### Sections

* [Endpoints and URL structures](#endpoints-and-url-structures)
* [Fields](#fields)

{% include endpoints_and_url_structures.md %}

## Fields

|Name|Type |Description|
|---|---|---|
|key|string|Your API key|
|response|[ResponseSet](#responseset)|Array of account info|

### Related Objects

#### ResponseSet

|Name|Type |Description|
|---|---|---|
|account_name|string|Name of organization|
|billing_start|date||
|billing_end|date||
|shares_this_cycle|integer||
|share_budget|integer||
|plan|string||
|monthly_cost|string||
