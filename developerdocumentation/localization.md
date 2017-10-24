---
layout: page
title: Developer-Documentation
nav: false
---

---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp;  [Architecture](architecture.html) &nbsp;&nbsp; [Execution Logger](execution-logger-implementation.html) &nbsp;&nbsp; [Gradle](gradle.html) &nbsp;&nbsp; [Groovy](groovy.html) &nbsp;&nbsp; Localization &nbsp;&nbsp; [MaryTTS](marytts.html)  &nbsp;&nbsp; [Vocon](vocon.html)


---
&nbsp;

## Localization

This pages gives a brief overview of localization workflow for DialogOS.

We want to make this software avaible for everyone, especially for schools.
To make this easier, we use the localization platform [PhraseApp](https://phraseapp.com)

This makes it possible to deploy new langugaes or fix translation mistakes.

If you want to help us out, just create a free PhraseApp account and send us your username to vincent.dahmen@informatik.uni-hamburg.de.

We will than add you to the project, where you can start translating.

### Provide new keys
If you want to add new keys (which have to be translated) to the project, simply add them into the corresponding ressource file.

To start the upload, use the [PhraseApp CLI tool](https://phraseapp.com/cli) and do a `phraseapp push` in the source directory.
DO NOT CHANGE THE CONFIGURATION FILE!


