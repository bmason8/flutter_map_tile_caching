# Statistics

`StoreStats`, accessed via `FMTCStore().stats`, allows access to cached statistics, as well as retrieval of a recent tile (as an image), and the watching over changes in the store.

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/StoreStats-class.html" %}

<pre class="language-dart" data-full-width="false"><code class="lang-dart"><strong>final stats = FMTCStore('storeName').stats;
</strong>
await stats.all; // Retrieve the size, length, hits, and misses of this store
await stats.size; // Retrieve the total number of KiBs of all tiles' bytes (not 'real total' size)
await stats.length; // Retrieve the number of tiles belonging to this store
await stats.hits; // Retrieve the number of successful tile retrievals when browsing
await stats.misses; // Retrieve number of unsuccessful tile retrievals when browsing
await stats.tileImage(); // Retrieve the tile most recently modified in the specified store
await stats.watchChanges(); // Watch for changes to statistics (including tile events) and metadata
</code></pre>
