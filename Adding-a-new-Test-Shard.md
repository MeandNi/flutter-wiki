## Requirements for a Flutter/LUCI build

A general outline of the requirements that a Flutter CI test shard has:

1. On LUCI, test shards map to builders. Each test shard must have its own LUCI builder. For the Framework, these are defined in [flutter/infra](https://github.com/flutter/infra/blob/master/config/framework_config.star). Generally you will need to have both a pre-submit ("try" in LUCI terminology) builder and a post-submit ("prod") builder.
1. This LUCI builder will specify a "recipe" to run. These are [starlark](https://github.com/bazelbuild/starlark) scripts that determine the actual CI steps to run, and are defined in [flutter.googlesource.com/recipes](https://flutter.googlesource.com/recipes). Most Framework tests use the [flutter/flutter_drone.py](https://flutter.googlesource.com/recipes/+/refs/heads/master/recipes/flutter/flutter_drone.py) recipe.
1. Entries in [try_builders.json](https://github.com/flutter/flutter/blob/master/dev/try_builders.json) and [prod_builders.json](https://github.com/flutter/flutter/blob/master/dev/prod_builders.json). These files are read by [Flutter's build dashboard](https://flutter-dashboard.appspot.com/#/build), and are used for scheduling pre-submit builds.

## Steps to add a new Framework Test Shard

It is important to land these changes in order to prevent any failing builds during the migration period:

1. Framework tests are run by a Dart test runner called [test.dart](https://github.com/flutter/flutter/blob/master/dev/bots/test.dart) that lives in the framework repository. Any new test shards must first be added to this file. Merge this framework change.
1. Next, add pre-submit ("try") and post-submit ("prod") builders to [flutter/infra](https://github.com/flutter/infra/blob/master/config/framework_config.star). More detailed instructions [in the flutter/infra README](https://github.com/flutter/infra#adding-new-framework-test-shards). Ensure that the "shard" and "subshard"/"subshards" properties match what was added to test.dart in the previous step. Merge this infra change.
1. Update [try_builders.json](https://github.com/flutter/flutter/blob/master/dev/try_builders.json) and [prod_builders.json](https://github.com/flutter/flutter/blob/master/dev/prod_builders.json) in the Framework tree to include the newly added builder. Verify that the entry in `prod_builders.json` is marked as flaky. New shards should always be marked as flaky and verified to be passing on master before being marked un-flaky. When opening this PR, a pre-submit check for the new test shard should be triggered. Merge this framework change.
1. Monitor the CI results of the new shard on the [Flutter build dashboard](https://flutter-dashboard.appspot.com/#/build). After 10 consecutive passing builds, you can remove the flaky parameter from `prod_builders.json` in the Framework tree. Merge this framework change.