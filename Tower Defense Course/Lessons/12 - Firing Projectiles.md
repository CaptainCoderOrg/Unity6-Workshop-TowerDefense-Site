In this lesson, you will implement a `TurretAttack` MonoBehaviour that will spawn **Projectile**s that will target enemies within the Turret's **Area of Engagement**.
## TurretAttack MonoBehaviour

### Challenge: Create the TurretAttack MonoBehaviour
Your `TurretAttack` will need to be able to check if there are any **Targets** in the `AreaOfEngagement`. If there is at least one target, it will need to `Instantiate` a `Projectile`. Then, it should wait for some amount of time before firing again. Finally, to be able to check if it can fire again, it should track if it is currently cooling down.

- [ ] Create a new `TurretAttack` MonoBehaviour Script
- [ ] Add an `AreaOfEngagement AoE` Property
- [ ] Add a `Projectile ProjectilePrefab` Property
- [ ] Add a `float CooldownTime` Property. Set the default value to 3.
- [ ] Add a `bool IsCoolingDown` Property. Set the default value to false.
- [ ] Add a **Turret Attack** component to your **Turret Prefab**
- [ ] Set the `AreaOfEngagement` in the **Inspector**
- [ ] Set the `ProjectilePrefab` in the **Inspector**

When you have finished, your **Turret Prefab** should be similar to the image below:

![[setup-turret-attack.png]]

## Turret Attack Test Scene
To help you test if your `TurretAttack` implementation is working in isolation, create a test scene. In this test, you will test that your **TurretAttack**:
* Fires at an **Enemy** that is within the **Area of Engagement**
* Changes targets when an **Enemy** in the **Area of Engagement** is destroyed
* Does not fire at an **Enemy** that is not within the **Area of Engagement**
### Challenges: Create a TurretAttack Test Scene
- [ ] Create a new Scene in your **Test Scenes** folder. Name it "TurretAttack Test Scene"
- [ ] Add a **Turret Prefab** to the **Scene**
- [ ] Add 2 **Enemy Prefabs** within the **Area of Engagement**
- [ ] Add a 3rd **Enemy Prefab** that is outside the **Area of Engagement**
- [ ] Set all of the **Enemies** to have at least 2 base health.

When you're done, your **TurretAttack Test Scene** should look similar to the image below:


![[turret-attack-test-scene-setup.png]]

### Fire()
Sometimes, it is easier to build a small part of a bigger challenge. Start by implementing a `Fire()` method that will `Instantiate` a clone of the `ProjectilePrefab`, set its `transform.position` to match the **Turret**'s `transform.position`, and set its `Target` to be the first element of `AoE`.

- [ ] Declare a `private void Fire()` method
- [ ] `Instantiate` a clone of the `ProjectilePrefab`
- [ ] Set the `transform.position` of the new `Projectile` to `this.transform.position` (the position of the Turret)
- [ ] Set the `Projectile.Target` to the first target in `AoE.Targets` 
- [ ] If necessary, update your `Projectile.Target` access modifier to `public`
![[implement-fire.png]]
### Invoke(string methodName, float time)
In your `Start()` method, you can use the `Invoke(string, float)` method to call the `Fire()` method after a specified amount of time has passed. `Invoke` is similar to `InvokeRepeating` but only calls the method once.

- [ ] Read the Friendly Manual: [Unity - Scripting API: MonoBehaviour.Invoke](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/MonoBehaviour.Invoke.html)
- [ ] Add a `Start()` method to your `TurretAttack` script
- [ ] In `Start()`, use `Invoke` to call `Fire` after 1 second (use `nameof(Fire)` rather than `"Fire"`)

**Note**: Waiting 1 second allows the `AreaOfEngagement` time to add the **Enemies** to the **Targets** list.

![[call-fire-in-start.png]]

If all went well, your **Turret** should fire exactly one projectile that deals damage to one of the enemies in the Area of Engagement.

![[test-firing-once.webp]]

### Challenge: Fire After Cooldown
Now that you have tested your `Fire()` method and have confidence that it is working, it is time to implement the full `TurretAttack` script

- [ ] Delete the `Start()` method, you don't need it
- [ ] Add an `Update()` method:
- [ ] If the `TurretAttack` `IsOnCooldown`, do nothing (`return`)
- [ ] If there `AoE.Targets` is empty, do nothing (`AoE.Targets.Count == 0`)
- [ ] Otherwise, call `Fire()`
- [ ] Set `IsOnCoolDown` to `true`
- [ ] `Invoke` a method that sets `IsOnCoolDown` to `false` after `CooldownTime` seconds

**Note**: Set the `CooldownTime` to a smaller number to increase the speed of the test.

If all went well, when you enter **Play Mode**, you should see:

1. Your **Turret** will fire a **Projectile** that hits an **Enemy**
2. Wait for the Cooldown
3. Fire a second **Projectile** that will destroy the **Enemy** (assuming it has 2 BaseHealth)
4. Wait for the Cooldown
5. An error will appear in the console saying there is a `MissingReferenceException`. You will solve this bug in the next part of the lesson. 


![[challenge-complete-missing-reference-exception.webp]]

