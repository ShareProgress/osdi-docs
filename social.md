Overview

The ShareProgress API will provide two interfaces -
one for traditional CRUD (create, read, update, delete) management of pages
and buttons via RESTful JSON application, and the other via JavaScript.

RESTful API
Organizations will be able to generate a unique API key that they will be able
to append to POST requests for authentication. A successful operation will -
in all cases - return a JSON object of the page that is being interacted with.

URL Endpoint and Encoding

Request content can be encoded as a form or as JSON

URL
https://run.shareprogress.org/api/version/object/method

PARAMETERS AS JSON ENCODED
{
    "key": "YOUR_KEY",
...
}
Parameters

Object: The class of object you’re operating on
Method: The method you’d like to invoke
Version: The API version number -
if not included, will default to the latest version of the API
Key: Your API key - accessible from https://run.shareprogress.org/account


Sample Response

{
    "success": true, // Boolean indicator
    "response": [...] // Will return all results in an array
    "message": [...] // If there’s an error will return an explanation here
}

Success: Indicates whether the operation was a success

Response: Will return all responses as an array - if requests are for singular
object, it will return response as the first element.

Rate Limit

The API is rate limited to 30 requests per minute. Requests are counted
progressively and are removed from the count after a minute - meaning you can
continuously make API requests if you stagger them every 2 seconds.

When you exceed your rate limit the API will return a 429 Header and a message
letting you know you’ve exceeded the rate limit.

The following http header values are returned with the API request to help
manage your application:

X-RateLimit-Limit - The number of requests allowed per minute

X-RateLimit-Remaining - The remaining number of requests available in the that
time window

X-RateLimit-Reset - The time when the count will begin to reset - keep in mind
it resets progressively


Overview
RESTful API
URL Endpoint and Encoding
Parameters
Sample Response
Rate Limit
PAGES AND BUTTONS
Fields
Methods
CREATE & UPDATE
Sample Request:
Simple Create New Page- autofilling variants from the page data
Create New Page - autofilling variants from the page data for unset variant
options
Edit Existing Page - Adding New Facebook Variant
Create New Page - With A/B Tests & Advanced Options
Create New Button - With A/B Tests & Advanced Options
Edit Page - Deleting A/B Variants from Email
Sample Response
Saving a Page
Saving a Button - using the Large Facebook (sp_fb_large) template
READ
sample request
sample response
ANALYZE
sample request
sample response
Page with A/B tests
Button with A/B tests
DESTROY
sample request
sample response
INDEX
sample request
Request first 10 pages
Request the next 10 pages after the first 10
sample response
Sample Page Request
Sample Button Request
WRAPPERS
CREATE & UPDATE
sample request
sample response
READ
sample request
sample response
DESTROY
sample request
sample response
INDEX
sample request
sample response
ACCOUNT INFO
READ
sample request
sample response
JavaScript API
Bind Share Event
Binding the Event
Security



PAGES AND BUTTONS
Object: page or button

Notes
Pages and Buttons have the following fields; some are specific to pages only
and some to buttons only. ShareProgress determines the difference between the
two depending on the object you specify in your URL endpoint.

The main difference is that buttons require a button_template field, which must
be one of the approved button templates listed below. Templates on this list
will never be removed, but additional ones will likely be added in the future.



Fields

id (optional) The ID of the page to update. If omitted, will create a new page
with the specified parameters.

page_url (required) URL of the page that the Share Page or Share Button will be
sharing. The page of the URL will be scraped upon posting to read in meta data,
which may optionally be used for variant content (see auto_fill for more
information). If the page cannot be returned - due to a malformed URL or down
server - it will return an error.

wrapper_id (optional) The ID of the wrapper that should be assigned to the
page - if blank will default to the organization’s default wrapper.

page_title (optional) The internal title of the Share Page or Share Button.
If not provided, will be scraped from the page_url.

html_title (optional, pages only) The HTML title of the Share Page. If not
provided, will use page_title or be scraped from the page_url.

auto_fill (optional, defaults to true) Specifies whether we should fill in any
missing variant information with what we scrape from the page_url. If listed as
false, variants will remain blank if not specified.

button_template (required, button only) Share Buttons require one of the
following templates to be rendered:
sp_em_small
sp_em_large
sp_tw_small
sp_tw_large
sp_fb_small
sp_fb_large
See the create button page for a preview of how each of these look


