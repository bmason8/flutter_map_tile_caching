# Quickstart

{% hint style="warning" %}
**FMTC is licensed under GPL-v3.**

If you're developing an application that isn't licensed under GPL, this affects you and your application's legal right to distribution. For more information, please see [#proprietary-licensing](../#proprietary-licensing "mention").
{% endhint %}

This page guides you through a simple, fast setup of FMTC that just enables basic browse caching, without any of the cool features that you can discover throughout the rest of this documentation.

## 1. [Install](installation.md)

Depend on the latest version of the package from pub.dev, then import it into the appropriate files of your project.

{% code title="Console/Terminal" %}
```sh
flutter pub add flutter_map_tile_caching
```
{% endcode %}

```dart
import 'package:flutter_map_tile_caching/flutter_map_tile_caching.dart';
```

## 2. [Initialise](../usage/initialisation.md)

Perform the startup procedure to allow usage of FMTC's APIs and allow FMTC to spin-up the underlying connections & systems.

Here, we'll use the built-in, default 'backend' storage, which uses [ObjectBox](https://pub.dev/packages/objectbox). We'll perform the intialisation just before the app starts, so we can be sure that it will be ready and accessible throughout the app, at any time.

<pre class="language-dart" data-title="main.dart"><code class="lang-dart">import 'package:flutter/widgets.dart';
import 'package:flutter_map_tile_caching/flutter_map_tile_caching.dart';

Future&#x3C;void> main() async {
    WidgetsFlutterBinding.ensureInitialized();
    
<strong>    await FMTCObjectBoxBackend().initialise(...);
</strong>    
    // ...
    
    runApp(MyApp());
}
</code></pre>

## 3. [Create a store](../usage/roots-and-stores/#without-automatic-creation)

Create a container that is capable of storing tiles, and can be used to [browse cache](#user-content-fn-1)[^1] and bulk download.

Here, we'll create one called 'mapStore', directly after initialisation. Any number of stores can be created, at any point!

<pre class="language-dart" data-title="main.dart"><code class="lang-dart">    // ...
    
<strong>    await FMTCStore('mapStore').manage.create();
</strong>    
    // ...
</code></pre>

## 4. [Connect to 'flutter\_map'](../usage/integration.md)

Add FMTC's specialised `TileProvider` to the `TileLayer`, to enable browse caching, and retrieval of tiles from the specified store.

{% hint style="warning" %}
Double check that the name of the store specified here is the same as the store created above!
{% endhint %}

<pre class="language-dart" data-title="map_view.dart"><code class="lang-dart">import 'package:flutter_map/flutter_map.dart';
import 'package:flutter_map_tile_caching/flutter_map_tile_caching.dart';

TileLayer(
    urlTemplate: 'https://tile.openstreetmap.org/{z}/{x}/{y}.png',
    userAgentPackageName: 'com.example.app',
<strong>    tileProvider: FMTCStore('mapStore').getTileProvider(),
</strong>    // Other parameters as normal
),
</code></pre>

## 5. Wow! Look at that caching...

{% hint style="success" %}
You should now have a basic working implementation of FMTC that caches tiles for you as you browse the map!

There's a lot more to discover, from store management to bulk downloading, and from statistics to exporting/importing.
{% endhint %}

{% hint style="warning" %}
Before using FMTC, especially to bulk download, ensure you comply with the appropriate restrictions and terms of service set by your tile server. Failure to do so may lead to any punishment, at the tile server's discretion.

This library and/or the creator(s) are not responsible for any violations you make using this package.

For example, OpenStreetMap's tile server forbids bulk downloading: [https://operations.osmfoundation.org/policies/tiles](https://operations.osmfoundation.org/policies/tiles).

For testing purposes, check out the testing tile server included in the FMTC project: [testing-tile-server.md](../usage/bulk-downloading/testing-tile-server.md "mention").
{% endhint %}

[^1]: This caching occurs automatically as the map is moved by the user, and new tiles load.
