---
layout: default
title: Button
--- 

# Button

This document defines the Button resource.

Button resources represent share buttons that supporters can use to disseminate
content via their social media networks.

### Sections
* [Endpoints and URL structures](#endpoints-and-url-structures)
* [Fields](#fields)
    * [Related Objects](#related-objects)
* [Scenarios](#scenarios)
    * [Scenario: Retrieving a collection of buttons (GET)](
#scenario-retrieving-buttons)
    * [Scenario: Retrieving an individual button (GET)](
#scenario-retrieving-button)
    * [Scenario: Retrieving the analytics for a button (GET)](
#scenario-retrieving-analytics-button)
    * [Scenario: Creating a button with defaults (POST)](
#scenario-creating-button-basic)
    * [Scenario: Creating a button, specifying A/B tests and options (POST)](
#scenario-creating-button-advanced)
    * [Scenario: Modifying a page to add a new A/B variant (PUT)](
#scenario-modifying-page-add-variant)
    * [Scenario: Modifying a page to remove an A/B variant (PUT)](
#scenario-modifying-page-remove-variant)
    * [Scenario: Deleting a button (DELETE)](
#scenario-deleting-button)

{% include endpoints_and_url_structures.md %}

The link relation label for a Button resource
is ```osdi:button``` for a single Button resource
or ```osdi:buttons``` for a collection of Button resources.

_[Back to top...](#)_

## Fields


| Name          | Type      | Description
|-----------    |-----------|--------------
|key|string|Your API key|
| id (optional) | integer | The ID of the page to update. If omitted, will create a new page with the specified parameters.
| page_url (required) | string | URL of the page that the Share Page or Share Button will be sharing. The page of the URL will be scraped upon posting to read in meta data, which may optionally be used for variant content (see auto_fill for more information). If the page cannot be returned - due to a malformed URL or down server - it will return an error.
| wrapper_id (optional) | integer | The ID of the wrapper that should be assigned to the page - if blank will default to the organization’s default wrapper.
| page_title (optional) | string | The internal title of the Share Page or Share Button.  If not provided, will be scraped from the page_url.
| auto_fill (optional, defaults to true) | boolean | Specifies whether we should fill in any missing variant information with what we scrape from the page_url. If listed as false, variants will remain blank if not specified.
| button_template (required) | string | Share Buttons require one of the following templates to be rendered: sp_em_small, sp_em_large, sp_tw_small, sp_tw_large, sp_fb_small, sp_fb_large. See the create button page for a preview of how each of these look.
| variants (optional) | [VariantSet](social_variant_set.html) | An array of the share content variants, grouped by sharing channel, which are currently facebook, twitter, and email. If more than one variant is included in a channel, a share content A/B test will be run between all specified variants. 
| advanced_options (optional) | [SharingOptionsSet](social_sharing_options_set.html) | These are additional customizations for a Share Page or Share Buttons. If omitted, they will default to an organization’s default account settings.

### Related Objects
* [VariantSet](social_variant_set.html)
* [SharingOptionsSet](social_sharing_options_set.html)
