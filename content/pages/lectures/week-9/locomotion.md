---
title: "Player movements"
---

## Setup first person character

Download this [package](https://dakotastateuniversity-my.sharepoint.com/:u:/g/personal/tate_carson_dsu_edu/ETeK_WIfsTNNvkYv1mfC3UMBtEn-s47S2wOB1POUR8YkEw?e=LoeznW) and import it into your project. Create a new scene, name it `Locomotion`, and doubleclick to open it.

Add a plane to your scene and reset its location to the origin. Next add the first person character prefab. Move it so its visible above the plane. Now you delete the other camera and add the pressure pad prefab to the scene. 

On the first person control script add a character controller by selecting the dropdown menu next to CC and choosing Firstperson (character controller). Your character will now be able to move around and jump. 

Add some trees to give your scene some landmarks. Add the Firstperson GameObject to the Player F variable of the Pressure Pad script. The pressure pad should now respond to the player. 

## First person footsteps 

To organize your scripts add a new folder called Audio and add your audio scripts to it. Create a new script in this folder called FirstPersonLocomotionSound then add it to your Firstperson GameObject. Reset the script to look like this: 

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class FirstPersonLocomotionSound : MonoBehaviour
{
    
}
```

Now add the following code to the script. This will handle playing footsteps at the correct rate for walking or running. 

```c#
public class FirstPersonLocomotionSound : MonoBehaviour
{
    public float FootstepFrequency = 1f; 
    private float _footstepDistanceCounter;

    public void PlayFootstep()
    {
        // setup running or walking frequency 
        if (_footstepDistanceCounter >= 1f/FootstepFrequency)
        {
            _footstepDistanceCounter = 0f;

        
        }
    }
}
```

Add the `AudioFunction.PlayRandomClip()` function where the comment says to play the footsteps. Don't forget to define your audio source and clips variables. Also add public variables to change the pitch min and max. 

```c#
public class FirstPersonLocomotionSound : MonoBehaviour
{
    public float FootstepFrequency = 1f; 
    private float _footstepDistanceCounter;

    public void PlayFootstep()
    {
        // setup running or walking frequency 
        if (_footstepDistanceCounter >= 1f/FootstepFrequency)
        {
            _footstepDistanceCounter = 0f;

            //
            // add audio function here 
            //
        }
    }
}
```

Next make the `_footstepDistanceCounter` variable increase by the velocity of the character and the delta time. 

```c#
public class FirstPersonLocomotionSound : MonoBehaviour
{
    public float FootstepFrequency = 1f; 
    private float _footstepDistanceCounter;
    public AudioSource LocomotionSource;
    public AudioClip[] FootstepSFX;

    public float pitchMin = 0.9f;
    public float pitchMax = 1.1f; 

    public void PlayFootstep(Vector3 velocity)
    {
        // setup running or walking frequency 
        if (_footstepDistanceCounter >= 1f/FootstepFrequency)
        {
            _footstepDistanceCounter = 0f;

            AudioFunction.PlayRandomClip(LocomotionSource, FootstepSFX, pitchMin, pitchMax); 
        }

        _footstepDistanceCounter += velocity.magnitude *  Time.deltaTime; 
    }
}
```

Now we need to call the `PlayFootstep()` function in the FirstPersonControl script. Open up that script and find the `ApplyMovement()` function. 

Define `LocomotionSound` like this at the top of the class:

```c#
public FirstPersonLocomotionSound LocomotionSound;
```

This gives you access to the `PlayFootstep()` function. Now call the `PlayFootstep()` function in the `ApplyMovement()` function. 

```c#
 private void ApplyMovement()
{        
    float y = _velocity.y;//backup

    Vector3 dir = new Vector3(Input.GetAxis("Horizontal"), 0, Input.GetAxis("Vertical")).normalized;
    dir = this.transform.TransformDirection(dir);
    _velocity = dir * Speed;

    _velocity.y = y;

    LocomotionSound.PlayFootstep(_velocity);
}
```

Drag the Firstperson GameObject onto the Locomotion Sound property of the First Person Control Script. This makes the FirstPersonLocomotionSound class available to the FirstPersonControl script.

The problem now is that you'll always hear the footsteps because the function is being called from the Update() function. To fix this add an if statement that checks if the player is moving. You can do this by checking the `dir.magnitude` variable. If it is 1 then the player is moving. Use `Debug.Log` to see the value of `dir.magnitude`. 

You should now be able to hear the footsteps of your character. Experiment with the footstep frequency, pitch min and max, and the volume of the footsteps.

The last problem we need to fix is that we still hear the footsteps when the player is jumping. Create a private bool called `_isJumping` to keep track of if the player is jumping or not. Set `_isJumping` to false in the if statement that checks for `CC.isGrounded`. If the player is grounded then the player is not jumping. Find the place in the script where the `ApplyJump()` function is called and set the `_isJumping` variable to true. Now go to your if statement that plays the footsteps and check if the player is not jumping. Remember that you can use the `!` operator to negate a boolean.

## Player emotes 

Emotes are the sounds the a player makes when they are doing something. For example, when they are walking they make a footstep sound. When they are running they make a running sound. When they are jumping they make a jump sound. They make the player sound much more realistic. We've already added footsteps, so lets add jumping and landing sounds. 

In your FirstPersonLocomotionSound script add two new functions `JumpEmote` and `LandEmote`. Also create two public AudioClip arrays `JumpSFX` and `LandSFX` to store the audio clips. Above your AudioClip arrays add a header, ` [Header("Audio Clips")]`, to label your interface in the inspector and make things more organized. 

Inside the `JumpEmote()` function add the `PlayRandomClip` method to play a random clip from the JumpSFX array. Use a new AudioSource called `EmoteSource`. We do this so that our emotes sounds don't overlap with our footstep sounds. Find the place in the FirstPersonControl script where jumping is triggered and run the `JumpEmote()` function. Make sure to add an AudioSource and clips to the `FirstPersonLocomotionSound` script in the Unity GUI. 

Follow the same steps to set sounds for when the player lands. The trick for the landing sound is figuring out when to run the function. You have to create an if statement to check for `_isJumping` before you set `_isJumping` to false in the script.

You should now have sounds for footsteps, jumping and landing. 