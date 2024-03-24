# Initialisation

FMTC relies on a self-contained 'environment', called a [backend](backends.md), that requires initialisation (and configuration) before it can be used. This allows the backend to start any necessary seperate threads/isolates, load any prerequisites, and open and maintain a connection to a database. This environment/backend is then accessible internally through a(\*[^1]) singleton, so initialisation is not required again.

## Initialisation

Initialisation should be performed before any other FMTC or backend methods are used, and so it is usually placed just before `runApp`, in the `main` method. This shouldn't have any significant effect on application startup time.

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

## Uninitialisation

It is also possible to un-initialise FMTC and the current backend. This should be rarely required, but can be performed through the `uninitialise` method of the backend if required. Initialisation is possible after manual uninitialisation.

[^1]: Internally, more than one singleton may be used in a backend, and to access a backend. However, this is beyond the scope of this page.
