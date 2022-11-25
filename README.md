# WORK IN PROGRESS

Not actually usable yet :)



# Tootpick

Tootpick is a privacy-preserving tooter, similar to the one on toot.kytta.dev.

Its purpose is providing an easy link target for a "Mastodon share button",
similar to other social media share buttons.

## Using Tootpick

To allow visitors to share a message via Mastodon, provide a link to

```
https://tootpick.org/#text=Your%20text%20here
```

This will let the visitor pick their Mastodon server and post the message "Your
text here". When sharing an article or web page, don't forget to include the
URL as part of the text. The text must be "URI encoded", i.e. spaces must be
replaced by `%20`, ampersands by `%26`, etcetera, just like is common for URLs.
It is customary to include several relevant hashtags; use `%23` for the `#`
sign.

## Self-hosting

Instead of using the central tootpick.org service, tootpick can also be
self-hosted by downloading the static HTML file. Tootpick is AGPL licensed, but
as long as it remains a static HTML page, the requirement of sharing the source
code of a derivative work is automatically fulfilled.

Self-hosting comes with a privacy trade-off: a self-hosted (modified) copy of
Tootpick could be used to collect the Mastodon instances used by the visitor,
but on the other hand hides their IP address from the server that hosts the
service on tootpick.org.

## Button image

No button image is provided at this point, but the [official Mastodon logo](https://github.com/mastodon/mastodon/tree/main/app/javascript/images)
is probably a good starting point for designing your own.

## Why not just link directly to Mastodon?

Mastodon is part of the fediverse, a federated network. By design, there is no
central server or central domain name, so the direct link option does not
exist. Please don't make the mistake of picking a large server and linking
directly to its /share URL, because the majority of Mastodon users will not be
on that server.

## Design goals

### Nothing fancy

The functionality is simple and does not requires bells and whistles. In true
KISS spirit, Tootpick is a single static HTML page. It can be used through
the hosted tootpick.org, or by self-hosting the single HTML file.

### Privacy

Tootpick abuses the "hash" or "fragment" part of the URL, which is not sent to
the HTTP server, for passing the message. Javascript is used to parse the URL
and pass the data onto the chosen Mastodon instance. Only the instance server
will actually receive the contents of the message to be posted.

Because Tootpick is a static page in between the article that has the "share"
link and the mastodon instance, the original Referer URL won't make it to the
instance, hiding any possibly sensitive tracking information from the instance
admins. (It is not possible for Tootpick to prevent sending the Referer to the
server that hosts Tootpick.)

### Multiple instances

Most existing instance pickers will provide an option to remember the last used
instance, but that's not sufficiently helpful for users who use multiple
instances, which is not entirely uncommon. Tootpick remembers multiple recently
used instances.

### Browser support

If it works for 99.9% of all internet users, and 98% get the site with the
intended aesthetics, that's good enough. Tootpick does not support ancient
browsers, and may look ugly on old browsers.

It should also be usable by people who use assistive technologies, but that
comes for free by using normal HTML.
