---
layout: default
title: SharePage
---
 
# SharePage

This document defines the SharePage resource.

SharePage resources represent share pages that supporters can use to disseminate
content via their social media networks.

### Sections
* [Endpoints and URL structures](#endpoints-and-url-structures)
* [Fields](#fields)
    * [Related Objects](#related-objects)
    * [Links](#links)
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
is ```osdi:share_page``` for a single Page resource
or ```osdi:share_pages``` for a collection of Page resources.

_[Back to top...](#)_

## Fields

| Name          | Type      | Description
|-----------    |-----------|--------------
| id | integer   | The ID of the page to update. If omitted, will create a new page with the specified parameters.
| page_url | string | URL of the page that the SharePage or ShareButton will be sharing. The page of the URL will be scraped upon posting to read in meta data, which may optionally be used for variant content (see auto_fill for more information). If the page cannot be returned - due to a malformed URL or down server - it will return an error.
| page_title | string | The internal title of the SharePage or ShareButton.  If not provided, will be scraped from the page_url.
| html_title | string | The HTML title of the SharePage. If not provided, will use page_title or be scraped from the page_url.
| auto_fill (defaults to true) | boolean | Specifies whether we should fill in any missing variant information with what we scrape from the page_url. If listed as false, variants will remain blank if not specified.
| variants | [VariantSet](#variantset) | An array of the share content variants
| advanced_options | [ShareOptionSet](#shareoptionset) | These are additional customizations for a SharePage or ShareButtons. If omitted, they will default to an organization’s default account settings.

### Related Objects

{% include variant_sets.md %}
{% include share_option_sets.md%}

### Links


{% include links_intro.md %}

|Name|Type|Description|
| wrapper | [PageWrapper](page_wrappers.html) | The wrapper that should be assigned to the page - if blank will default to the organization’s default wrapper.

## Related Resources

* [PageWrapper](page_wrappers.html)

