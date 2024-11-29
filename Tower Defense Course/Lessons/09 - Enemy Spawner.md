In this section, you will implement an **Enemy Spawner** that repeatedly spawns new Enemies for your player to destroy!

## High Level Overview

* Creates an Enemy
* Sets the Enemies first **Target Waypoint**
* Waits for 5 seconds before repeating

### Challenge: Enemy Spawner Prefab

Before implementing the **Enemy Spawner** script, create a **Prefab** that can be placed on your map where **Enemies** will spawn. Then, place one in your world at the start of your path.

When you're finished, it will look similar to the image below. **Note**: You can hide your **Waypoint**s from being viewed in the **Scene View** by clicking the **Eye Icon** in the **Hierarchy** next to the parent container. This can be helpful when placing your **Enemy Spawner**.

![[example-enemy-spanwer-prefab.png]]

## EnemySpawner Properties
- [ ] Create an `EnemySpawner` MonoBehaviour Script with the following properties
	- [ ]  `Waypoint StartTarget` - This will be the first **Target Waypoint** for the spawned **Enemy**
	- [ ] `EnemyMovement Enemy` - This will be the **Enemy** that will be spawned
	- [ ] `float Delay` - This will be the number of seconds between spawns
- [ ] Serialize each property so they can be specified in the **Inspector**

![[enemy-spawner-properties.png]]

## Spawn Method
To keep your code organized, add a `Spawn()` method that creates an Enemy and sets the Enemy's first **Target** waypoint.  To create a Game Object during game play, you can call `Object.Instantiate`. This will add the specified **Game Object** to the Scene.

- [ ] Read the Friendly Manual: [Unity - Scripting API: Object.Instantiate](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Object.Instantiate.html)
- [ ] Add a `Spawn()` method
	- [ ] Call `Object.Instantiate` specifying the `Enemy`
	- [ ] Set the new **Enemy**'s **Target** to the `StartingWaypoint`

![[first-draft-spawn.png]]

You likely noticed that the `Target` property of your `EnemyMovement` cannot be set because it is `private`. Before your program will compile, you need to modify the `EnemyMovement` script to allow the `Target` property to be set.

- [ ] Update your `EnemyMovement.Target` property to have a `public` setter

**Note**: It is considered a good practice to use `private` access modifiers whenever possible. This reduces the potential search space for bugs related to that property being modified. When you change it to `public` the property can be accessed anywhere in your code which mean you can introduce bugs related to the property anywhere in your code.

![[update-target-to-public.png]]

With the `EnemyMovement.Target` updated, your `EnemySpawner` should now compile

## Test the Spawn Method
For now, test your `Spawn` method by calling it once in `Start()`

- [ ] Call `Spawn()` from the `EnemySpawner.Start` method

![[call-spawn-in-start.png]]

### Setting up the Enemy Spawner
Before you can test your `Spawn()` method, you need give your **Prefab** the **Enemy Spawner** component and specify the initial values.

- [ ] In the **Inspector** add a **Enemy Spawner** component to your **Enemy Spawner** prefab.
- [ ] Set the initial **StartingWaypoint** from your scene's **Hierarchy**

![[set-starting-waypoint.png]]

You might be tempted to set the `Enemy` property using the **Enemy** object in your Scene. However, if this object is destroyed, it will break your **Spawner**. Instead, you can use a **Prefab** from your **Project** which won't be destroyed in the **Scene**.

- [ ] Delete the **Enemy** that is currently in your **Hierarchy**
- [ ] Set the **Enemy** property to use the **Enemy Prefab** from your **Project View**

![[set-enemy-with-prefab.png]]

With your **Enemy Spawner** wired up, enter **Play Mode** to verify that a new **Enemy** is spawned. If all went well, you should see a new **Enemy(Clone)** in your **Hierarchy** as well as an **Enemy** moving between your **Waypoint**s.

![[verify-spawn-method.webp]]

## InvokeRepeating
You can use Unity's `MonoBehaviour.InvokeRepeating` method to repeatedly call a method by its name.

- [ ] Read the Friendly Manual: [Unity - Scripting API: MonoBehaviour.InvokeRepeating](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/MonoBehaviour.InvokeRepeating.html)
- [ ] In `EnemySpawner.Start()` call `InvokeRepeating` on the `Spawn` method
	- **Pro Tip**: Use `nameof(Spawn)` rather than a hard coded string.

![[invoke-repeating.png]]
## Testing the EnemySpawner

Enter **Play Mode** to test your **Enemy Spawner**. You may find it helpful to set the `Delay` to a smaller number for testing. **Note**: Because you use `Delay` in your `Start` method, you cannot change the `Delay` of the **Enemy Spawner** while in **Play Mode**.

If all went well, your game should look similar to the video below:

![[verify-repeating-spawn.webp]]

## Challenge: Limit Number of Spawns
In this challenge, you will update your **Enemy Spawner** to only spawn a specified number of **Enemies**. After the specified number of **Enemies** have spawned, you will use `MonoBehaviour.CancelInvoke()` to stop the `EnemySpawner`.

- [ ] Read the Friendly Manual: [Unity - Scripting API: MonoBehaviour.CancelInvoke](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/MonoBehaviour.CancelInvoke.html)
- [ ] Add a property `SpawnsRemaining` to your `EnemySpawner`
	- Set the default value to 5.
- [ ] In your `Spawn()` method, decrement `SpawnsRemaining`
- [ ] When `SpawnsRemaining` is `0`, call `CancelInvoke()`

When you have successfully implemented this challenge, your game should look similar to the video below.

![[verify-repeating-spawn 1.webp]]

## Edge Case: Disabling the Spawner
If the `EnemySpawner` becomes disabled, `InvokeRepeating` will continue to execute. This is typically not the desired behaviour. It is considered a best practice to call `CancelInvoke()` in your `OnDisable()` method to prevent strange side effects that might occur when using `InvokeRepeating`.

- [ ] Read the Friendly Manual: [Unity - Scripting API: MonoBehaviour.OnDisable()](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/MonoBehaviour.OnDisable.html)
- [ ] Add `OnDisable()` to your `EnemySpawner`
- [ ] Call `CancelInvoke()` in `OnDisable()`

![[ondisable-cancelinvoke.png]]

Verify that your enemies stop spawning if you disable the `EnemySpawner`:

![[verify-ondisable.webp]]

### Challenge: Continue Spawning OnEnable
You may have noticed that when you re-enable the **Enemy Spawner**, the remaining **Enemies** do not continue spawning. This is because `Start()` is only called once per **Game Object** the first time it becomes active in the **Scene**. If you would like to run code every time a **Game Object** becomes active, you an use `OnEnable()`.

- [ ] Read the Friendly Manual: [Unity - Scripting API: MonoBehaviour.OnEnable()](https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnEnable.html)
- [ ] Update your `EnemySpawner` to have an `OnEnable` method
- [ ] Use `OnEnable` to call `InvokeRepeating` instead of the `Start()` method

When implemented correctly, your game should act similar to the video below:

![[verify-onenable.webp]]

## What's Next
Now that you are able to spawn enemies into you game. It is time to design a turret that can be used to destroy the enemies.
