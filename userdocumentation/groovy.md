---
layout: page
title: User-Documentation
nav: false
---

---
[Introduction](/userdocumentation.html) &nbsp;&nbsp; [Execution Logger](executionlogger.html) &nbsp;&nbsp; Groovy

---
&nbsp;

## Introduction to Groovy

Groovy is an object-oriented language that is very similar to Java; most valid Java code is also valid Groovy code. With Groovy, complex coding can be achieved within a DialogOS graph.

More information about how to code in Groovy can be found here: http://groovy-lang.org/index.html

## Global Functions and variables

### Global Variables

DialogOS provides two options for global variables; those which can only be used and changed in Groovy code, and those which can be used and changed both in Groovy code and the in-house Script. The reason for this difference is that the in-house script code is limited to only a few types of variables, while Groovy code can use any Object - the user could hypothetically even create their own Object class in a Groovy node and save it to the Groovy variables. The type of global variables which are not Groovy-specific cannot be changed in Groovy script; an error will occur. It is, however, possible to change the type of a Groovy-exclusive global variable in the code. These global variables can be found under the tab "Graph" under "Variables" and "Groovy Variables".

The following two images show the global variables the global Groovy variables, respectively, for the following example:

![](https://gogs.mafiasi.de/05koehn/dialogossose17/src/master/pictures/groovy_pictures/groovy_1.PNG)
![](https://gogs.mafiasi.de/05koehn/dialogossose17/src/master/pictures/groovy_pictures/groovy_2.PNG)

This image shows the first Groovy node in the graph, in which we initialize the Groovy variable responseMap, since it is not possible to initialize Groovy variables outside of the graph.

![](https://gogs.mafiasi.de/05koehn/dialogossose17/src/master/pictures/groovy_pictures/groovy_4.PNG)

### Global Functions

Groovy global functions can be accessed in the "Graph" tab, under "Global Groovy Functions". These functions can be used in any Groovy Node on the graph. The program makes these functions useable simply by adding the code from the global script  to the top of the code within every Groovy node when the node is run. This code is therefore run at the beginning of every Groovy node. Thus, it is not advisable to change global variables within the global Groovy code (outside an uncalled function) unless these variables should be reset at the beginning of every groovy node. 

The following images shows the global Groovy functions that will be used in the graph:
![](https://gogs.mafiasi.de/05koehn/dialogossose17/src/master/pictures/groovy_pictures/groovy_3.PNG)

## Multiple Edges
It is possible to have multiple outgoing edges from a Groovy node. The program determines which of these edges to traverse based on the return value of the Groovy script. The return value is given either through a return statement or is the value of the last statement run in the Groovy node. If the return value does not match the value of any of the edges, the default edge (which cannot be deleted) will be chosen. The value of an edge should never be empty or the same as another outgoing edge of the same node.

The node in the following image has multiple edges. The first line in the node references the global Groovy function updateResponses. We may assume that the node previous to this node received an input, newResponse, from the user. As seen in the global Groovy functions code above, this function adds the response to the HashMap mapResponse and increases the variable currentNumResponses by one. After this function returns, if the variables currentNumResponses and maxNumResponses are not equal, the node will traverse the default edge, which leads to a different node to receive a new input from the user, and then returns to the node pictured. This will continue until currentNumResponses and maxNumResponses are equal, and thus "done" will be returned, and the other edge will be traversed.
![](https://gogs.mafiasi.de/05koehn/dialogossose17/src/master/pictures/groovy_pictures/groovy_5.PNG)

