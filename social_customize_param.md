---
layout: default
title: CustomizeParams
---

# CustomizeParams

Specifies an additional, channel-specific URL parameter to be included with the page link when shared, to allow outside systems to track where visitors are coming from - especially useful for logging actions. Only active if the prompt field is set

| param | string | The name of the URL parameter that specifies the share channel from which the visitor are recruited, i.e. a prompt value of "source" would result in the inclusion of &source=facebook in the URL, if the visitor was coming from Facebook and the f field was set to "facebook"
| f | integer | Parameter value for visitors recruited from Facebook sharing
| e | integer | Parameter value for visitors recruited through email sharing
| t | integer | Parameter value for visitors recruited from Twitter sharing
| o | integer | Parameter value for visitors recruited from click-to-copy link sharing
