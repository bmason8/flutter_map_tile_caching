# 2️⃣ Prepare For Downloading

[`BaseRegion`s](regions.md) must be converted to `DownloadableRegion`s before they can be used to download tiles.

These contain the original `BaseRegion`, but also some other information necessary for downloading, such as zoom levels and URL templates.

```dart
final downloadableRegion = region.toDownloadable(
    minZoom: 1,
    maxZoom: 18,
    options: TileLayer(
        urlTemplate: '_',
        userAgentPackageName: 'com.example.app',
    ),
),
```

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/BaseRegion/toDownloadable.html" %}

{% hint style="info" %}
The `TileLayer` passed to the `options` parameter must include both a `urlTemplate` (or WMS configuration) and a `userAgentPackageName`, unless it is only being used to [`check` the number of tiles in the region](prepare.md#checking-number-of-tiles).
{% endhint %}

## Checking Number Of Tiles

Before continuing to downloading the region, you can use `check()` to count the number of tiles it will attempt to download. This is accessible through `FMTCStore().download`.

The method takes the `DownloadableRegion` generated above, and will return an `int` number of tiles. For larger regions, this may take a few seconds.

{% hint style="warning" %}
This figure will not take into account any skipped sea tiles or skipped existing tiles, as those are handled at the time of download.
{% endhint %}
