# MagikarpGirl Animation Workshop

In this workshop you will learn the basics for setting up a functional character animation system by
creating and managing animation states, transitions and blend trees, and linking these animations to a Cinemachine state-driven camera that automatically changes angles based on the character’s current animation state.

It's recommended to also read the call-outs between the different steps to get the most out of this workshop.

<hr>

## Getting started !
1. **Clone this repository:**
```
git clone https://github.com/aronhuinink/workshop-animation.git
```
2. **Add the project `workshop-animation` in Unity Hub and open it.**

**Important !**
- Install the Input System Package (if it has not already been installed)
- Install the Cinemachine Package (if it has not already been installed)
- It's recommended to use Unity version: ```6000.2.6.f2```, but any other version might work as well.

Now you should be ready to get started with the workshop !
<hr>

## Animator Component 💃
### Step 1: Create and Configure an Animator
First off, you will be creating an Animator Controller which will manage all the animations 
you add to it in a specified order and control how transitions between these animations take place.

1. Select the Idle animation clip in the `Animations` folder and change its **Rig Type** from ```Generic``` to ```Humanoid``` in the Inspector. Click **'Apply'** to save the changes.
> *By setting the rig to Humanoid, you can assign an Avatar to the model which enables you to
> retarget humanoid animations. This allows you to easily use the same set of animations between different humanoid models 
> as long as they contain an Avatar reference.*

2. Check  the **Loop Time** box in the animation clip so the animation won't stop after a single execution.
3. Create an **Animator Controller** component asset in the **Assets/Animator** folder by right clicking 
and navigating to: **Create -> Animation -> Animator Controller**.
4. Attach the Animator Controller to the Player Prefab in the Inspector. 
5. Open the **Animator Window** by double-clicking the Animator Controller. This is where you will be editing the Animator Controller.

### Step 2: Blend Tree & Movement
1. Create a **Blend Tree** state in the Animator Controller and rename it to "Movement".
> Blend Trees allow for smooth blending of animations with similar motions such as walking and running.
2. Open the Blend Tree and change the **Blend Type** to `2D Freeform Directional`.
> A 2D Freeform Directional Blend Tree allows you to add multiple animations in the same direction 
> (e.g., walk forward and run forward, strafe walk left and strafe run left) using two parameters opposed to a Simple Directional Blend Tree which only allows
> you to add one animation in every direction.
3. Create two float parameters called `VelocityX` and `VelocityZ` in the Animator Window and change both Blend Tree parameters in the Inspector.
> `VelocityX` should reference strafing speed and `VelocityZ` should reference forward speed so pay attention to which parameter you assign which Velocity parameter !
The parameter values are being updated using the pre-made `PlayerController` script.
4. Add a **Motion** field and assign the Idle animation clip.
5. For the Idle animation, leave the PosX and PosY at `0`. This is the default animation of the player inside the Blend Tree when no inputs are provided.
6. Disable **'Apply Root Motion'** in the Animator Component in the Inspector.
> When Root Motion is enabled, the position and rotation of the character will be controlled by the animation itself instead 
> of being script based (e.g., transform). This can be useful in certain situations but you will not be using this during this workshop.
7. Run the game. *(Your character should play the Idle animation :] )*

8. Inside the Blend Tree, add more Motion fields. You will notice that a Blend Tree Diagram popped up. 
9. Assign the animations to the fields. Don't forget to set the **Rig Type** and **Loop Time** settings correctly again for these !
   - Running Forward and set `Pos X = 0` and `Pos Y = 1`
   - Running Backward and set `Pos X = 0` and `Pos Y = -1`
   - Strafe Left and set `Pos X = -1` and `Pos Y = 0`
   - Strafe Right and set `Pos X = 1` and `Pos Y = 0`</br>
   
   > After assigning the following animations to the fields, you can drag around the red dot to see how the different animations blend for different `VelocityX`(`Pos X`)
        and `VelocityZ` (`Pos Y`) values. You can see the model in the inspector move accordingly by clicking the _Play_ button in the inspector. 
   The circles that appear around the blue diamonds (the animations) show which animations influence the blend at the current values.

### Step 3: Add more Animation States
1. Return to the **Base Layer** in the Animator Controller and add a new Empty State named ```PushUp```.
2. Rename the state to "Push Up" and assign the animation clip "PushUp" to that state.
3. Create two transitions between the Movement Blend Tree and the Push Up state.
4. Uncheck **"Has Exit Time"** in the transition Movement -> Push Up.
5. Change the **Transition Duration** value to make the transition blend more smoothly. 
6. Create a trigger parameter named ```PushUpTrigger```
7. Inside the transitions, add a new field for **Conditions** and select ```PushUpTrigger```

- While playing the game you can now press **'P'** on your keyboard. It will switch from the Movement Blend Tree state to the Push Up state and play the push-up animation. 
Pressing **'P'** again will switch from the Push Up state back to the Blend Tree state.

<hr>

## Cinemachine Component 🎥

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












