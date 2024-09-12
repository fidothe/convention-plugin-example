# Cross-subproject dependency problems

This repo is a trivial build demonstrating the problem I'm having applying custom precompiled script plugins in a precompiled script convention plugin.

The idea is that the `editorial-convention-plugin` applies the `com.saxonica.build.editorial` plugin and then defines the tasks needed.

The real use case for us with this is having multiple 'editions', each built by a subproject whose build logic is essentially identical, differing only in a few default values and some minor configuration of a couple of the tasks. This build logic uses several internal custom plugins (`.kt` files in `buildSrc/src/main/kotlin`) which are registered through buildSrc's `build.gradle.kts` and are used in a number of other subproject build scripts.

Currently gradle fails, complaining with:

```
> Task :buildSrc:generatePrecompiledScriptPluginAccessors FAILED

FAILURE: Build failed with an exception.

* Where:
Precompiled script plugin '/saxonica/convention-plugin-example/buildSrc/src/main/kotlin/editorial-convention-plugin.gradle.kts' line: 1

* What went wrong:
Plugin [id: 'com.saxonica.build.editorial'] was not found in any of the following sources:

- Gradle Core Plugins (plugin is not in 'org.gradle' namespace)
- Plugin Repositories (plugin dependency must include a version number for this source)
```
