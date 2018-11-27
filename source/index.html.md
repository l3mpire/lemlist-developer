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

# Definitions

## Lead

A lead, recipient or buddy-to-be is a person that you try to contact using lemlist. Lead is the developer term in the API and is the same thing than buddy-to-be in the app. You know... marketing...

## Unsubscribe

Unsubscribe is the developer term for the graveyard. Where person decide that they don't want to receive email from you anymore.

# Authentication

> To authorize, use this code:

```shell
curl https://app.lemlist.com/api/team \
  --user ":YourApiKey"
```

> Make sure to replace `YourApiKey` with your API key.

lemlist uses API keys to allow access to the API. You can get your lemlist API key at our [integration page](https://app.lemlist.com/integrations).

You need to add the `Authorization` header using the `Basic` authentication type. `login:password` where the login is always empty and the password is the API key.

<aside class="notice">
Don't forget to add the semicolon (<code>:</code>) before your API key in curl command.
</aside>
