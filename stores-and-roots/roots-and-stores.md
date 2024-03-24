# Introduction

FMTC uses a _root_ and _stores_ to structure its data.

There is generally a single root (which generally corresponds to a single [backend](../general/initialisation.md#backends)), which contains multiple stores. Cached tiles can belong to multiple stores, which keeps duplication minimized.

{% hint style="warning" %}
The structures use the ambient backend when a method is invoked on it, not at construction time.

Therefore, it is possible to construct an `FMTCStore`/`FMTCRoot` (see below) before initialisation, but 'using' it will throw `RootUnavailable`.
{% endhint %}
