---
layout: post
title:  "Percussive Flow"
date:   2019-04-23
categories: pieces
---

Music visualizers generally fit into two categories: either they are rendered in advance for a specific song, or they react in live time to an audio input. For the latter, they often struggle to accurately convey the emotion of a song beyond its tempo/pulse and volume. This is especially true of a song's percussion, which is often stripped down to big bass and snare hits. For this piece, I hope to better represent the feelings behind each component of a drumkit, as well as the emotions behind certain styles of playing. It is also important that the piece reacts in live time, as this allows the user to visualize the music as they play it, adjusting their playing as they explore the various emotions that the piece can produce.

This visualization takes place entirely in Processing.js. I use the Midibus Processing library to interpret the MIDI data received from the TD-17 drum module. Each MIDI note includes a `pitch` value and a `velocity` value. Every pad on the e-kit has a unique `pitch`, such as 36 for the bass drum or 40 for a snare rim shot. The `velocity` simply measures how hard the pad was hit on a scale of 0-127. 

For the visualization itself, the background uses the MeshRender class from the [Tracer](http://www.objectstothinkwith.com/tracer/) library to create a series of circular paths. Tracers follow these paths behind the scenes and, when two tracers are within a minimum distance of one another, a line is drawn between the two. As the the user plays more notes per second, the minimum distance determining these connections increases. As a result, as note density increases, the MeshRender begins to fill in the background. 

On top of this I am drawing shapes that correspond to different pads throughout the kit, the part of the pad that is hit, and the velocity behind the note. I created the shapes by extending  the `Polygon2D` and `Ellipse` classes from the [toxiclibs](http://toxiclibs.org) library, creating my own `DrumPolygon`, `SnarePolygon`, `DrumEllipse`, and `CymbalEllipseStack` classes. All of these classes visualize things in slightly different ways, but share a few characteristics. The size and color of each one, when it is hit, is set relative to the velocity of the note. The size approaches the maximum set size, and the color approaches the maximum set brightness using HSB. The size and brightness then gradually lower with each frame, shrinking the shape back to its initial state.

Each shape represents the feeling behind the corresponding part of the kit. The polygons in the top corners represent the splashy, resonant nature of crashes. The ellipse on the bottom represents the dark, low tone that bubbles up and quickly dissipates. The snare in the middle deforms further and further as the time between hits increases, as the snare as often the centerpiece of any groove, the backbeat that everybody comes back to, and thus it becomes uncomfortable with long periods of nonuse. The combination of the mathematical mesh in the background and abstract shapes in the foreground represet the quantiative creativity that is percussion. 

Click on the image below to check out a demo of this piece:

[![Percussive Flow Demo](http://img.youtube.com/vi/Rln4jtj6fJQ/0.jpg)](http://www.youtube.com/watch?v=Rln4jtj6fJQ "Percussive Flow Demo")


Explore the [soure code](https://github.com/stonemathers/percussive-flow)!