variants (optional) An array of the share content variants, grouped by sharing
channel, which are currently facebook, twitter, and email. If more than one
variant is included, a share content A/B test will be run between all specified
variants. Some things to keep in mind:

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


endpoint: /v1/pages/update or /v1/buttons/update
request type: POST

Sample Request:

Simple Create New Page- autofilling variants from the page data

{
    "key": "YOUR_API_KEY",
    "page_url": "http://your-page-url.com",
    "page_title": "The Page Title",
    "auto_fill" : true,
}

Create New Page - autofilling variants from the page data for unset variant
options

{
    "key": "YOUR_API_KEY",
    "page_url": "http://your-page-url.com",
    "auto_fill" : true,
    "variants" : {
        "facebook": [
            {
                "facebook_title": "Alternative Facebook Post Title",
                "facebook_description": "Alternative Facebook Post Description",
            },
            {
                "facebook_title": "Other Facebook Post Title",
            }
        ]
    }
}

Edit Existing Page - Adding New Facebook Variant
{
    "id" : 10,
    "key": "YOUR_API_KEY",
    "variants" : {
        "facebook": [
            {
                "facebook_title": "Facebook Post Title",
                "facebook_description": "Facebook Post Description",
                "facebook_thumbnail": "http://direct-link-to-image.png...",
                "id": 1
            },
            {
                "facebook_title": "Alternate Facebook Post Title",
                "facebook_description": "Facebook Post Description",
                "facebook_thumbnail": "http://direct-link-to-image.png..."
            }
        ],
        "email": [
            {
                "email_subject": "Your Email Subject...",
                "email_body": "Your Email Body - make sure to include {LINK}",
                "id": 5
            }
        ],
        "twitter": [
            {
                "twitter_message": "Your tweet - include a {LINK}",
                "id": 6
            }
        ]
    }
}

Create New Page - With A/B Tests & Advanced Options
{
    "key": "YOUR_API_KEY",
    "page_url": "http://your-page-url.com",
    "page_title": "The Page Title",
    "auto_fill" : true,
    "variants" : {
        "facebook": [
            {
                "facebook_title": "Facebook Post Title",
                "facebook_description": "Facebook Post Description",
                "facebook_thumbnail": "http://direct-link-to-image.png...",
            }
        ],
        "email": [
            {
                "email_subject": "Your Email Subject...",
                "email_body": "Your Email Body - make sure to include {LINK}",
            },
            {
                "email_subject": "Alternate Email Subject...",
                "email_body": "Your Email Body - make sure to include {LINK}"
            }
        ],
        "twitter": [
            {
                "twitter_message": "Your tweet - include a {LINK}",
            }
        ]
    },
    "advanced_options": {
        "prompt": "Share with your friends!",
        "automatic_traffic_routing": true,
        "customize_params": {
            "param": "param_to_use",
            "e": "email_source",
            "f": "facebook_source",
            "t": "twitter_source",
            "o", "dark_social_source"
        },
        "id_pass": {
            "id": "track_id",
            "passed": "referrer_id"
        }
    }
}

Create New Button - With A/B Tests & Advanced Options
{
    "key": "YOUR_API_KEY",
    "page_url": "http://your-page-url.com",
    "page_title": "The Page Title",
    "button_template": "sp_em_large"
    "auto_fill" : true,
    "variants" : {
        "email": [
            {
                "email_subject": "Your Email Subject...",
                "email_body": "Your Email Body - make sure to include {LINK}",
            },
            {
                "email_subject": "Your Email Subject...",
                "email_body": "Your Email Body - make sure to include {LINK}"
            }
        ]
    },
    "advanced_options": {
        "automatic_traffic_routing": true,
        "buttons_optimize_actions": true,
        "customize_params": {
            "param": "param_to_use",
            "e": "email_source",
            "f": "facebook_source",
            "t": "twitter_source",
            "o", "dark_social_source"
        }
    }
}

