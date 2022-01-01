+++
title = "Inform, entertain, immerse"
outputs = ["Reveal"]
[reveal_hugo]
theme = "solarized"
+++

# What's the purpose of audio in games?

{{% note %}}

* What is the purpose of audio in games? What makes a player turn up the vol­ume in a game instead of streaming their favorite music playlist?

* Games have come a long way since the days of the Atari 2600 and its embryonic soundtracks, the blips and noises still in our collective memory today.
Remember back to last week and the documentary we watched. We can do much more now, but this means that we need to take greater care to not overdo, and to do artfully.

* Yet, even with the recent technological advances, crafting a compelling soundtrack remains a tricky affair at best, reminding us that technology isn’t everything, and that, at its core, the issues facing the modern sound designer have at least as much to do with the narrative we strive so hard to craft as with the tools at our disposal.
Still, creating a compelling narrative is the most important part, not mastery over the tools and techniques.

{{% /note %}}

---

# Inform, Entertain, Immerse

* Data + Context = Information

{{% note %}}

* If we had to sum up the purpose of sound in games and interactive media we could, perhaps, do it with these three words: inform, entertain, immerse.
* It is easy to understand the entertain portion of our motto. The soundtrack \(a term that refers to music, dialog and SFX\) of a AAA game today should be able to compete with a high­end TV or film experience.
* Additionally, however, in order to create a fully encompassing gaming experience, it is also important that we provide useful feedback to the player as to what is happening in the game both in terms of mechanics and situational awareness.
* Using the soundtrack to provide gamers with information that will help them play better and establish a dialog with the game is a very powerful way to maximize the impact of the overall experience.

What is data, and how is it different from information? 

data - Data are units of information, often numeric, that are collected through observation. In a more technical sense, data are a set of values of qualitative or quantitative variables about one or more persons or objects, while a datum is a single value of a single variable.

information - Information, in a general sense, is processed, organized and structured data. 

{{% /note %}}

---

# What immerses us in our daily lives? 

* Think of and write down all of the different aural cues that allowed you to walk from your car, to the classroom.

{{% note %}}

* Effective aural communication will also certainly greatly contribute to and enhance the sense of immersion that so many game developers aspire to achieve.

* Yet con­stantly in our daily lives we are analyzing hundreds of aural stimuli throughout the day that provide us with information on our surroundings, the movement of others, alert us to danger or the call of a loved one and much, much more.

* In effect, we experience immersion on a daily basis; we simply call it reality, and although gaming is a fundamentally different experience, we can draw upon these cues from the real world to better understand how to provide the user with information and how to, hopefully, achieve immersion.
  
Think of and write down all of the different aural cues that allowed you to walk from your car, to the classroom.

{{% /note %}}

---

# Inform: How, What

* What is our visual field in degrees (Think of an angle, 0-360)? 

{{% note %}}

* In a 3D or VR environment sound can and must play an important role when it comes to conveying information about the immediate surroundings of the user. Keeping in mind that the visual window available to the player usually covers between 90–120 degrees out of 360 at any given time, sound quickly becomes indispensable when it comes to conveying information about the remaining portion of the environment.
* As humans our field of focus is very narrow, 120 but much of that is periph­eral.

{{%/ note %}}

---

# Geometry / Environment: Spatial Awareness

{{% note %}}

* In a game engine, the term geometry refers to the main architectural elements of the level, such as the walls, stairs, large structures and so on. 
* Sound conveys information about geometry
* Creating a convinc­ing environment for sound to propagate in is often another side of the audio cre­ation process, known as environmental modeling.

{{%/ note %}}

---

## Examples

* indoors
    * what is the size of the room?
* outdoors
    * are there any large structures around, manmade or otherwise?

{{% note %}}

Lets walk outside and answer the same question, how do we know that we are outside. It isn't just about the content of the sound, but about its propogation.

{{%/ note %}}

---

# Occlusion, obstruction, exclusion

{{% note %}}

* Do we have a clear line of sight with the sound we are hearing, or are we partially or fully cut off from the source of the sound? We can iso­ late three separate scenarios:
Occlusion, obstruction, exclusion

{{%/ note %}}

---

## Occlusion

We are fully cut off from the audio source. The sound is happening in an adjacent room or outside. There is no path for the direct or reflected sound to get to the listener.

{{% note %}}

Someone stand on the other side of this door, describe how the sound changes when the door is opened or closed.

