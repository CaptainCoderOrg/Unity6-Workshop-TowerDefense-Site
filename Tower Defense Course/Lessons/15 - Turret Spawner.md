## Challenge: Create an OnCursorClick event
To be able to detect when the player has clicked on a tile, you will add a new event to the `TileController` that can be used to forward click events. 

- [ ] Add an `UnityEvent<TileController> OnCursorClick` property to your `TileController`
	- Hint: [[14 - Tile Cursor#TileController OnCursorEnter Event]]

- [ ] Verify that the event is now available in the inspector.

![[verify-on-cursor-click-inspector.png]]

- [ ] Add a `NotifyCursorClicked()` method that invokes `OnCursorClick`
	- Hint: [[14 - Tile Cursor#NotifyCursorEnter]]
- [ ] In your **Tile Prefab** update the model's `OnClick` event to invoke the `NotifyCursorClicked` method.

![[on-click-notify-cursor-clicked.png]]

## TurretSpawner
Now that you have an event that sends an event when a tile is clicked, you add in a Turret Spawner that will listen for clicks. If the tile is not occupied, it will spawn a turret at that location.

- [ ] Create a new `MonoBehaviour` called `TurretSpawner`
- [ ] Add a `GameObject TurretPrefab` property to your `TurretSpawner`
- [ ] Add the `[field: SerializeField]` attribute to the `TurretPrefab` property

![[15 - Spawning a Turret.png]]
 - [ ] Create a new `GameObject` in the **Turret Spawn Test Scene**, this will be your TurretSpawner
 - [ ] Add the `TurretSpawner` component
 - [ ] In the **Inspector** set the `TurretPrefab` to use the prefab you created for your Turret

![[set-turret-prefab.webm]]

### SpawnTurret(TileController)
- [ ] Add a `SpawnTurret(TileController)` method to your `TurretSpawner`
- [ ] In `SpawnTurret`, check to see if the specified `TileController` `IsOccupied` . 
- [ ] If it is, do nothing.  (`return`)
- [ ] If it is not occupied, `Instantiate` a `TurretPrefab` and set the position to match the position of the `TileController`

![[SpawnTurretMethod.png]]
### Testing SpawnTurret
Before writing a handler to register your `TurretSpanwer` on all tiles, it is helpful to test if the `SpawnTurret` method is working against a single tile.
- [ ] In the **Hierarchy** select a `Tile`
- [ ] In the **Inspector** add listener to the `OnCursorClick` event
![[select-tile.webm]]
- [ ] Add your `TurretSpanwer` as the listening object
- [ ] Select the `TurretSpawner.SpawnTurret` method as the method to invoke
![[set-spawn-turret-invoke.webm]]
- [ ] Take note of the tile that you updated.
- [ ] Enter Play Mode and click on that tile, if all went well, a turret was spawned into the scene
![[spawn-turret.webm]]

## Bug: Cursor Blocked
You likely noticed that after you placed your turret, the cursor stops registering on tiles that are near your turret. This is because the collider the turret is using to detect enemies is blocking the tile. To prevent this, you can create **Collision Layers** for your objects and specify which layers mouse events detect.

## Adding a Tile Collision Layer

- [ ] From the top menu select `Edit` > `Project Settings`
- [ ] On the left side, select the `Tags and Layers` tab
![[Assets/m15-Spawning a Turret/tags-and-layers.png]]

- [ ] If necessary, open the `Layers` drop down. (Ensure you are not in `Sorting Layers` / `Rendering Layers`)
- [ ] Add a `Tiles` layer
![[add-tile-layer.png]]

### Apply the Tile Layer to your Tile Prefabs
- [ ] In the **Project** explorer tab, navigate to your `Prefabs > Tiles` folder
- [ ] Select all of your Tile prefabs
- [ ] In the **Inspector**, change the `Layer` to `Tile`
- [ ] When prompted, select change children
- [ ] This will apply the `Tile` layer to all of your tile objects and their models
![[apply-tile-layer.webm]]

### Challenge: Update Camera Culling to Include Tiles
If you switch to the **Game** tab or enter **Play Mode** you will no longer see your tiles. This is because the Camera does not render them.
- [ ] Update the camera's `Culling Mask` to see the `Tile` layer

### Camera Event Layer
By default, the Camera will detect all collision layers. 

### Challenge: HandleClickEvent
Recall how the `TileCursor` listens to all tiles in your grid. Unfortunately, there is no way to set this in the **Inspector**. But, it is possible to modify the `Camera.eventMask` field using a script.

- [ ] Read the Friendly Manual: [Unity - Scripting API: Camera.eventMask](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Camera-eventMask.html)
- [ ] Read the Friendly Manual: [Unity - Scripting API: LayerMask](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/LayerMask.html)
- [ ] Create a new `MonoBehaviour` called `CameraEventMaskController`
- [ ] Add a `LayerMask EventMask` property 
![[eventmask.png]]
- [ ] In the **Hierarchy** select your **Main Camera**
- [ ] In the **Inspector**, add a `CameraEventMaskController`
- [ ] Set the `EventMask` to `Tile`
![[set-event-mask-tile.webm]]
- [ ] Add an `Awake()` method to your `CameraEventMaskController`
- [ ] In `Awake()`
- [ ] Use `GetComponent<Camera>()` to find the `Camera` component
- [ ] Set the `camera`'s `eventMask` to the `EventMask` property
![[15 - Spawning a Turret 1.png]]
- [ ] Enter Play mode and test that you can still see the selected tile after placing a turret
![[layer-mask-working.webm]]
## Challenge: Listen to all tiles
Now that you have verified that you can spawn a single turret, you are ready to listen to all of the tiles in a grid.
- [ ] Remove the listener you added to the tile in your scene
- [ ] Review how you listen to all tiles in `TileCursor` 
Update `TurretSpawner` such that
- [ ] OnEnable, listen to all of the tiles in your test scene's grid
- [ ] OnDisable, stop listening to all of the tiles in your test scene's grid

When you have finished, you should be able to click on any tile in the scene to spawn a turret:
![[spawn-many-turrets.webm]]

## Bug: Spawning Multiple Turrets on the Same Tile
Currently, if you click the same tile multiple times, it will spawn multiple turrets. This is because you never set `tilecontroller.IsOccupied` to `true` after spawning a turret in `SpawnTurret` Can you fix this bug?
- [ ] Update `SpawnTurret` to set `tileController.IsOccupied` to `true`
- Hint: You will also need to modify `TileController`

## What's Next?
Now that you are able to spawn turrets on a tile, it is time to add a TileCursor and a `TurretSpawner` to your map.