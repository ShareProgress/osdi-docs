##### EmailVariant

Content for email shares

##### Fields

|Name|Type|Description|
|---|---|---|
|id|string|Will cause the existing variant share content to be updated. If the variant lacks an id parameter, it will be used to generate a new share content variant.|
|\_destroy|boolean|If true, will delete the variant|
|email_subject|string|The subject line of the email when the link is shared by email|
|email_body|string|The body of the message when the link is shared by email. Must include the text "{LINK}"|
