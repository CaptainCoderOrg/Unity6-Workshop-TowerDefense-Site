In this lesson, you will create a `MouseEvents` **MonoBehaviour Script** that will allow you to send messages between **Game Objects** when the mouse cursor interacts with them.

## Challenge: Create a MouseEvents Test Scene

Start by creating a test scene where you will be able to test your `MouseEvents` script in isolation. In this scene, you will create a small map 5x5 **Grid**. On the **Grid** you will have tiles that you the player can interact with (empty tiles) and tiles that the player cannot interact with (occupied tiles).  

- [ ] Create a new scene in your **Test Scenes** folder. I recommend naming it **Tile MouseEvents Test Scene**
- [ ] Create a 5x5 **Grid** of **Tiles**
- [ ] Ensure that you have at least 1 empty **Tile** that can be built upon
- [ ] Ensure that you have at least 1 blocked **Tile** that cannot be built upon
- [ ] Adjust your **Main Camera** to an **Isometric Perspective** with your **Grid** centered

When you're finished you should have a **Scene** that looks similar to the picture below:

![[occupied-spaces.png]]

![[isometric-camera-preview.png]]

## MonoBehaviour.OnMouseEvents
Unity provides several methods that can be used to detect mouse events that occur on **Game Objects** that have a **Trigger Collider**. To make use of this, you will write a script that detects **Mouse Events** that events.

### Create a MouseEvents Script
- [ ] Read the Friendly Manual: [Unity - Scripting API: MonoBehaviour.OnMouseEnter()](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/MonoBehaviour.OnMouseEnter.html)
- [ ] Create a **MonoBehaviour Script** called `MouseEvents`
- [ ] Add an `OnMouseEnter()` method to the script
- [ ] In `OnMouseEnter()` add a `Debug.Log` message to help test the script
- [ ] In `Debug.Log`, specify `this` as the context object. This will allow you to click on it in the console to see the attached **Game Object**.

![[mouse-events-on-mouse-enter.png]]

### Attach the Script to the Tile's Model
For a **Game Object** to receive mouse events, it must have a **Trigger Collider** attached. When the mouse cursor interacts with that **Trigger Collider** any **MonoBehaviours** that are attached to the same **Game Object** have their appropriate `OnMouseXYZ` method invoked.

- [ ] Open your **Tile Prefab** (this should be your empty tile that can be built upon)
- [ ] Add the `MouseEvents` component to the `model` child component
- [ ] Add a `BoxCollider` component to the `model` child component
- [ ] Click the `Edit Collider` icon to verify the shape of the collider matches your model

When you have finished, your **Tile Prefab** should look similar to the image below:

![[add-components-to-tile-model.png]]

### Test MouseEvents
Test to ensure your `MouseEvents` are being triggered

- [ ] Enter **Play Mode**
- [ ] Move the mouse over the empty tiles
- [ ] Click on the log message in the **Console** to highlight the context in the **Hierarchy**

![[verify-on-mouse-entered.webp]]

## OnEnter UnityEvent
Next, you will add a **UnityEvent** so the parent **Tile** can listen to the mouse events and perform an action.

- [ ] Add a `UnityEvent OnEnter` to your `MouseEvents` script
- [ ] When the `OnMouseEnter` method triggers, it should invoke the `OnEnter` event

![[add-on-enter-event.png]]

### UnityEvents in the Inspector
One of the biggest benefits of a `UnityEvent` is the ability to add functionality through the **Inspector**. To test that your event is firing properly, you can attach an action to it in the **Inspector**.

- [ ] Locate the `OnEnter` event in the **Inspector**

![[find-mouse-events.png]]

- [ ] Click the `+` icon to add an event listener

![[add-on-enter-event.webp]]

- [ ] Attach the `Tile` parent object to the new listener

![[attach-tile-to-onenter.webp]]

- [ ] Click the **Function** drop down
- [ ] Select, **Game Object > SetActive(bool)**

 ![[gameobject-set-active.png]]

- [ ] If necessary, **UNCHECK** the box below the `SetActive` function. 

![[leave-set-active-false.png]]

- [ ] Enter **Play Mode** 
- [ ] Move the mouse over your tiles

If all went well, the **Tile**s should deactivate in the **Hierarchy**. This is because you have registered `Tile.SetActive(false)` to be invoked when the `OnEnter` event is triggered.

![[verify-tiles-deactivate.webp]]

## Challenge: Change the Tile Name On Enter
- [ ] Remove the `SetActive` event from the event list
- [ ] Register a listener that changes the `Tile`'s name in the **Hierarchy** to "MouseEntered"

When you have finished, your scene should act similar to the video below:

![[change-tile-name-challenge.webp]]

## Challenge: OnMouseExit and OnMouseUpAsButton
- [ ] Read the Friendly Manual: [Unity - Scripting API: MonoBehaviour.OnMouseExit()](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/MonoBehaviour.OnMouseExit.html)
- [ ] Read the Friendly Manual: [Unity - Scripting API: MonoBehaviour.OnMouseUpAsButton()](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/MonoBehaviour.OnMouseUpAsButton.html)
- [ ] Add an `OnExit` UnityEvent to your `MouseEvents` script
- [ ] Add an `OnClick` UnityEvent to your `MouseEvents` script
- [ ] Use `OnMouseExit` to `Invoke` `OnExit`
- [ ] Use `OnMouseUpAsButton` to `Invoke` `OnClick`
- [ ] When exited, the **Tile**'s name in the **Hierarchy** should be "Exited"
- [ ] When clicked, the **Tile** should be set to inactive

When you have finished this challenge, your **Test Scene** should act similar to the video below:

![[challenge-enter-exit-click-complete.webp]]

## What's Next
With a `MouseEvents` implemented and ready to use, you can now create a **TileController** script that will allow your player to place a **Turret** in a specific location.

