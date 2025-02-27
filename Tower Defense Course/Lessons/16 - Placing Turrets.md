## Challenge: Create a TurretSpawner Prefab
To be able to use your `TurretSpanwer` in any scene, you can turn it into a prefab.
- [ ] Turn your `TurretSpawner` into a prefab

## Practice: Update Your Level's Camera
- [ ] Open your level scene
You'll notice that in your level scene, your camera no longer renders your Tiles. This is because you moved your `Tile` prefabs to the `Tile` layer. 
- [ ] Update your main camera's culling mask to show the `Tile` layer
## Add a TileCursor and TurretSpawner
- [ ] Add a `TileCursor` and a `TurretSpawner` to your scene
- [ ] In the **Inspector**, set your `TileCursor` and `TurretSpawner` to listen to the tiles in your level's grid
![[add-tilecurser-and-spawner.webm]]
- [ ] Enter Play Mode and test that you can now place turrets
![[test-place-turret.webm]]
## Practice: Fix Layer Collisions
You may have noticed that you are unable to place turrets within another turrets **Area of Engagement**. Recall that you fixed this for your Test Scene in [[15 - Turret Spawner#Camera Event Layer]].
- [ ] Update your camera to only interact with the `Tile` layer

## Create a `GameCamera` Prefab
As you continue to add new scenes to your game, you may need to adjust the camera again. Ideally, the camera will work the same in every scene. To help create this consistency, you can create a `GameCamera` prefab that can be reused in your test scenes. Additionally, it can be useful to have the camera nested in a parent object just in case you need to add sibling game objects.
- [ ] In the **Hierarchy**, create a parent object for your `Main Camera` and name it **GameCamera**
- [ ] Turn the **GameCamera** object into a **Prefab**

![[create-game-camera-prefab.webm]]

## Practice: Remove existing Turrets
Now that you have a way to spawn turrets into your scene during Play Mode, you can remove the starting turrets from the scene.
- [ ] Remove any turrets that you placed directly in your scene
## Creating a Place Turret Button
Next, you will add a button to your scene that enables the `TileCursor` and `TurretSpawner` GameObjects when clicked.

### Enabling and Disabling TileCursor and TurretSpawner
Verify that disabilng TileCursor and TurretSpawner disables the ability to place turrets.
- [ ] Select both `TileCursor` and `TurretSpawner` in the **Hierarchy**
- [ ] In the **Inspector**, disable both game objects
- [ ] Enter **Play Mode** and verify that you can no longer place turrets
- [ ] While in **Play Mode** enable both `TileCursor` and `TurretSpawner`
- [ ] Verify that you can place turrets while they're enabled
![[test-enable-disable-turret-cursor.webm]]
### Add a Button to your Scene
- [ ] In the **Hierarchy**, click the `+` icon
- [ ] Select `UI` > `Button - TextMeshPro`
![[Add button textmeshpro.png]]

The first time you add a `TextMeshPro` object to a Unity Project, you will be prompted to import the **Text Mesh Pro** library.

- [ ] Import Text Mesh Pro Essentials
![[import-tmp-essentials.png]]
- [ ] You do not need to Import the Examples & Extras

After the library has been imported, you should see 3 new **Game Objects** in your **Hierarchy**
![[after-importing-button.png]]
### What is a Canvas/EventSystem
You may be wondering what are the **Canvas** and **EventSystem** objects that were added to your scene. The **Canvas** in Unity is a component that acts as the root for all UI elements, determining how they are rendered and positioned in the game world or screen space. The **EventSystem** is responsible for processing and managing user input, such as mouse clicks, touches, and controller interactions, ensuring that UI elements respond correctly. Together, the Canvas and EventSystem enable interactive user interfaces by handling rendering and input events within Unity’s UI system.
## Positioning the Button
If you are in the **Scene** tab, you probably do not see the **Button** you added. This is because the button is added to the **Canvas** which, by default, exists as a screen overlay.
- [ ] Open the **Game** view tab
- [ ] Verify that there is a button in the center of the screen
![[verify-button-in-center.png]]
In the **Scene** view, you can switch to 2D mode to more easily view the button on the canvas.
- [ ] Open the **Scene** view tab
- [ ] Select the **2D** mode in the top right of the **Scene** view
- [ ] Double click on the **Canvas** in the **Hierarchy** to focus the camera on the canvas
![[view-canvas-in-scene-view.webm]]
### Moving the Button
- [ ] Select the **Move** tool
- [ ] Move the Button to the bottom left corner of the canvas
![[reposition-button.webm]]
### Different Screen Resolutions
Unfortunately, setting the position of the button in this way will only work if your player is using the exact same resolution as you. Unity provides tools for testing different resolutions so you can determine how your game will work in different screen modes.
- [ ] Open the **Game** view tab
- [ ] Toggle between different resolutions
- [ ] Observe the button moving to different screen positions
![[button-changes-resolution.webm]]

### UI Pivots
This is happening because your button was positioned relative to the center of the screen. Thus, if the user is using a smaller resolution, the button will appear closer to the center of the screen. To help with this, Unity provides a way to specify a **Pivot** point.
- [ ] Select the your **Button** from the **Hierarchy**
- [ ] In the **Inspector**, find the **Rect Transform** component
- [ ] Click the **Pivot** icon to open the "quick" pivot and anchor settings
- [ ] Click the Bottom Left Corner pivot icon
![[set-pivot-bottom-left.webm]]
This sets the objects position to be relative to the bottom left corner of the users screen regardless of their resolution.
- [ ] If necessary, adjust the buttons position so it is near the bottom left corner
- [ ] Enter Play Mode
- [ ] Change Resolutions
- [ ] Observe that the button doesn't change position
- [ ] The size of the button may appear to change -- however, this is because the zoom scale is changing.
![[observe-pivot.webm]]

### Button.OnClick Listener
By default, Unity's UI button object comes with an OnClick Listener that can be used in the **Inspector** to invoke a method on an object.
- [ ] Select your button in the **Hierarchy**
- [ ] In the **Inspector** find the `Button` component
- [ ] Within the `Button` component, locate the `On Click` event
- [ ] Add a Listener by clicking the `+` icon
![[create-button-listener.webm]]

- [ ] Add the `TileCursor` to the listener
- [ ] Invoke the `GameObject.SetActive` method and set it to true (enable checkbox)
![[set-tile-cursor-active.webm]]
- [ ] Enter **Play Mode**
- [ ] Verify that the cursor does not display if you move on a tile
- [ ] Click the **Button**
- [ ] Verify that the cursor does display if you move on a tile
![[test-button.webm]]
### Practice: Enable TurretSpawner
- [ ] Update the button such that it will enable both the **TileCursor** and **TurretSpawner** when the button is clicked

When you're finished, your game should operate similar to the video below
![[practice-turretspawner.webm]]

### Changing the Button Text
- [ ] Expand the **Button** in the **Hierarchy**
- [ ] Select the **Text (TMP)** child
- [ ] In the **Inspector** find the **Text** component
- [ ] Update the **Text** component to display "Build"
![[change-build-text.webm]]
# What's Next?
Now that you have a basic understanding about adding a button to your scene that can invoke methods on your other GameObjects, it is time to add in resources that will determine if the player is able to place a turret on the map.

[[17 - Building Resources]]