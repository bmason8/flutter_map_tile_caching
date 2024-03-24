# Introduction

## Structure

FMTC uses a _root_ and _stores_ to structure its data.

There is generally a single root (which generally corresponds to a single [backend](../general/initialisation.md#backends)), which contains multiple stores. Cached tiles can belong to multiple stores, which keeps duplication minimized.

{% hint style="warning" %}
The structures use the ambient backend when a method is invoked on it, not at construction time.

Therefore, it is possible to construct an `FMTCStore`/`FMTCRoot` (see below) before initialisation, but 'using' it will throw `RootUnavailable`.
{% endhint %}

## Stores

Stores are referenced by name, the single argument of `FMTCStore`. Stores contain any metadata associated with them, cached statistics, and maintain a reference to all the tiles that belong to it.

{% hint style="warning" %}
Ensure names of stores are consistent across every access. "Typed"/code-generated stores are not provided, to maintain flexibility.
{% endhint %}

Construction of an `FMTCStore` object does not imply/infer that the underlying store has been created and is ready for use. Therefore, a store will require creation via its `StoreManagement` object (accessed via `FMTCStore.manage`) before it can be used.

<pre class="language-dart"><code class="lang-dart"><strong>// final store = FMTCStore('storeName');
</strong>await FMTCStore('storeName').manage.create(); // Refers to the same store as above
</code></pre>

### Actions

After a store reference is constructed, the following actions can be performed with it:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Management:</strong> <code>manage</code></td><td>Control the store: create it, delete it, rename it, etc.</td><td><a href="stores/management.md">management.md</a></td></tr><tr><td><strong>Statistics:</strong> <code>stats</code></td><td>Retrieve information about the store and its contents</td><td><a href="stores/statistics.md">statistics.md</a></td></tr><tr><td><strong>Metadata:</strong> <code>metadata</code></td><td>Access simple persistent storage, with no direct influence on FMTC's functioning</td><td><a href="stores/metadata.md">metadata.md</a></td></tr><tr><td><em><strong>Bulk Download:</strong></em> <em><code>download</code></em></td><td>Prepare/plan, start, and manage bulk downloads</td><td><a href="../bulk-downloading/introduction.md">introduction.md</a></td></tr><tr><td><em><strong>Integrate With</strong><strong> </strong><strong><code>TileLayer</code></strong></em></td><td><em>Generate a specialised <code>TileProvider</code> that allows flutter_map to access cached tiles</em></td><td><a href="integration.md">integration.md</a></td></tr></tbody></table>

## Root

Similarly to stores, the root is accessed via `FMTCRoot` - but is not named. Roots contain cached statistics and recovery information.

<pre class="language-dart"><code class="lang-dart"><strong>// final root = FMTCRoot;
</strong>final size = await FMTCRoot.stats.realSize;
</code></pre>

### Actions

After the root reference is constructed, the following actions can be performed with it:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Statistics:</strong> <code>stats</code></td><td>Retrieve information about the store and its contents</td><td><a href="roots/statistics.md">statistics.md</a></td></tr><tr><td><strong>Recovery:</strong> <code>recovery</code></td><td>Recovery from unexpectedly failed bulk downloads</td><td><a href="roots/recovery.md">recovery.md</a></td></tr><tr><td><em><strong>External:</strong> <code>external</code></em></td><td>Export &#x26; import store archives</td><td><a href="../external/introduction.md">introduction.md</a></td></tr></tbody></table>

{% hint style="info" %}
Management of the root is not provided by `FMTCRoot`. Instead, the backend should implement any necessary methods.
{% endhint %}
