---
layout: page
title: Developer-Documentation
nav: false
---

---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp; [Architecture](architecture.html) &nbsp;&nbsp; Execution Logger &nbsp;&nbsp; [Gradle](gradle.html) &nbsp;&nbsp; [Groovy](groovy.html) 

---
&nbsp;

## Execution Logger Implementation
With the [Execution Logger](TODO add link) it is possible to log the execution of a graph to a XML file. This is realized with the class `ExecutionLogger`. Logging can be switched on and off in the Run Configurations (default is off). This setting is saved in the `Preferences` class as well as the path where the log is saved. The default path is */.dialogOS/logs/* in the user home directory. 


### How the log works
The `ExecutionLogger` gets created in `SingleDocument.execute()` and then gets passed to `Graph.execute()` and through the nodes execute methods as a parameter. The `saveDocAsXML()` method gets called in `SingleDocument.execute()` in the finally block, so the log will definitely be saved after the graph ran succesfully or an exception occured while executing.

The XML document is build using [jdom 2](http://www.jdom.org/), a tool to build and output XML files in Java. The XML tag names are saved as class constants to minimize chances of spelling mistakes.

### What gets logged
#### Variables
##### Initial Variables
The method `logInitialVariables()` logs variables to the `global_variables` element in the setup element of the document. So this method is just called on start of execution in `Graph.execute()`.
##### Updated Variables
If any global variable gets changed, this gets logged. This is being realized by calling the method `logUpdatedVariable()` in a ChangeListener that gets added to every variable.

#### Nodes
If the execute method in a node gets called (the graph flow reaches the node), the first line of `execute()` should be:
```java
logNode(logger);
```
This calls the method `logNode()` in Node which calls `logNode()` in the ExecutionLogger.
##### Subgraph Node
If a node is a GraphNode, not `logNode()` but `logGraphNode()` gets called. The global variables declared in the Subgraph get added to the GraphNode element as well as all the nodes in a GraphNode.

#### Exceptions
If an exception occurs while executing the graph, a `NodeExecutionException` gets thrown. The `ExecutionLogger` should be passed to the exception, so it will be logged. The method `logException()` in the `ExceptionLogger` gets called by the constructor of the `NodeExecutionException`.

### Validation
To guarantee that the outputs are consistent the XML document gets validated against a XML schema before saving. The schema is written in [RELAX NG Compact](http://www.relaxng.org/compact-tutorial-20030326.html) and can be found here: TODO insert link to log_schema.rnc
The document is validated using [Jing](https://github.com/relaxng/jing-trang), a tool that can use RELAX NG Compact Schemas to validate XML files in Java. If a document does not pass this validation it does not get saved.

*At the moment the validation is disabled, because of conflicts between Jing and the MaryTTS plugin. If the conflict is removed, the validation can be enabled again by setting `_validationEnabled` in `ExecutionLogger` to true and uncommenting the import of Jing in the `build.gradle` of Diamant.*
