---
layout: page
title: User-Documentation
nav: false
---

---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp; Execution Logger &nbsp;&nbsp; [Groovy](groovy.html) 

---
&nbsp;

## Execution Logger
In DialogOS it is possible to log the execution of a graph as an XML file. To do this you need to go to *Dialog > Run Configuration* and tick the *"Save Log File"* checkbox. The path where the XML file will be saved can also be set there.
The file name of of the log contains the date and time of execution and the project name:
YYYY-MM-DD_HH-MM-SS_ProjectName.xml

### Log components
#### Header
The header includes the name of the project, the date and time when the graph was executed and all global variables of the main graph with their name, value and type. 
```xml
<setup>
    <project name="ProjectName.xml"/>
    <start date="2017-06-27" time="15:45:53"/>
    <global_variables>
        <var name="x" value="5" type="int"/>
    </global_variables>
</setup>
```
#### Nodes
When the graph execution reaches a node, the node gets logged with its name, the type of the node and the transition time. The transition time is displayed in miliseconds relative to the start time and measured before the node gets executed.
```xml
<node name="Start" type="com.clt.diamant.graph.nodes.StartNode" transition_time_ms="4"/>
```
##### Subgraph Nodes
A special node is the subgraph node. Global variables declared in a subgraph are logged as an element in the subgraph node as well as all the nodes within the subgraph. 
```xml
<node name="Subgraph" type="com.clt.diamant.graph.nodes.GraphNode" transition_time_ms="20">
    <global_variables>
        <var name="y" value="25" type="int"/>
    </global_variables>
    <node name="Start" type="com.clt.diamant.graph.nodes.StartNode" transition_time_ms="21"/>
    ...
    <node name="Return" type="com.clt.diamant.graph.nodes.ReturnNode" transition_time_ms="426"/>
</node>
```

#### Variable changes
If a global variable is set to a new value, a variable_updated element is being added to the execution tab containing a name, value and type attribute. If the value of a global variable is being changed multiple times in a Groovy node, just the last change is being added to the log.
```xml
<variable_updated name="x" value="12" type="int"/>
```

#### Exceptions
If an exception occurs while executing the graph, an exception element is being added to the execution tab with the source and message of the exception. 
```xml
<error name="NodeExecutionException" transition_time_ms="29" source="Groovy" message="Can't change type of global variables in Groovy script"/>
```

### Validation
Before saving the XML file is being validated against a [RELAX NG Compact](http://www.relaxng.org/compact-tutorial-20030326.html) schema. The validation is a requirement for the saving of the log. So every execution log created by DialogOS satisfies this schema. You can find the schema for the execution log below.

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

