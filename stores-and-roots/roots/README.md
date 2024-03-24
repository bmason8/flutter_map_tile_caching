# Roots

Roots contain cached statistics and recovery information.

Because there is only a single root at any time, the root is not named. Instead, it is accessed via `FMTCRoot` - and all members are static.

<pre class="language-dart"><code class="lang-dart"><strong>// final root = FMTCRoot;
</strong>final size = await FMTCRoot.stats.realSize;
</code></pre>

After the root reference is constructed, the following actions can be performed with it:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Statistics:</strong> <code>stats</code></td><td>Retrieve information about the store and its contents</td><td></td></tr><tr><td><strong>Recovery:</strong> <code>recovery</code></td><td>Recovery from unexpectedly failed bulk downloads</td><td></td></tr><tr><td><strong>Import:</strong> <code>import</code></td><td>Import a prevously exported store</td><td></td></tr></tbody></table>

{% hint style="info" %}
Management of the root is not provided by `FMTCRoot`. Instead, the backend should implement any necessary methods.
{% endhint %}
