
#### VariantSet
An collection of the share content variants, grouped by sharing channel, which are currently facebook, twitter, and email. If more than one variant is included, a share content A/B test will be run between all specified variants. Some things to keep in mind:


* Variants can optionally include an id parameter, which will cause the existing variant share content to be updated. Any variants lacking an id parameter will be used to generate a new share content variant.
* Variants passed the "\_destroy: true" parameter will be deleted.
* Each variant type has several field types, depending on the sharing channel,
and all text-fields have a character limit that will be enforced on creation
and update.
* Two fields, twitter_message and email_body, require the text “{LINK}” to be
included in the string, which will be enforced on creation and update.
* Additionally, the facebook_thumbnail parameter is advised to be greater than
200px x 200px, but this is not enforced.

##### Fields

| Name | Type | Description
|------|------|-----------
| facebook | [facebook[]](#related-objects) | Content for facebook sharing
| twitter  | [twitter[]](#related-objects) | Content for twitter sharing
|email| [email[]](#related-objects) | Content for email sharing

##### Related Objects

{% include facebooks.md %}
{% include twitters.md %}
{% include emails.md %}