Edit Page - Deleting A/B Variants from Email
{
    "key": "YOUR_API_KEY",
    "page_url": "http://your-page-url.com",
    "page_title": "The Page Title",
    "button_template": "sp_em_large"
    "auto_fill" : true,
    "variants" : {
        "facebook": [
            {
                "facebook_title": "Facebook Post Title",
                "facebook_description": "Facebook Post Description",
                "facebook_thumbnail": "http://direct-link-to-image.png...",
                "id":1
            }
        ]
        "email": [
            {
                "email_subject": "Your Email Subject...",
                "email_body": "Your Email Body - make sure to include {LINK}",
            },
            {
                "email_subject": "Your Email Subject...",
                "email_body": "Your Email Body - make sure to include {LINK}"
                "id" : 5,
                "_destroy" : true
            },
            {
                "email_subject": "Your Email Subject...",
                "email_body": "Your Email Body - make sure to include {LINK}"
                "id" : 6,
                "_destroy" : true
            }
        ],
        "twitter": [
            {
                "twitter_message": "Your tweet - include a {LINK}",
                "id": 6
            }
        ]
    }
}



Sample Response

Notes
The following information is returned after a successful create/update call:


found_snippet Indicates whether we found the ShareProgress code snippet on
the specified share page - snippets are required to track viral visitors and
viral actions.

share_page_url The URL of the created/updated Share Page - will use a custom
domain or subdomain if one has been specified for your organization.

share_button_html The HTML tag to render the created/updated Share Button.

variants the variants and their ids, important as if you want to update these
later you’ll need to include the id

Saving a Page
{
    "success":true,
    "response": [
        {
            "id":10,
            "page_url": "http://your-page-url.com",
            "wrapper_id": 30,
            "found_snippet":true,
            "share_page_url": "http://shpg.org/1/10",
            "variants" :
                "facebook": [
                    {
                        "facebook_title": "Facebook Post Title",
                        "facebook_description": "Facebook Post Description",
                        "facebook_thumbnail": "http://direct-link-to-image.png...",
                        "id":1
                    }
                ]
                "email": [
                    {
                        "email_subject": "Your Email Subject...",
                        "email_body": "Your Email Body {LINK}",
                    },
                    {
                        "email_subject": "Your Email Subject...",
                        "email_body": "Your Email Body {LINK}"
                        "id" : 5,
                    },
                    {
                        "email_subject": "Your Email Subject...",
                        "email_body": "Your Email Body {LINK}"
                        "id" : 6,
                    }
                ],
                "twitter": [
                    {
                        "twitter_message": "Your tweet - include a {LINK}",
                        "id": 6
                    }
                ]
            },
            "advanced_options": {
                "prompt": "Your action has been submitted....",
                "automatic_traffic_routing": true,
            }
        }
    ]
}

Saving a Button - using the Large Facebook (sp_fb_large) template
{
    "success":true,
    "response": [
        {
            "id": 10,
            "page_url": "http://your-page-url.com",
"wrapper_id": 50,
            "found_snippet":true,
            "share_button_html": "<div class='sp_10 sp_fb_large' ></div>",
            "variants" : {
                "facebook": [
                    {
                        "facebook_title": "Facebook Post Title",
                        "facebook_description": "Facebook Post Description",
                        "facebook_thumbnail": "http://direct-link-to-image.png...",
                        "id":1
                    },
                    {
                        "facebook_title": "Facebook Post Title",
                        "facebook_description": "Facebook Post Description",
                        "facebook_thumbnail": "http://direct-link-to-image.png...",
                        "id":3
                    },
                    {
                        "facebook_title": "Facebook Post Title",
                        "facebook_description": "Facebook Post Description",
                        "facebook_thumbnail": "http://direct-link-to-image.png...",
                        "id":10
                    }
                ]
        },
            "advanced_options": {
                "prompt": "Your action has been submitted....",
                "automatic_traffic_routing": true,
            }
        }
    ]
}





READ
Will return information on the specified Share Page or Share Button (URL,
variants, etc).

endpoint  /v1/pages/read or /v1/buttons/read
request type POST, GET

sample request

{
    "id" : 10,
    "key": "YOUR_API_KEY",

}

sample response

Notes
The following information is returned after a successful read call:

is_active Specifies whether you are are running a share content A/B test (e.g.
two or more variants for the same share channel) and whether there have been
any visitors.

advanced_options Whatever advanced options are set for the Share Page or
Share Button. If you have not set custom advanced options for the page or
button, READ will return the default values for the organization.

