---
title: "Final Mix" 
---

Open the SampleScene. Make sure you're viewing the scene in 3D. Drag the AudioManager GameObject to your prefabs folder if you haven't done it already in an earlier lesson.

Open the PointAndClick scene and drag in your AudioManager prefab. Only do this if you needed to import the AudioManager. If you already had it just leave it there. The AudioManger should have the MusicSource, AmbiSource and Clickable Source GameObjects. 

Fix your AudioSources in your Thirdperson prefab, they won't stay in when you add it to a new scene. Also, add Ellen to the Player T parameter of the Pressure Pad script to get her to collider with the pressure pad. 

## Audio Mixer 

Open the Audio Mixer pane and create a new Mixer called AudioMixer. Create the following groups: 

* Music Volume
    * Music
* SFX Volume 
    * SFX 
    * Voices
    * Ambiences 
    * Player     

Make a mixing view that hides the Music volume and SFX volume groups so that its easier to see what you need to mix. 

Now go to all of your audio sources and assign their outputs to the proper groups in the Audio Mixer. If you search in the hierarchy by type you can find all your AudioSources easily. Create a mix of your elements that makes sense for the scene. 

## Bonus - Reverb zones 

Add a reverb zone to a corner of your plane so that it doesn't fill up the whole plane. Pick an interesting preset and experiment with it.  