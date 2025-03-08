Currently, in your game, the player starts with a limited amount of gold that they can spend to build Turrets. Unfortunately, the player has no way to generate additional resources. Next, you will create a new type of building that the player can place that will generate Gold for them over time.
## Practice: Create a GoldGenerator Prefab
- [ ] Create a new GameObject to represent your GoldGenerator building
- [ ] Add a model (or multiple models) as children objects to the GoldGenerator
* Feel free to use any model you would like! In this document, I will combine two of the Kenney models together.
- [ ] If necessary, adjust the models positions within the parent object to fit nicely on a tile
- [ ] Convert your object into a Prefab

When you are finished, you should have a GoldGenerator Prefab that you can place on any tile in your game scene:

![[gold-generator example.webm]]
### Practice: GoldGenerator MonoBehaviour
- [ ] Create a new **MonoBehaviour** called `GoldGenerator`
- [ ] Add a `float Delay` property which represents how often it will generate gold
- [ ] Add an `int Gold` property which represents how much gold is generated
- [ ] Add a `GoldGenertor` component to your **GoldGenerator** prefab
- [ ] In the **Inspector** set `Delay` to 2 and `Gold` to 1

When you've finished your prefab should look similar to the image below:

![[gold-generator.png]]

### Referencing the PlayerController
To be able to update the player's gold, the `GoldGenerator` requires a reference to the `PlayerController`. You will not be able to set this in the **Prefab** because the **PlayerController** does not exist here. One way you can acquire a reference to it without the need to set it in the **Inspector** is to assume that the **PlayerController** will be a parent of the **GoldGenerator**. Then, use `GetComponentInParent` to set the reference.
- [ ] Add a `PlayerController Controller` property to your `GoldGenerator`
- [ ] Add an `Awake()` method
- [ ] In `Awake()` use `GetComponentInParent<PlayerController>()` to assign `Controller`

![[cache-player-controller.png]]
### Testing the PlayerController Reference
- [ ] Add a `GoldGenerator` to your game scene as a child of the `PlayerController`
- [ ] Enter **Play Mode**
- [ ] Observe that the `PlayerController` property is set when the game starts

![[verify-player-controller-set.webm]]

## Challenge: GenerateGold Method
- [ ] Review how you used `InvokeRepeating` and `CancelInvoke` to spawn enemies into your game
- [ ] Add a `GenerateGold()` method to your `GoldGenerator` **MonoBehaviour**
- [ ] Use `InvokeRepeating` to cause `GenerateGold()` to execute every `Delay` seconds
- [ ] Don't forget to use `CancelInvoke` when the **GoldGenerator** is disabled
- [ ] Enter **Play Mode** to test that your **Gold** is now increasing

When you're finished, your game should look similar to the video below:
![[gold-generating-invoke-repeating.webm]]
## Spawning GoldGenerators
The **TurretSpawner** you created previously does almost everything you need to be able to spawn **GoldGenerator**s into your game.
- [ ] Select your **TurretSpawner** in the **Hierarchy**
- [ ] In the **Inspector** change the **Turret Prefab** property to your **GoldGenerator** prefab
- [ ] Enter **Play Mode** and place a **GoldGenerator**
- [ ] Observe the error that occurs

![[gold-generator-nullreference-exception.webm]]
### Setting the Parent Transform
If you investigate the error, you will find that the newly spawned `GoldGenerator` does not have a `PlayerController`. This is because the object is being instantiated without a parent.

The `Instatiate` method has several overloaded versions that allow you to specify additional information about how to create the specified GameObject. One version allows you to specify the parent object: `Instantiate(GameObject, Transform)`
- [ ] Update `TurretSpawner.SpawnTurret` to set the parent of the object of the turret to be the PlayerController's transform when it is spawned. (`Controller.transform`)
![[set-parent-object.png]]
- [ ] Enter **Play Mode** to test that you are able to spawn your **Gold Generator**s
When you are finished, your game should look and act similar to the video below:  

![[spawning-gold-generators.webm]]
## Changing the Prefab
Currently, you only have a single **Build** button that enables the `TurretSpawner` game which knows references your **GoldGenerator** prefab. Next, you will update the **Build** button to set the prefab.
- [ ] Update your `TurretSpawner.TurretPrefab` field to have a public setter
![[ensure-set-public.png]]
- [ ] Select the **Button** in the **Hierarchy**
- [ ] In the **Inspector** add a listener to the **On Click** event
- [ ] Set the **TurretSpawner** as the listening object
- [ ] Select  the `TurretSpanwer.TurretPrefab` property
- [ ] Set the GameObject to be your **Turret** prefab

![[set-turret-prefab-on-click.webm]]
- [ ] Enter **Play Mode** and test that your **TurretSpawner** field is changed when the button is clicked. This results in the player being able to spawn Turrets (rather than GoldGenerators)

![[test-prefab-build-button.webm]]
## Challenge: Create a Generator Button
Currently, your player is only capable of building Turrets when they click the **Build** button. Can you add another button that allows them to create generators?
- [ ] Add a button to your Canvas
- [ ] The button should be labeled "Generator"
- [ ] Use Pivots and Anchors to set the buttons position relative to the screen
- [ ] When the button is clicked, the player should be able to place generators
- [ ] Enter **Play Mode** to test that both of your buttons works

When you have finished, your game should look and act similar to the video below:
![[test-buttons.webm]]

# What's Next?
Although it is now possible to spawn different types of buildings/turrets, you are not able to easily change the cost (the gold cost of 50 is hard coded). Additionally, the user hints could be more descriptive based on the type of building you want to place. In the next lesson, you will create a **ScriptableObject**  building type that will allow you to quickly and easily create new building types and easily add them to your player's UI.

[[19 - BuildingData]]