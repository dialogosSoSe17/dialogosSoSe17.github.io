---
layout: page
title: Developer-Documentation
nav: false
---

---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp; [Architecture](architecture.html) &nbsp;&nbsp; Execution Logger &nbsp;&nbsp; [Gradle](gradle.html) &nbsp;&nbsp; [Groovy](groovy.html) &nbsp;&nbsp; [Localization](localization.html) &nbsp;&nbsp; [MaryTTS](marytts.html)  &nbsp;&nbsp; [Vocon](vocon.html)


---
&nbsp;


## Execution Logger Implementation
With the [Execution Logger](TODO add link) it is possible to log the execution of a graph to a XML file. This is realized with the class `ExecutionLogger`. Logging can be switched on and off in the Run Configurations (default is off). This setting is saved in the `Preferences` class as well as the path where the log is saved. The default path is */.dialogOS/logs/* in the user home directory. 


### How the log works
The `ExecutionLogger` is being created in `SingleDocument.execute()` and then gets passed as a parameter to `Graph.execute()` and through the `execute()` methods implemented in the different nodes. The `saveDocAsXML()` method gets called in `SingleDocument.execute()` in the finally block, so the XML file will definitely be saved after the graph ran succesfully or an exception occured while executing.

The XML document is build using [jdom 2](http://www.jdom.org/), a tool to build and output XML files in Java. The XML tag names are saved as class constants to minimize chances of spelling mistakes.

### What gets logged
#### Variables
##### Initial Variables
The method `logInitialVariables()` logs variables to the `global_variables` element in the setup element of the document. So this method is just called on start of execution in `Graph.execute()`.
##### Updated Variables
If any global variable is being changed, this gets logged. This is being realized by calling the method `logUpdatedVariable()` in a ChangeListener that gets added to every variable.

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
*At the moment the validation is disabled because of conflicts between Jing and the MaryTTS plugin. (Presumably MaryTTS tries to use Jing as a XML validator which results in a crash while starting DialogOS.)*
```
Error at xsl:strip-space on line 36 of :
   XTSE0280: Element name *|text() is not a valid QName
   marytts.exceptions.MaryConfigurationException: Cannot start MARY server
```
*Similar issue: <https://github.com/marytts/marytts/issues/455>
If the conflict is removed, the validation can be enabled again by setting `_validationEnabled` in `ExecutionLogger` to true and uncommenting the import of Jing in the `build.gradle` of Diamant.*

To guarantee that the outputs are consistent the XML document gets validated against a XML schema before saving. The schema is written in [RELAX NG Compact](http://www.relaxng.org/compact-tutorial-20030326.html).
The document is validated using [Jing](https://github.com/relaxng/jing-trang), a tool that can use RELAX NG Compact Schemas to validate XML files in Java. If a document does not pass this validation it does not get saved.

#### XML Schema (in RELAX NG Compact)
```
start = Log
Log = element log { Setup, Execution }
Setup = element setup { Project, Start, Global_variables }
Project =
	element project { 
		attribute name { text }
	}
Start =
	element start {
		attribute date { text },
		attribute time { text }
	}
Global_variables = element global_variables { Var* }
Var = 
	element var {
		Var_attr
	}
Var_attr = 
	attribute name { text },
	attribute value { text },
	attribute type { text },
	attribute is_groovy_only { text }

Execution = 
	element execution { 
		Graph 
	}
Graph = ( Node | Variable_updated | Error )*
Node = 
	element node {
		attribute name { text },
		attribute type { text },
		attribute transition_time_ms { xsd:nonNegativeInteger },
		Global_variables?,
		Graph?
	}
Variable_updated = 
	element variable_updated {
		Var_attr
	}
Error = 
	element error {
		attribute name { text },
		attribute source { text },
		attribute message { text },
		attribute transition_time_ms { xsd:nonNegativeInteger }
	}
```






