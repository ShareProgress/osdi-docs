---
layout: default
title: AdvancedOption
---

# AdvancedOptions

These are additional customizations for a Share Page or Share Buttons. If omitted, they will default to an organization’s default account settings.

| prompt (limit 120 characters) | string | A small block of text that appears on share pages, prompting the user to share. Character limit will be enforced on creation and update.
| automatic_traffic_routing (defaults to true) | boolean | A flag to let ShareProgress know whether to route share content A/B test traffic automatically via a multi-arm bandit algorithm, or whether traffic is even split across all variants until a winner is selected.
| customize_param | [CustomizeParam](customize-param.html) |  Specifies an additional, channel-specific URL parameter to be included with the page link when shared, to allow outside systems to track where visitors are coming from - especially useful for logging actions. Only active if the prompt field is set
| id_pass (pages only)| boolean  | Allows a sharer identification parameter to be propagated through the URL of the shared link, allowing some CRMs to keep track of who referred new visitors to the website. Only active if the id field is set.
| id | string | The name of the identification parameter that ShareProgress will look for in the Share Page URL.
| passed | string | The name of the referrer parameter that ShareProgress will use for specifying the id value when users share page_url. E.g., if id is set to "my_id" and passed is set to "referred_by", then someone who visits a Share Page with the following URL: http://shpg.org/1/25?my_id=1234 would share links with the following additional parameter included: http://my_url.com?sp_ref=sp_stuff_goes_here&referred_by=1234

## Related Resources

* [CustomizeParam](customize-param.html)
