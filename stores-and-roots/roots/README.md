# Roots

Roots contain cached statistics and recovery information.

Because there is only a single root at any time, the root is not named. Instead, it is accessed via `FMTCRoot` - and all members are static.

<pre class="language-dart"><code class="lang-dart"><strong>// final root = FMTCRoot;
</strong>final size = await FMTCRoot.stats.realSize;
</code></pre>

After the root reference is constructed, the following actions can be performed with it:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Statistics:</strong> <code>stats</code></td><td>Retrieve information about the store and its contents</td><td><a href="statistics.md">statistics.md</a></td></tr><tr><td><strong>Recovery:</strong> <code>recovery</code></td><td>Recovery from unexpectedly failed bulk downloads</td><td><a href="recovery.md">recovery.md</a></td></tr><tr><td><em><strong>External:</strong> <code>external</code></em></td><td>Export &#x26; import store archives</td><td><a href="../../external/introduction.md">introduction.md</a></td></tr></tbody></table>

{% hint style="info" %}
Management of the root is not provided by `FMTCRoot`. Instead, the backend should implement any necessary methods.
{% endhint %}