Page with no A/B tests & default advanced options
{
    "success": true
    "response" : [
        {
            "id" : 10
            "page_url": "http://your-page-url.com",
            "page_title": "The Page Title",
"wrapper_id": 30,
            "found_snippet" : true,
            "is_active" : false,
            "variants" : {
                "facebook": [
                    {
                        "facebook_title": "Facebook Link Title",
                        "facebook_description": "Facebook Link..",
                        "facebook_thumbnail": "http://diremage.png...",
                        "id":1
                    }
                ],
                "email": [
                    {
                        "email_subject": "Your Email Subject...",
                        "email_body": "Your Email Body include {LINK}",
                        "id": 5
                    }
                ],
                "twitter": [
                    {
                        "twitter_message": "Tweet, include a {LINK}",
                        "id":6
                    }
                ]
            },
            "advanced_options": {
                "prompt": "Your action has been submitted....",
                "automatic_traffic_routing": true,
            }
        }
    ]
}

Page with A/B tests & advanced options
{
    "success": true
    "response" : [
        {
            "id" : 10
            "page_url": "http://your-page-url.com",
            "share_page_url": "http://shpg.org/1/10",
            "page_title": "The Page Title",
            "wrapper_id": 30,
            "is_active" : true,
            "variants" : {
                "facebook": [
                    {
                        "facebook_title": "Facebook Link Title",
                        "facebook_description": "Facebook Link..",
                        "facebook_thumbnail": "http://diremage.png...",
                        "id":1
                    },
                    {
                        "facebook_title": "Alternate Facebook ...",
                        "facebook_description": "Facebook Link...",
                        "facebook_thumbnail": "http://direct-le.png...",
                        "id":2,
                    }
                ],
                "email": [
                    {
                        "email_subject": "Your Email Subject...",
                        "email_body": "Your Email Body include {LINK}",
                        "id": 5
                    },
                    {
                        "email_subject": "Alternate Email Subject...",
                        "email_body": "Your Email Body include {LINK}",
                        "id": 13
                    },
                    {
                        "email_subject": "Alternate Email Subject...",
                        "email_body": "Your Email Body include {LINK}",
                        "id": 30
                    }
                ],
                "twitter": [
                    {
                        "twitter_message": "Tweet, include a {LINK}",
                        "id":6
                    }
                ]
            },
            "advanced_options": {
                "prompt": "Your action has been submitted....",
                "automatic_traffic_routing": true,
                "customize_params": {
                    "param": "param_to_use",
                    "e": "email_source",
                    "f": "facebook_source",
                    "t": "twitter_source",
                    "o", "dark_social_source"
                },
                "id_pass": {
                    "id": "track_id",
                    "passed": "referred_id"
                }
            }
        }
    ]
}

Button with A/B tests & advanced options
{
    "success": true
    "response" : [
        {
            "id" : 10
            "page_url": "http://your-page-url.com",
            "page_title": "The Page Title",
            "share_button_html": "<div class='sp_10 sp_tw_large' ></div>",
            "found_snippet" : true,
            "is_active" : true,
            "variants" : {
                "twitter": [
                    {
                        "twitter_message": "Tweet 1, include a {LINK}",
                        "id":6
                    },
                    {
                        "twitter_message": "Tweet 2, include a {LINK}",
                        "id":7
                    },
                    {
                        "twitter_message": "Tweet 3, include a {LINK}",
                        "id":8
                    },
                    {
                        "twitter_message": "Tweet, include a {LINK}",
                        "id":10
                    }
                ]
            },
            "advanced_options": {
                "automatic_traffic_routing": true,
                "customize_params": {
                    "param": "param_to_use",
                    "e": "email_source",
                    "f": "facebook_source",
                    "t": "twitter_source",
                    "o", "dark_social_source"
                }
            }
        }
    ]
}


ANALYZE
This method will return analytics from the specified Share Page or Share
Button - including a timestamp of when analytics were last updated.

endpoint  /v1/pages/analytics  or /v1/buttons/analytics
request type POST, GET

sample request

{
    "id" : 10,
    "key": "YOUR_API_KEY",
}

sample response

Notes
This will return an object that closely resembles a ShareProgress analytics
pages. Updated results are generated at most every five minutes. One major
difference between Share Pages and Share Buttons are that pages also track
viral actions, a count of how many people visited the shared URL and the
Share Page - meaning they completed the given action.

generations Breakdown of the number of visits and shares per social generation

share_types Breakdown of the number of visits, shares, and viral visits by
sharing channel. “Dark social” specifies sharing via the click-to-copy button.

