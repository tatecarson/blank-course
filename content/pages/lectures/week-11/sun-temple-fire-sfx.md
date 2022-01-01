---
title: "Sun Temple Fire SFX"
---

## Setup

We're now going to add sounds to a more complex game environment, the Sun Temple. Go to the asset store and download the [project](https://assetstore.unity.com/packages/3d/environments/sun-temple-115417). Download and import it into to your project. 

To get an error to go away I had to edit the MinDrawer.cs file. I just removed the reference to `using UnityEngine.PostProcessing;` and it seems to be working. If you scene is running very slowly try to turn off the post processing effects in the post processing profile. 

Find the camera and add an audio listener to it.

## Fire sound 

Each of the fires is a prefab. To find the prefab you can search in the Hierarchy for `fx_bonfire`. This shows you all the versions of the prefab. Right click and go to Prefab -> Select asset. You should now be able to see this prefab in your inspector. 

Download the [fire](https://www.dropbox.com/sh/meqasgqwqnm1omb/AADUoK2gtZNE_6YxUcVYChMAa?dl=0) sounds. Layer them and make them into a loop. Create an Audio folder in your Assets folder and add the fire loop. Double check that it loops ok by playing the sound on loop in the inspector. 

Add an Audio Source component to the FX_Bonfire_A in the bonfire prefab and drag the fire sound into the AudioClip. Apply overrides to the prefab to update each prefab. Update the distance parameters to sensible numbers. 

HINT: you can audition the sounds without going into play mode by toggling the audio on in the scene view. 

There's one problem with bonfires that are close together. Because the loop starts at the same time there is a possibility of phase cancellation issues if the player is between the two fires. To fix this we can add a delay to the loop. To fix this add a script named AudioFireController and add it to the FX_Bonfire_A GameObject inside the Prop_Firewood_A prefab. 

In the script create an AudioSource. In the Start function set the time of the audio source to a random value between 0 and the length of the audio clip. You can set the time by accessing the time property of the audio source. The clip length can be accessed by accessing the clip property of the audio source and then the length property. 

Check that this worked by opening the profiler in Analysis -> profiler. Scroll to the audio section and make sure you can see the detailed view. If you hit play, you should be able to see that the fire flips are all playing with different time values. 