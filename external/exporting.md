# Exporting

The `export()` method copies the stores, along with all necessary tiles, to a seperate archive at the specified location (creating it if non-existent, overwriting it otherwise), in the FMTC (.fmtc) format.

```dart
await FMTCRoot.external('~/path/to/file.fmtc').export(['storeName']);
```
