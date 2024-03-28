# Introduction

{% hint style="warning" %}
Before using FMTC, especially to bulk download or import/export, ensure you comply with the appropriate restrictions and terms of service set by your tile server. Failure to do so may lead to any punishment, at the tile server's discretion.

This library and/or the creator(s) are not responsible for any violations you make using this package.

For example, OpenStreetMap's tile server forbids bulk downloading: [https://operations.osmfoundation.org/policies/tiles](https://operations.osmfoundation.org/policies/tiles). And Mapbox has restrictions on importing/exporting from outside of the user's own device.

For testing purposes, check out the testing tile server included in the FMTC project: [testing-tile-server.md](../bulk-downloading/testing-tile-server.md "mention").
{% endhint %}

FMTC allows stores (including all necessary tiles and metadata) to be [exported](exporting.md) to an 'archive'/a standalone file, then [imported](importing.md) on the same or a different device!

{% hint style="info" %}
FMTC does not support exporting tiles to a raw Z/X/Y directory structure that can be read by other programs.
{% endhint %}

For example, this can be used to create backup systems to allow user's to store maps for later off-device, sharing/distribution systems, or to distribute a preset package of tiles to all users without worrying about managing IO or managing assets, and still allowing users to update their cache afterward!

***

External functionality is accessed via `FMTCRoot.external('~/path/to/file.fmtc')`.

All functionalities require the path to an archive file. The file may not necessarily exist: for the `export` method only, the file will be created if it does not exist, and overwritten if it does. Other methods require the file to exist, and be in a valid format.

{% hint style="warning" %}
Archives are backend specific. They cannot necessarily be imported by a backend different to the one that exported it.
{% endhint %}
