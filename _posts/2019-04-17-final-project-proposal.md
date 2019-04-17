---
layout: post
title:  "Final Project Proposal"
date:   2019-04-17
categories: blogs
---
# Project: Percussive Flow

### Conceptual Description

Music visualizers generally fit into two categories: either they are rendered in advance for a specific song, or they react in live time to an audio input. For the latter, they often struggle to accurately convey the emotion of a song beyond its tempo/pulse and volume. This is especially true of a song's percussion, which is often stripped down to big bass and snare hits. For this piece, I hope to better represent the feelings behind each component of a drumkit, as well as the emotions behind certain styles of playing. It is also important that the piece reacts in live time, as this allows the user to visualize the music as they play it, adjusting their playing as they explore the various emotions that the piece can produce.

###Interaction Description

The user will interact with the piece by playing a TD-17KV electronic drumkit, which is connected to the laptop displaying the visualization. If the goal is to allow the audience to see the visualization, such as when I am playing it as a demo, then the visualization will be facing them. Otherwise, if the user is the one exploring the visualization, then the screen will be facing them. Ideally, the laptop will always be facing the user, while also being connected to a projector facing the audience. The intended audience is absolutely anybody who enjoys music or simply hitting things. The piece is incredibly simple to interact with and requires no skills in playing the drumkit to manipulate. However, those who do play may gain a greater appreciation for the emotions conveyed and an ability to create even more complex visualizations. Interaction drives the creation of the visualization, as there would be no emotion conveyed without it. Audience interaction and creative expression are themselves the idea behind the visualization they create.

### Technical Details

This visualization takes place entirely in Processing.js. I use the Midibus Processing library to interpret the MIDI data received from the TD-17 drum module. Each MIDI note includes a `pitch` value and a `velocity` value. Every pad on the e-kit has a unique `pitch`, such as 36 for the bass drum or 40 for a snare rim shot. The `velocity` simply measures how hard the pad was hit on a scale of 0-127. For the visualization itself, I plan to explore a variety of Processing libraries as I cycle through the many ideas floating around my head. I am almost certainly settled on using Tracer to create a mesh background that fills in as the note density increases. For the shapes that are produced by each pad, I plan to look at various geometry libraries such as ComputationalGeometry, Culebra, and Toxiclibs.js.

Because this piece is dependent on having a TD-17 drum module connected to the computer running it, I don't plan to host it online anywhere. Instead, I will create a well-documented github repository for anyone who wants to download it to their own machine and/or extend my work.

The code itself is structured very simply. With Midibus, I can quickly set up an object that takes in MIDI input from "TD-17" and does not send output anywhere:

```javascript
MidiBus myBus = new MidiBus(this, "TD-17", -1);
```

Then, everytime the MidiBus receives a new MIDI note, it calls the function `noteOn()`. Within this function I set `lastPitch` and `lastVelocity` to then be used in the next `draw()` call:

```javascript
void noteOn(int channel, int pitch, int velocity) {
  lastPitch = pitch;
  lastVelocity = velocity;
}
```

Lastly, I use the `draw()` function to update the visualization. This could be based on what was last played, how loudly it was played, how many notes have been played in a certain amount of time, if a pattern is detected, or any other number of variables. In a basic example, I draw a centered square whose color is based on the pad that was last hit and whose size is based on the velocity of the last hit:

```javascript
void draw() {
  float r = map(lastPitch, 22, 59, 0, 255);
  float g = map(lastPitch, 22, 59, 0, 50);
  float b = map(lastPitch, 22, 59, 0, 255);
  float w = map(lastVelocity, 0, 127, 0, width);
  float h = map(lastVelocity, 0, 127, 0, height);
  fill(r, g, b);
  rect(width/2, height/2, w, h);
}
```

In another basic example, I move a square around the screen based on the pitch and velocity of the last hit:

```javascript
void draw() {
  background(0);
  float r = map(globPitch, 22, 59, 0, 255);
  float g = map(globPitch, 22, 59, 0, 50);
  float b = map(globPitch, 22, 59, 0, 255);
  float x = map(globPitch, 22, 59, 0, width);
  float y = map(globVelocity, 0, 127, 0, height);
  fill(r, g, b);
  rect(x, y, 80, 80);
}
```

All of the code for this project will be held in my github repository [stonemathers/percussive-flow](https://github.com/stonemathers/percussive-flow).