---
title: How to use URL parameters
menu: How to use URL params
category: general
permalink: /how-to-use-url-parameters
---

There are a few ways we determine where a visitor comes from. We automatically detect the previous page (referrer) from the visitor's browser, but you can also add a URL parameter to override this and set a custom referrer.

## Using a URL parameter

If the current URL on your site includes a parameter named `ref`, `source`, or `utm_source`, we use this value instead of the browser's previous page.

For example, if you were to include this link in an email newsletter, Simple Analytics records the referrer as `email` in your dashboard, no matter where user actually comes from:

```
https://example.com/path?ref=email
```

### Forbidden characters

Certain character are not allowed in the URL parameter. Letters and numbers are always okay, but if you want to use special characters (like spaces, `;`, `/`, `?`, `:`, `@`, `&`, `=`, `+`, `$`, or `,`) you need to escape your URL parameter. A good website that does this for you is [urlencoder.io](https://www.urlencoder.io/?ref={{ site.hostname }}).

Valid examples of URL parameters:

```
https://example.com/?ref=email-button
https://example.com/?ref={{ site.hostname }}
https://example.com/?ref=android%3A%2F%2Fcom.example.app%2Fpath
https://example.com/?ref=exister%2C%20avoir%20une%20r%C3%A9alit%C3%A9
```

## Using the referrer URL

> The referrer URL is only used if there are none of the URL parameters mentioned above

If there is no referral parameter found, we save the URL of the referring page from the visitor's browser. We only save the part of the referrer before `?` or `#`, so if the referrer URL is `https://referrer.example.com/search?query=sensitive+information`, we only store `referrer.example.com/search`. Note that the protocol (`https://`) is also removed. We also ignore common subdomains like `www.`, `m.`, `l.`, and `www2.`.

> You don't have to do anything to make this work.

## Parsing of values

We parse the URL parameter differently than the referrer URL. Because you generate the URL parameters yourself, we don't want to touch these too much. Instead, we decode their values (so you can use forbidden characters) and convert hostnames to more general names. For example, we convert `www.google.com` to `google`. We still store the original value, but we show `google` as the referrer in the dashboard. We do this so we can combine similar referrers, such as `www.google.com`, `google.nl`, and `google.fr`, into simply `google`.

Referrer URLs contain the full URL that the browser gives us, such as `https://www.example.com/search?query=sensitive+information`. From this URL we store `referrer.example.com` as the referrer and keep `www.example.com/search` as the original URL. We drop the query (`?query=sensitive+information`), protocol (`https://`), and common subdomain (`www.`).

<img class="undraw-svg" src="/images/undraw_segment.svg" alt="">
