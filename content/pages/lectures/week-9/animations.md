---
title: "Animations"
---

## Understanding Animations 

First open the animation window by going to window -> animation -> animation. Then add it to the dock next to the console window. 

Next create a cube and reset the transform so it's in the center of the scene. Create three more cubes to make a sign. Add a material to each cube to give the sign some color. 

Select the sign and create a new animation clip. Create a folder inside your assets folder and name it "sign squeak". Now add the transition properties of position and rotation to the animation. Click on record mode then put the timeline on 10 seconds. Then move the sign so that it's swinging forward. Move the timeline to 30 seconds and move the sign so it swings backwards. Go to 40 seconds and copy and paste the first two keyframes from the start to this point. 

## Adding Audio to Events

Open the animator window to see the animation events. 

Download this [pack](https://dakotastateuniversity-my.sharepoint.com/:u:/g/personal/tate_carson_dsu_edu/Eec23CQer6ZGoW4lCOV1vvsBzgnXvzVcWDeF074L83-RDw?e=Z90zSm) and add it to your project. Then add the pressure pad prefab to your scene. View the triggered and deactivated animations of the pressure pad. Open up the pressure pad script and analyze the code that will respond to a player walking over a GameObject. 

Create a capsule called Player and reset the transform. Add a Ridgidbody onto the player for the collisions to work then disable its gravity. Move the camera to get a better view by selecting it then in the menu selecting GameObject -> Align with view. Temporarily disable the sign by un-checking the box it its inspector. Add the player GameObject to the Player F public variable on the inspector of the PressurePad script. If the player is on the pressure pad and if you play the pressure pad should be activated. 

Open the PressurePad script to add audio playing functions. Add a public function called TriggeredAudio. Inside run the AudioFunction.PlayRandomClip() method and give it a public AudioSource and AudioClips. Add the PRESSUREPLATE_M_DOWN_01 and PRESSUREPLATE_M_DOWN_02 audio files to the clips list of the PressurePad script. 

Add a new AudioSource to the PressurePad GameObject and call it `PressurePadSource`. Go into the AudioSource and un-check play on awake and set the sound to a 3d spatial blend. Give the 3d sound settings some reasonable settings. Add the PressurePadSource to the AudioSource of the PressurePad script. 

Go to the PressurePad_Triggered animation on the PressurePad. Find the point in the animation where the pressure pad first starts to activate and add an event there. Then choose the TriggeredAudio() function. Play your scene. Move the Player on and off of the trigger and you should hear the sound being triggered. 

Now add the sound for when the trigger goes back up. This requires adding another function in the PressurePad script. Redo the rest of the steps from the trigger sound to make the deactivate trigger sound work. 

Now that you know how to add sounds to animations go back to your swinging sign and add realistic sound effects to its animation. 