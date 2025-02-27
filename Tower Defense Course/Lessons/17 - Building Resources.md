# PlayerController Class
Currently, when your player clicks the **Build** button, it enables the **TurretSpawner** which, in turn allows them to click on tiles to spawn multiple turrets. Next, you will create a `PlayerController` class that will track a `Gold` resource for the player that limits their ability to place towers. When the player builds a tower, it will reduce the player's `Gold`.

## Practice: Create a PlayerController Class and GameObject

- [ ] Create a new `MonoBehaviour` named `PlayerController`
- [ ] Add an `int Gold` Property
- [ ] In your scene, add a new **GameObject** that has a `PlayerController` component . 
- [ ] Set the `Gold` property in the **Inspector** to `200`

When you have finished, your scene should look similar to the image below:

![[add-player-controller-gold-200.png]]

## Add a Text Label for Gold
To help the player know how much gold they have, add a **Text Label** to your **Canvas**
- [ ] In the **Hierarchy**, right click on your **Canvas**
- [ ] Select Create > UI > Text - TextMeshPro

![[create-gold-label.webm]]
### Practice: Anchor the Gold Label to the Top Left Corner
Recall how you anchored your **Build** button to the bottom left corner of the screen (see: [[16 - Placing Turrets#UI Pivots]]). You can do the same thing with any UI component. Additionally, if you hold Shift and Alt while selecting a pivot, it will move your UI component to that position.
- [ ] Select your `Gold Label`
- [ ] In the **Inspector** click the **Pivot** icon on the **Rect Transform**
- [ ] Press and hold Shift + Alt
- [ ] Click the Top Left Corner pivot icon
- [ ] Observe that the text moves to the top left corner, additionally the anchor and pivot values update.
![[set-anchor-and-pivots.webm]]
- [ ] Adjust the `Pos X` and `Pos Y` values slightly to keep the text from touching the edge of the screen.
![[adjust-x-and-y.webm]]
- [ ] Update the default text to display "Gold: 0"
![[adjust-x-and-y 1.webm]]

## Updating the Gold Label
Now that you have a Gold Label, you can make it reference your `PlayerController` and update the text component to display the current amount of Gold the player has available.

### Create a GoldLabelController MonoBehaviour
- [ ] Create a new `MonoBehaviour` named `GoldLabelController`
- [ ] Add a `PlayerController Controller` property
- [ ] Add a `TextMeshProGUI Label` property
- [ ] Add an `Update()` method:
- [ ] Set `Label.text` to display `Controller.Gold`

![[GoldLabelController.png]]
### Attach the GoldLabelController component
- [ ] Add a `GoldLabelController` component to your `GoldLabel`
- [ ] Connect the `PlayerController` and `Label` properties in the **Inspector**
	- Note: `Label` should reference the **Gold Label** (self)
- [ ] Enter Play Mode to confirm the label updates
- [ ] Adjust the `PlayerController`'s **Gold** property to observe the change
![[update-gold.webm]]

## Spending Gold to Spawn

### Practice: Reference PlayerController in TurretSpawner
To be able to check if we can spawn a turret, the **TurretSpawner** must check if the player has enough gold.
- [ ] Add a `PlayerController Controller` property to the `TurretSpawner` **MonoBehaviour**
- [ ] In the **Inspector** connect the **PlayerController** to the **TurretSpawner**
When you have finished, your inspector should look similar to the image below:

![[reference-player-controller.png]]

### Challenge: Add a CanSpawn Method to TurretSpawner
- [ ] Add a `bool CanSpawn(TileController tileController)` method to the `TurretSpawner` **MonoBehaviour**:
- [ ] The method returns `false` if the `tileController` is occupied 
- [ ] The method returns `false` if the `Controller` does not have at least 50 gold
- [ ] Otherwise, the method returns `true`
- [ ] Update the `SpawnTurret` method to use `CanSpawn` to determine if a turret can be spawned
- [ ] Update the `SpawnTurret` method to reduce `Controller.Gold` by 50
- [ ] Enter **Play Mode** to test your spawner
- [ ] You should only be able to place 4 turrets
- [ ] After placing each turret, you should observe that the gold decreases

When you have finished, you should see something similar to the video below:
![[testing-can-spawn.webm]]

## Interaction Hints
Currently, your player does not receive much information about what the result of clicking on a tile will be. This can be both confusing and frustrating. How were they supposed to know the turret was going to cost 50 gold! Maybe they didn't see that they were out of gold and don't understand why clicking is not placing a turret. To help create a better user experience, you will add in a text label that will display information to the player.

### Practice: Add an Information Label to your Canvas
- [ ] Add a **Text - TextMeshPro** to your **Canvas** (Info Label)
- [ ] Change the default text to "Player Interaction Info Label"
- [ ] Position and resize the text on the screen to your liking
- **Note**: In the preview project, the information label will be on the bottom center of the screen 
When you have finished, your game view should look like the video below:
![[player-interaction-info-label.png]]

### Practice: Add InfoLabel to PlayerController
- [ ] Add a `TextMeshProGUI InfoLabel` to your `PlayerController` **MonoBehaviour**
- [ ] Add a `Start()` method to `PlayerController`
- [ ] Set `InfoLabel.text` to display "Click Build to Place a Turret"
- [ ] Connect the **InfoLabel** in the **Inspector**
- [ ] Enter **Play Mode** to test that the **InfoLabel** updates when the game starts
When you have finished, your scene should look similar to the video below:
![[place-build-test.webm]]

### Disable Raycast Target
By default, Text labels intercept click events of a mouse. This can be useful if you want to detect if a mouse is hovering over a label. However, this can be problematic if your label is blocking a button or your game scene. This can be disabled in the `Extra Settings` section of the `TextMeshPro - Text(UI)` component. 
- [ ] Disable **Raycast Target** in your **Info Label** / **Gold Label** to prevent them from blocking your buttons / turret placements.
![[disable-raycast-target.webm]]
### TurretSpawner.ShowInfo(TileController)
- [ ] Add a `ShowInfo(TileController)` method to `TurretSpawner`:
- [ ] If the `tileController.IsOccupied` display "Cannot build here"
- [ ] If the `Controller.Gold < 50` display "<color=red>Not enough gold</color>"
- [ ] else display "50 Gold - Place Turret"

![[show-info-method.png]]
### Challenge: Display Info to the Player
- [ ] Update your `TurretSpanwer` **MonoBehaviour** in the following ways
- [ ] When enabled, display "Select a Tile"
- [ ] Add a listener such that `ShowInfo` is called when the cursor enters a tile
- [ ] Add a listener such that "Select a Tile" is displayed when the cursor exits a tile
- [ ] After a turret is placed, disable the **TurretSpawner**
- [ ] Be sure to remove any listeners when **TurretSpawner** is disabled
- [ ] When disabled, display "Click Build to Place a Turret"
- [ ] Enter **Play Mode** to test your changes

When you have finished, your game should behave similar to the scene below:

![[17-challenge-complete.webm]]