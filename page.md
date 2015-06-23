---
layout: default
title: Page
---
 
# Page

This document defines the Page resource.

Page resources represent share pages that supporters can use to disseminate
content via their social media networks.

### Sections
* [Endpoints and URL structures](#endpoints-and-url-structures)
* [Fields](#fields)
* [Related Resources](#related-resources)
* [Scenarios](#scenarios)
    * [Scenario: Retrieving a collection of pages (GET)](
#scenario-retrieving-pages)
    * [Scenario: Retrieving an individual page (GET)](
#scenario-retrieving-page)
    * [Scenario: Retrieving the analytics for a page (GET)](
#scenario-retrieving-analytics-page)
    * [Scenario: Creating a page, with defaults (POST)](
#scenario-creating-page-basic)
    * [Scenario: Creating a page, specifying A/B tests and options (POST)](
#scenario-creating-page-advanced)
    * [Scenario: Modifying a page to add a new A/B variant (PUT)](
#scenario-modifying-page-add-variant)
    * [Scenario: Modifying a page to remove an A/B variant (PUT)](
#scenario-modifying-page-remove-variant)
    * [Scenario: Deleting a page (DELETE)](
#scenario-deleting-page)

{% include endpoints_and_url_structures.md %}

The link relation label for a Page resource
is ```osdi:page``` for a single Page resource
or ```osdi:pages``` for a collection of Page resources.

_[Back to top...](#)_

## Fields

| Name          | Type      | Description
|-----------    |-----------|--------------
| id (optional)   | integer   | The ID of the page to update. If omitted, will create a new page with the specified parameters.
| page_url (required) | string | URL of the page that the Share Page or Share Button will be sharing. The page of the URL will be scraped upon posting to read in meta data, which may optionally be used for variant content (see auto_fill for more information). If the page cannot be returned - due to a malformed URL or down server - it will return an error.
| wrapper_id (optional) | integer | The ID of the wrapper that should be assigned to the page - if blank will default to the organization’s default wrapper.
| page_title (optional) | string | The internal title of the Share Page or Share Button.  If not provided, will be scraped from the page_url.
| html_title (optional) | string | The HTML title of the Share Page. If not provided, will use page_title or be scraped from the page_url.  
| auto_fill (optional, defaults to true) | boolean | Specifies whether we should fill in any missing variant information with what we scrape from the page_url. If listed as false, variants will remain blank if not specified.
| variants (optional) | [VariantSet](LINK TO VARIANT) | An array of the share content variants
| advanced_options (optional) | string | These are additional customizations for a Share Page or Share Buttons. If omitted, they will default to an organization’s default account settings.
| prompt (limit 120 characters) | string | A small block of text that appears on share pages, prompting the user to share. Character limit will be enforced on creation and update.
| automatic_traffic_routing (defaults to true) | boolean | A flag to let ShareProgress know whether to route share content A/B test traffic automatically via a multi-arm bandit algorithm, or whether traffic is even split across all variants until a winner is selected.
| custom_params | | Specifies an additional, channel-specific URL parameter to be included with the page link when shared, to allow outside systems to track where visitors are coming from - especially useful for logging actions. Only active if the prompt field is set
| prompt | | The name of the URL parameter that specifies the share channel from which the visitor are recruited, i.e. a prompt value of "source" would result in the inclusion of &source=facebook in the URL, if the visitor was coming from Facebook and the f field was set to "facebook"
| f | | Parameter value for visitors recruited from Facebook sharing
| e | | Parameter value for visitors recruited through email sharing
| t | | Parameter value for visitors recruited from Twitter sharing
| o | | Parameter value for visitors recruited from click-to-copy link sharing
| id_pass (pages only)|  | Allows a sharer identification parameter to be propagated through the URL of the shared link, allowing some CRMs to keep track of who referred new visitors to the website. Only active if the id field is set.
| id | | The name of the identification parameter that ShareProgress will look for in the Share Page URL.
| passed | | The name of the referrer parameter that ShareProgress will use for specifying the id value when users share page_url. E.g., if id is set to "my_id" and passed is set to "referred_by", then someone who visits a Share Page with the following URL: http://shpg.org/1/25?my_id=1234 would share links with the following additional parameter included: http://my_url.com?sp_ref=sp_stuff_goes_here&referred_by=1234

## Related Resources

* [VariantSet](LINK TO VARIANT_SET)