{{%/ note %}}

---

## Obstruction

The path between the audio source and the player is partially obstructed, as in a small wall or architectural feature \(such as a col­umn for instance\) blocking our line of sight. In this case the direct audio path is blocked, but the reflected audio path is clear. 

---

## Exclusion

The direct path is clear, but the reflected sound path isn’t, blocking the reverberated sound: this is known as exclusion.

{{% note %}}

Think of when you hear sound at a concert bouncing off of walls

{{%/ note %}}

---

# Distance 

How can we determine the distance between the sound source and the listener?

{{% note %}}

* We have for a long time understood that the perception of distance was based primarily on the amount of dry vs. reflected sound that reaches our ears and that therefore reverberation played a very important role in the perception of distance.

* Energy from reverberant signals decays more slowly over distance than dry signals, and the further away from the listener the sound is, the more reverb is heard.

* air absorption 
* temperature, humidity and distance.
* noticeable loss of high frequency content, an overall low pass filtering effect.

{{%/ note %}}

---

# Location

* The perception of the location of a sound in terms of direction in 360 degrees
    * Interaural time difference
    * interaural intensity difference
    * Preceence effect  

{{% note %}}
* Interaural time difference: the time difference it takes for sound to reach both the left and right ears.  
* interaural intensity difference: the difference in intensity, or amplitude, between the left and right ears.
* the precedence effect: When a sound is followed by another sound separated by a sufficiently short time delay, listeners perceive a single auditory event; its perceived spatial location is dominated by the location of the first-arriving sound.


* it is almost impossible to determine the location of a continuous tone, such as a sine wave playing in a room \(Cook ’99\).
Try an expleriment of playing a sine tone and see if we can hear it coming from the speakers

* The process currently used to recreate these cues on headphones is a tech­nology called Head Related Transfer Functions,

* Another somewhat complimentary technology when it comes to spatial audio is ambisonic recording. While not used to actually recreate the main cues of human spatial hearing, it is a great way to compliment these cues by recording a 360­degree image of the space itself. The Unity game engine supports this technology, which their website describes as an ‘audio skybox’

{{%/ note %}}

---

# User Feedback and Game Mechanics

Telling the player what is happening in the game through feedback sounds. 

{{% note %}}

* On a basic level, audio based user feedback is easily understood by anyone who ever had to use a microwave oven, digital camera or any of the myriad consumer electronics goods that surround us in our daily lives.
This is simple sonification. Lets try to think of all the things in our daily lives that include audio feedback. 

ex: 
Car engine - tells pedestrians that a car is around
dinging elevator 
dinging microwave
wake up alarm

* The simplest kind of feedback one can provide through sound is whether an action was completed successfully or not.

What makes a feedback tone portray success or failure of an action?

* The chime almost universally symbolizes successful completion of an action, or positive feedback.

* The buzzer, of course, is noisy, unpleasant to the ear and associated with negative feedback and negative sen­ timents.

* These qualities, being easy to hear in a noisy environment, easy to under­ stand when heard \(also known as legibility\), make them prime examples of the specific demands that user feedback sound design requires.

* Sound can provide much more complex and subtle feedback as well. Add­ ing a low tone to the mix when entering a room can induce an almost sub­ liminal sense of unease in the player;
Great example of this is sinua sacrifice, dialoge in the head adding to a sense of disturbance.

* Contact sounds, the sound the game makes if you hit a target, for instance, are one such great example, but there are far too many for us to list here.

* We all know how much less scary or intense even the most action­packed shots look when watched with the sound off. If you haven’t tried, do so.
Watch some of our example games with the sound off

{{%/ note %}}

<!-- * 2\. Entertain

* a. Sound Design

## [Page 7](x-devonthink-item://86F0CBA7-8C3B-44A8-BE5D-1E39FAB35BF9?page=6)
* While this book does not focus on music composition and production, it would be a mistake to consider sound design and music in isolation from each other.

* The soundtrack of any game \(or movie\) should be considered as a whole, made up of music, dialog, sound effects and sometimes narration. At any given time, one of these elements should be the predominant one in the mix, based on how the story unfolds. A dynamic mix is a great way to keep the player’s attention and create a truly entertaining experience.
A mix is really important. 

What scenes benifit from music and which would be better with little music and mostly environmental sounds? Think about the purpose of music vs sound effects and how each helps with the story and giving the play valuble information.

