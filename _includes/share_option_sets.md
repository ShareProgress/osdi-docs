### ShareOptionSet

These are additional customizations for a SharePage or ShareButtons. If omitted, they will default to an organization’s default account settings.

| Name | Type | Description
|------|------|-----------
| prompt | string | A small block of text that appears on share pages, prompting the user to share. 
| automatic_traffic_routing (defaults to true) | boolean | A flag to let the application know whether to route share content A/B test traffic automatically via a multi-arm bandit algorithm, or whether traffic is even split across all variants until a winner is selected.
| customize_param | [ShareChannelParameter](#sharechannelparameter) |  Specifies an additional, channel-specific URL parameter to be included with the page link when shared, to allow outside systems to track where visitors are coming from - especially useful for logging actions. Only active if the prompt field is set
| id_pass (pages only)| boolean  | Allows a sharer identification parameter to be propagated through the URL of the shared link, allowing some CRMs to keep track of who referred new visitors to the website. Only active if the id field is set.
| id | string | The name of the identification parameter that the application will look for in the SharePage URL.
| passed | string | The name of the referrer parameter that the application will use for specifying the id value when users share page_url. E.g., if id is set to "my_id" and passed is set to "referred_by", then someone who visits a SharePage with the following URL: http://shpg.org/1/25?my_id=1234 would share links with the following additional parameter included: http://my_url.com?sp_ref=sp_stuff_goes_here&referred_by=1234

#### Related Objects

##### ShareChannelParameter

Specifies an additional, channel-specific URL parameter to be included with the page link when sharedi. This allows outside systems (e.g., CRM systems) to track where visitors are coming from.  Especially useful for logging actions. Only active if the prompt field is set

Example: When using ActionKit, setting "param" to "source" and "f" to "sp_facebook" will log that the action taker came from a facebook share.

| Name | Type | Description
|------|------|-----------
| param | string | The name of the URL parameter that specifies the share channel from which the visitor are recruited, i.e. a prompt value of "source" would result in the inclusion of &source=facebook in the URL, if the visitor was coming from Facebook and the f field was set to "facebook"
| f | string | Parameter value for visitors recruited from Facebook sharing
| e | string | Parameter value for visitors recruited through email sharing
| t | string | Parameter value for visitors recruited from Twitter sharing
| o | string | Parameter value for visitors recruited from click-to-copy link sharing
