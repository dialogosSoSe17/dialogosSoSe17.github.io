---
layout: page
title: Developer-Documentation
nav: false
---

---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp; [Architecture](architecture.html) &nbsp;&nbsp; [Execution Logger](executionlogger.html) &nbsp;&nbsp; [Gradle](gradle.html) &nbsp;&nbsp; Groovy &nbsp;&nbsp; [Localization](localization.html) &nbsp;&nbsp; [Vocon](vocon.html)


---
&nbsp;

## Introduction to Groovy

Groovy is an object-oriented language that is very similar to Java; most valid Java code is also valid Groovy code. With Groovy, complex coding can be achieved within a DialogOS graph.

More information about how to code in Groovy can be found [here](http://groovy-lang.org/index.html)

## Groovy Node Implementation
The code within a [Groovy Node](TODO: add link) is run when the graph reaches the Groovy Node and the execute() function of the node is called. Here, a new [GroovyShell](http://docs.groovy-lang.org/latest/html/api/groovy/lang/GroovyShell.html) is created. A [Binding](http://docs.groovy-lang.org/latest/html/api/groovy/lang/Binding.html) for the shell is created and all of the graph's global variables - both those specifically for Groovy and those that can be used both by Groovy and the in-house Script code - are added to it. The global Groovy functions are appended to the beginning of the Groovy Node's script. The resulting script is then run using the function evaluate() of the GroovyShell, which returns an Object. This return value is  used to determine which outgoing edge the graph should traverse next. If the return value, when converted to a String, matches the labels of any of the outgoing edges, that edge will be traversed. Otherwise, the default edge will be traversed.

The global variables are then retrieved from the binding of the GroovyShell. The code iterates through the list of the (old) global variables. If the value of a global variable in the new list is different than in the old list, the variable is updated with the new value. If the type of a (non-Groovy-exclusive) variable has been changed, an exception will be thrown. The type of a Groovy-only variable, however, may be changed freely in the code.

## Global Functions and variables

### Global Variables

DialogOS provides two options for global variables; those which can only be used and changed in Groovy code, and those which can be used and changed both in Groovy code and the in-house Script. The reason for this difference is that the in-house script code is limited to only a few types of variables, while Groovy code can use any Object - the user could hypothetically even create their own Object class in a Groovy node and save it to the Groovy variables. The type of global variables which are not Groovy-specific cannot be changed in Groovy script; an exception will be thrown if this attempted. It is, however, possible to change the type of a Groovy-exclusive global variable in the code. Currently, it is not possible to initialize the Groovy-only variables when first creating them; they must be declared in the Groovy variables window and initialized at some point in the graph.

### Global Functions

Groovy global functions can be accessed in the "Graph" tab, under "Global Groovy Functions". These functions can be used in any Groovy Node on the graph. The program makes these functions useable simply by adding the code from the global script  to the top of the code within every Groovy node when the node is run. This code is therefore run at the beginning of every Groovy node. Thus, it is not advisable to change global variables within the global Groovy code (outside an uncalled function) unless these variables should be reset at the beginning of every Groovy node. A possible area for improvement in the implementation of Groovy code within DialogOS could be making these global functions accessible to all Groovy nodes without having to run this code before each Groovy node.

## Multiple Edges
It is possible to have multiple outgoing edges from a Groovy node. The program determines which of these edges to traverse based on the return value of the Groovy script. The return value is given either through a return statement or is the value of the last statement run in the Groovy node. If the return value does not match the value of any of the edges, the default edge (which cannot be deleted) will be chosen. The value of an edge should never be empty or the same as another outgoing edge of the same node.

### The Groovy Node Editor

[NodePropertiesDialog](TODO: add link), the JDialog used to edit a node, is created in the method editProperties of the abstract class [Node](TODO: add link). This method calls an abstract method of Node, createEditorComponent, that is implemented by each class which implements Node, and which returns a Container to be used to create the NodePropertiesDialog for the node. GroovyNode's implementation of this function returns a JTabbedPane with two tabs: one for editing Groovy script, and one for editing the outgoing edges of the GroovyNode.

The tab for editing Groovy script is created in the function createGroovyScriptEditor of NodePropertiesDialog. This editor contains an [RSyntaxTextArea](http://bobbylight.github.io/RSyntaxTextArea/) that provides syntax editing for Groovy script.

The tab for editing the outgoing edges is created in the function createOutgoingEdgesEditor in NodePropertiesDialog.

## Groovy in the speech synthesis (TTSNode)
Beside the Text and Expression (in the DialogOS script language) option, there is an Groovy script option where a speech output can be created using Groovy script. The evaluation works in the same way as the Groovy node. Global Groovy functions and variables can be accessed as well as the non-Groovy global variables. The evaluation result of the script is passed to the speech synthesis and must be a String. The evaluation result of a Groovy script is the result of the last line of the script or the return value passed after a return statement.



