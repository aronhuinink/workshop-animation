# MagikarpGirlAnimationWorkshop

**Goal**

In this workshop you will have a better vision of how to use and set up a functional character animation system, creating and managing animation states, transitions and blend trees, and linking these animations to a Cinemachine state-driven camera that automatically changes angles based on the character’s current animation state.

**Important!**
- Install the Input System Package (if it was not already installed)
- It's recommended to use Unity version: ```6000.2.6.f2```, but any other version might work as well.



## Animator Component 💃
**Step 1: Create and Configure an Animator**
- Find the Idle animation clip in the ***Animations*** folder and change it's ***Rig Type*** from ```Generic``` to ```Humanoid``` in the Inspector by selecting the animation.
- Make sure  ***Loop Time*** is enabled in the animation clip.
- Create a new ***Animator Controller*** in the ***Assets/Animator*** folder by right clicking and navigate to: **Create -> Animation -> Animator Controller**
- Attach the Animator on the Player Prefab in the Inspector
- Create a ***Blend Tree*** state for the Idle animation in the Animator
- Open the Blend Tree and change the ***Blend Type*** to ```2D Freeform Directional```
- Create two float parameters called: ```VelocityX``` and ```VelocityZ``` and change both *'Blend'* parameters in the Inspector
- Add a Motion Field
- Choose the Idle animation clip and assign it to the Motion Field
- Leave the PosX and PosY on ```0```
- Run the game. *(Your character should play the Idle animation)*
- Make sure ***Loop Time*** is enabled for the Idle animation clip
- Disable ***'Apply Root Motion'*** on the Animator in the Inspector

***What you have learned of creating this setup?***

*The reason why you need to use a Humanoid rig, is so you can use aq avatar on the model which can be used to retarget humanoid animations. This is usefull for when you want use the same set of animations on a different humanoid model.*

*The reason why you use a 2D Freeform Directional blend tree is to smoothly blend between animations based on movement direction, allowing your character to transition between forward, backward, and sideways motions for more realistic movement.*

**Step 2: Blend Tree and Movement**

Inside the Blend Tree, add more motion fields for: 
1. Running Forward and set ```Pos X = 0``` and ```Pos Y = 1```
2. Running Backward and set ```Pos X = 0``` and ```Pos Y = -1```
3. Strafe Left and set ```Pos X = -1``` and ```Pos Y = 0```
4. Strafe Right and set ```Pos X = 1``` and ```Pos Y = 0```


**Step 3: Add more Animation States**
- Add a new Empty State called ```PushUp```
- Assign the animation clip "PushUp" to that state
- Create two transitions between Idle and Push Ups
- Uncheck "Has Exit Time" in the transition Idle -> Push
- Create a trigger parameter named: ```PushUpTrigger```
- Add a new field in Conditions and select ```PushUpTrigger```

- While playing the game you can now press **'P'** on your keyboard. It will switch from Blend Tree state to Push Up state, which means the push-up animation will play. Pressing **'P'** again will switch from the PushUp state back to the Blend Tree state.


## 2 Cinemachine Component 🎥

Now that your animation state machine works, we will make the camera change angles based on it.
For ease of use, we’ll use a Composite Camera setup.

**Basic prep**
-Just in case something went wrong regarding cinemachine, please make sure cinemachine is installed.
**Create a State-Driven Camera**    
- Create a State-Driven Camera Object in your scene.
- Drag your character into the Animated Target field.
>The camera should now have access to the Animator States.
- Add several child cameras under the state-driven camera. You can do this from the inspectortab with the plus sign under child cameras.
- Position these child cameras in different places so it’s easy to see when the view changes.
>For ease of use you can align a camera with your viewport by **rightclicking** the camera and choosing **align with view**

**Link States to Cameras**
- In the State-Driven Camera settings, add rows to connect animator states to specific cameras. You can do this through the inspector under the instructions header
- In each row, select a State and a Camera.
- Play the game and observe whether the camera angles switch smoothly based on animation states.

**Fine-Tune the Camera**
- Experiment with Default Blends in the main State-Driven Camera to control how transitions between cameras feel.
- Adjust blend times, easing, and field of view until the result feels natural and dynamic.

 **Result** ✅
You now have a fully functioning animated character that transitions smoothly between animations, and a Cinemachine system that dynamically changes camera angles depending on those animation states.












