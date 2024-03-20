# 1️⃣ Initialisation

FMTC [backends](backends.md) require initialisation before they can be used, to allow them to start necessary background threads, load required resources, and connect to databases. FMTC and backends work using singletons, so after the initial initialisation, it should not be required again.

This should be performed before any other FMTC or backend methods are used, and so it is usually placed just before `runApp`, in the `main` method. This shouldn't have any significant affect on application startup time.

{% hint style="warning" %}
If initialising in the `main` method before `runApp` is called, ensure you also call `WidgetsFlutterBinding.ensureInitialised()` prior to the backend initialisation.
{% endhint %}

<pre class="language-dart" data-title="main.dart"><code class="lang-dart">import 'package:flutter/widgets.dart';
import 'package:flutter_map_tile_caching/flutter_map_tile_caching.dart';

Future&#x3C;void> main() async {
    WidgetsFlutterBinding.ensureInitialized();   
    
    try {
<strong>        await FMTCObjectBoxBackend().initialise(...); // The default/built-in backend
</strong>    } catch (error, stackTrace) {
        // See below for error/exception handling
    }
    
    // ...
    
    runApp(MyApp());
}
</code></pre>

{% hint style="danger" %}
Do not call any other FMTC methods before initialisation. Doing so will cause a `RootUnavailable` error to be thrown.
{% endhint %}

{% hint style="danger" %}
Do not attempt to initialise the same backend multiple times, or initialise multiple backends simultaenously. Doing so will cause a `RootAlreadyInitialised` error to be thrown.
{% endhint %}

{% hint style="warning" %}
Avoid using FMTC in a seperate thread/`Isolate`. FMTC backends already make extensive use of multi-threading to improve performance.

If it is essential to use FMTC in a seperate thread, ensure that the initialisation is called in the thread where it is used. Be cautious of using FMTC manually across multiple threads simultaneously, as backends may not properly support this, and unexpected behaviours may occur.
{% endhint %}

## Exception Handling

FMTC methods may throw errors when a precondition isn't met or the operation failed - either due to incorrect usage (which are usually descended from type `FMTCBackendError`), or a backend failure (such as a database reaching it's maximum size limit).

These exceptions may be caught using standard `try`/`catch` blocks; it's not usually recommended to catch `FMTCBackendError`s - [see this post for more information](https://groups.google.com/a/dartlang.org/g/misc/c/lx9CXiV3o30/m/s5l\_PwpHUGAJ) about the difference between `Exception`s and `Error`s.

{% hint style="info" %}
FMTC automatically adjusts and changes the thrown `StackTrace` to include useful additional info, and ensures that the trace is followed across the many isolates and asynchronous gaps (eg. streams) of the FMTC internals.
{% endhint %}

### During `initialise`

One particular place where exceptions can occur more frequently is during initialisation. The code sample above includes a `try`/`catch` block to catch these errors. If an exception occurs at this point, it's likely unrecoverable (for example, it might indicate that the underlying database has been corrupted), and the best course of action is often to manually delete the FMTC root directory from the filesystem.

The default directory can be found and deleted with the following snippet (which requires 'package:path' and 'package:path\_provider':

```dart
import 'dart:io';

import 'package:path/path.dart' as path;
import 'package:path_provider/path_provider.dart';

final dir = Directory(
  path.join(
    (await getApplicationDocumentsDirectory()).absolute.path,
    'fmtc',
  ),
);

await dir.delete(recursive: true);

// Then reinitialise FMTC
```