## MissingReferenceException
A `MissingReferenceException` occurs when you attempt to reference a **Game Object**  or **Component** that has been destroyed and removed from the **Scene**. In this case, you have destroyed the **Enemy** but it has not been removed from the **Area of Effect**'s `Targets` list. If you look closely in the documentation for `OnTriggerExit`, you will see that it states, "Deactivating or destroying a Collider while it is inside a trigger volume will not register an on exit event."

- [ ] Read the Friendly Manual: [Unity - Scripting API: Collider.OnTriggerExit(Collider)](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Collider.OnTriggerExit.html)

This means that you need to manually remove the target from the `AreaOfEngagement` when it is destroyed.
## UnityEvents to the Rescue
There are several ways that you could implement a solution to this bug. One common way is to use a `UnityEvent` to notify the `AreaOfEngagement` when the **Enemy** has been destroyed.

A **UnityEvent** is a way to trigger actions when something happens, like clicking a button or reaching a goal, or in this case, when an enemy dies.
### The OnDeath Event
Create an `OnDeath` event inside your `Health` script that is invoked before the object is destroyed. 
- [ ] Read the Friendly Manual: [Unity - Scripting API: UnityEvent](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Events.UnityEvent.html)
- [ ] Open your `Health` MonoBehaviour Script
- [ ] Add a `UnityEvent<Health> OnDeath` Property
- [ ] Update your `ApplyHit` method to invoke the `OnDeath` event before destroying the `gameObject`

![[health-on-death-event.png]]

### Only Target Enemies with Health
Now that you have implemented a `Health` component, you can refactor your `AreaOfEngagement` to track the `Health` of the **Enemy** rather than just the `Transform`.
- [ ] Open the `AreaOfEngagement` Script
- [ ] Refactor the `Targets` list to be a `List<Health>`. You will only fire at enemies that have a `Health` component.
- [ ] Refactor `OnTriggerEnter` and `OnTriggerExit` to find the `Health` component on collider
- [ ] If there is no `Health` component, return early
- [ ] Otherwise, add / remove the `Health` component

![[refactor-area-of-engagement.png]]

- [ ] If necessary, refactor any references to `AreaOfEngagement.Targets` to use the `transform` of the component. For example, the `TurretAttack` script may need to be refactor to:

![[refactor-fire.png]]

Before continuing, be sure to test that your **Test Scene** continues to function the same way it did previously.
### OnDeath.AddListener
You can use the `UnityEvent.AddListener` method to "listen" for the `OnDeath` event to be invoked. In this case, you can use it to call a method that accepts a `Health` parameter and use it to remove the associated target. To do this, you first need to write a method that will remove a `Health` component from the **Targets** list.

- [ ] Read the Friendly Manual: [Unity - Scripting API: Events.UnityEvent.AddListener](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Events.UnityEvent.AddListener.html)
- [ ] Add a method `void RemoveOnDeath(Health targetHealth)` to your `AreaOfEngagement` script
- [ ] This method simply calls `Target.Remove(targetHealth)`

![[remove-on-death-method.png]]

- [ ] Update the `OnTriggerEnter` method such that the `RemoveOnDeath` method to the is added as a listener to the `Health.OnDeath` event.

![[adding-on-death-listener.png]]

Similar to the `UnityEvent.AddListener` method, there is also a `UnityEvent.RemoveListener` method which is used to stop listening to the event. You should do this when the enemy exits the `AreaOfEngagement`. If you do not and the enemy is destroyed by another turret, it will notify all `AreaOfEngagement`'s it has ever entered.

- [ ] Update the `OnTriggerExit` method such that the `RemoveOnDeath` method stops listening to the `Health.OnDeath` event using `OnDeath.RemoveListener`

![[ondeath-remove-listener.png]]

- [ ] Finally, run your **TurretAttack Test Scene**

If all went well, you should see the following:

1. The **Turret** fires a projectile that hits the first enemy
2. A cooldown occurs
3. The **Turret** fires a second projectile that hits and destroys the first enemy
4. A cooldown occurs
5. The Turret fires a third projectile that hits the second enemy
6. A cooldown occurs
7. The Turret fires a fourth projectile that hits the second enemy and destroys it
8. The test is complete, the Turret does not fire on the 3rd and final enemy as it is not within the AoE

![[turret-attack-completed.webp]]

## Test Your Level
With your **TurretAttack Test Scene** demonstrating the **Turret** working in isolation, you now have a little confidence that your turrets will work in your game.

- [ ] Save your **TurretAttack Test Scene**
- [ ] Load your level **Scene**
- [ ] Test if your **Turrets** fire on passing enemies!
- [ ] You may need to adjust the Y position of your **Projectile Prefabs** model so it appears above the ground (I recommend setting the model's Y position to 0.5)
- [ ] If necessary, adjust the speed of your projectiles / enemies

![[turret-projectile-in-scene.webp]]

## Challenge: More Practice with UnityEvents
In this lesson, you used a `UnityEvent` to notify the `AreaOfEffect` when your enemy died. In this challenge you will continue to develop your skills using `UnityEvents` -- TO DO: Add challenge

## What's Next
With a simple turret, projectile, and enemy implemented, it is now time to add the ability for the player to be able to place turrets onto the map.