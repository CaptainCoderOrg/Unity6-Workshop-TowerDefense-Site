## Challenge: Create a Tile Cursor Prefab
During game play, it will be helpful to your player to be able to tell more easily which tile they are hovering / selecting. To do this, you can use the `selection-a` or `selection-b` model which fit nicely around a tile.

![[tile-cursor-model-examples.png]]

- [ ] Create a new Prefab to represent your **Tile Cursor**
- [ ] Add a `model` child of the **Prefab** (I will be using `selection-a`)
- [ ] To appear above a tile, set the Y-position to at least 0.201 (tiles are 0.2 units thick)
- [ ] Add a **Tile Cursor** prefab to your scene

## Challenge: TileController MonoBehaviour
Currently, your **Tile Prefab** has no components attached to it. When placing a turret, it will be useful to track if the `Tile` is occupied. To do this, create a `TileController` MonoBehaviour Script that has a property `bool IsOccupied`. By default, this will be `false`.
- [ ] Create a `TileController` MonoBehaviour Script
- [ ] Add a property `bool IsOccupied` that is false by default
- [ ] Add a `TileController` component to your **Tile Prefab**

![[tile-controller-is-occupied-false.png]]

## TileController OnCursorEnter Event
The `TileCursor` will need to listen to your `TileController`s to know if the mouse has entered them. To do this, you will add an event to your `TileController` that will notify listeners when the mouse has entered.

- [ ] Add a `UnityEvent<TileController> OnCursorEnter`

![[add-on-cursor-enter.png]]

- [ ] Open your **Tile Prefab**
- [ ] If necessary, remove any events you've added to the `model`'s `MouseEvents`

![[clear-events.webp]]

### NotifyCursorEnter
You may have noticed that you cannot call `TileController.OnCursorEnter.Invoke` from the `MouseEvents.OnEnter` listener in the **Inspector**. This is because you must provide a `TileController` to call `OnCursorEnter.Invoke`. However, you can create a method that invokes it that takes no arguments.

- [ ] Add a method `NotifyCursorEnter()`
- [ ] In `NotifyCursorEnter()` invoke `OnCursorEnter` with `this`
![[notify-cursor-enter.png]]

- [ ] In the **Inspector**, add a listener to `MouseEvents.OnEnter` that will invoke `TileController.NotifyCursorEnter()`

![[tile-cursor-notify-cursor-enter.png]]

## TileCursor.HandleTileEntered
With your `TileController` propagating itself to listeners, you can now register your `TileCursor` on them and update its position to match.

- [ ] Create a `TileCursor` **MonoBehaviour** Script
- [ ] Add an `HandleTileEntered(TileController)` method
- [ ] In `HandleTileEntered`, set the `transform.position` of the cursor to match the `transform.position` of the `TileController`.

![[tile-cursor.png]]

- [ ] In your **Scene Hierarchy**, select one of your **Tiles**
- [ ] In the **Inspector**, locate the `Tile Controller` component
- [ ] Add a listener to the `OnCursorEnter` event
- [ ] Add your **Tile Cursor** to the event

![[add-tilecursor-to-tile.webp]]

By using a **Unity Event** that sends a `TileController`, you gain access to **Dynamic TileController** functions in the **Function Drop Down**. When you use this function, it will send the `TileController` as an argument to the specified method.

- [ ] Select the **Function Drop Down**
- [ ] Select **TileCursor > HandleTileEntered**  (the first option under Dynamic TileController)

![[dynamic-tile-controller.png]]

- [ ] Enter **Play Mode** and test that your **Tile Cursor** moves when the mouse moves over the **Tile** that you registered the event on.

![[verify-cursor-moves.webp]]

## GetComponentsInChildren
To move the **Tile Cursor** to the most recently entered **Tile**, you need to register the **Tile Cursor** on all of your `Tile Controller`s. Doing this through the **Hierarchy** and **Inspector** is challenging and error prone. To make things worse, if you decide to change your map, you have to do it again! Remember, as a programmer, any time you find yourself performing a repetitive task, you should ask yourself if there exists a way to automate it. If not, you should consider how difficult it would be to create your own automation.

Because all of your `TileController`s are children of your **Grid**, you can retrieve them all using the `GetComponentInChildren` method which retrieves all of the components of a specified type from the specified **GameObject** and all of its children.

- [ ] Read the Friendly Manual: [Unity - Scripting API: GameObject.GetComponentsInChildren](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/GameObject.GetComponentsInChildren.html#:~:text=GetComponentsInChildren%20checks%20the%20GameObject%20on%20which%20it%20is,a%20matching%20Component%20of%20the%20type%20T%20specified.)
- [ ] Add a `GameObject TargetGrid` to your `TileCursor`
- [ ] Add a `ListenToTilesIn(GameObject)` method to your `TileCursor`
- [ ] In `ListenToTileIn`, iterate through all of the `TileController` components and add a listener to call `HandleTileEntered`

![[listen-to-tiles-in.png]]

- [ ] Add a `OnEnable()` method to `TileCursor`
- [ ] In `OnEnable`, call `ListenToTilesIn(TargetGrid)`

![[on-enable.png]]

- [ ] In the **Inspector** add your **Grid** as the `TargetGrid` for your **TileCursor**

![[register-grid.png]]

- [ ] Enter **Play Mode** and test that your cursor changes between tiles as it moves between **Tiles**

![[verify-cursor-working.webp]]
## Challenge: On Disable
Recall that it is good practice to remove a listener if the listening object becomes inactive (e.g. `OnDisable`).

- [ ] Write a `StopListeningToTilesIn(GameObject grid)` method
- [ ] In `StopListeningToTiles` you should iterate through the specified grid searching for `TileController`s and call `OnCursorEnter.RemoveListener` on each one found.
- [ ] Add an `OnDisable` method
- [ ] In `OnDisable`, call `StopListeningToTiles` on the `TargetGrid`

## Challenge: OnCursorExit
Currently, when the player moves the mouse off of map into a space on the screen that does not contain a tile, the **TileCursor** remains on the most recently entered **Tile**. Instead, you should hide the **Tile Cursor**s `model`.

- [ ] Add an `UnityEvent<TileController> OnCursorExit` property to your `TileController`
- [ ] Add a `NotifyCursorExit()` method that invokes `OnCursorExit`
- [ ] Add a `GameObject Model` property to your `TileCursor`
- [ ] Add a `HandleTileExited(TileController)` method to `TileCursor`
- [ ] In `HandleTileExited`, call `Model.SetActive(false)` to hide the `TileCursor`'s model
- [ ] In `HandleTileEntered`, call `Model.SetActive(true)` to show the `TileCursor`'s model
- [ ] Connect all necessary events in the **Inspector**, `OnEnable`, and `OnDisable`

When you have successfully completed this challenge, your test scene should look similar to this:

![[complete-challenge-part-14.webp]]

## What's Next
With the ability to easily see which tile the player is interacting with, it is time to implement an `OnCursorClicked` event and an `OnTileSelected` method that will allow your player to spawn a turret.