# Backends

{% hint style="info" %}
This page covers more advanced FMTC usage, and is not appropriate for beginners or simple use cases.

TLDR; FMTC provides a single storage mechanism by default, named `FMTCObjectBoxBackend`.
{% endhint %}

***

FMTC supports attachment of any custom storage mechanism, through an `FMTCBackend`. This allows users to pick their favourite database engine, or conduct in-memory testing.

{% hint style="success" %}
Only one backend is built-into FMTC: the `FMTCObjectBoxBackend`. This backend uses the [ObjectBox library](https://pub.dev/packages/objectbox) to store data.
{% endhint %}

> More info coming soon...
