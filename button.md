---
layout: default
title: Button 
# Button

This document defines the Button resource.

Button resources represent share buttons that supporters can use to disseminate
content via their social media networks.

### Sections
* [Endpoints and URL structures](#endpoints-and-url-structures)
* [Fields](#fields)
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
is <code>osdi:button</code> for a single Button resource
or <code>osdi:buttons</code> for a collection of Button resources.

_[Back to top...](#)_

## Fields

| Name          | Type      | Description
|-----------    |-----------|--------------
| id (optional) | integer | The ID of the page to update. If omitted, will create a new page with the specified parameters.
| page_url (required) | string | URL of the page that the Share Page or Share Button will be sharing. The page of the URL will be scraped upon posting to read in meta data, which may optionally be used for variant content (see auto_fill for more information). If the page cannot be returned - due to a malformed URL or down server - it will return an error.
| wrapper_id (optional) | integer | The ID of the wrapper that should be assigned to the page - if blank will default to the organization’s default wrapper.
| page_title (optional) | string | The internal title of the Share Page or Share Button.  If not provided, will be scraped from the page_url.
| auto_fill (optional, defaults to true) | boolean | Specifies whether we should fill in any missing variant information with what we scrape from the page_url. If listed as false, variants will remain blank if not specified.
| button_template (required) | string | Share Buttons require one of the following templates to be rendered: sp_em_small sp_em_large sp_tw_small sp_tw_large sp_fb_small sp_fb_large See the create button page for a preview of how each of these look
| variants (optional) | array of variants | An array of the share content variants, grouped by sharing channel, which are currently facebook, twitter, and email. If more than one variant is included, a share content A/B test will be run between all specified variants. Some things to keep in mind:

Variants can optionally include an id parameter, which will cause the
existing variant share content to be updated. Any variants lacking an id
parameter will be used to generate a new share content variant.
Variants passed the "_destroy": true parameter will be deleted.
Each variant type has several field types, depending on the sharing channel,
and all text-fields have a character limit that will be enforced on creation
and update.
Two fields, twitter_message and email_body require the text “{LINK}” to be
included in the string, which will be enforced on creation and update.
Additionally, the facebook_thumbnail parameter is advised to be greater than
200px x 200px, but this is not enforced.

facebook
facebook_title (limit 100 characters) The title of the post when the link is
shared on Facebook

facebook_description (limit 260 characters) The description of the post when
the link is shared on Facebook

facebook_thumbnail (advised to be larger than 200px x 200px - not enforced)
URL for the thumbnail image of the post when the link is shared on Facebook

twitter
twitter_message (limit 140 characters, must include {LINK}) The text of the
post when the link is shared on Twitter. The {LINK} tag is counted as 22
characters, the standard length for a URL on Twitter.

email
email_subject (limit 100 characters) The subject line of the message when the
link is shared by email

email_body (limit 750 characters, must include {LINK} tag) The body of the
message when the link is shared by email. The {LINK} tag is counted as seven
characters here.

advanced_options (optional) These are additional customizations for a Share
Page or Share Buttons. If omitted, they will default to an organization’s
default account settings.

prompt (page only, limit 120 characters) A small block of text that appears
on share pages, prompting the user to share. Character limit will be enforced
on creation and update.

automatic_traffic_routing (defaults to true) A flag to let ShareProgress know
whether to route share content A/B test traffic automatically via a multi-arm
bandit algorithm, or whether traffic is even split across all variants until
a winner is selected.

buttons_optimize_actions (button only, defaults to false) A flag to let
ShareProgress know whether to optimize for viral actions as opposed to viral
clicks when running A/B tests with share buttons. Viral actions are tracked
via a conversion tag of the form: <div class='sp_ID sp_conversion'></div>

custom_params Specifies an additional, channel-specific URL parameter to be
included with the page link when shared, to allow outside systems to track
where visitors are coming from - especially useful for logging actions. Only
active if the prompt field is set

prompt The name of the URL parameter that specifies the share channel from
which the visitor are recruited, i.e. a prompt value of "source" would result
in the inclusion of &source=facebook in the URL, if the visitor was coming
from Facebook and the f field was set to "facebook"

f Parameter value for visitors recruited from Facebook sharing
e Parameter value for visitors recruited through email sharing
t Parameter value for visitors recruited from Twitter sharing
o Parameter value for visitors recruited from click-to-copy link sharing

id_pass (pages only) Allows a sharer identification parameter to be
propagated through the URL of the shared link, allowing some CRMs to keep
track of who referred new visitors to the website. Only active if the id
field is set.

id The name of the identification parameter that ShareProgress will look for
in the Share Page URL.

passed The name of the referrer parameter that ShareProgress will use for
specifying the id value when users share page_url.

E.g., if id is set to "my_id" and passed is set to "referred_by", then
someone who visits a Share Page with the following URL:

http://shpg.org/1/25?my_id=1234

would share links with the following additional parameter included:

http://my_url.com?sp_ref=sp_stuff_goes_here&referred_by=1234

Methods
CREATE & UPDATE

Notes
API users will be able to create or updated Share Pages and Share Buttons by
specifying the URL of the page to be shared and, optionally, the Share Page /
Share Button title. The request will auto-generate the share content variants
from a scrape of the provided URL. API users can optionally pass an array of
share content variants to override the content generated from URL scraping and,
if multiple variants are included, set up share content A/B tests.


