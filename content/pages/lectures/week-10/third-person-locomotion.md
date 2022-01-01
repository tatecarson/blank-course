---
title: "Third person movements" 
---

Disable the Firstperson GameObject by un-checking it in the inspector. Drag the third person prefab into your Hierarchy. Create a new script inside the scripts/audio folder called `ThirdPersonLocomotionSound`. Use the same code from your first person script but remove the capability to measure footstep frequency. Add this script to Ellen. Make the AudioClip variables match this:

```c#
public AudioClip[] FootstepSFX;
public AudioClip[] LandSFX;
public AudioClip[] JumpEmote;
public AudioClip[] LandEmote; 
```

Also make sure you have four functions to play each sound. 

Add an AudioSource called LocomotionSource to Ellen. If you just added it to the Thirdperson it wouldn't follow Ellen. Place both sources where you think the sound should emanate from in the scene. Uncheck play on awake for both sources.  

Uncheck play on awake, make the sound 3d and adjust the min distance of both sources so that the are in line with the audio listener. Now add sounds into the AudioClips on the Third Person Locomotion Sound script. Add the emote sounds. Then add the run sounds to footstep sfx. And finally add both landing sounds to  land sfx.

Find the `EllenRunForward` animation in the Project folder and double click it. Then click edit to edit its properties. Scroll down to the Events section. This is where you will add events to the animation. Add an event at the point of each footstep. Be sure to now click the apply button so the events are saved. 

Now do the same process to add jump sounds to the EllenJumpTakeoff animation. 

We will use the script method to add our landing sounds. In the CharacterControl script add `public ThirdPersonLocomotionSound LocomotionSound;` to reference the sound script. Add Ellen to that variable in the inspector.

Add the following code to the place in the code that checks if we are grounded. You must check before te boolean is set to false. 

```c#
if (AC.GetBool("IsJumping"))
{
    LocomotionSound.PlayLandEmote();
    LocomotionSound.PlayLand();
}
```
