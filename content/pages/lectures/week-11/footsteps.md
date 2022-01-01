---
title: "Adding footsteps"
---

We'll build a footstep system for our environment that has the following properties:
* player is grounded
* match player's speed
* random + no repeats 
* material specific 
  
Our materials in this project are stone, dirt/grass, and wooden floors. We can check if a player is on the terrain and if the player is in a building. If they're inside then they are standing on a wooden floor. Then we can assume that if they player is outside, then they're on stone or on dirt. 

First we need to check if we're grounded. To do that create a new script called `CheckIfGrounded` and add it to the FpsController. Add the following code: 

```c#
public class CheckIfGrounded : MonoBehaviour
{
    public Collider playerCollider;

    public bool isGrounded;
    public bool isOnTerrain;
    public bool isInside;

    RaycastHit hit; 

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

We create a variable for our player collider, three for our isGrounded, isOnTerrain, and isInside booleans, and a variable for our raycast hit. We'll use this to check if the player is grounded. To figure this out we fire a raycast down from the collider of the player. We'll use the [`Physics.Raycast`](https://docs.unity3d.com/ScriptReference/Physics.Raycast.html) function. See the parameters that the raycast takes in the link above. We'll add this function to our class:

```c#
 bool PlayerGrounded()
{
    return Physics.Raycast(transform.position, Vector3.down, out hit, playerCollider.bounds.extents.y + 0.5f );
}
```

Here we assign the position of our player to the starting point of the raycast, then we point the raycast down towards the ground. Hit stores information about the object that the raycast hits. We'll use this to check if the player is grounded. Then we set the maxDistance of the raycast with `playerCollider.bounds.extents.y + 0.5f`. 

Next add the following function to check if we're on the terrain: 

```c#
bool CheckOnTerrain()
{
    return hit.collider != null && hit.collider.tag == "Terrain"; 
}
```

We use the hit variable that has raycast data to know if we're on terrain. If the tag of hit is "Terrain" then we're on the terrain. Otherwise we're not. 

Now we'll check if we're inside using the method from the previous lesson. 

```c#
bool CheckIfInside()
{
    return SunTemple.ExposureManager.instance.zoneCounter > 0; 
}
```

Now run the functions in the Update function and assign them to your boolean variables: 

```c#
void Update()
{
    isGrounded = PlayerGrounded();
    isOnTerrain = CheckOnTerrain();
    isInside = CheckIfInside(); 
}
```

Drag the FpsController GameObject onto the PlayerCollider variable. Find the `Terrain` GameObject and give it a tag of `Terrain`. You will have to add this tag yourself. 

## Create the CheckTerrainTexture script and variables

In Unity Terrain textures are stored as Alpha Maps or “Splat Maps”, which are arrays of values that hold the mix of each different texture at every point on the Terrain.  It’s possible to detect what mix of textures the player is standing on at any given moment by converting the player’s current transform position to a coordinate on the alpha map image. This can then be used to check the Alpha Map data at that position. This is ideal for determining what footstep sound should play. In this post I’ll show you how to detect what surface material the player is standing on step by step and how you can use that data to trigger footstep sounds.

Now that we know we are on terrain, we need to know what specific texture we're standing on when we're on the terrain. To do this we'll create a new script called `CheckTerrainTexture` and add it to the FpsController. Add the following variables:

```c#
public Transform playerTransform;
public Terrain terrainObject;

public int posX;
public int posZ;

public float[] textureValues; 
```

In the start function add the following code: 

```c#
terrainObject = Terrain.activeTerrain;
playerTransform = gameObject.transform; 
```

## Convert the player’s position to an alpha map coordinate

Add the following function to covert the player’s position to an alpha map coordinate:

```c#
 // Translate world position into alphamap position 
