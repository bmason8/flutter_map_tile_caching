# 📂 Using Roots & Stores

## Structure

FMTC uses _roots_ and _stores_ to structure its data.

There is generally a single root (which generally corresponds to a single [backend](../initialisation.md#backends)), which contains multiple stores. Cached tiles can belong to multiple stores (the relationship between stores and tiles is many-to-many), which keeps duplication minimized.

Stores also contain any metadata. Both roots and stores also contain cached statistics to boost performance.

Each structure provides access to categorized methods, listed below.

{% hint style="warning" %}
The structures use the ambient backend when a method is invoked on it, not at construction time.

Therefore, it is possible to construct an `FMTCStore`/`FMTCRoot` (see below) before initialisation, but 'using' it will throw `RootUnavailable`.
{% endhint %}

## Accessing Stores

Stores are referenced by name, the single argument of `FMTCStore`.

{% hint style="warning" %}
Ensure names of stores are consistent across every access. "Typed"/code-generated stores are not provided, to maintain flexibility.
{% endhint %}

Construction of an `FMTCStore` object does not imply/infer that the underlying store has been created and is ready for use. Therefore, a store will require creation via its `StoreManagement` object (accessed via `FMTCStore.manage`) before it can be used.

<pre class="language-dart"><code class="lang-dart"><strong>// final store = FMTCStore('storeName');
</strong>await FMTCStore('storeName').manage.create(); // Refers to the same store as above
</code></pre>

After a store reference is constructed, the following actions can be performed with it:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Management:</strong> <code>manage</code></td><td>Control the store: create it, delete it, rename it, etc.</td><td><a href="store-management.md">store-management.md</a></td></tr><tr><td><strong>Statistics:</strong> <code>stats</code></td><td>Retrieve information about the store and its contents</td><td></td></tr><tr><td><strong>Metadata:</strong> <code>metadata</code></td><td>Access simple persistent storage, with no direct influence on FMTC's functioning</td><td></td></tr><tr><td><strong>Download:</strong> <code>download</code></td><td>Prepare/plan, start, and manage bulk downloads</td><td></td></tr><tr><td><strong>Export:</strong> <code>export</code></td><td>Export a store to a seperate database that may be imported at another point</td><td></td></tr><tr><td><em><strong>Integrate With</strong><strong> </strong><strong><code>TileLayer</code></strong></em></td><td><em>Generate a specialised <code>TileProvider</code> that allows flutter_map to access cached tiles</em></td><td></td></tr></tbody></table>

## Accessing The Root

Similarly to stores, the root is accessed via `FMTCRoot` - but is not named.

<pre class="language-dart"><code class="lang-dart"><strong>// final root = FMTCRoot;
</strong>final size = await FMTCRoot.stats.realSize;
</code></pre>

After the root reference is constructed, the following actions can be performed with it:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Statistics:</strong> <code>stats</code></td><td>Retrieve information about the store and its contents</td><td></td></tr><tr><td><strong>Recovery:</strong> <code>recovery</code></td><td>Recovery from unexpectedly failed bulk downloads</td><td></td></tr><tr><td><strong>Import:</strong> <code>import</code></td><td>Import a prevously exported store</td><td></td></tr></tbody></table>

{% hint style="info" %}
Management of the root is not provided by `FMTCRoot`. Instead, the backend should implement any necessary methods.
{% endhint %}
