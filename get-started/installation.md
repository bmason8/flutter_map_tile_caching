# Installation

{% hint style="warning" %}
**FMTC is licensed under GPL-v3.**

If you're developing an application that isn't licensed under GPL, this affects you and your application's legal right to distribution. For more information, please see [#proprietary-licensing](../#proprietary-licensing "mention").
{% endhint %}

{% hint style="success" %}
Looking to start using FMTC in your project? Check out the [quickstart.md](quickstart.md "mention") guide!
{% endhint %}

## Depend On

### From [pub.dev](https://pub.dev/packages/flutter\_map\_tile\_caching)

This is the recommended method of installing this package as it ensures you only receive the latest stable versions, and you can be sure pub.dev is reliable.

Just import the package as you would normally, from the command line:

```shell
flutter pub add flutter_map_tile_caching
```

### From [github.com](https://github.com/JaffaKetchup/flutter\_map\_tile\_caching)

If you urgently need the latest version, a specific branch, or a specific fork, you can use this method.

{% hint style="info" %}
Commits available from Git (GitHub) may not be stable. Only use this method if you have no other choice.
{% endhint %}

First, add the normal dependency following the [#from-pub.dev](installation.md#from-pub.dev "mention") instructions. Then, add the following lines to your pubspec.yaml file under the `dependencies_override` section:

{% code title="pubspec.yaml" %}
```yaml
dependency_overrides:
    flutter_map_tile_caching:
        git:
            url: https://github.com/JaffaKetchup/flutter_map_tile_caching.git
            # ref: a commit hash, branch name, or tag (otherwise defaults to master)
```
{% endcode %}

## Import

After installing the package, import it into the necessary files in your project:

```dart
import 'package:flutter_map_tile_caching/flutter_map_tile_caching.dart';
// You'll also need to import flutter_map and (likely) latlong2 seperately
```

{% hint style="success" %}
Also ensure you've followed flutter\_map's installation instructions!
{% endhint %}
