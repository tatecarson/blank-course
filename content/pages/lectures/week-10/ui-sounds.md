---
title: "UI sounds"
---

## Setup 

Create a new scene in the scene folder named `UI` and open it. In Unity UI GameObjects exist inside of Canvas GameObjects. Create a button GameObject and see how its inside of Canvas. Toggle 2D view in the scene pane. This allows you to see the Canvas like a player will. Set the aspect ratio of the Game pane to 16:9. Place the button in the center of the Canvas if it isn't already. Select the EventSystem GameObject and play the scene. Notice the feedback in the lower right side of the screen. See the pointer position and the boolean for clicking on the button or not. 

## Add sounds 

Add another button to the scene. To play a sound we will attach a function to the click event of the button. Create a new script in the script folder named `ButtonSound`. We only want to play one sound for each button so we need to create a new function instead of using our AudioFunction script.  

Create a function that takes an AudioClip as a parameter. This function will be called when the button is clicked. Create a public AudioSource then inside the function assign the audio clip to the AudioSource and play the sound. Look back at your AudioFunction if you're not sure how to do this. 

Create a GameObject AudioSource called ButtonSource then add the script to it. Add the ButtonSource to the script variable. In the button on click section find the function you created and select it. Add the ButtonSource game object to it, because it has the script attached to it. This is now where you can add a clip to the source. We do it this way so that each button can play a different clip through the same AudioSource. 

Create two more buttons and add sounds to them. To one of the buttons add an Event Trigger component to it. This allows you to trigger functions on all sorts of events. Choose the pointer enter event. This will trigger the function when the pointer enters the button.

See the [supported events](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/SupportedEvents.html) list for more details on other types of events. 

## Scene switching 

Now we'll use a button to go from the UI to our Locomotion scene. First, go to file -> build settings and add open scene to the scenes in build list. Now open open the Locomotion scene and do the same thing. 

Create a new script called SceneSwitch. Add this line to the top of the script `using UnityEngine.SceneManagement;`. This gives us access to the scene management functions. Then create a public function that runs the following code `SceneManager.LoadScene(1);` This will load scene 1. If we have multiple scenes you would choose different numbers. Now trigger this function with the on click event of the button. You should now be able to switch scenes. 

For a final addition switch back to the UI scene when the player walks over the trigger. 