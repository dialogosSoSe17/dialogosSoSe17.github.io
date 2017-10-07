---
layout: page
title: Developer-Documentation
nav: false
---

---
[Introduction](/developerdocumentation.html) &nbsp;&nbsp; [Architecture](architecture.html) &nbsp;&nbsp; [Execution Logger](executionlogger.html) &nbsp;&nbsp; [Gradle](gradle.html) &nbsp;&nbsp; [Groovy](groovy.html) &nbsp;&nbsp; [Localization](localization.html) &nbsp;&nbsp; MaryTTS &nbsp;&nbsp; [Vocon](vocon.html)


---
&nbsp;

## MaryTTS

1. [Introduction to MaryTTS](#introduction-to-marytts)

2. [Replacing with MaryTTS](#replacing-old-tts-with-marytts)

3. [Prototype](#prototype)

4. [Integration of voice packs](#integration-of-voice-packs)

5. [MaryXML](#maryxml)

6. [Left overs](#left-overs)

### Introduction to MaryTTS

MaryTTS is an open source text to speech synthesis platform that was implemented in DialogOS to replace the proprietary text to speech software from AT&T.

This documentation is mostly about the integration of MaryTTS, to find more information about MaryTTS itself, please refer to the the [official page](http://mary.dfki.de/documentation/index.html).

The current status is that the remodeled text to speech plugin completely works with MaryTTS, it's also possible to edit the properties of the MaryTTS output (speed, pitch etc.) along with a few more new possibilities e.g. an
automated MaryXML generation tool.

### Replacing old TTS with MaryTTS

#### Welcome MaryTTS-plugin!


### Analysis


### Prototype

After nearly two weeks of analyzing the original DialogOS, we've put together a small prototype of an integration of MaryTTS to find out how exactly it works which was built up on a few youtube and github tutorials.

The prototype consists of an `Audioplayer`, a sub class of the `Thread` class from java, which is used to play the output of MaryTTS from an `AudioInputStream` and a class `TextToSpeech`, which creates an instance of the `MaryInterface`, in this example called `marytts`, and the `AudioPlayer`. The audio for the AudoInputStream is created via  `marytts.generateAudio(String text)`. After asigning the audio to the `AudioInputStream` and setting the `AudioPlayer` to play it, the given String can be heard.

For MaryTTS to speak, a few extra jar files from the [MaryTTS github page](https://github.com/marytts/marytts) have to be downloaded, the easiest way to get those packages is to [download MaryTTS](https://github.com/marytts/marytts/releases) and to start the `marytts-component-installer`, from where you can access all supported voices and languages for MaryTTS.

[The YouTube tutorial](https://www.youtube.com/watch?v=OLKxBorVwk8) for further reference (link to the github in the description)

### Integration of voice packs

To include more voice packs for MaryTTS in the gradle project, they need to be noted in the build.gradle file of the 
MaryTTSClient like in this example for the english male voice:

```
compile group: 'de.dfki.mary', name: 'voice-cmu-slt-hsmm', version: '5.2'
```

This way, they will be included in the pull down menu in DialogOS to choose as you configure a TTS node.


###  MaryXML

MaryTTS uses his own XML scheme, which is needed to further configure the TTS process, i.e. change pitch, speed etc.
Since the original DialogOS had the option to edit those configurations and still has this external node, we needed to implement the MaryXML scheme ourselves. So the input format of MaryTTS was changed from any string to MaryXML.

To show the syntax of MaryXML, here's the example code from the [MaryTTS documentation](http://mary.dfki.de/documentation/maryxml/).

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<maryxml version="0.4"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns="http://mary.dfki.de/2002/MaryXML"
xml:lang="en">
<prosody rate="+20%" pitch="+20%" range="-10%" volume="loud">
This is something you have to see!
</prosody>
</maryxml>
```

This form allows for far further customization, i.e. changing the prosody settings or varying languages in one text.

**Note:** At the time of writing this, it is not possible to change the volume in the prosody settings. 

#### Prompt to MaryXML Tab

### Left overs

- Crashes (sometimes) on Linux when playing audio too frequently.



