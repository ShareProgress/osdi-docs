
#### VariantSet
A collection of the share content variants, grouped by sharing channel, which are currently facebook, twitter, and email. If more than one variant is included, a share content A/B test will be run between all specified variants. 

##### Fields

| Name | Type | Description
|------|------|-----------
| facebook | [FacebookVariant](#related-objects) | Content for facebook sharing
| twitter  | [TwitterVariant](#related-objects) | Content for twitter sharing
|email| [EmailVariant](#related-objects) | Content for email sharing

##### Related Objects

{% include facebook_variants.md %}
{% include twitter_variants.md %}
{% include email_variants.md %}
