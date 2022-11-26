# Tootpick

Tootpick is a privacy-preserving tooter.

Its purpose is providing an easy link target for a "Mastodon share button",
similar to other social media share buttons.

## Using Tootpick

To allow visitors to share a message via Mastodon, provide a link to

```
https://tootpick.org/#text=Everyone%20should%20visit%20https://example.org/
```

This will let the visitor pick their Mastodon server and post the message
"Everyone should visit https://example.org/". When sharing an article or web
page, don't forget to include the URL as part of the text. The text must be
"URI encoded", i.e. spaces must be replaced by `%20`, ampersands by `%26`,
etcetera, just like is common for URLs. It is customary to include several
relevant hashtags; use `%23` for the `#` sign. In JavaScript, this kind of
encoding is available as `EncodeURIComponent()`.

Most Mastodon servers have a 500 character limit so it's wise to keep your
message shorter than that. Tootpick does not check the length of the message.

## Self-hosting

Instead of using the central tootpick.org service, tootpick can also be
self-hosted by downloading the static HTML file. Tootpick is AGPL licensed, but
as long as it remains a static HTML page, the requirement of sharing the source
code of a derivative work is automatically fulfilled.

Self-hosting comes with a privacy trade-off: a self-hosted (modified) copy of
Tootpick could be used to collect the Mastodon instances used by the visitor,
but on the other hand hides visitor IP addresses from the server that hosts the
service on tootpick.org.

## Button image

No button image is provided at this point, but the [official Mastodon logo](https://github.com/mastodon/mastodon/tree/main/app/javascript/images)
is probably a good starting point for designing your own.

## Why not just link directly to Mastodon?

Mastodon is part of the fediverse, a federated network. By design, there is no
central server or central domain name. That direct link option you might be
thinking about, does not exist. Please don't make the mistake of picking a
large server and linking directly to its /share URL, because the majority of
Mastodon users will not be on that server.

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

> Hi, it's me, the author of Tootpick. Because I'm not collecting any data
> from Tootpick users, I have no idea who uses it. If you're using Tootpick on
> your website, and want to let me know, please "star" the project on GitHub or
> send me a message on Mastodon (`@whreq@hsnl.social`) - that way I know
> whether I should keep maintaining it. Thanks!

### Multiple instances

Most existing instance pickers will provide an option to remember the last used
instance, but that's not sufficiently helpful for users who use multiple
instances, which is not entirely uncommon. Tootpick remembers multiple recently
used instances.

### Browser support

If the main feature works for 99% of all internet users, and 98% get the site
with the intended aesthetics, that's good enough. Tootpick does not support
ancient browsers like IE, and may look ugly and have degraded feature
availability on old browsers. (The percentages are completely made up and just
for illustrating the point.)

It should also be usable by people who use assistive technologies, but that
comes for free by using normal HTML.

### Fix PEBCAKs

Real people make mistakes, and some common mistakes can be recognised and fixed
by the script. A user may provide the wrong domain, a URL instead of the bare
domain name, an account, or the account domain instead of the web domain, and
Tootpick tries to recover from that and do the right thing.

## Similar projects

Tootpick is not the first of its kind. It draws inspiration from:

- [toot](https://codeberg.org/kytta/toot)
- [Advanced Sharer for Mastodon](https://sharetomastodon.github.io/about/)
- [Mastodon Share Button](https://aly-ve.github.io/Mastodon-share-button/)

## Future improvements

At some point in the future, I hope to:

- Have an alternative "light mode" for people who don't like dark pages.
- Detect the visitor's language and show translated texts.
- Supply a list of existing instances. Not sure if it's useful enough to add
  extra weight, and not sure how to determine which instances to include or
  exclude. Please let me know what you think!
