+++
title = "Challenges of game audio"
outputs = ["Reveal"]
[reveal_hugo]
theme = "solarized"
+++

# Challenges of Game Audio

{{% note %}}
Even though we have access to much more powerful technology than what we have been discussing with historical games, we still have to deal with technical limitations because our goal is to provide a much more complete and immersive experience. The technical limitations can also vary greatly depending on target platform, hardware, and software.

---

## Implementation

* sounds played at the right time
* the right sound level 
* and processed in the correct way 

{{% note %}}

In simplistic terms, implementation consists of making sure that the proper sounds are played at the right time, at the right sound level and distance and that they are processed in the way the sound designer intended.

We will be implementing audio using unity and FMOD; but there are other popular tools such as Wwise. To implement sounds in Unity we'll be using the C# language. 

---

## Repetition and Fatigue Avoidance

1. Pitch
2. Amplitude
3. Sample Selection
4. Sample concatenation – the playback of samples sequentially 5. Interval between sample playback
6. Location of sound source
7. Synthesis parameters of procedurally generated assets

{{% note %}}
Early game developers had to be creative, because of technological limitations, when dealing with the problems of repetition and fatigue.

The use of random and semi­random techniques in sound and music, also known as Stochastic techniques, had been pioneered by avant­garde composers such as John Cage and Iannis Xenakis in the 1950s and 1960s. These techniques, directly or indirectly, have proved to be extremely helpful for game developers.

It takes a bit of care to ensure that randomness seems realistic and not just..random. Such techniques might include randomizing multiple parameters at once and having one respond to another.. 

---

## Interactive Elements and Prototyping

* vehicles
* machines 
* spaceships? 

{{% note %}}
Interactive elements can be the most challenging part of the process; especially for those who are used to linear media. 

A vehicle for instance will have the sound variations of acceleration, braking, and turning. We can't know ahead of time how these need to sound. 

These interactions can be prototyped in other sound environments such as Max, SuperCollider or Pure Data. 

Show Max patch 

For instance, in order to recreate the sense of a vehicle accelerating, the engine loop currently playing back might get pitched up; inversely, when the user is slamming on the breaks the sample will get pitched down, and eventually, in more complex simulation, another sample at lower RPM might get triggered if the speed drops below a certain point and vice versa.

---

## Physics 

<img src="ball.jpg" width="50%">

{{% note %}}
A game having realistic physics for objects is a challenge for sound designers because objects behave in unpredictable ways.

A simple barrel with physics turned on could now be tipped over, dragged, bounce or roll at ranges of velocities, each requiring their own sound, against any number of potential materials, such as concrete, metal, wood etc.

It isn't possible to create enough samples to play for each possible combination of physics properties. These situations is where we need to used physical modeling techniques  so we can model the behavior of the barrel and generate the appropriate sound, in real time, based on parameters passed onto us by the game engine.

These modeling techniques are not always available, some are expensive plugins. So, we can mimic them by using samples and parameter randomization and have that mapped directly from the physics of the game engine. 

---

## Environmental Sound Design and Modeling

* Room tones: drones, hums.
* Environmental sounds: street sounds, weather.
* Dialog and chatter.
* Foley: footsteps, movement sounds.
* Non­player characters: AI, creatures, enemies.
* Weapons: small arms fire, explosions.
* Machinery: vehicles, complex interactive elements.  
* Music.

{{% note %}}
It's important to consider the soundtrack of a game as a cohesive whole, not as a series of individual sounds. This will create a more believable environment. 

In a game we are mixing together all of these elements to create a soundscape or a sound collage that is intended to recreate a place and an environment and provide the player with an overall sonic context. 

To do this we rely on tools such as reverb, filtering and sound propagation. 

This idea started in film pioneered by sound designers and film editors such as Walter Murch that aims at recreating the sonic properties of an acoustical space – be it indoors or outdoors – and provides our sounds a believable space to live in. 

---

## Mixing 

---

## Asset Management and Organization

* version control
* deadlines
* consistency and format 
* naming conventions 
    * Hero_Fstps_Walk_Wood_01.wav 
    * Hero_Fstps_Walk_Metal_02.wav 
    * Hero_Fstps_Run_Stone_09.wav

{{% note %}}

An asset delivery checklist, usually in the form of a spreadsheet, is a must. It should contain information about the following, but this list is not exhaustive:
 * Version control: you will often be dealing with multiple versions of a sound, level, game build etc. due to fixes or changes. Making sure you are working with and delivering the latest or correct file is obviously imperative.
*  Deadlines: often the work of the sound design team is split up into multiple deadlines for various assets types in order to layer and opti­mize the audio integration and implementation process. Keeping track of and managing multiple deadlines is a highly prized and useful organ­ izational skill.
 * Consistency and format: making sure that all the files you will be delivering are at the proper format, sample rate, number of channels and at consistent sound levels across variations, especially for sounds that are related (such as footsteps for instance), quickly becomes challenging and an area where it is easy to make mistakes.
  * Naming convention: dealing with a massive number of assets requires a naming convention that can easily be followed and understood by all