share_tests Results for all share content A/B tests. This will only return
results for a specific sharing channel if there are more than one share
content variant of that type.

total A top-line breakdown of the number of visits, shares, viral visits, and
viral actions for the Share Page or Share Button. Viral actions are only
included for Share Pages.

Page with A/B tests
{
    "success" : true,
    "response" : [
        {
            "id": 10
"generations": [
                {
                    "shares": 7217,
                    "visits": 39964,
                    "generation": 1
                },
                {
                    "shares": 462,
                    "visits": 1432,
                    "generation": 2
                },
                {
                    "shares": 41,
                    "visits": 104,
                    "generation": 3
                },
                {
                    "shares": 1,
                    "visits": 8,
                    "generation": 4
                }
            ],
            "share_types": {
                "email": {
                    "shares": 2100,
                    "viral_visits": 2001,
                    "viral_actions": 840
                },
                "facebook": {
                    "shares": 5087,
                    "viral_visits": 4171,
                    "viral_actions": 622
                },
                "twitter": {
                    "shares": 363,
                    "viral_visits": 150,
                    "viral_actions": 36
                },
                "dark_social": {
                    "shares": 177,
                    "viral_visits": 175,
                    "viral_actions": 46
                }
            },
            "share_tests": {
                "email": [
                    {
                        "shares": 676,
                        "successful_shares": 168,
                        "conversion": 24.9,
                        "ci": 3.3,
                        "confidence": "--",
                        "improvement": "--",
                        "winner": true,
                        "id": 908,
                        "weight": "0.0%"
                    },
                    {
                        "shares": 711,
                        "successful_shares": 171,
                        "conversion": 24.1,
                        "ci": 3.1,
                        "confidence": "36.4%",
                        "improvement": "-3.2%",
                        "winner": false,
                        "id": 909,
                        "weight": "0.0%"
                    }
                ],
                "facebook": [
                    {
                        "shares": 1804,
                        "successful_shares": 148,
                        "conversion": 8.2,
                        "ci": 1.3,
                        "confidence": "--",
                        "improvement": "--",
                        "winner": false,
                        "id": 910,
                        "weight": "0.0%"
                    },
                    {
                        "shares": 1791,
                        "successful_shares": 203,
                        "conversion": 11.3,
                        "ci": 1.5,
                        "confidence": "99.9%",
                        "improvement": "38.2%",
                        "winner": true,
                        "id": 911,
                        "weight": "0.0%"
                    }
                ],
                "twitter": [
                    {
                        "shares": 126,
                        "successful_shares": 6,
                        "conversion": 4.8,
                        "ci": 3.7,
                        "confidence": "--",
                        "improvement": "--",
                        "winner": true,
                        "id": 912,
                        "weight": "0.0%"
                    },
                    {
                        "shares": 122,
                        "successful_shares": 3,
                        "conversion": 2.5,
                        "ci": 2.8,
                        "confidence": "16.6%",
                        "improvement": "-48.4%",
                        "winner": false,
                        "id": 913,
                        "weight": "0.0%"
                    }
                ]
            },
            "total": {
                "total_visitors": "41478",
                "total_shares": 7721,
                "total_viral_visitors": 6497,
                "total_viral_actions": 1544
            }
        }
    ]
}
Button with A/B tests
{
    "success" : true,
    "response" : [
        {
            "id" : 30
            "generations": [
                {
                    "shares": 3108,
                    "visits": 7685,
                    "generation": 1
                },
                {
                    "shares": 215,
                    "visits": 419,
                    "generation": 2
                },
                {
                    "shares": 4,
                    "visits": 19,
                    "generation": 3
                }
            ],
            "share_types": {
                "email": {
                    "shares": 810,
                    "viral_visits": 207
                },
                "facebook": {
                    "shares": 2276,
                    "viral_visits": 259
                },
                "twitter": {
                    "shares": 142,
                    "viral_visits": 13
                },
                "dark_social": {
                    "shares": 99,
                    "viral_visits": 20
                }
            },
            "share_tests": {
                "facebook": [
                    {
                        "shares": 676,
                        "successful_shares": 168,
                        "conversion": 24.9,
                        "ci": 3.3,
                        "confidence": "--",
                        "improvement": "--",
                        "winner": false,
                        "id": 803,
                        "weight": "53.6%"
                    },
                    {
                        "shares": 711,
                        "successful_shares": 171,
                        "conversion": 24.1,
                        "ci": 3.1,
                        "confidence": "36.4%",
                        "improvement": "-3.2%",
                        "winner": false,
                        "id": 816,
                        "weight": "46.4%"
                    }
                ]
            },
            "total": {
                "Total_visitors": "8123",
                "Total_shares": 3327,
                "Total_viral_visitors": 499
            }
        }
    ]
}

