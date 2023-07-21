---
title: "Re-Visiting Old Work - SOLI Sketches"
date: "2021-10-30"
---



A few years ago, [I was a participant in Google ATAP’s Project Soli Alpha Developer program](https://nickarner.com/projects_and_work/o_soli_mio/). The program gave access to early Soli hardware; a mm-wave radar development kit and software package to various academics, companies, and independent researchers such as myself. Some of the work I had done as part of this program was [published in a paper](http://homes.create.aau.dk/dano/nime17/papers/0054/index.html), as well as shown in a [video that was presented at Google I/O 2016](https://www.youtube.com/watch?v=H41A_IWZwZI).

Soli would later be included in the [Pixel smartphone](https://www.theverge.com/2019/10/15/20908083/google-pixel-4-project-soli-radar-motion-sense-explainer) and the [Nest Hub](https://www.cnet.com/home/smart-home/googles-new-nest-hub-tracks-your-sleep-with-soli-no-camera-required-heres-how-it-works/).

During the course of the Alpha Developer Program, participants were only able to show work that was disseminated via an academic publication. While some of the work I had done was able to get published; some wasn’t. But now that the Developer Program has ended, I’m able to share the remainder of this old work. 

What follows is a write-up I did following some prototypes I made in June of 2017: 
————————————————————————————————————————————————————————

Having focused my initial work with Soli around interacting with music, I was interested in exploring how it could be used when interacting with visual systems. The sketches described and shown here are the first in a series I have planned that focuses on showing how simple gestures can be used to add interactivity to creative coding projects. 



### Micro-Gestures: Soli’s Strength

There have been many types of gesture recognition systems developed that the creative coding community has used to make their project interactive, such as the Kinect or the Leap Motion. Unlike those sensors, which focus on large hand gestures or pose detection, Soli is able to detect gestures that show the subtlety and capability of the human hand. 
Soli’s strength lies in the fact that it uses [millimeter-wave radar to detect hand gestures](http://dl.acm.org/citation.cfm?id=2925953) - giving it the ability to detect what can effectively be called micro-gestures. These gestures, subtler and smaller than gestures that make use of a wider hand-space, or the entire body of a user. Google ATAP showed off these sensing capabilities at I/O 2016, in which they [demonstrated](https://www.youtube.com/watch?v=Na89OzXllkk) how Soli could effectively be used to control both a smartwatch, and an audio speaker. 



### Gesture Recognition

For these sketches, gesture recognition was performed using an [OpenFrameworks](https://openframeworks.cc/) example project that was provided in the Soli Alpha Developers’ SDK. This allowed for training simple gesture recognizers, the result of which would be sent via OSC ([Open Sound Control](http://opensoundcontrol.org/)) to the sketches. Depending on what gesture was detected by the Soli sensor, a corresponding event would occur in the sketch. 

For these first sketches, I focused on two simple gestures: finger snaps and hand/finger wiggling:

![FingerSnap](/blog_assets/2021/FingerSnap.gif)

![FingerSnap](/blog_assets/2021/Hand+FingerWiggling.gif)



The reason for this was that it was easy to train the Soli gesture recognition system to recognize these with a limited amount of training data, and a limited number of test subjects (I was the only person training the system, and the only person using the system). 

&nbsp;

### Sketch 1 Soli + Fireworks
[![](http://img.youtube.com/vi/UdcWsFA_-cE/0.jpg)](https://youtu.be/UdcWsFA_-cE "")



The first sketch is modified from the “CircleWorks” patch included in the Max “Jit.mo” package by [Cycling74](http://cycling74.com/). In the original patch, a timer was in-place that would trigger a firework-launch event. I modified the patch so that whenever a finger-snap is detected by Soli, the fireworks are lit off. As long as the user is snapping their fingers, then the patch will keep shooting off fireworks. 

&nbsp;

### Soli + Simple Particle System

[![](http://img.youtube.com/vi/22S9U2UqKts/0.jpg)](https://youtu.be/22S9U2UqKts "")

This sketch is based off of the Dynamic Particles example that’s included in the [Processing](http://processing.org/) download. In the original sketch, the position of the particle system was determined by where the user moved their mouse on the screen of the sketch. 
My modifications involved changing the speed and gravity of the particle system, based on the type of gesture the user was making. When the hands are held in a static, still position above the sensor, the system’s particles shoot downwards from a central point in the middle of the sketch. If you snap your fingers above the sensor, the particles will shoot out at a high velocity. When the fingers and hands are wiggling over top of the Soli sensor, the particles float out away from the central point in a more gentle manner. 

&nbsp;

### Soli + Complex Particle System

[![](http://img.youtube.com/vi/49kmKQpguI0/0.jpg)](https://youtu.be/49kmKQpguI0 "")



This is similar in concept to the second sketch. However, the behavior of the particle system is a bit more complex, and consequently, a bit more visually interesting. This particular sketch is a modified version of the Attraction2D example from [Karsten Schmidt](http://thi.ng/)’s [toxiclibs library](http://toxiclibs.org/). 

As was the case with the Simple Particle System, the original version of this sketch consisted of a particle system in which the position of the system was controlled via mouse. Additionally, however, this sketch would also add and remove attractors for the particle system...where there were attractors, that was where the particle system would coalesce around.

I modified the sketch so that if the hands were held, the particles coalesce around a central point. Finger snaps cause the particles to shoot out from this central point. Wiggling the fingers and hands above the sensor keeps the particles floating closer to the surface area on the sketch - when the wiggling motions stop, then they are allowed to migrate back around to their central point on the screen.

&nbsp;

### Lessons Learned on Training Gesture Recognition Systems and Workflows

When training machine learning systems for gesture recognition in general: take breaks! If you keep making the same gestures over and over while training your system, they start to lose their coherency. In the case of making gestures, if you train your system in a long, single setting; your gestures will start to become sloppy, or perhaps stiff and wooden...adversely affecting the training data for your gesture recognition pipeline. 

Additionally, try to anticipate any of the subtle variations in which you (or your users, if you’re creating a system to be used by more than just yourself) may make a gesture. For example, if you want are training your system to recognize finger wiggles, and you’re training your system at the end of the day when you’re tired, you’re not going to make finger wiggles the same way when you wake up the next day and have had your double shot of espresso. The more you train a gesture recognition system with slight variations of similar gestures over a longer period of time with multiple sessions, the more robust the gesture recognition system will be in the pipeline. 

### Instrumentality and Potential for Interactivity

While using these sketches, I became aware of something - using them felt like playing an instrument. I have a background as a bass guitarist, and while performing the various gestures, I wasn’t able to shake the feeling that I was playing an instrument - even after having worked with a trained gesture recognition + sketch for a period of time, while filming the demo videos, I found that I had to “rehearse” my gestures to get the desired visual output from the sketches. I was definitely relying on muscle memory to perform the gestures in a way that made the output of the sketches make sense. This feeling only reinforced how I feel about Soli’s potential as a tool for adding interactivity to creative coding environments. 

While Soli certainly has lots of potential for various “utilitarian” applications (including the IoT, industrial robotics, AR/VR, etc), it also continues to show promise as a way for adding gesture recognition capabilities to creative audio and visual applications. I believe these sketches are stepping stones in showing how gestural interaction, provided via Project Soli, can enhance the way we interact with creative computational environments.
