# Metadata

`StoreMetadata`, accessed via `FMTCStore().metadata`, allows access and control over a simple peristent storage mechanism, designed for use with custom data/properties/fields tied to the store (such as a [`CacheBehavior`](../integration.md#cache-behavior) or URL template).

Data is interpreted in key-value pair form, where both the key and value are `String`s. Internally, the default backend stores it as a flat JSON structure. The metadata is stored directly on the store: if the store is deleted, it is deleted, and an exported store will retain its metadata. More advanced requirements will require use of a seperate persistance mechanism.

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/StoreMetadata-class.html" %}

{% hint style="info" %}
Remember that `metadata` does not have any effect on internal logic: it is simply an auxiliary method of storing any data that might need to be kept alongside a store.
{% endhint %}

<pre class="language-dart" data-full-width="false"><code class="lang-dart"><strong>final md = FMTCStore('storeName').metadata;
</strong>
await md.read; // Retrieve (all) the stored metadata
await md.set(); // Set a single key-value pair (overwriting any existing value for the key)
await md.setBulk(); // Set multiple key-value pairs (overwriting any existing value for each key)
await md.remove(); // Remove the specified key (and corresponding value)
await md.reset(); // Remove all keys (and values)
</code></pre>

