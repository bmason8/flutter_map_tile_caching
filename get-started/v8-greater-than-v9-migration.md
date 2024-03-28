# v8 -> v9 Migration

{% hint style="success" %}
v9 is a complete rewrite of FMTC internals, written over hundreds of hours. It focuses on:&#x20;

* improved future maintainability by modularity
* improved stability & performance across the board
* support of 'tiles across stores': reduced duplication

Check out the CHANGELOG: [https://pub.dev/packages/flutter\_map\_tile\_caching/changelog](https://pub.dev/packages/flutter\_map\_tile\_caching/changelog)! This page only covers breaking changes, not feature additions and fixes.

Please consider donating: [#supporting-me](../#supporting-me "mention")! Any amount is hugely appriciated!
{% endhint %}

These migration instructions will not cover every scenario, because the number of breaking changes is so high. I've done my best to organise them into categories.

## Universally Affecting

{% hint style="warning" %}
Stores and roots from previous versions will be incompatible with v9, and will not be migratable.

This is because the underlying storage technology has chnaged from Isar to ObjectBox (in the default instance, at least).

Therefore, before publishing a version of your app with v9, it may be beneficial to notify users of the upcoming change, so the sudden dissappearance of their cached data is not unexpected.

Removal of the old cache will need to be performed manually.
{% endhint %}

<details>

<summary>Removed the <code>FlutterMapTileCaching</code>/<code>FMTC</code> object, in favour of direct usage of <code>FMTCStore</code> and <code>FMTCRoot</code> (which replace <code>StoreDirectory</code> &#x26; <code>RootDirectory</code>)</summary>

Much of the configuration and state management performed by the `FlutterMapTileCaching` top-level object singleton, and it's close relatives, were transferred to the backend, and as such, there is no longer a requirement for these objects.

Additionally, the name 'directory' has been outdated for a while. Therefore, these changes were merged into one.

To migrate, follow these patterns:

{% code title="Previous" %}
```dart
// Get a store directory
final StoreDirectory oldStore = FlutterMapTileCaching.instance('storeName'); // (or `FMTC.`)

// Access the root statistics
final RootDirectory oldRoot = FlutterMapTileCaching.instance.rootDirectory; // (or `FMTC.`)
final RootStats oldRootStats = oldRoot.stats;
```
{% endcode %}

<pre class="language-dart" data-title="Migrated"><code class="lang-dart">// Get a store
<strong>final FMTCStore newStore = FMTCStore('storeName');
</strong>
// Access the root statistics
<strong>final RootStats newRootStats = FMTCRoot.stats;
</strong>// `FMTCRoot` must now be used immediately, because it is not an object instance
</code></pre>

See below for information about migrating initialisation.

</details>

<details>

<summary>Changed the method of initialisation &#x26; error handling</summary>

Due to the removal of the `FMTC` object, and introduction of multiple-backend support, initialisation is now performed directly on a backend. The backend then creates a link between itself and its implementation to the abstracted convienience methods and front.

Additionally, error handling has been improved throughout FMTC, and is now more consitent and stable, doesn't rely on callbacks, and error `StackTrace`s include more useful information.

For the default, built-in backend, migration is simple:

{% code title="Previous" %}
```dart
await FlutterMapTileCaching.initialise(
    errorHandler: (FMTCInitialisationException e) {},
);
```
{% endcode %}

{% code title="Migrated" %}
```dart
try {
    await FMTCObjectBoxBackend().initialise();
} catch (error, stackTrace) {
    // Improved error handling
}
```
{% endcode %}

For more information, see [initialisation.md](../general/initialisation.md "mention") & [error-handling.md](../general/error-handling.md "mention").

</details>

<details>

<summary>Removed support for synchronous operations (and renamed asynchronous operations to reflect this)</summary>

These were incompatible with the new `Isolate`d `FMTCObjectBoxBackend`, they've been removed, in favour of backends implementing their own `Isolate`ion as well.

There is no direct migration instructions, as the correct new solution is case-dependent. In non-widget environments, use asynchronous techniques. In widget builds, make use of `FutureBuilder`s.\
However, the members have all been renamed in the same form: `*Async` is now just `*`.

</details>

## Bulk Downloading

<details>

<summary>Refactored <code>DownloadableRegion</code> &#x26; removed <code>RegionType</code></summary>

`DownloadableRegion` no longer contains the outline `points` of the `BaseRegion` it was formed from. It also no longer contains `parallelThreads`, `preventRedownload`, and `seaTileRemoval`: these are now configurable at download-time. `errorHandler` has been removed altogether.

Additionally, `DownloadableRegion` now makes use of sealed typing by using the type argument to contain the type of `BaseRegion`, so `RegionType` has become redundant and been removed.

</details>
