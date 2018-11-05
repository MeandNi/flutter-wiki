Several of our dependencies are automatically rolled (updated) by bots.

## Skia to Engine

We use an auto-roller for Skia rolls. It's status can be viewed at <https://skia-flutter-roll.skia.org/>. In case of  build failures or other errors, ping the Flutter-Skia chat channel. In case you get no response, you can login with an @google.com account and pause the roller (or ask someone with an @google.com account to do so). Please specify a descriptive reason and file a bug to re-enable the rollers as soon as possible.

The bot updates the `skia_revision` line of <https://github.com/flutter/engine/blob/master/DEPS>.

Skia also uses an auto-roller for Fuchsia; see <https://fuchsia-roll.skia.org/>.

## Engine to Framework

The engine is automatically rolled to the framework.

The bot updates <https://github.com/flutter/flutter/blob/master/bin/internal/engine.version> to point to the latest revision of the engine whose artifacts built successfully.