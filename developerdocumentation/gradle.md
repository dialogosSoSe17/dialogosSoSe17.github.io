---
layout: page
title: Developer-Documentation
nav: false
---

---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp; [Architecture](architecture.html) &nbsp;&nbsp; [Execution Logger](executionlogger.html) &nbsp;&nbsp; Gradle &nbsp;&nbsp; [Groovy](groovy.html) &nbsp;&nbsp; [Localizaiton](localization.html)


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

### Gradle Setup

DialogOS is set up as a [Multi-project Build](https://docs.gradle.org/4.0/userguide/multi_project_builds.html). Its directory structure looks like this:

```
dialogos/
  ClientInterface/
    src/
    build.gradle
  com.clt.audio/
    src/
    build.gradle
  ...
  build.gradle
  settings.gradle
```

Each subproject defines its own dependencies in its `build.gradle` file. Note that some of the subprojects run the lexer generator [JFlex](http://jflex.de) and the parser generator [cup](http://www2.cs.tum.edu/projects/cup/) as [ant tasks](https://docs.gradle.org/4.0/userguide/ant.html).

The root directory's `build.gradle` contains common configuration and defines all subprojects as its dependencies (so that everything gets build with the root `build` task). The root project also uses the `application` plugin that configures the `run` task.

`settings.gradle` contains a list of all subproject names.

### Building a single project

To build a single project, either run:

```
./gradlew PROJECT_NAME:build
```

or switch in the respective directory and run (with the correctly adapted path to the `gradlew` executable):

```
../gradlew build
```

### Other Gradle Tasks

This command shows a full list of available tasks:

```
./gradlew tasks
```

Some notable tasks include:
- `shadowJar`: generates a "fat jar" to `build/libs/dialogos-all.jar` using the [Gradle Shadow plugin](https://github.com/johnrengelman/shadow) that contains the DialogOS application with all dependencies and can be distributed and launched with `java -jar`
- `allJavadoc`: generates Javadoc for all projects
- `downloadLicenses`: generate a license report with the [License Gradle Plugin](https://github.com/hierynomus/license-gradle-plugin)