* Often, it is the dialog that domi­ nates, since it conveys most of the story and narrative.

* Please see the companion website for some examples of films and games that will illustrate these points further.

* During one of his lectures, he played the opening scene to the movie The Shining by Stanley Kubrick. However, he kept changing the music playing with the scene.
<iframe width="560" height="315" src="https://www.youtube.com/embed/LjLip2FZLuA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

* b. Music and the Mix

## [Page 8](x-devonthink-item://86F0CBA7-8C3B-44A8-BE5D-1E39FAB35BF9?page=7)
* During that exercise it became obvious to us that music could not only influence the perceived narrative by being sad or upbeat or by changing styles from rock to classical but that, if we are not careful, music also has the power to obliterate the narrative altogether.

* Inevitably, a solo instrument links us emotionally to one of the characters, while an orchestral approach tends to take the focus away from individuals and shifts it toward the overall narrative.

* 3\. Defining Immersion

* immersion – or presence – as

* Non­immersive systems: typically, simple Augmented Reality systems that affect one sensory input. Playing a 3D game on a laptop is a com­ mon example. This is the type of system most people are familiar with.  Semi­immersive systems: typically allows the users to experience a 3D world while remaining connected to the real world. A flight simulator game played on a multiscreen system with realistic hardware, such as a flight yoke, would be a good example of such a system.  Fully immersive systems: affect all or most sensory inputs and attempt to completely cut off the user from their surroundings through the use of head mounted displays, headphones, and additional systems such as gaming treadmills, which allow the user to walk or even run though a virtual environment.

* An early definition of presence based on the work of Minski, 1980 would be: The sense an individual experiences of being physically located in an envi­ ronment different from their actual environment, while also not realizing the role technology is playing in making this happen

## [Page 9](x-devonthink-item://86F0CBA7-8C3B-44A8-BE5D-1E39FAB35BF9?page=8)
* Narrative immersion happens when a player or reader is so invested in the plot that they momentarily forget about their surroundings.

* So, what are the elements that scientists have been able to identify as most likely to create immersion? The research of psychologist Werner Wirth suggests that successful immer­ sion requires three steps: 1. Players begin to create a representation in their minds of the space or world the game is offering. 2. Players begin to think of the media space or game world as their main reference \(aka primary ego reference\). 3. Players are able to obtain useful information from the environment.

* Characteristics that create immersion tend to fall in two categories: 1. Characteristicsthatcreatearichmentalmodelofthegameenvironment. 2. Characteristics that create consistency amongst the various elements of the environment.

* Clearly, sound can play a significant role in all these areas.

* We can establish a rich mental model of an environment through sound by not only ‘scoring’ the visuals with sound but by also by adding non­diegetic elements to our soundtrack.
look at some game examples and name all the elements that make the scene immersive

* Consistency, this seemingly obvious concept, can be trickier to implement when it comes to creature sounds or interactive objects such as vehicles.

## [Page 10](x-devonthink-item://86F0CBA7-8C3B-44A8-BE5D-1E39FAB35BF9?page=9)
* Indeed, when the human brain receives conflicting information between audio and visual channels, the brain will inevitably default to the visual chan­ nel. This is a phenomenon known as the Colavita visual dominance effect.

* It is clear that sensory rich environments are much better at achieving immersion. The richness of a given environment maybe given as:  Multiple channels of sensory information.  Exhaustiveness of sensory information.  Cognitively challenging environments.  Possessing a strong narrative element.

* Additionally, while immersion can be a rather tricky thing to achieve, it is rather easy to break. In order to maintain immersion, research suggests that these elements are crucial:  Lack of incongruous audio/visual cues.  Consistent behavior from objects in the game world.  Continuouspresentationofthegameworld–avoidcommercials,level reset after a loss.  The ability to interact with objects in the game world.

* The third point presented in this list, ‘continuous presentation of the game world’, is well illustrated by the game Inside by Playdead studios. Inside is the follow­up to the acclaimed game Limbo, and Inside’s developers took a very unique approach to the music mechanics in the game.

## [Page 11](x-devonthink-item://86F0CBA7-8C3B-44A8-BE5D-1E39FAB35BF9?page=10)
* . This is sometimes referred to as the ‘Fan Gene’. As a result, two users may have wildly differing experiences when it comes to the same experience, based, partially, on their willingness to ‘be immersed’.
A player must wish to be immersed


 -->
