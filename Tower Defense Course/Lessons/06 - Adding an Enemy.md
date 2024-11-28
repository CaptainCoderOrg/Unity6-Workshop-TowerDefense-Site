In this section, you will create a simple enemy that can move around the map.
## Import Assets
Kenney provides hundreds of free assets to the public domain that can be used to help in your prototypes (and even commercial projects). In this section, you will use the Graveyard Kit to create an enemy using one of the 5 provided models and animations.

Before starting, you should import the **FBX Models** from this asset pack: [Graveyard Kit · Kenney](https://kenney.nl/assets/graveyard-kit)

If you need help importing the models, you can refer to the Importing Asset section of [[02 - Creating a Tile Grid#Importing Assets]]

Here is a quick check list to help you:
- [ ] Download the Asset Pack
- [ ] Extract the ZIP archive
- [ ] Find the **FBX Model** folder
- [ ] Import the **FBX Models** into your **Assets**
- [ ] Rename the folder (I recommend **Kenny Graveyard Kit**)
## Creating an Enemy Prefab

Start by creating an Empty **Game Object** in your **Hierarchy** that will act as the base for your **Enemy**.

- [ ] Right click in the **Hierarchy**
- [ ] Select **Create Empty**
- [ ] Rename the **Game Object**. (I recommend calling it Enemy)

![[create-empty.png]]

**Note:** Double check that the new **Game Object** is not a child of any other object.

![[ensure-top-level-enemy.png]]

In the **Kenney Graveyard Kit** you will find 5 character models that can be used as a model for your Enemy:

* character-digger
* character-ghost
* character-skeleton
* character-vampire
* character-zombie

In the **Project** tab, if you search for `character-`, you should see the 5 models:

You can search your assets for a specific file by using the search bar at the top of the **Project** explorer tab.

![[kenney-character-models.png]]

- [ ] Drag one of the character models onto your **Enemy** game object to make it a child object.
	- **Note**: For this part of the project, I will be using the `character-zombie` model. However, feel free to use any of the models.

![[add-model-to-enemy.webp]]
### Practice: Unpack Model Prefab

Can you remember how to unpack a prefab? Notice, the `character-xyz` model you have selected is a **Prefab** in the **Hierarchy**. Can you unpack it?

- [ ] Unpack the `enemy-ufo-` model in your **Hierarchy**
- [ ] Rename the game object to be `model`

When you have finished, your **Hierarchy** should look similar to the image below:

![[practice-renaming-unpacking.png]]

### Practice: Create the Enemy Prefab
Now that you have an Enemy game object, turn it into a **Prefab**. At this point, you now have multiple types of **Prefabs** (tiles and enemies). Create a folder for each within your **Prefabs** folder to help organize them.

- [ ] Create a folder for your Enemy prefabs
- [ ] Create a folder for your Tile prefabs
- [ ] Move all of your prefabs to the appropriate folder

When you have finished, your **Prefabs** folder should look similar to the folders below:

![[create-prefabs-folders.webp]]
## Creating an EnemyMovement MonoBehaviour
To make your Enemy move, you will need to create a **MonoBehaviour**. A **MonoBehaviour** is a scripted component that provides methods for managing the behaviour of your **Game Object**s while the game is running.

Create a **MonoBehaviour** script for your enemies movement called **EnemyMovement**

- [ ] In the **Project** tab, create a Folder called **Scripts**

![[create-scripts-folder.webp]]

- [ ] Right click inside the **Scripts** folder
- [ ] Select **Create > Scripting > MonoBehaviour Script**

![[create-mono-behaviour-script.png]]

- [ ] Name the script EnemyMovement
	- **Note**: You should not use spaces and you should use CameCasing when naming Scripts
- [ ] Double click to open the **EnemyMovement** script

After the script loads, verify that the class name is `EnemyMovement`. If you did not rename the script immediately upon creation in Unity, the template will set the name to be `NewMonoBehaviourScript`. It is important to rename this when you open the file for the first time.

![[common-mistake.png]]

When named correctly, it should match the name of the file. For example, in VS Code:

![[verify-name.png]]

## Attaching a MonoBehaviour to a GameObject

Now that you have a **EnemyMovement** script, you can attach it to your **Enemy** **Game Object**

- [ ] Select your **Enemy** from the **Hierarchy**
- [ ] In the **Inspector** select **Add Component**
- [ ] Search for **EnemyMovement** and Select it

If all went well, you should now see an **Enemy Movement** component in the **Inspector**


![[add-enemy-movement.webp]]

You may have noticed that the **Enemy Movement** component in your inspector has a small green plus icon next to it. This means that the component you added only exists on this instance of your **Enemy** and not your **Enemy Prefab**.

![[enemy-movement-prefab-overrid.png]]

### Practice
Can you remember how to apply **Overrides** to your **Prefab**?

- [ ] Apply the override to your **Enemy Prefab** to make the **Enemy Movement** script part of the **Prefab**

When you are done, the green plus icon should no longer be visible on the **Enemy Movement** component in the inspector.

![[enemy-movement-override-applied.png]]

## Moving with the Update Method

One of the most useful methods that are provided by a **MonoBehaviour** is the **Update** method. This method is called by the **Unity Engine** each frame your game is running. This can be used to update the Transform Position of a **GameObject** each frame to make it move in the game world.

Change your **EnemyMovement** script's **Update** method to increase the enemy's **transform.position** on the X axis each frame.

![[increment-transform-enemy-movement.png]]

Be sure to save your work. Then, return to the **Unity Editor** and enter **Play Mode**. If all went well, you should see your Enemy moving along the x-axis of your game world. You can verify this in the **Inspector**.

- [ ] Enter **Play Mode**
- [ ] Verify your **Enemy Movement** script is updating the Transform's Position in the **Inspector**

![[playmode-move-enemy.webp]]

## Delta Time

You may have noticed the Enemy is not moving at a consistent rate. This is because, the **Enemy Movement** scripts **Update** method is being called each frame. This makes the movement of the **Enemy** dependent on the **Frame Rate** of the game.

To help with this, you can scale the movement using the amount of time that has passed between frames. In Unity, this value can be accessed using the `Time.deltaTime` property.

- [ ] Update your movement to be scaled with `Time.deltaTime`

![[scale-movement-with-delta-time.png]]
Once again, enter Play Mode and verify your **Enemy**'s Transform Position is updating. You will notice your **Enemy** moves much slower than it did before. This is because it is now moving at 0.1 units **per second**. You can think of the expression `* Time.deltaTime` as "per second". For example, if you want an object to move 5 units per second, you would use `5 * Time.deltaTime`.

![[playmode-move-enemy-deltaTime.webp]]

## Creating a Speed Property

Different Enemies will move at different speeds. To help accommodate this, add a `Speed` property to your `EnemyMovement` script. 

- [ ] Add a `float Speed` property to your `EnemyMovement` class
	- Following "good" programming practices, create a public getter and a private setter
- [ ] Set the default value of `Speed` to `1f`

![[add-speed-to-enemy-movement.png]]

- [ ] In your **Update** method, use the `Speed` property rather than the **float literal** `0.1`.

![[update-method-with-speed-property.png]]
Once again, enter **Play Mode** and verify that your **Enemy** moves at 1 unity per second.

![[playmode-move-at-1unit-per-second.webp]]

## Serializing Properties in the Inspector
It is useful to be able to modify a property from the Unity Inspector. To do this, you must **Serialize** your property by adding the \[field: SerializeField\] attribute to the property that you would like to see in the inspector. 

- [ ] Add the `[field: SerializeField]` to your **Speed** property

![[serialize-speed-property.png]]

Now, when you select your **Enemy**, you will see the **Speed** property in the **Enemy Movement** component in the **Inspector**. You can adjust this value directly in the **Inspector** to change the speed of your **Enemy**. You can even do this while in **Play Mode**! However, be aware that when you exit **Play Mode** any changes you made will be reset to their original values.

- [ ] Modify the **Enemy**'s **Speed** directly in the inspector setting it to 2
- [ ] Enter **Play Mode**
- [ ] While in **Play Mode**, adjust the **Speed**
- [ ] Exit **Play Mode**
- [ ] Notice, that the **Speed** resets to the original value: 2

![[adjusting-speed-in-inspector.webp]]

## Challenge: EnemyRotation Script
Using what you've learned in this lesson, create a new MonoBehaviour Script called "EnemyRotation" that allows you to specify how quickly an Enemy rotates on the Y axis.

- [ ] Read the Friendly Manul: [Unity - Scripting API: Transform.Rotate](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Transform.Rotate.html)
	- This method allows you to rotate a **Game Object**
- [ ] Create a `EnemyRotation` script
- [ ] In Update, rotate the enemy on the Y-axis
- [ ] Add a RotationSpeed property to the script
	- Initialize the default value to `90f` (e.g. 90 degrees per second)
- [ ] The script should serialize a RotationSpeed property so the value can be modified in the **Inspector**
	- Follow good programming practices an use a `private setter`
- [ ] Be sure to scale the rotation speed using `Time.deltaTime`

When you have successfully implemented the **EnemyRotation** script, it should work similar to the image below:

![[rotation-challenge-complete.webp]]

## What's Next

In the next section you will create a **Waypoint** component that you can use to specify the path your enemies will take.

[[07 - Waypoints]]