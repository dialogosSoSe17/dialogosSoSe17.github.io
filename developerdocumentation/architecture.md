---
layout: page
title: Developer-Documentation
nav: false
---

---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp;  Architecture &nbsp;&nbsp; [Execution Logger](executionlogger.html) &nbsp;&nbsp; [Gradle](gradle.html) &nbsp;&nbsp; [Groovy](groovy.html) &nbsp;&nbsp; [Localization](localization.html)

---
&nbsp;

## Project Architecture

This page gives a brief overview of the DialogOS project architecture. This is the project dependency graph, excluding external dependencies:

[![](/pictures/dependencies.png)](/pictures/dependencies.png)

The `Diamant` project contains the DialogOS main class as well as the application's user interface.

For historical reasons, the speech recognition and synthesis components are DialogOS plugins that depend on the `Diamant` package.

The "Client" paradigm exists for historical reasons as well. It encapsulates the connection of Java code with the native speech recognition and synthesis software and is not needed anymore as these components are pure Java in the open source version of DialogOS.

## Make your own Plugin

The DialogOS plugin architecture uses the [Java ServiceLoader](https://docs.oracle.com/javase/8/docs/api/java/util/ServiceLoader.html) mechanism. The closed source version of DialogOS implemented its own custom plugin system (which was very similar to ServiceLoader) because ServiceLoader wasn't introduced until Java 6. We exchanged the custom system with Java's implementation to benefit from its stability and in order to remove custom classes that dealt with loading of `.jar` files. The previous system's functionality of loading encrypted `.jar`s is not needed anymore in the open source version of DialogOS.

Plugins need to implement the `com.clt.dialogos.plugin.Plugin` interface and place a provider-configuration file with the same name in their `META-INF/services` resources directory.

A basic plugin that is [built with Gradle](gradle.html) has the following structure:

```
myplugin/
  src/main/
    java/...
      MyPlugin.java
    resources/META-INF/services/
      com.clt.dialogos.plugin.Plugin
  build.gradle
```

To be loaded as a plugin, these requirements have to be met:
- The `MyPlugin` class implements the `Plugin` interface.
- `MyPlugin` needs a zero-argument constructor that will be called when loading the plugin.
- The provider-configuration file contains the fully qualified class name of the `MyPlugin` class.
- The plugin `.jar` is in the classpath when launching DialogOS

Any costly setup (like starting a text-to-speech server) should take place in the `initialize()` method which is called immediately by the plugin loader. Do not perform costly operations upon loading the class to ensure that the program is responsive at all times. Static resources should be initialized as [lazy-loaded singletons](https://en.wikipedia.org/wiki/Initialization-on-demand_holder_idiom).

The `terminate()` method is called on all loaded plugins when DialogOS quits. Perform any teardown or cleanup operations in your implementation of this method.

All plugins have to provide an identifier, name, icon, version number as well as a non-null settings screen. Empty default implementations are provided for the `initialize()` and `terminate()` methods of the `Plugin` interface.

