# MagikarpGirlAnimationWorkshop

**Goal**

In this workshop you will have a better vision of how to use and set up a functional character animation system, creating and managing animation states, transitions and blend trees, and linking these animations to a Cinemachine state-driven camera that automatically changes angles based on the character’s current animation state.


## Animation Setup 💃
**Step 1: Create and Configure an Animator**
- Find the Idle animation clip in the ***Animations*** folder and change it's ***Rig Type*** from ```Generic``` to ```Humanoid```
- Enable ***Loop Time*** in the animation clip.
- Create a new ***Animator Controller*** in the ***Assets/Animator*** folder by right clicking and navigate to: **Create -> Animation -> Animator Controller**
- Attach the Animator on the Player Prefab in the Inspector
- Create a ***Blend Tree*** state for the Idle animation in the Animator
- Open the Blend Tree and change the ***Blend Type*** to ```2D Freeform Directional```
- Create two float parameters called: ```VelocityX``` and ```VelocityY``` and change both *'Blend'* parameters in the Inspector
- Add a Motion Field
- Choose the Idle animation clip and assign it to the Motion Field
- Leave the PosX and PosY on ```0```
- Run the game. *(Your character should play the Idle animation)*
- Make sure ***Loop Time*** is enabled for the Idle animation clip
- Disable ***'Apply Root Motion'*** on the Animator in the Inspector

***What you have learned of creating this setup?***

---

**Step 2: Blend Tree and Movement**

Inside the Blend Tree, add more motion fields for: 
1. Running Forward and set ```Pos X = 1``` and ```Pos Y = 0```
2. Running Backward and set ```Pos X = -1``` and ```Pos Y = 0```
3. Strafe Left and set ```Pos X = -1.5``` and ```Pos Y = 0```
4. Strafe Right and set ```Pos X = 1.5``` and ```Pos Y = 0```


**Step 3: Add more Animation States**
- Add a new Empty State called ```PushUp```
- Assign the animation clip "PushUp" to that state
- Create two transitions between Idle and Push Ups
- Uncheck "Has Exit Time" in the transition Idle -> Push
- Create a trigger parameter named: ```PushUpTrigger```
- Add a new field in Conditions and select ```PushUpTrigger```

- While playing the game you can now press **'P'** on your keyboard. It will switch from Blend Tree state to Push Up state, which means the push-up animation will play. Pressing **'P'** again will switch from the PushUp state back to the Blend Tree state.


*What *
















Create a transition between Idle and Push Ups.

Add a Boolean parameter (e.g., DoPushUps) to control when to perform push-ups.

Create a transition back to Idle when the Boolean is set to false.

Go to the Idle animation clip again and ensure Loop Time is enabled.







## 2 Cinemachine Component 🎥

**Set Up State-Driven Camera** 
- Now that your animation state machine works, we will make the camera change angles based on it.
- For ease of use, we’ll use a Composite Camera setup.


**Create a State-Driven Camera**
- Create a State-Driven Camera Object in your scene.
- Drag your character into the Animated Target field.
- The camera should now have access to the Animator States.
- Add several child cameras under the state-driven camera.
- Position these child cameras in different places so it’s easy to see when the view changes.

**Link States to Cameras**
- In the State-Driven Camera settings, add rows to connect animator states to specific cameras.
- In each row, select a State and a Camera.
- Play the game and observe whether the camera angles switch smoothly based on animation states.

**Fine-Tune the Camera**
- Experiment with Default Blends in the main State-Driven Camera to control how transitions between cameras feel.
- Adjust blend times, easing, and field of view until the result feels natural and dynamic.

 **Result** ✅
You now have a fully functioning animated character that transitions smoothly between animations, and a Cinemachine system that dynamically changes camera angles depending on those animation states — creating a polished, game-ready presentation.












