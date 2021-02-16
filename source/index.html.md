---
title: lemlist Developer Documentation

toc_footers:
  - <a href='https://lemlist.com'>lemlist Homepage</a>
  - <a href='http://help.lemlist.com'>lemlist Faq</a>
  - <a href='https://github.com/peernohell/lemlist-developer/blob/master/source/index.html.md'>Report an issue in this doc</a>

includes:
  - team
  - campaigns
  - leads
  - activities
  - unsubscribes
  - hooks
  - errors

search: true
---

# Introduction

Welcome to the lemlist Developer Documentation.

lemlist is very customizable and open. You'll find on this page all the API and integration you can do with lemlist.

# Rate Limit

lemlist's API rate limits requests in order to prevent abuse and overload of our services.  
Rate limits are applied on all routes and per-account performing the request.  
The rate limits are **20** requests per **2** seconds.  
The response provide any information you may need about it:

> Example of values for the rate limit headers

```json
{
  "Retry-After": 2,
  "X-RateLimit-Limit": 20,
  "X-RateLimit-Remaining": 7,
  "Retry-After" : "Tue Feb 16 2021 09:02:42 GMT+0100 (Central European Standard Time)"
}
```

Header    | Description
--------- | -----------
Retry-After | The number of second in which you can retry
X-RateLimit-Limit | The maximum requests in that time
X-RateLimit-Remaining | The number of remaining requests you can make
X-RateLimit-Reset | The date when the rate limit will reset

# Definitions

## Lead

A lead, recipient or buddy-to-be is a person that you try to contact using lemlist. Lead is the developer term in the API and is the same thing than buddy-to-be in the app. You know... marketing...

## Unsubscribe

Unsubscribe is the developer term for the graveyard. Where person decide that they don't want to receive email from you anymore.

# Authentication

> To authorize, use this code:

```shell
curl https://api.lemlist.com/api/team \
  --user ":YourApiKey"
```

> Make sure to replace `YourApiKey` with your API key.

All API routes are using the dedicated sub domain `api.lemlist.com`.

lemlist uses API keys to allow access to the API. You can get your lemlist API key at our [integration page](https://app.lemlist.com/integrations).

You need to add the `Authorization` header using the `Basic` authentication type. `login:password` where the login is always empty and the password is the API key.

<aside class="notice">
Don't forget to add the semicolon (<code>:</code>) before your API key in curl command.
</aside>
