# Stores

Stores contain any metadata associated with them, cached statistics, and maintain a reference to all the tiles that belong to it.

They are referenced by name, the single argument of `FMTCStore`.

{% hint style="warning" %}
Ensure names of stores are consistent across every access. "Typed"/code-generated stores are not provided, to maintain flexibility.
{% endhint %}

Construction of an `FMTCStore` object does not imply/infer that the underlying store has been created and is ready for use. Therefore, a store will require creation via its `StoreManagement` object (accessed via `FMTCStore.manage`) before it can be used.

<pre class="language-dart"><code class="lang-dart"><strong>// final store = FMTCStore('storeName');
</strong>await FMTCStore('storeName').manage.create(); // Refers to the same store as above
</code></pre>

After a store reference is constructed, the following actions can be performed with it:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Management:</strong> <code>manage</code></td><td>Control the store: create it, delete it, rename it, etc.</td><td><a href="management.md">management.md</a></td></tr><tr><td><strong>Statistics:</strong> <code>stats</code></td><td>Retrieve information about the store and its contents</td><td><a href="statistics.md">statistics.md</a></td></tr><tr><td><strong>Metadata:</strong> <code>metadata</code></td><td>Access simple persistent storage, with no direct influence on FMTC's functioning</td><td><a href="metadata.md">metadata.md</a></td></tr><tr><td><em><strong>Bulk Download:</strong></em> <em><code>download</code></em></td><td>Prepare/plan, start, and manage bulk downloads</td><td><a href="../../bulk-downloading/introduction.md">introduction.md</a></td></tr><tr><td><em><strong>Integrate With</strong><strong> </strong><strong><code>TileLayer</code></strong></em></td><td><em>Generate a specialised <code>TileProvider</code> that allows flutter_map to access cached tiles</em></td><td><a href="../integration.md">integration.md</a></td></tr></tbody></table>
