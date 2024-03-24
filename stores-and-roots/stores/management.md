# Management

`StoreManagement`, accessed via `FMTCStore().manage`, allows control over the store and its contents.

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/StoreManagement-class.html" %}

<pre class="language-dart" data-full-width="false"><code class="lang-dart"><strong>final mgmt = FMTCStore('storeName').manage;
</strong>
await mgmt.ready; // Check whether the store exists
await mgmt.create(); // Create the store
await mgmt.delete(); // Empty tiles from the store, and delete it
await mgmt.reset(); // Empty tiles from the store, and reset hits &#x26; misses
await mgmt.rename('newStoreName'); // Change the name of the store
await mgmt.removeTilesOlderThan(DateTime.timestamp()); // Empty all tiles last modified before the specified timestamp
</code></pre>