void UpdatePosition()
{
    Vector3 terrainPosition = playerTransform.position - terrainObject.transform.position;
    Vector3 mapPosition = new Vector3(terrainPosition.x / terrainObject.terrainData.size.x, 0,
        terrainPosition.z / terrainObject.terrainData.size.z);
    float xCoord = mapPosition.x * terrainObject.terrainData.alphamapWidth;
    float zCoord = mapPosition.z * terrainObject.terrainData.alphamapHeight;

    posX = (int)xCoord;
    posZ = (int)zCoord; 
}
```

##  Retrieve the texture mix at that position

The following code will retrieve the texture mix at the player’s position. We will use a new type of array, a 3D array. With this we can store 3 values for each index. The 3 dimensions of the alpha map array relate to the x position, z position and the texture that each splat map belongs to.

Each float value in the array is a texture mix, which is a value between 0 and 1, that corresponds to how much of the texture is applied at that position. I can use this to find out what mix of surfaces the player is standing on.

We fill this splatMap array using the GetAlphaMaps function. It takes these four parameters:

* x offset
* z offset
* sample size width
* sample size height

```c#
void CheckTexture()
{
    // create 3d array 
    float[,,] splatMap = terrainObject.terrainData.GetAlphamaps(posX, posZ, 1, 1);

    textureValues[0] = splatMap[0, 0, 0];
    textureValues[1] = splatMap[0, 0, 1];
    textureValues[2] = splatMap[0, 0, 2];
    textureValues[3] = splatMap[0, 0, 3];
}
```

Back in Unity add four elements to the Texture Values array. Here you will be able to see which texture you're standing on. 

![](../texture-mix.png)

Finally, add the following function to run both the UpdatePosition and CheckTexture functions:

```c#
public void GetTerrainTexture()
{
    UpdatePosition();
    CheckTexture();
}
```

This GetTerrainTexture function will be called in the next script we make, only when the player is walking.

## Use terrain texture data to trigger different footstep sounds

What’s great about this method is that, unlike a tag, it doesn’t just return a true or false value. It’s a mix value, between 0 and 1 that can be used for more natural sounding footstep sounds.

To create natural landscapes, textures on terrain objects are often blended together. There’s often no hard division between one surface and another. You might be standing on 80% stone and 20% sand, or 100% grass, or 50/50 mud and rocks.

It’s possible to blend footstep sound effects in the same way for a really effective footsteps system.

We can do it with the following steps

* Get the terrain alpha map values by using the method above.
* If any texture mix value is more than 0, play a footstep sound from an array of clips for that material.
* Trigger it with Play One Shot, not Play (which takes a volume scale parameter).
* Pass in the texture mix value for the Volume Scale parameter of Play One Shot to blend the sound with any others that are playing.

This will smoothly blend the footstep clips together depending on what the player’s standing on. Because it uses a volume scale, you will still be able to adjust the total volume of all the footsteps on the Audio Source if you need to.

Add an AudioSource to the FpsController. Uncheck play on awake and leave it as a 2d sound. Create a new script called footsteps and add it to the FpsController. Add the following variables:

```c#
 public CheckIfGrounded checkIfGrounded;
public CheckTerrainTexture checkTerrainTexture;

public AudioSource audioSource;

public AudioClip[] stoneClips;
public AudioClip[] dirtClips;
public AudioClip[] woodClips;
public AudioClip[] sandClips; 


AudioClip previousClip;

CharacterController character;
float currentSpeed;
bool walking;
float distanceCovered;
public float modifier = 0.5f;

float airTime; 
```

In the start function select the character controller and assign it to the character variable.

```c#
character = gameObject.GetComponent<CharacterController>(); 
```

We'll now create functions to check the players speed and if they are walking. We get the magnitude of the velocity of the player, which is the speed. We also check if the player is walking by checking if the player is grounded and if the speed is greater than 0.

```c#
float GetPlayerSpeed()
{
    float speed = character.velocity.magnitude;
    return speed; 
}

