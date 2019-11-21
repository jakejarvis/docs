---
title: Server side
category: script
category_order: 2
order: 20
permalink: /server-side-tracking
---

When you send data from your server to Simple Analytics you need to provide a few fields:

| Field       | Type    | Example                 | Required  | Explanation                                                                                        |
| ----------- | ------- | ----------------------- | --------- | -------------------------------------------------------------------------------------------------- |
| url         | string  | https://example.com/    | yes       | The current URL of the page                                                                        |
| ua          | string  | Mozilla/5.0 ...         | sometimes | We use this if there is no User Agent present in the headers                                       |
| width       | number  | 1440                    | no        | The viewport width of the device (not possible via server)                                         |
| unique      | boolean | true                    | no        | This tells us if this visit is unique. Don't send this field if you don't detect unique page views |
| timezone    | string  | Europe/Amsterdam        | no        | The time zone of the current user so we can detect the country                                     |
| referrer    | string  | https://duckduckgo.com/ | no        | The referrer of the current page (if any)                                                          |
| urlReferrer | string  | blog                    | no        | The value of `?ref=...` in the URL ([more info](/how-to-use-url-parameters))                       |

> If we find a User Agent in the headers, we will use that.

Please strip all sensitive data from your URLs. We do this at our end as well, but it's better to have this done on your server.

<style>
  table td, table th {
    white-space: nowrap;
  }
  table tr td:last-of-type, table tr th:last-of-type {
    white-space: inherit;
  }
</style>

In JSON a request could look like this:

```json
{
  "url": "https://example.com/",
  "ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:70.0) Gecko/20100101 Firefox/70.0",
  "width": 1440,
  "unique": true,
  "timezone": "Europe/Amsterdam"
}
```

The response for this request will look like this:

```json
{
  "success": true,
  "duration_ms": 1,
  "message": "Thank you",
  "location": "Reykjavík, Iceland"
}
```

[Let us know](https://simpleanalytics.com/contact) if we can help you with anything!