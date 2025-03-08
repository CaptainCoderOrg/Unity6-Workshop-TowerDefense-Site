# Challenge: Design a New Building
So far, you have created two buildings: one that fires projectiles when enemies are within its Area of Engagement and another that continuously generates Gold. In this challenge, you should define a new structure of your own choosing. Below are a few ideas to choose from.
- [ ] A turret that has a larger range but longer cooldown
- [ ] A turret that fires at all enemies within its Area of Engagement
- [ ] A building that doubles the amount of gold of all GoldGenerates adjacent to it
- [ ] A building that slows down enemies that are within its AreaOfEngagment
- [ ] A building of your own design
# Challenge: Add a Build Button for your new Building
- [ ] Add a third button that can be used to place your new building
- [ ] Enter Play Mode to test that your building works as expected
If all went well, you should have a scene that looks similar to the one below. For the demo, I've created a Cannon turret that has a wider range than the original Turret but has a longer cooldown.

![[adding-new-building.webm]]
# BuildingData
Currently, the cost of each building is set to 50 directly in the code. To give your player more interesting choices, you can make each building have a different cost. To do this, you will create a **ScriptableObject**.
## Defining a Scriptable Object
A `ScriptableObject` can be used to define and edit data in the **Unity Inspector** that does not exist on a Game Object.
- [ ] **Read the Friendly Manual**: [Unity - Manual: ScriptableObject](https://docs.unity3d.com/6000.0/Documentation/Manual/class-ScriptableObject.html)
- [ ] In your `Scripts` folder right click
- [ ] Select **Create** > **Scripting** > **ScriptableObject Script**
- [ ] Name the **ScriptableObject**: "BuildingData"

![[scriptable-object.png]]
- [ ] Open the `BuildingData` script
- [ ] Verify that the class is named `BuildingData`
- [ ] Verify that the class extends `ScriptableObject`
- [ ] Verify the `menuName` is set to `Scriptable Objects/BuildingData` 
![[verify-buildingdata.png]]
## Creating a Scriptable Object
- [ ] Create a new folder in `Assets` called `Data`
- [ ] Open the `Data` folder
- [ ] Right click and select **Create** > **Scriptable Objects** > **BuildingData**
**Note:** The option to select **Scriptable Objects > BuildingData** was defined by the `CreateAssetMenu` attribute in your `BuildingData` script.

![[create-building-data.webm]]

- [ ] Rename the new `BuildingData` object to `TurretData`

![[TurretData.webm]]
## Adding Properties to BuildingData
- [ ] Open the `BuildingData` script
- [ ] Add a `string Name` property
- [ ] Add an `int Cost` property
![[fields.png]]
## Editing Properties in the Inspector
Similar to **MonoBehaviours** you can modify serialized properties in Unity's **Inspector**.
- [ ] Select `TurretData` in your **Project** window
- [ ] Set the `Cost` in the **Inspector**
- [ ] Set the `Name` in the **Inspector**

![[SetTurretData.webm]]

### Practice: Add a BuildingPrefab Property
- [ ] Add a `GameObject BuildingPrefab` property to `BuildingData`
- [ ] In the **Inspector** set **BuildingPrefab** to be your Turret Prefab

When you've finished, your `TurretData` should look similar to the image below:

![[turret-prefab-set.png]]

## Creating Multiple Instances
One of the benefits of a `ScriptableObject` is the ability to create multiple instances each with their own values.
- [ ] In your `Data` folder:
- [ ] Create a **BuildingData** for your **GoldGenerator**
- [ ] Create a **BuildingData** for the building you defined at the beginning of this lesson

When you're done, your `Data` folder and objects should look similar to the video below:

![[BuildingDatas.webm]]
# Building Spawner
Your `TurretSpawner` has outgrown its original functionality. Its initial purposed was meant to spawn turrets. However, it is time to replace it with a `BuildingSpawner` that can be used to place anything defined as a `BuildingData`.
## Rename TurretSpawner to BuildingSpawner
- [ ] Select the `TurretSpawner` script
- [ ] Rename the script to `BuildingSpawner`

![[rename-building-spawner.webm]]
- [ ] Open the script
- [ ] Update the class name to match the file name `BuildingSpanwer` 

![[classname-match.png]]
## Update References in the Scene
- [ ] Select your **TurretSpawner** from the **Hierarchy**
- [ ] Rename it to **BuildingSpawner**
- [ ] Verify that it has a **Building Spawner** component in the **Inspector**

![[verify-name-component.png]]
## Refactor `BuildingSpawner` to use BuildingData
- [ ] Open the `BuildingSpawner` **MonoBehaviour**
- [ ] Remove the `TurretPrefab` property
- [ ] Add a `BuildingData Selected` 

![[selected-1.png]]
- [ ] Update your `Instatiate` call to use the `Selected.BuildingPrefab` property
![[instantiate-update.png]]
- [ ] If necessary, update any other references to `TurretPrefab` to use `Selected.BuildingPrefab`
## Update Buttons
- [ ] In the **Hierarchy** select **Turret Button**
- [ ] Update the **OnClick** listener to set **Selected** to **TurretData** 
- [ ] Enter **Play Mode** to test that you can place your **Turret**

![[turret-placement.png]]
- [ ] Repeat this process for your other 2 buildings

When you have finished, your game should look and act similar to the video below:

![[verify-all-buttons.webm]]
## Use `Selected.Cost`
- [ ] In `BuildingSpawner.SpawnTurret`: 
- [ ] Update your code such that `Controller.Gold` is reduced by `Selected.Cost` when the building is placed.

![[selectedcost.png]]
- [ ] Enter **Play Mode** and test that each building used the specified amount

![[verify-using-cost.webm]]
## Challenge: Fix BuildingSpawner
Currently, `BuildingSpawner` always displays `50 Gold - Place Turret` even when placing non-turret buildings. Additionally, you can build structures that cost too much so long as you have at least 50 gold.
- [ ] The Info Label should display the cost and name of `Selected`
- [ ] The Info Label should display `Not Enough Gold` if the player does not have enough gold to build the selected building
- [ ] Update `CanSpawn` to use `Selected.Cost`
- [ ] Update your InfoLabel's starting text to be empty (or another message of your choice)

When you have finished, your game should look and act similar to the video below:

![[its-almost-a-game.webm]]

## Challenge: Create 2 More Buildings
Create 2 more buildings of your choice.
- [ ] Create a **Prefab** for each building
- [ ] Create a **ScriptableObject** for each building
- [ ] Add a button for each building

# What's Next?
In the next lesson, you will add a Tower to your game that takes damage when enemies reach it and, if destroyed, shows a game over screen to the player.

[[20 - Tower]]