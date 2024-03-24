# Statistics

`RootStats`, accessed via `FMTCRoot.stats`, allows access to cached statistics, as well as listing of all existing stores, and the watching over changes in multiple/all stores and the bulk download recovery system.

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/RootStats-class.html" %}

<pre class="language-dart" data-full-width="false"><code class="lang-dart"><strong>final stats = FMTCRoot.stats;
</strong>
await stats.storesAvailable; // List all the available/existing stores
await stats.realSize; // Retrieve the actual total size of the database in KiBs
await stats.size; // Retrieve the total number of KiBs of all tiles' bytes (not 'real total' size) from all stores
await stats.length; // Retrieve the total number of tiles in all stores
await stats.watchRecovery(); // Watch for changes to the recovery system
await stats.watchStores(); // Watch for changes in the specified (or all) stores
</code></pre>

{% hint style="info" %}
Remember that the `size` and `length` statistics in the root may not be equal to the sum of the same statistics of all available stores, because tiles may belong to many stores, and these statistics do not count any tile multiple times.
{% endhint %}
