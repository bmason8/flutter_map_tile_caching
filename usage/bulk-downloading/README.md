# 📲 Bulk Downloading

FMTC also provides the ability to bulk download areas of maps in one-shot, known as 'regions'. There are multiple different types/shapes of regions available: [#types-of-region](regions.md#types-of-region "mention").

{% hint style="warning" %}
Before using FMTC, especially to bulk download or import/export, ensure you comply with the appropriate restrictions and terms of service set by your tile server. Failure to do so may lead to any punishment, at the tile server's discretion.

This library and/or the creator(s) are not responsible for any violations you make using this package.

For example, OpenStreetMap's tile server forbids bulk downloading: [https://operations.osmfoundation.org/policies/tiles](https://operations.osmfoundation.org/policies/tiles). And Mapbox has restrictions on importing/exporting from outside of the user's own device.

For testing purposes, check out the testing tile server included in the FMTC project: [testing-tile-server.md](testing-tile-server.md "mention").
{% endhint %}

Downloading is extremely efficient and fast, and uses multiple threads and isolates to achieve write speeds of hundreds of tiles per second (if the network/server speed allows). After downloading, no extra setup is needed to use them in a map (other than the usual [integration.md](../integration.md "mention")).

It is also simple to understand and implement:

1.  [Create a region based on the user's input](regions.md)

    _↳ Optionally,_ [_create a `FlutterMap`_ _`Polygon`_](regions.md#converting-to-drawable-polygons)
2. [Convert that region into a downloadable region](prepare.md)\
   _↳ Optionally,_ [_check the number of tiles in the region_](prepare.md#checking-number-of-tiles) _before downloading_
3. [Start downloading that region](foreground.md)\
   _↳ Optionally, when testing,_ [_try the miniature tile server_](testing-tile-server.md)
4. [Listen for progress](foreground.md#listen-for-progress) events to update your user
5. Optionally, [control (pause/resume/cancel) the download](control-downloads.md)
