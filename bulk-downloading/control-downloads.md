# Control Downloads

There are 3 methods available to control a download, and 1 method to check the download's current state.

{% embed url="https://pub.dev/documentation/flutter_map_tile_caching/latest/flutter_map_tile_caching/DownloadManagement-class.html" %}

{% hint style="info" %}
It may take some time to perform these operations if the download has a low TPS, as each thread checks the current state/awaits a signal between each of their tiles.

`pause` & `cancel` are asynchronous for this reason, and will complete when all threads are paused or cancelled. `resume` returns immediately.
{% endhint %}

## Pause/Resume

If your user needs to temporarily pause the download, with the ability to resume it at some point later (within the same app session), use `pause` and `resume`.

`pause` allows all threads to finish the tile they're currently downloading, then forces them to wait for a signal sent by `resume` before they can download their next tile. It does not write any buffered tiles to the store.

Use `isPaused` to check whether the download is currently paused.

## Cancel

If your user needs to stop the download entirely, use `cancel`.

`cancel` allows all threads to finish the tile they're currently downloading, then forces them to cleanup and 'kill' themselves. Any buffered tiles are written to the store before the future returned by `cancel` is completed.

It is safe to use `cancel` after `pause` without `resume`ing first.