bool CheckIfWalking()
{
    return currentSpeed > 0 && checkIfGrounded.isGrounded;
    
}
```

Now add both of those functions to the update function so they are constantly checked. 

```c#
void Update()
{
    currentSpeed = GetPlayerSpeed();
    walking = CheckIfWalking();
}
```

Next we'll make a function that selects a random clip from an array of clips. This function takes a clip array. First a random clip is picked. Then we check 3 times if that clip is the same as the last clip that was picked. If it is, we pick another clip. If it isn't, we return the clip.

```c#
AudioClip GetClipFromArray(AudioClip[] clipArray)
{
    int attempts = 3;
    AudioClip selectedClip = clipArray[Random.Range(0, clipArray.Length)];

    while (selectedClip == previousClip && attempts > 0)
    {
        selectedClip = clipArray[Random.Range(0, clipArray.Length)];
        attempts--; 
    }

    previousClip = selectedClip;

    return selectedClip; 

}
```

Create a new function to play footstep sounds. We set the pitch and volume of our source to random values. Then we check if the player is on the terrain. Then we update the texture values by running ` checkTerrainTexture.GetTerrainTexture();`. Next we have a series of if statements that check for each terrain value. If the texture value is greater than 0, we play a random clip from the array of clips for that texture. The second parameter of Play One Shot is the volume scale. We use the texture mix value so that the if we're on more than one texture at once, the clips will blend together and not sound too loud. Finally, if we're not on the terrain we check if the player is inside. If the player is neither on the the terrain or inside, then we play the stone footsteps. 

```c#
void TriggerNextClip()
{
    audioSource.pitch = Random.Range(0.9f, 1.2f);
    audioSource.volume = Random.Range(0.8f, 1.0f);

    if (checkIfGrounded.isOnTerrain)
    {
        checkTerrainTexture.GetTerrainTexture();

        if (checkTerrainTexture.textureValues[0] > 0)
        {
            audioSource.PlayOneShot(GetClipFromArray(stoneClips), checkTerrainTexture.textureValues[0]);
        }


        if (checkTerrainTexture.textureValues[1] > 0)
        {
            audioSource.PlayOneShot(GetClipFromArray(dirtClips), checkTerrainTexture.textureValues[1]);
        }


        if (checkTerrainTexture.textureValues[2] > 0)
        {
            audioSource.PlayOneShot(GetClipFromArray(dirtClips), checkTerrainTexture.textureValues[2]);
        }

        if (checkTerrainTexture.textureValues[3] > 0)
        {
            audioSource.PlayOneShot(GetClipFromArray(sandClips), checkTerrainTexture.textureValues[3]);
        }
    }   else if (checkIfGrounded.isInside)
    {
        audioSource.PlayOneShot(GetClipFromArray(woodClips), 1);
    }
    else
    {
        audioSource.PlayOneShot(GetClipFromArray(stoneClips), 1);
    }
   
    
}
```

Create a function to handle if the player is falling. If the player is not grounded increase the airTime as the player is falling. If the player has been falling for more than 0.25 seconds trigger the next clip once the player is grounded and reset the airTime.

```c#
void PlaySoundIfFalling()
{
    if(!checkIfGrounded.isGrounded)
    {
        airTime += Time.deltaTime; 
    } else
    {
        if(airTime > 0.25f)
        {
            TriggerNextClip();
            airTime = 0; 
        }
    }
}
```

Add the following code to the update function. Check if the player is falling. If the player is walking only play a sound if the distance covered by the player is greater than 1 then reset the distance covered counter. 

```c#
PlaySoundIfFalling();

if(walking)
{
    distanceCovered += (currentSpeed * Time.deltaTime) * modifier;

    if(distanceCovered > 1)
    {
        TriggerNextClip();
        distanceCovered = 0; 
    }
}
```

Finally, go back to the FpsController GameObject and setup the footsteps script as follows:

![](../footsteps-script.png)

Find the free footsteps asset from the Unity Asset store and drag your clips into the clips array.

## Mixer setup

Create a new mixer called PlayerMixer. Create a group called footsteps. Drag the PlayerMixer mixer into the AudioMixer then select the footsteps group. Now go to your footsteps audio source and set the output to the footsteps group.

You should now hear different footsteps and be able to mix the levels in relation to all other sounds in the scene.