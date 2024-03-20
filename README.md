---
description: A plugin for 'flutter_map' providing advanced offline functionality
cover: .gitbook/assets/OpenStreetMap Screenshot.jpg
coverY: -47.966226138032305
---

# flutter\_map\_tile\_caching

{% hint style="info" %}
You're currently browsing the docs for v9, which is currently in beta prerelease.

Browse the current v8 docs: [v8](https://app.gitbook.com/o/1aKKbSpe255wyVNDoFYc/s/fPX4iWzEnN3gw4KJGc0k/ "mention").
{% endhint %}

[![pub.dev](https://img.shields.io/pub/v/flutter\_map\_tile\_caching.svg?label=Latest+Version)](https://pub.dev/packages/flutter\_map\_tile\_caching) [![stars](https://badgen.net/github/stars/JaffaKetchup/flutter\_map\_tile\_caching?label=stars\&color=green\&icon=github)](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching/stargazers) [![likes](https://img.shields.io/pub/likes/flutter\_map\_tile\_caching?logo=flutter)](https://pub.dev/packages/flutter\_map\_tile\_caching/score)        [![Open Issues](https://badgen.net/github/open-issues/JaffaKetchup/flutter\_map\_tile\_caching?label=Open+Issues\&color=green)](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching/issues) [![Open PRs](https://badgen.net/github/open-prs/JaffaKetchup/flutter\_map\_tile\_caching?label=Open+PRs\&color=green)](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching/pulls)

## Highlights

<table data-card-size="large" data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><p><mark style="color:blue;">◉</mark> 📲</p><p><strong>Integrated Caching × Bulk Downloading</strong></p></td><td>Get both dynamic browse caching that works automatically as the user browses the map, and bulk downloading to preload regions onto the user's device, all in one convenient, integrated API!</td><td><ul><li><a data-footnote-ref href="#user-content-fn-1">Multi-cache ('store') support</a> with <a data-footnote-ref href="#user-content-fn-2">minimized tile duplication</a></li><li><a data-footnote-ref href="#user-content-fn-3">Download any shape of area</a></li><li><a data-footnote-ref href="#user-content-fn-4">Automatic sea tile skipping</a></li><li><a data-footnote-ref href="#user-content-fn-5">Super-controllable downloads</a></li><li><a data-footnote-ref href="#user-content-fn-6">Optional download rate limiting</a></li></ul></td><td></td></tr><tr><td><p><mark style="color:red;">◉</mark> 🏃</p><p><strong>Ultra-fast &#x26; Performant</strong></p></td><td>No need to bore your users to death anymore! Bulk downloading is super-fast, and can even reach speeds of over 1500 tiles per second<a data-footnote-ref href="#user-content-fn-7">*</a>. Existing cached tiles can be displayed on the map almost instantly.</td><td><ul><li>Multi-threaded setup to minimize load on main thread, even when browse caching</li><li>Streamlined internals to reduce memory consumption</li></ul></td><td></td></tr><tr><td><p><mark style="color:green;">◉</mark> 🧩</p><p><strong>Import &#x26; Export</strong></p></td><td>Export and share stores, then import them later, or on other devices! You could even remote control your organization's devices, by pushing tiles to them, keeping your tile requests (&#x26; costs) low!</td><td></td><td></td></tr><tr><td><p><mark style="color:purple;">◉</mark> 💖</p><p><strong>Quick To Implement &#x26; Easy To Experiment</strong></p></td><td>A basic caching implementation can be setup in four quick steps, and shouldn't even take 5 minutes to set-up. Check out our <a data-mention href="get-started/quickstart.md">quickstart.md</a> instructions.</td><td>Ready to experiment with bulk downloading, but don't want to make costly and slow tile requests? Check out the testing tile server included in the FMTC project: <a data-mention href="bulk-downloading/introduction.md#testing-your-application">#testing-your-application</a>!</td><td></td></tr></tbody></table>

### How can FMTC elevate my app to the next level?

Too easy :smile:! Take a look at Google Maps, or Strava, or whichever other app of your choice.

<details>

<summary>All I see are rectangles. Why download whole regions of map that will never be even glanced at? Because most routes or areas aren't square and rectangles!</summary>

Whether it's walking along a remote winding river using the [Line region](bulk-downloading/regions.md#poly-line), downloading all of central London ready for that weekend exploration using the [Circle region](bulk-downloading/regions.md#circle) (roaming fees + maps gets expensive fast!), or tracking your belongings across a vast, shapeless space using the [Custom Polygon region](bulk-downloading/regions.md#custom-polygon), FMTC has your user's back - but not all of their storage space!

</details>

<details>

<summary>Those massive lakes and coastlines near me really interrupt the view. If only there was a way to remove them from the picture...</summary>

Oh wait, there is! With Sea Tile Skipping, you can avoid storing those unneccessary tiles of sea of out-of-tile-server-bounds-void, then use the client's functonality to just paint the spaces the same color as the sea. This also preserves sea tiles that aren't so empty after all - that boat path could come in handy for some scuba diving. Just another way FMTC keeps your user's phone a [tight ship](#user-content-fn-8)[^8] ;)

</details>

<details>

<summary>I need to download something else for a moment. Do I really have to stop the entire download and start again?</summary>

Not with FMTC! Downloads can be paused and resumed at any time, and with Download Recovery, downloads that stopped unexpectedly can be restarted without your user having to select the entire region again.

</details>

<details>

<summary>I wonder how much it costs the app developers?</summary>

FMTC supports bulk downloading from any tile server\*[^9], so you can choose whichever one suits you best.

Our browse caching mechanism doesn't result in any extra requests to the tile server, and in fact can reduce costs by serving tiles to users from their local cache without cost. Or, if you're running your own server, you can reduce the strain on it, keeping it snappy with fewer resources!

Downloads can be rate limited to avoid running up to the server's rate limit or excess fee.

And with export/import functionality, user's can download regions just once, then keep the download themselves for another time. Or, you can provide a bundle of tiles to all your user's, while still allow it to be updated per-user in future!\*[^10]

</details>

***

## Supporting Me

I work on all of my projects in my spare time, including maintaining (along with a team) Flutter's № 1 (non-commercially maintained) mapping library 'flutter\_map', bringing it back from the brink of abandonment, as well as my own plugin for it ('flutter\_map\_tile\_caching') that extends it with advanced caching and downloading.\
Additionally, I also own the Dart encoder/decoder for the QOI image format ('dqoi') - and I am slowly working on 'flutter\_osrm', a wrapper for the Open Source Routing Machine.

Sponsorships & donations allow me to continue my projects and upgrade my hardware/setup, as well as allowing me to have some starting amount for further education and such-like.\
And of course, a small amount will find its way into my Jaffa Cakes fund ([https://en.wikipedia.org/wiki/Jaffa\_Cakes](https://en.wikipedia.org/wiki/Jaffa\_Cakes)) - why do you think my username has "Jaffa" in it?

Many thanks for any amount you can spare, it means a lot to me!

{% embed url="https://github.com/sponsors/JaffaKetchup" %}
Sponsor Me via GitHub Sponsors
{% endembed %}

## (Proprietary) Licensing

_I am not a lawyer, and this information is to the best of my understanding. You are urged to read the license yourself for a thorough understanding._

This project is released under GPL v3. For detailed information about this license, see [https://www.gnu.org/licenses/gpl-3.0.en.html](https://www.gnu.org/licenses/gpl-3.0.en.html). [choosealicense.com](https://choosealicense.com/licenses/gpl-3.0/) summarises the license with the following paragraph:

> Permissions of this strong copyleft license are conditioned on **making available complete source code of licensed works and modifications, which include larger works using a licensed work, under the same license**. Copyright and license notices must be preserved. Contributors provide an express grant of patent rights.

Essentially, whilst you can use this code within commercial projects, they must not be proprietary - they incorporate this 'licensed work' so they must be available under the same license. You must distribute your source code (at least on request) (under the same GPL v3 license) to anyone who uses your program.

I learnt (and am still learning) to code with free, open-source software due to my age and lack of money, and for that reason, I believe in promoting open-source wherever possible to give equal opportunities to everybody, no matter their age, financial position, or any other characteristic. I'm not sure it's fair for commercial & proprietary applications to use software made by people for free out of generosity without giving back to the ecosystem or maintainer(s).\
On the other hand, I recognise that commercial businesses may want to use my projects for their own proprietary applications, and are happy to support me, and I am also trying to make a small amount of money from my projects, by donations and by selling licenses!

Therefore, if you would like a license to use this software within a proprietary application, I am willing to sell a (preferably yearly) license. If this seems like what you'd be interested in, please do not hesitate to get in touch at [fmtc@jaffaketchup.dev](mailto:fmtc@jaffaketchup.dev). Please include details of your project if you can, and the approximate scale/audience for your app; I try to find something that works for everyone, and I'm happy to negotiate! If you're a non-profit organization, I'm happy to also offer an alternative license for free\*[^11]!

## Get Help

Not quite sure about something? No problem, I'm happy to help!

Please get in touch via the correct method below for your issue, and I'll be there to help ASAP!

* For bug reports & feature requests: [GitHub Issues](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching/issues)
* For implementation/general support: The _#plugin_ channel on the [flutter\_map Discord server](https://github.com/fleaflet/flutter\_map#discord-server)
* For other inquiries and licensing: [fmtc@jaffaketchup.dev](mailto:fmtc@jaffaketchup.dev)

[^1]: Keep your users' tiles organized, and even let them control what goes where!

[^2]: Tiles can belong to multiple stores, and tiles from different sources (template URLs) can be stored in a single store!

[^3]: Download rectangles, circles, line-based, and any other freehand polygon!

[^4]: Avoid downloading redundant, waste-of-space tiles that cover oceans, with this unique functionality, and bless your users with the gift of more usable capacity for useful maps!

[^5]: Bulk downloads come with the ability to pause, resume, and cancel downloads mid-way! Give your users choice.

[^6]: Downloading from a server with a rate limit? No problem: just enable rate limiting and we'll do our best to stick to it!

[^7]: Speed is very dependent on tile server ability, network delays, and device processing power. Actual speed is likely to be considerably lower.



    1500 tiles was tested from the included testing tile server running on localhost, on a Windows 11 (Intel 12th Gen i7-12700H CPU & DDR5 4800MHz RAM) with 10 downloading threads & a buffer of 500 tiles.

[^8]: without unneccesary bloat

[^9]: Those compatible with flutter\_map. Some tile server's may forbid bulk downloading.

[^10]: Some tile servers may forbid this activity. Check your tile server's ToS.

[^11]: Decision will be case dependent. Please get in touch, and I'll be happy to talk!
