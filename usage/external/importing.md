---
description: fmtc_plus_sharing Module
---

# Importing

An exported store must be re-imported before it can be used again.

{% hint style="warning" %}
Attempting to import a damaged/corrupted store may result in a fatal app crash, or major errors at least.

See [#initialisation-safety](../initialisation.md#initialisation-safety "mention") for more information about how this may be handled in future.
{% endhint %}

## With Platform GUI (`withGUI`)

{% embed url="https://pub.dev/documentation/fmtc_plus_sharing/latest/fmtc_plus_sharing/FMTCImportSharingModule/withGUI.html" %}

## With A Known `File` (`manual`)

{% embed url="https://pub.dev/documentation/fmtc_plus_sharing/latest/fmtc_plus_sharing/FMTCImportSharingModule/manual.html" %}

## Collision/Conflict Resolution

In the event that a store with the same name already exists as the store that is trying to be imported, FMTC has only simple conflict resolution behaviour.

When a collision is detected, the defined callback `collisionHandler` is called asynchronously, with the filename of the import file in addition to the real name of the contained store. It can return either:

* `true`: Override the _entire_ existing store and its contents
* `false`: Skip/cancel the import
