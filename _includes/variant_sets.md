
#### VariantSet

A collection of the share content variants, grouped by sharing channel, which are currently facebook, twitter, and email. If more than one variant is included, a share content A/B test will be run between all specified variants. 

##### Fields

| Name | Type | Description
|------|------|-----------
| facebook | [FacebookVariant[]](#related-objects) | List of Facebook variants 
| twitter  | [TwitterVariant[]](#related-objects) | List of Twitter variants 
|email| [EmailVariant[]](#related-objects) | List of email variants 

##### Related Objects

##### FacebookVariant[]

Content for Facebook shares

##### Fields

|Name|Type|Description|
|---|---|---|
|id|string|Will cause the existing variant share content to be updated. If the variant lacks an id parameter, it will be used to generate a new share content variant.|
|\_destroy|boolean|If true, will delete the variant|
|facebook_title|string|The title of the post when the link is shared on Facebook|
|facebook_description|string|The description of the post when the link is shared on Facebook|
|facebook_thumbnail|string|URL for the thumbnail image of the post when the link is shared on Facebook|

##### TwitterVariant[]

Content for Twitter shares

##### Fields

|Name|Type|Description|
|---|---|---|
|id|string|Will cause the existing variant share content to be updated. If the variant lacks an id parameter, it will be used to generate a new share content variant.|
|\_destroy|boolean|If true, will delete the variant|
|twitter_message |string |The text of the post when the link is shared on Twitter. Must include the text "{LINK}"|

##### EmailVariant[]

Content for email shares

##### Fields

|Name|Type|Description|
|---|---|---|
|id|string|Will cause the existing variant share content to be updated. If the variant lacks an id parameter, it will be used to generate a new share content variant.|
|\_destroy|boolean|If true, will delete the variant|
|email_subject|string|The subject line of the email when the link is shared by email|
|email_body|string|The body of the message when the link is shared by email. Must include the text "{LINK}"|