DESTROY
This call deletes the specified Share Page or Share Buttons.

endpoint  /v1/pages/delete  or /v1/buttons/delete
request type POST

sample request

{
    "id" : 10,
    "key": "YOUR_API_KEY",
}

sample response

{
    "success":true,
    "response": [
        {
            "id": 10
        }
    ]
}

INDEX
Lists all Share Pages and Share Buttons - each organized into a separate array.
API user can specify the limit, offset, and a search parameter for the
title / URL.

endpoint  /v1/pages  or /v1/buttons
request type POST, GET

sample request

Notes
Be default, will return the first 50 pages. Can specify both a limit and
offset in the request.

Request first 10 pages
{
    "key": "YOUR_API_KEY",
    "limit": "10",
}
Request the next 10 pages after the first 10
{
    "key": "YOUR_API_KEY",
    "offset": "10",
    "limit": "10",
}

sample response

Notes
Will return the id, page_url, page_title, share_page_url / share_button_html,
and whether the Share Page or Share Buttons are actively running an experiment.

Sample Page Request
{
    "success":true,
    "response": [
        {
            "id": 10
            "page_url":"http://this-page.com",
            "page_title":"My great title",
            "share_page_url":"http://shpg.org/1/12",
            "is_active": true,
        },
        {
            "id": 11
            "page_url":"http://this-other-page.com",
            "page_title":"My other title",
            "share_page_url":"http://shpg.org/1/11",
            "is_active": false,
        }

    ]
}

Sample Button Request
{
    "success":true,
    "response": [
        {
            "id": 10
            "page_url":"http://this-page.com",
            "page_title":"My great title",
            "button_template":"sp_tw_small",
            "share_button_html": "<div class='sp_10 sp_tw_small' ></div>",
            "is_active": true,
        },
        {
            "id": 11
            "page_url":"http://this-other-page.com",
            "page_title":"My other title",
            "share_page_url":"http://shpg.org/1/11",
            "button_template":"sp_fb_large",
            "share_button_html": "<div class='sp_10 sp_fb_large' ></div>",
            "is_active": false,
        }

    ]
}
WRAPPERS
CREATE & UPDATE

endpoint  /v1/wrappers/update
request type POST

Notes
Creates or updates a wrapper - validates presence of the {SHAREACTION} in the
HTML block.
Default (optional) If defined as true - will override the current default
wrapper.

sample request
{
"id": 48,
    "name": "Default Wrapper",
    "default": false,
    "html": "<!doctype html>\r\n<html lang=\"en\">\r\n<head>\r\n\r\n  <meta charset=\"utf-8\">\r\n\r\n  <title>PAGE_TITLE</title> <!-- this will be replaced automatically -->\r\n\r\n  <meta http-equiv=\"X-UA-Compatible\" content=\"IE=edge;chrome=1\">\r\n  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1, maximum-scale=1\">\r\n  \r\n  <link href=\"/basic.css\" media=\"all\" rel=\"stylesheet\" type=\"text/css\" />\r\n</head>\r\n\r\n<body>\r\n  <iframe src=\"http://localhost:3000\"></iframe>\r\n\r\n  <div id=\"header\">\r\n    <div id=\"header_content\">\r\n      <h1>new org</h1>\r\n    </div> <!-- #header_content -->\r\n  </div> <!-- #header -->\r\n\r\n  <div class=\"content\">\r\n  {ShareAction}\r\n  </div> <!-- .content -->\r\n\r\n  <div id=\"footer\">\r\n    <div id=\"footer_content\">\r\n      Page Disclaimer\r\n    </div> <!-- #footer_content -->\r\n  </div> <!-- #footer -->\r\n\r\n</body>\r\n</html>\r\n",
        }
    ]
}

sample response
{
    "success": true
    "response": [
        {
            "id": 48,
            "name": "Default Wrapper"
        }
    ]
}

READ

endpoint  /v1/wrappers/read
request type POST, GET

