---
layout: page
title: Developer-Documentation
nav: false
---

---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp; [Architecture](architecture.html) &nbsp;&nbsp; [Execution Logger](executionlogger.html) &nbsp;&nbsp; Gradle &nbsp;&nbsp; [Groovy](groovy.html) &nbsp;&nbsp; [Localization](localization.html) &nbsp;&nbsp; [MaryTTS](marytts.html)  &nbsp;&nbsp; [Vocon](vocon.html)


---
&nbsp;

## Building DialogOS with Gradle

DialogOS is built with the [Gradle Build Tool](https://gradle.org) using the [Gradle Wrapper](https://docs.gradle.org/4.0/userguide/gradle_wrapper.html). To build and run DialogOS, first make sure you have Java 8.

On Linux and macOS, execute:

```
./gradlew run
```

or analogously on Windows:

```
gradlew.bat run
```

The Gradle Wrapper script will download and install a local copy of Gradle, if needed, and then build and run the application.

When configuring the DialogOS project in an IDE, enter `run` as the Gradle task in the build settings.

### Our Gradle Setup

DialogOS is set up as a [Gradle Multi-project Build](https://docs.gradle.org/4.0/userguide/multi_project_builds.html). It was migrated from [Apache Ant](http://ant.apache.org) to Gradle to profit from the [Gradle DSL](https://docs.gradle.org/4.0/dsl/) and [plugin system](https://docs.gradle.org/4.0/userguide/plugins.html) as well as Gradle's flexibility and better Ant task support (needed for legacy dependencies) in comparison to [Maven](https://maven.apache.org), which is another common choice for current build tools. [This StackOverflow answer](https://stackoverflow.com/questions/1163173/why-use-gradle-instead-of-ant-or-maven/1165553#1165553) provides more information on the three build tools.

The Multi-project setup allowed us to leave the [modular project structure](architecture.html) unchanged:

```
dialogos/
  ClientInterface/
    src/
    build.gradle
  com.clt.audio/
    src/
    build.gradle
  com.clt.base/
    src/
    build.gradle
  ...
  build.gradle
  settings.gradle
```

There are around 15 Java modules in the project that were each converted to a Gradle subproject. A subproject defines its own dependencies in its `build.gradle` file. Note that some of the subprojects run the lexer generator [JFlex](http://jflex.de) and the parser generator [cup](http://www2.cs.tum.edu/projects/cup/) as [Ant tasks](https://docs.gradle.org/4.0/userguide/ant.html). The resulting parser and lexer classes are used for language model grammars as well as the internal scripting language, which will be superseded by [Groovy](groovy.html).

Almost all external dependencies that were previously distributed as `.jar` files were exchanged for updated versions that are available in the [Maven](http://maven.org) and [JCenter](https://bintray.com/bintray/jcenter) repositories. An exception is the JRendezvous (now named [JmDNS](http://jmdns.sourceforge.net)) package that is only available in newer versions that are incompatible with the project. The dependency should be updated or dropped in the future instead of shipping the outdated version.

The root directory's `build.gradle` contains common configuration and defines all subprojects as its dependencies (so that everything gets build with the root `build` task). The root project also uses the `application` plugin that configures the `run` task.

`settings.gradle` contains a list of all subproject names.

Due to the expressive Gradle DSL, the 2000+ lines of Ant `build.xml` files were condensed to roughly 200 lines of `build.gradle` files, even though [more useful tasks](#other-gradle-tasks) were added in the Gradle setup. Another key benefit of the transition to Gradle is the Gradle Wrapper that allows developers to work with the same version of the tool without any need for installation or configuration.

### Building a single subproject

To build a single module, either run:

```
./gradlew PROJECT_NAME:build
```

or switch in the respective directory and run (with the correctly adapted path to the `gradlew` executable):

```
../gradlew build
```

### Using an IDE

In your favorite IDE, import the DialogOS project as a Gradle project. In the gradle configuration, select the DialogOS root folder as the project to run. As the Gradle task, enter `run`.

[![](/pictures/idea-gradle-setup.png)](/pictures/idea-gradle-setup.png)

### Other Gradle Tasks

This command shows a full list of available tasks:

```
./gradlew tasks
```

Some notable tasks include:
- `shadowJar`: generates a "fat jar" to `build/libs/dialogos-all.jar` using the [Gradle Shadow plugin](https://github.com/johnrengelman/shadow) that contains the DialogOS application with all dependencies and can be distributed and launched with `java -jar`
- `allJavadoc`: generates Javadoc for all projects
- `downloadLicenses`: generate a license report with the [License Gradle Plugin](https://github.com/hierynomus/license-gradle-plugin)

