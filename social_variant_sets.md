---
layout: default
title: VariantSet
---


# VariantSet
An array of the share content variants, grouped by sharing channel, which are currently facebook, twitter, and email. If more than one variant is included, a share content A/B test will be run between all specified variants. Some things to keep in mind:


* Variants can optionally include an id parameter, which will cause the existing variant share content to be updated. Any variants lacking an id parameter will be used to generate a new share content variant.
* Variants passed the "\_destroy: true" parameter will be deleted.
* Each variant type has several field types, depending on the sharing channel,
and all text-fields have a character limit that will be enforced on creation
and update.
* Two fields, twitter_message and email_body, require the text “{LINK}” to be
included in the string, which will be enforced on creation and update.
* Additionally, the facebook_thumbnail parameter is advised to be greater than
200px x 200px, but this is not enforced.

| Name | Type | Description
|------|------|-----------
| facebook_title (limit 100 characters) | string | The title of the post when the link is shared on Facebook
| facebook_description (limit 260 characters) | string | The description of the post when the link is shared on Facebook
| facebook_thumbnail (advised to be larger than 200px x 200px - not enforced) | string | URL for the thumbnail image of the post when the link is shared on Facebook
| twitter_message (limit 140 characters, must include {LINK}) | string | The text of the post when the link is shared on Twitter. The {LINK} tag is counted as 22 characters, the standard length for a URL on Twitter.
| email_subject (limit 100 characters) | string | The subject line of the message when the link is shared by email
| email_body (limit 750 characters, must include {LINK} tag) | string | The body of the message when the link is shared by email. The {LINK} tag is counted as seven characters here.


