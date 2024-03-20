# 1️⃣ Create A Region

Regions (`BaseRegion`s) are geographical areas that do not yet have any of the necessary extra information to start a download (like `DownloadableRegion`s).

The [example-application.md](../../get-started/example-application.md "mention") contains a great way you might want to allow your users to choose a region to download, and it shows how to use Provider to share a created region and the number of approximate tiles it has to a download screen. It even allows the user to follow the download, tile-by-tile!

## Types Of Region

{% tabs %}
{% tab title="Rectangle" %}
The most basic type of region, defined by two North West and South East coordinates that create a `LatLngBounds`.

```dart
final region = RectangleRegion(
    LatLngBounds(
        LatLng(), // North West coordinate
        LatLng(), // South East coordinate
    ),
);
```

This is usually all you get from most apps, so why not give your user a unique experience with some of our other region types...
{% endtab %}

{% tab title="Circle" %}
A more advanced type of region, defined by a center coordinate and radius (in kilometers).

Many cities are circular, so this could be used to download a planned tourist adventure, for example.

```dart
final region = CircleRegion(
    LatLng(), // Center coordinate
    0, // Radius in kilometers
);
```

If you have two coordinates, one center, and one on the edge of the circle you want, you can use ['latlong2's `Distance.distance()`](https://pub.dev/documentation/latlong2/latest/latlong2/Distance/distance.html) method, as below:

```dart
final region = CircleRegion(
    LatLng(), // Center coordinate
    const Distance(roundResult: false).distance(
        LatLng(), // Center coordinate
        LatLng(), // Edge coordinate
    ) / 1000; // Convert to kilometers
);
```
{% endtab %}

{% tab title="(Poly)Line" %}
A more advanced type of region, defined by a list of coordinates and radius (in meters).

This could be used to download tiles along a planned travel route, for example hiking or long-distance driving. Import coordinates from a routing engine, or from a GPX/KML file for maximum integration!

```dart
final region = LineRegion(
    [LatLng(), LatLng(), ...], // List of coordinates
    0, // Radius in meters
);
```

{% hint style="warning" %}
This type of region may consume more memory/RAM when generating tiles than other region types.
{% endhint %}
{% endtab %}

{% tab title="Custom Polygon" %}
The most advanced type of region, defined by a list of coordinates defining the outline of a polygon.

```dart
final region = CustomPolygonRegion(
    [LatLng(), LatLng(), ...], // List of coordinates
);
```

{% hint style="warning" %}
Polygons with self intersections are likely to be handled incorrectly, but the algorithm will not crash.
{% endhint %}

{% hint style="info" %}
A polygon is converted into tiles through a three-step process:

1. Split the polygon into triangles using an [ear clipping (earcutting)](https://en.wikipedia.org/wiki/Two\_ears\_theorem) algorithm
2. Generate the tiles of each of the triangles' edges using [Bresenham's line algorithm](https://en.wikipedia.org/wiki/Bresenham's\_line\_algorithm)
3. For each of the triangles, generate the tiles in the empty space between the outlines
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Interested to see how the tile generation algorithms for the different region types work under the hood, in a visual way?

Start a download in the example app, and tap/click the 'eye' icon in the top-left. Watch as you follow along with the download, tile-by-tile.
{% endhint %}

After you've created your region, you can convert it to a drawable polygon (below), or [convert it to a `DownloadableRegion`](prepare.md) ready for downloading.

## Converting To Drawable Polygons

All `BaseRegions` can be drawn on a map with minimal effort from you or the user, using `toDrawable()`.

Internally, this uses the `toOutline(s)` method to generate the points forming the `Polygon`, then it places this/these polygons into a `PolygonLayer`.
