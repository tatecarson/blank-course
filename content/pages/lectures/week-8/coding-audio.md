  
First create an empty GameObject called AudioManger and add another GameObject as a child called Clickable Source. Add an audio source to the ClickableSource GameObject. Also add two more GameObjects to the AudioManger, one that plays music and one that plays ambience. 

Create a play sound script with this code: 

```c#
public class PlayASound : MonoBehaviour
{
    public AudioSource MusicSource;
    public AudioClip MusicClip;

    // Start is called before the first frame update
    void Start()
    {
        PlaySound(MusicSource, MusicClip);
    }

    void PlaySound(AudioSource source, AudioClip clip) {
        source.clip = clip;
        source.Play(); 
    }
}
```
  
Add that script to your AudioManager empty GameObject. Make sure it has a musical source as a child. Then add music to the source and clip to the script on the AudioManager. 

Now expand the PlaySound script be able to play an ambience. 

## Static classes

* are meant to be called by other classes 

First create a function called AudioFunction with this code: 

```C#
public static class AudioFunction
{
    public static void DeleteMeLater()
    {
        return;
    }
}
```

Call `AudioFunction.DeleteMeLater()` in the Start function PlayASound script and see how it works.

## Playing sound variations 

Lets now make the AudioFunction class play sounds from an array. Delete the contents of the AudioFunction class and add this code:

```c#
public static class AudioFunction
{
    public static void PlayRandomClip(AudioSource source, AudioClip[] clips,
            float pitchMin = 1f, float pitchMax = 1f) {

        // if the clips array is less than 2 don't do anything
        if (clips.Length < 2) return; 

        source.pitch = Random.Range(pitchMin, pitchMax); 

        // Creates a random value between 0-8
        int newValue = Random.Range(0, clips.Length);

        // make sure values do not repeat one after another 
        while(source.clip == clips[newValue])
        {
            newValue = Random.Range(0, clips.Length);
        }

        // inserts new value into array
        source.clip = clips[newValue];
        source.Play();
    }
}
```

Now lets add the ability to alter the pitch. Add this code to the PlayASound script:

```c#
public class PlayASound : MonoBehaviour
{
    public AudioSource MusicSource;
    public AudioClip MusicClip;
    public AudioSource AmbiSource;
    public AudioClip[] AmbiClip;

    // Start is called before the first frame update
    void Start()
    {
        PlaySound(MusicSource, MusicClip);
        AudioFunction.PlayRandomClip(AmbiSource, AmbiClip, 0.5f, 1.2f);
    }

    void PlaySound(AudioSource source, AudioClip clip) {
        source.clip = clip;
        source.Play(); 
    }
}
```

Now add two sounds to the AmbiClips array and make sure you have a random clip play everything you start the scene. 

## Adding Prefabs

Download this [vegetation package](https://dakotastateuniversity-my.sharepoint.com/:u:/g/personal/tate_carson_dsu_edu/EYILmeL5ajVGhGFVsLRO8a4B1UDFXRZhfG0U4d_03-mFyQ?e=Ycxq3B) and add it to your project. Then create a new scene called point and click then add a plane to the scene. Drag the AudioManger GameObject into the prefabs folder to make it a prefab. You can now use this prefab in any scenes. 

Add two trees to the scene and adjust their capsule colliders to take up the height of the tree. 

Create a new script called ClickableObjectSound and add this code:

```c#
public class ClickableObjectSound : MonoBehaviour
{
    public AudioSource ClickableSource;
    public AudioClip[] ClickableClip;

    public Vector2 PitchRange;

    private void OnMouseDown()
    {
        if(!ClickableSource.isPlaying)
        {
            AudioFunction.PlayRandomClip(ClickableSource, ClickableClip, PitchRange.x, PitchRange.y);
        }
    }
}
```

Then add the script to each tree prefab. Now you can add the three woods ambiences into the clickable clip array on the ClickableObjectSound script. Make sure the prefabs are locked before attempting to do this. 

Create a Clickable Source audio object in your audio manager folder. Add this source to your ClickableObjectSound script on the first tree prefab. Then unclick the lock and under modified component apply prefab to the second tree prefab.

Add some more trees! 

Now test your game and make sure that each tree is playing a random sound and pitch. 