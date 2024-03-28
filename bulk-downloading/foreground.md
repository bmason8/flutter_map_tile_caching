# 3️⃣ Start Download

Now that you have constructed a `DownloadableRegion`, you're almost ready to go.

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/DownloadManagement/startForeground.html" %}

## Customization Options

Before you call `startForeground` (via `FMTCStore().download`) to start the download, check out the customization parameters:

* `parallelThreads` (defaults to 5)\
  The number of simultaneous download threads to run
* `maxBufferLength` (defaults to 200)\
  The number of tiles to temporarily persist in memory before writing to the cache
* `skipExistingTiles` (defaults to `true`)\
  Whether to avoid re-downloading tiles that have already been cached
* `skipSeaTiles` (defaults to `true`)\
  Whether to avoid caching tiles that are entirely sea
* `rateLimit`\
  The maximum number of tiles that can be attempted per second
* `maxReportInterval` (defaults to 1 second)\
  The duration in which to emit _at least_ one `DownloadProgress` event

## Start Download

{% hint style="warning" %}
Before using FMTC, especially to bulk download or import/export, ensure you comply with the appropriate restrictions and terms of service set by your tile server. Failure to do so may lead to any punishment, at the tile server's discretion.

This library and/or the creator(s) are not responsible for any violations you make using this package.

For example, OpenStreetMap's tile server forbids bulk downloading: [https://operations.osmfoundation.org/policies/tiles](https://operations.osmfoundation.org/policies/tiles). And Mapbox has restrictions on importing/exporting from outside of the user's own device.

For testing purposes, check out the testing tile server included in the FMTC project: [testing-tile-server.md](testing-tile-server.md "mention").
{% endhint %}

```dart
final progressStream = FMTCStore('storeName').download.startForeground(
    region: downloadableRegion,
    // other options...
);
```

{% hint style="info" %}
Whilst not recommended, it is possible to start and control multiple downloads simultaneously, by using a unique `Object` as the `instanceId` argument. This 'key' can then later be used to control its respective download instance.

Note that this option may be unstable.
{% endhint %}

## Listen For Progress

The `startForeground` method returns a (non-broadcast) `Stream` of `DownloadProgress` events, which contain information about the overall progress of the download, as well as the state of the latest tile attempt.

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/DownloadProgress-class.html" %}

<mark style="background-color:orange;">\<link to</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`TileEvent`</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">api docs here></mark>

To reflect the information from a single event back to the user, use a `StreamBuilder`, and build the UI dependent on the 'snapshots' of the stream. If you need to keep track of information from across multiple events, see [#keeping-track-across-events](foreground.md#keeping-track-across-events "mention") below.

### Keeping Track Across Events

In addition to display each individual event to your user, you may also need to keep track of information from across multiple `DownloadProgress` events. In this case, you'll likely need to use the `latestTileEvent` getter to access the latest `TileEvent` object, and keep track of its properties.

For example, you may wish to keep a list of all the failed tiles' URLs.

However, there are 3 important things to keep in mind when doing this:

<details>

<summary>Memory Consumption</summary>

Avoid keeping a list of _all_ emitted events. Instead, keep a 'circular buffer' of the useful subset of events.

A single download can have many events, and storing them all will consume a lot of memory. It is easy to consume all of the remaining allocated memory, and crash the app.

</details>

<details>

<summary>Data Loss</summary>

Avoid keeping track of required information internally through a `StreamBuilder` intended to display a UI.

A `StreamBuilder` will not necessarily call the `builder` callback once per event, especially if the download has a high TPS. Therefore, events may be lost.

</details>

<details>

<summary>Data Duplication</summary>

Avoid keeping track of events where the `latestTileEvent.isRepeat` property is `true`.

These `TileEvents` are exact repeats of the previous event, usually due to the `maxReportInterval` functionality. Therefore, including both in a dataset would be erroneous.

</details>
