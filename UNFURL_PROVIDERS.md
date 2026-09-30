# Kuyo Link-Preview Providers

When link previews are enabled, Kuyo rewrites a supported public-post URL so that Discord renders it through the service below. Discord fetches the rewritten address; the service sees the post identifier and any image selection in it, but not the surrounding message text or the author's Discord ID.

| Site | Preview service |
| --- | --- |
| Twitter/X | fxtwitter.com; vxtwitter.com for GIF posts; g.fxtwitter.com for media the preview cannot hold |
| e621 | The operator's own relay, which attaches the media to the Discord message |
| Instagram | oginstagram.com |
| Reddit | fxddit.com |
| TikTok | tnktok.com |
| Bluesky | fxbsky.app |
| Threads | fzthreads.com |
| Facebook | facebed.com |
| Mastodon | fxmas.to |
| Truth Social | fxtruthsocial.com |
| Tumblr | tpmblr.com |
| Pixiv | www.phixiv.net; multi-page works are drawn by Kuyo from pixiv.net and phixiv data. Works pixiv rates R-18 or R-18G, or whose rating cannot be read, are previewed only in age-restricted channels and otherwise left as posted |
| DeviantArt | fixdeviantart.com |
| Fur Affinity | xfuraffinity.net |
| Newgrounds | fixnewgrounds.com |
| Imgur | fximgur.com |
| Twitch Clips | fxtwitch.seria.moe |
| Bilibili | fxbilibili.seria.moe |
| Spotify | fxspotify.com |
| 4chan | boards.fx4chan.org |
| PTT | fxptt.seria.moe |
| eBay | fxebay.com |
| Kick Clips | clkick.com |
| AliExpress | ali.tdy.app |
| BOOTH | No rewriting; extra product photos are linked from booth.pximg.net |

To choose the address, Kuyo itself makes one lookup per post for some sites, sending only the post identifier: api.fxtwitter.com for X, pixiv.net and www.phixiv.net for Pixiv, and booth.pm for BOOTH. It does not download media for any site except e621. Adult e621 media, adult BOOTH product photos, and age-restricted pixiv works are previewed only in channels marked age-restricted, unless the operator has configured an installation whose servers are all for adults.

Steam links and short links are left as posted, except TikTok share links, whose short code is passed to tnktok.com without Kuyo following the redirect.
