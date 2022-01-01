---
title: Projects
---

## Project 1

Add sounds to 5 GameObjects in pyramid tutorial project. Move them with the scripts you already had and listen to how the doppler effect works.

## Project 2

Use sounds freesound.org to replace the sounds of the FPS project. You may need to edit the sounds from freesound, or manipulate them. Experiment with filters and effects. 

* Add another room using the tutorial. 
* Add an enemy using the tutorial. 
    * Give the new enemy some sounds.  
* Add different background music for each of the four rooms. 
* Add a lose sound and background music for the lose screen.
* Add a win sound and background music for the win screen. 
* Add music to the intro screen 
* Remember that music should play continuously but the win and lose sound should only play once. 

## Project 3  

Recreate sound effects from your game sound database game. Pick three different categories of sound effects. You should turn in five variations of each category, totaling 15 sounds. Variations can include different types of vocalizations of a creature, footsteps on different surfaces, or guns shooting different types of bullets. 

Use a combination of the studio and field recording techniques, along with audio manipulation and effects in a DAW. Remember that most sound effects are layered from multiple recording sources. You may use all the techniques we've learned so far whether recording studio techniques or sound design manipulations. You may not use any audio sources except what you record and manipulate. 

In order to match your sound effect to the game you will need to download the youtube clip and import it into Reaper. [Btclod](https://btclod.com) is a good option to do download the video. Create a new track in Reaper and import the video into the track. Turn the volume fader all the way down to not hear the audio, muting mutes the video as well as the audio. 

Duplicate [this Air Table base](https://airtable.com/invite/l?inviteId=invhJnHYWv0A3CnLW&inviteToken=4a50a52c1e144b4c59274f64f2935928630646b578e945c97f95cd495553613f&utm_source=email) to create your assets list. Fill out the base for each of your sounds. Come up with a naming convention and use it for all your effects. For instance, an ambience might start with AMB and a creature might start with CRE. Write a few sentences for each sound effect type describing what about about this object is influencing your sound design decisions. 

Rubric: 

* 30 points for creating 5 sounds of each type. Each sound is 6 points.
* 10 points for filling out the spreadsheet with the information needed to create the sounds.

Total - 40 points 

<h2 id="final">Final Project</h2>

Add sound effects to a prefab environment. You can pick from any of the free ones on the [Unity Asset Store](https://assetstore.unity.com/3d/environments?category=3d%2Fenvironments&free=true&orderBy=1). You have freedom to pick, but ask me first so we can make sure the environment is complex enough to be interesting. The environment should not already have sound implemented in it. 

Some good choices are: 

* [Flooded Grounds](https://assetstore.unity.com/packages/3d/environments/flooded-grounds-48529), 
* [Viking Village](https://assetstore.unity.com/packages/essentials/tutorial-projects/viking-village-urp-29140), 
* [Destroyed City](https://assetstore.unity.com/packages/3d/environments/sci-fi/destroyed-city-free-6459#description). 
* [Japanese Otaku City](https://assetstore.unity.com/packages/3d/environments/urban/japanese-otaku-city-20359#content)
* [Abandoned Asylum](https://assetstore.unity.com/packages/3d/environments/urban/abandoned-asylum-49137) 
* [Sample Racer Environment Pack](https://assetstore.unity.com/packages/3d/environments/urban/sample-racer-environment-pack-63641#content)
 
If you pick an environment that already has sound in it, I will be expecting improvements on the implementation and more sounds added to the scene.

There are many environments that are very cheap, under 20 dollars. These would be good to use if you want to work with a more dynamic environment.

Make sure to pick an environment with dynamic elements that you can add sounds to. Think of the fire from the Sun Temple Project. The environment should also have some building or structures that you can go inside of. If yours doesn't have them you can find some from the Asset store and add them. 

A successful project will include: 

* A user interface that allows the player to start the game. This interface should have music looping in the background. The player should be able to pause the game and return to this user interface by pressing the escape key.
* A first/third person character that can move around the environment and jump.
    * Sounds will play for all of the possible character actions, walking, running, jumping, landing. 
    * [First Person All-in-one](https://assetstore.unity.com/packages/tools/input-management/first-person-all-in-one-135316) is a great option. 
    * [DarkTree FPS](https://assetstore.unity.com/packages/templates/systems/darktree-fps-v1-4-142383#description) is another option more based on making FPS games instead of just exploring. This already has sounds implemented for all of the actions. Because of this you need to improve on them. 
    * The footstep sounds should vary in pitch and volume. The should also change based on the surface the character is walking on.
* The character should be able to interact with the environment in some way. Each of these interactions should have sounds associated with them.
    * Throwing, shooting, moving objects
    * [This tutorial](https://www.patrykgalach.com/2020/03/16/pick-up-items-in-unity/) is good for picking up and throwing objects. 
    * Also review this [tutorial](https://learn.unity.com/tutorial/sound-effects-scripting-1?projectId=5f4e4ee3edbc2a001f1211df#5f4f7032edbc2a0021ccd904)
    * Review the FPS Microgame for more ideas 
* Environment
    * Add environmental effects to the scene if they aren't already there. 
    * Weather 
        * Add rain with the [Rain Maker](https://assetstore.unity.com/packages/vfx/particles/environment/rain-maker-2d-and-3d-rain-particle-system-for-unity-34938) asset. Automate the rain so that it's only raining sometimes. 
        * The wind should not always be blowing. Turn it off sometimes with a coroutine. 
        * You should have at least two of these environmental effects in the scene. Each effect should have sound design associated with it.  
        * Occasionally chang the time of day by rotating the directional light. Do this on a coroutine so it happens gradually. 
    * Wildlife 
        * Have some sounds that play intermittently like birds chirping, etc. These will use a Coroutine to play them.
        * These sounds will depend on the environment.
* Employ environmental modeling   
    * If the player is inside of a building the outside sound should be quieter. 
    * Also, if inside a building the players sounds should have reverb, to simulate the sound of a building.
* Create original sound design for all of the elements in your game. An exception can be made if the sound is not possible to record or synthesize, ex: a tiger roaring. If something already has a sound, replace the sound with a sound you created. 
* Mix your sounds using AudioMixers and effects to create a convincing environment.
* Finally build your game for your target platform. 

Give a presentation to the class showing your process with video clips demonstrating immersive audio. You will turn in your project by submitting the video and a built version of the project.  
