---
title: "Sun Temple Ambient SFX"
---

## Setup

Download some [ambient SFX loops](https://www.dropbox.com/sh/sw2swsmqp39558b/AADtsehHN2b0lRMaE0QJv6Dda?dl=0). These are already loops, so you don't need to edit them.  

Add a GameObject as a child of the camera to hold some audio sources. Add an audio source and add the wind sound to as its clip. 

## Random crickets 

Add another audio source to play the cricket sound but set its volume to 0. We will create a script to fade in and fade out this sound randomly. Create a new script called CricketsAudio and add it to the CricketSource GameObject. 

This script will play the cricket sound at random intervals and random volumes. There is no pre-built way of doing this in Unity, so we need to code our own system.  

First initiate an AudioSource for the crickets sound and a variable to hold the fade time.

```c#
public AudioSource cricketsAudioSource;
public float fadeTime = 5f;
```

Next, create a function that sets a random time off, time on and volume. 

```c#
public float minTimeOff = 5f;
public float maxTimeOff = 15f;
float timeOff;

public float minTimeOn = 5f;
public float maxTimeOn = 15f;
float timeOn;

public float minVol = 0.5f;
public float maxVol = 1;
float cricketsVol;

// ... put these variables at the top of your class and the RandomizeValues function below the update function 

void RandomizeValues()
{
    timeOff = Random.Range(minTimeOff, maxTimeOff);
    timeOn = Random.Range(minTimeOn, maxTimeOn);
    cricketsVol = Random.Range(minVol, maxVol);
}
```

Now we will create a new type of function, a coroutine, that allows us to schedule the function to play at specific times. Normally functions are run on events or at the start of the script. We need our crickets to sound at random times, so we need to schedule the function to play at random times. Coroutines are defined by the keyword `IEnumerator` then the function name. 

The FadeCrickets function takes three parameters: the start value, end value and the time to fade. We can see below a new type of control structure, the while loop. You can read more about that [here](https://www.w3schools.com/cs/cs_while_loop.php). It runs the code inside its brackets while the condition in the parentheses is true. While the currentTime is less than or equal to the duration, run the code inside the brackets.

Now inside the while loop we set the volume of the cricket audio source over time (basically a fade in/ fade out automation) using a [Mathf.Lerp](https://docs.unity3d.com/ScriptReference/Mathf.Lerp.html) function. The lerp function is a linear interpolation function. It takes the start value, end value and the time since the function has been triggered divided by the duration of the fade and returns a value between the start value and end value. You can think of this as an automation curve where we need to calculate the time needed to get from one value to another. 

```c#
IEnumerator FadeCrickets (float startValue, float endValue, float duration)
{
    float currentTime = 0;

    while(currentTime <= duration)
    {
        cricketsAudioSource.volume = Mathf.Lerp(startValue, endValue, (currentTime / duration));
        currentTime += Time.deltaTime;

        yield return null; 
    }
}
```

In the start function we need to call the RandomizeValues function to initialize its variables. We can now start the coroutine by calling it in the update function. First initialize these variables that will be used in the update function: 

```c#   
public float timer;
public float timeTillNextEvent;

bool cricketsPlaying;
```

The time keeps track of when to play the crickets. We set it using `Time.deltaTime` which is the time since the last frame. We need to use a time variable so that we can eventually set 
it to 0 and use it to calculate the timeTillNextEvent. 

We want to run the function if the time is greater than the timeTillNextEvent. We can use the `if` statement to check if the time is greater than the timeTillNextEvent. We also need to check if the crickets are already playing. If they are, we don't want to run the function again.

If the crickets are already playing we run the coroutine using `StartCoroutine`. We pass in the FadeCrickets function and the parameters current cricket volume, 0 and fade time. This causes the crickets to fade from their current volume to 0 over the fade time. We need to ask the cricket source what volume to fade from because we are randomly setting it with the RandomizeValues function.

Next we set the cricketsPlaying bool to false, causing the current if statement to not run. Then we set the timeTillNextEvent variable as the timeOff pluse the fadeTime. We have to add the fade time here so that the time off value is started after the sound is totally faded out. 

In the else if statement the reverse of the if statement is done. We fade from 0 up to the cricketsVol value. Finally after each playing of the crickets the timer is reset to 0. 

Make sure to add a line  tot he start function setting the timeTillNextEvent to the time off, `timeTillNextEvent = timeOff;`. 

The update function should look like this: 
```c#
void Update()
{
    timer += Time.deltaTime;

    if(timer > timeTillNextEvent)
    {
        if(cricketsPlaying)
        {
            StartCoroutine(FadeCrickets(cricketsAudioSource.volume, 0, fadeTime));
            cricketsPlaying = false;
            RandomizeValues();
            timeTillNextEvent = timeOff + fadeTime;
        } else if(!cricketsPlaying)
        {
            StartCoroutine(FadeCrickets(0, cricketsVol, fadeTime));
            cricketsPlaying = true;
            RandomizeValues();
            timeTillNextEvent = timeOn + fadeTime; 
        }

        timer = 0; 
    }
}
```

To see if this is working play your scene. YOu should be able to hear the crickets fade in and out, and also see the time value increasing in the inspector. 

## Audio mixer 

Now that are starting to have multiple audio sources, we need a way to control the volume of all the sources. To do this lets add an audio mixer. This is done from the Audio Mixer window. Create a new audio mixer and call it `AudioMixer`. Add a group called `OutsideMixer` to this audio mixer. Now create a new audio mixer called `OutsideMixer`. Drag the `OutsideMixer` Audio Mixer onto the `AudioMixer`. A popup window should appear asking you to select the audio mixer. Select the `OutsideMixer` audio mixer. We are now routing the outside mixer to the master mixer. You can think of this as a submixer.

Now we will create a few groups on our `OutsideMixer` audio mixer: fires, wind, and crickets. Route audio sources to these groups by setting their outputs to the corresponding groups. Make sure when setting the fire output you do it to all prefabs and not just one. Check your game to make sure each element is routed through the correct group. Rebalance the groups to to create a more balanced mix.

## Inside building effect

On the `AudioMixer` create a second snapshot called `InsideBuilding`. Rename the first snapshot to `Default`. We will switch to the `InsideBuilding` snapshot when the player is inside the building. We want the volume of the `OutsideMixer` to be quieter when we're in a building and also sound farther away. We can do this by reducing the volume and applying a low pass filter. 

Select the `InsideBuilding` snapshot and add a lowpass effect to the `OutsideMixer`. The default settings are ok here. Also reduce the volume of the group by around -10 dB. On the default snapshot change the cutoff frequency of the filter to be 22 kHz, making it have no effect. Audition this by turning the audio on and off. Hear the difference by clicking back to the default snapshot. 

Buildings already have something called an exposure area. This is used by the game to control lighting when inside a building. We can add code to the exposure area manager script that sets our snapshot to the `InsideBuilding` snapshot when the player is inside the building. Find the `ExposureManager` script on the `ExposureAreaManager` GameObject and open it. Select an ExposureArea and teleport to it. Also open the `ExposureArea` script attached it it. I'm in ExposureArea1, but any house will do. 

On the `ExposureManager` script add the following code to allow us to call audio functions:

```c#
using UnityEngine.Audio;
```

Add two variables for the snapshots and one for a zone counter: 

```c#
public AudioMixerSnapshot defaultSnapshot;
public AudioMixerSnapshot insideSnapshot; 
public int zoneCounter; 
```

Add this function to the end of the class. We will fill in the rest later. 

```c#
public void UpdateAudioZone()
{

}
```

Now lets connect our mixer snapshots. Find the `ExposureAreaManager` GameObject and add the mixer snapshots to the public variables you just created. 

To handle possible overlapping trigger zones we will keep a count each time we enter a zone. Go back to the `ExposureArea` script and find the `OnTriggerEnter` function. Add the following code to incriment the zone counter and update the audio zone

```c#
void OnTriggerEnter(Collider other)
{
    if (scriptIsEnabled) {
        if (other.tag == ExposureManager.instance.PlayerTag)
            ExposureManager.instance.SetSunIntensityToInterior();
            ExposureManager.instance.zoneCounter += 1; // this is the new code
            ExposureManager.instance.UpdateAudioZone(); // this is the new code
    }

}
```

Decrease the count when exiting the zone.

```c#
  void OnTriggerExit(Collider other)
{
    if (scriptIsEnabled) {
        if (other.tag == ExposureManager.instance.PlayerTag)
            ExposureManager.instance.SetSunIntensityToExterior();
            ExposureManager.instance.zoneCounter -= 1;
            ExposureManager.instance.UpdateAudioZone(); // this is the new code
    }

}
```

Now go back to the manger script and lets finish the `UpdateAudioZone` function. If we are inside a building we want to switch to the `InsideBuilding` snapshot. If we are outside we want to switch to the `Default` snapshot.

```c#
 public void UpdateAudioZone()
{
    // inside a building
    if(zoneCounter > 0)
    {
        insideSnapshot.TransitionTo(1f); 
    } else
    {
        defaultSnapshot.TransitionTo(1f); 
    }
}
```

Test this by entering buildings and leaving them. You should hear the audio fade in and out. This doesn't seem to work on the sun temple itself but on other smaller buildings. 