sample request
{
    "id" : 10,
    "key": "YOUR_API_KEY",
}

sample response
{
    "success":true,
    "response": [
        {
            "id": 10,
"name": "Default Wrapper",
"default": true,
    "html": "<!doctype html>\r\n<html lang=\"en\">\r\n<head>\r\n\r\n  <meta charset=\"utf-8\">\r\n\r\n  <title>PAGE_TITLE</title> <!-- this will be replaced automatically -->\r\n\r\n  <meta http-equiv=\"X-UA-Compatible\" content=\"IE=edge;chrome=1\">\r\n  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1, maximum-scale=1\">\r\n  \r\n  <link href=\"/basic.css\" media=\"all\" rel=\"stylesheet\" type=\"text/css\" />\r\n</head>\r\n\r\n<body>\r\n  <iframe src=\"http://localhost:3000\"></iframe>\r\n\r\n  <div id=\"header\">\r\n    <div id=\"header_content\">\r\n      <h1>new org</h1>\r\n    </div> <!-- #header_content -->\r\n  </div> <!-- #header -->\r\n\r\n  <div class=\"content\">\r\n  {ShareAction}\r\n  </div> <!-- .content -->\r\n\r\n  <div id=\"footer\">\r\n    <div id=\"footer_content\">\r\n      Page Disclaimer\r\n    </div> <!-- #footer_content -->\r\n  </div> <!-- #footer -->\r\n\r\n</body>\r\n</html>\r\n",
        }
    ]
}


DESTROY

endpoint  /v1/wrappers/delete
request type POST, GET

sample request
{
    "id" : 10,
    "key": "YOUR_API_KEY",
}

sample response
{
    "success":true,
    "response": [
        {
            "id": 10
        }
    ]
}

INDEX

endpoint  /v1/wrappers
request type POST, GET


sample request

{
    "key": "YOUR_API_KEY",
}

sample response
{
    "success":true,
    "response": [
        {
            "id": 10,
            "name": "Default Wrapper",
            "default": false
        },
        {
            "id": 40,
            "name": "Christmas Present Wrapper",
            "default": false

        },
        {
            "id": 13,
            "name": "Freestyle Wrapper",
            "default": false

        },
        {
            "id": 20,
            "name": "Other Wrapper",
            "default": true

        }
    ]
}

ACCOUNT INFO
READ
Returns an organization’s billing cycle, share budget, shares that cycle, and
plan.

endpoint  /v1/account
request type POST, GET


sample request

{
    "key": "YOUR_API_KEY",
}

sample response
{
    "success":true,
    "response": [
        {
            "account_name": "My Organization",
            "billing_start": "2013-02-28T23:14:27+00:00",
            "billing_end": "2013-03-28T23:14:27+00:00",
            "shares_this_cycle": 50,
            "share_budget": 1250,
            "plan": "basic",
            "monthly_cost": "50"
        }
    ]
}

JavaScript API

The JavaScript API will provide functionality to associate events with user
behavior on the Share Page or on pages with Share Buttons:

Bind Share Event
We will call share events on the window when a share clicked on share pages
or on a share button - passing share type (e.g., email, Facebook), the
clicked object, visit ID, and share language variant to the specified function.

Event Data Additional data will be appended onto the event object - giving
more information about various details about the event - including:

share type The share type of the event: Facebook, Twitter, email, other

share object The DOM object where the share took place

visit_id The ID assigned to this visitor

variant_id The ID of the variant assigned to this visitor

Binding the Event
// Plain Javascript for IE 8+
window.addEventListener('share',function(event) {

    var share_data = event.share,
        share_type = share_data.share_type,
        share_object = share_data.share_object,
        visit_id = share_data.visit_id,
        variant_id = share_data.variant_id

    //... do something with all this stuff here
})


// jQuery
jQuery(window).bind('share',function(event){

    // With jQuery you'll need to reference the Original Event object
    var share_data = event.originalEvent.share,
        share_type = share_data.share_type,
        share_object = share_data.share_object,
        visit_id = share_data.visit_id
        variant_id = share_data.variant_id,
        variant = share_data.variant

    //... do something with all this stuff here
})





Security

The RESTful API should be very straightforward - orgs will be able to view
and generate (or regenerate) an API key.

For JavaScript, no back-end access with be exposed in the current version of
the API, so there will not be any security risks involved.
