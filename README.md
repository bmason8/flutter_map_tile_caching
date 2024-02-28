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

[![Pub](https://camo.githubusercontent.com/fa5d2e07c3ec99015333a47431c8f9c36fdd2e1b2d13e0931957165bfdbc24bd/68747470733a2f2f696d672e736869656c64732e696f2f7075622f762f666c75747465725f6d61705f74696c655f63616368696e672e7376673f6c6162656c3d4c61746573742b537461626c652b56657273696f6e)](https://pub.dev/packages/flutter\_map\_tile\_caching) [![likes](https://camo.githubusercontent.com/069b79d31629eac956d0bc39433b7417b922797243949aad8029618c357f5f61/68747470733a2f2f696d672e736869656c64732e696f2f7075622f6c696b65732f666c75747465725f6d61705f74696c655f63616368696e673f6c6162656c3d7075622e6465762b4c696b6573)](https://pub.dev/packages/flutter\_map\_tile\_caching/score) [![pub points](https://camo.githubusercontent.com/5f65f19f02c681109ee3cc29f56f32393a7a8a543d48f1c0470171eed8b76e40/68747470733a2f2f696d672e736869656c64732e696f2f7075622f706f696e74732f666c75747465725f6d61705f74696c655f63616368696e673f6c6162656c3d7075622e6465762b506f696e7473)](https://pub.dev/packages/flutter\_map\_tile\_caching/score)\
[![GitHub stars](https://camo.githubusercontent.com/066e78e1a3534dd759cfa7585cbda5c406c4b3c93dac6aa31da5ddd2d0809a3e/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f73746172732f4a616666614b6574636875702f666c75747465725f6d61705f74696c655f63616368696e672e7376673f6c6162656c3d4769744875622b5374617273)](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching/stargazers/) [![GitHub issues](https://camo.githubusercontent.com/d64e0e0d2a1d2921b4b697e7d23488c38e47132f2957436141c2bcbf742cd40f/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6973737565732f4a616666614b6574636875702f666c75747465725f6d61705f74696c655f63616368696e672e7376673f6c6162656c3d497373756573)](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching/issues/) [![GitHub PRs](https://camo.githubusercontent.com/091d49c5807d3fa7cb445f4f90c2fd58a369375aa8a13d76cfe7885dce5f0daa/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6973737565732d70722f4a616666614b6574636875702f666c75747465725f6d61705f74696c655f63616368696e672e7376673f6c6162656c3d50756c6c2532305265717565737473)](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching/pulls/)

{% embed url="https://github.com/stars/JaffaKetchup/lists/fmtc-modules" %}

<table data-card-size="large" data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><p><mark style="color:blue;">◉</mark> 📲</p><p><strong>Caching × Bulk Downloading</strong></p></td><td>Get both dynamic caching that works automatically as the user browses the map, and bulk downloading to preload regions onto the user's device, all in one convenient package!</td><td><ul><li><a data-footnote-ref href="#user-content-fn-1">Multi-cache ('store') support</a> with <a data-footnote-ref href="#user-content-fn-2">minimized tile duplication</a></li><li><a data-footnote-ref href="#user-content-fn-3">Download any shape of area</a></li><li><a data-footnote-ref href="#user-content-fn-4">Automatic sea tile skipping</a></li><li><a data-footnote-ref href="#user-content-fn-5">Super-controllable downloads</a></li><li><a data-footnote-ref href="#user-content-fn-6">Optional download rate limiting</a></li></ul></td><td></td></tr><tr><td><p><mark style="color:red;">◉</mark> 🏃</p><p><strong>Ultra-fast &#x26; Performant</strong></p></td><td>No need to bore your users to death anymore! Bulk downloading is super-fast, and can even reach speeds of over 1500 tiles per second<a data-footnote-ref href="#user-content-fn-7">*</a>. Existing cached tiles can be displayed on the map almost instantly.</td><td><ul><li>Multi-threaded setup to minimize load on main thread</li><li>Streamlined internals to reduce memory consumption</li></ul></td><td></td></tr><tr><td><p><mark style="color:green;">◉</mark> 🧩</p><p><strong>Import &#x26; Export</strong></p></td><td>Export and share stores, then import them later, or on other devices! You could even remote control your organization's devices, by pushing tiles to them, keeping your tile requests (&#x26; costs) low!</td><td></td><td></td></tr><tr><td><p><mark style="color:purple;">◉</mark> 💖</p><p><strong>Quick To Implement &#x26; Easy To Experiment</strong></p></td><td>A basic caching implementation can be setup in four quick steps, and shouldn't even take 5 minutes to set-up. Check out our <a data-mention href="get-started/quickstart.md">quickstart.md</a> instructions.</td><td>Ready to experiment with bulk downloading, but don't want to make costly and slow tile requests? Check out the testing tile server included in the FMTC project: <a data-mention href="bulk-downloading/introduction.md#testing-your-application">#testing-your-application</a>!</td><td></td></tr></tbody></table>

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

Essentially, whilst you can use this code within commercial projects, they must not be proprietary - they incorporate this 'licensed work' so they must be available under the same license. You must distribute your source code on request (under the same GPL v3 license) to anyone who uses your program.

However, I am willing to sell custom alternative proprietary licenses on a case-by-case basis and on request.

I learnt (and am still learning) to code with free, open-source software due to my age and lack of money, and for that reason, I believe in promoting open-source wherever possible to give equal opportunities to everybody, no matter their age or financial position. I'm not sure it's fair for commercial proprietary applications to use software made by people for free out of generosity. On the other hand, I am also trying to make a small amount of money from my projects, by donations or by selling licenses. And I recognise that commercial businesses may want to use my projects for their own proprietary applications.

Therefore, if you would like a license to use this software within a proprietary application, I am willing to sell a (preferably yearly or usage based) license for a reasonable price. If this seems like what you want/need, please do not hesitate to get in touch at [fmtc@jaffaketchup.dev](mailto:fmtc@jaffaketchup.dev).

## Get Help

Not quite sure about something? No problem. Please get in touch via any of these methods, and I'll be with you as soon as possible:

* For bug reports & feature requests: [GitHub Issues](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching/issues)
* For implementation/general support: The _#plugin_ channel on the [flutter\_map Discord server](https://github.com/fleaflet/flutter\_map#discord-server)
* For other inquiries: [fmtc@jaffaketchup.dev](mailto:fmtc@jaffaketchup.dev)

[^1]: Keep your users' tiles organized, and even let them control what goes where!

[^2]: Tiles can belong to multiple stores, and tiles from different sources (template URLs) can be stored in a single store!

[^3]: Download rectangles, circles, line-based, and any other freehand polygon!

[^4]: Avoid downloading redundant, waste-of-space tiles that cover oceans, with this unique functionality, and bless your users with the gift of more usable capacity for useful maps!

[^5]: Bulk downloads come with the ability to pause, resume, and cancel downloads mid-way! Give your users choice.

[^6]: Downloading from a server with a rate limit? No problem: just enable rate limiting and we'll do our best to stick to it!

[^7]: Speed is very dependent on tile server ability, network delays, and device processing power. Actual speed is likely to be considerably lower.



    1500 tiles was tested from the included testing tile server running on localhost, on a Windows 11 (Intel 12th Gen i7-12700H CPU & DDR5 4800MHz RAM) with 10 downloading threads & a buffer of 500 tiles.
