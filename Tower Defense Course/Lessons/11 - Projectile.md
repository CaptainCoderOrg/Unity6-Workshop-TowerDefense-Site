In this lesson, you will create a Projectile that will move toward an Enemy. Upon reaching the Enemy, it will apply damage. If an enemy receives enough damage, it will be destroyed.

## Challenge: Create a Projectile Prefab
Before your turrets can shoot a projectile, you must first create a **Projectile Prefab** to spawn.

- [ ] Create a new **Prefab** for your Projectile
- [ ] Add a model to the **Prefab** (I will be using `weapon-ammo-arrow` but you can use any model you like)
- [ ] Create a `Projectile` MonoBehaviour Script
- [ ] Add the `Projectile` component to the **Prefab**

When you're finished it should look similar to the image below:

![[projectile-completed.png]]

## Projectile Test Scene
It is often quicker to create a new scene to test your **Prefabs** and **Scripts** to see if they work in a constrained environment before putting them into your game.

- [ ] Create a new Folder called **Test Scenes**
- [ ] Right click, **Create > Folder**
- [ ] Create a **Projectile Test Scene**
- [ ] Rick click, **Create > Scene > Scene**

![[create-scene-scene.png]]

## The Projectile Test
Within the **Projectile Test Scene**, you will set up a situation to determine if the **Projectile** is working as intended.

* A **Projectile** will have a **Target** that it will move toward. 
* When it reaches the **Target**, it should deal damage to the **Enemy**. 
* When it reaches the **Target**, it should be removed from the **Scene**.
* If the **Enemy** has sustained **Damage** equal to or greater than their **Health**, the enemy should be removed from the **Scene**.

### Enemy Health and Damage
Before you are able to create your test, you will need to add health and damage to your **Enemy**.

- [ ] Create a new `Health` MonoBehaviour Script
- [ ] Add a `float BaseHealth` property
- [ ] Add a `float Damage` property

![[health-script-base.png]]

- [ ] Add a **Health** component to your **Enemy Prefab**

![[add-health-to-enemy.png]]

### Projectile Properties
- [ ] In your `Projectile` script 
- [ ] Add a `float Speed` property, set the default value to 2
- [ ] Add a `float Damage` property, set the default value to 1
- [ ] Add a `Transform Target` property

![[projectile-speed-damage-target.png]]

### Setting up the Test

- [ ] Open your **Projectile Test Scene**
- [ ] Add an **Enemy** to the **Scene**
- [ ] Set the **Enemy**'s `BaseHealth` to 2
- [ ] Add 2 **Projectiles** to the **Scene**
- [ ] Position the **Projectiles** such that one is further away from the **Enemy**
- [ ] Set the **Projectiles** **Target** to be the **Enemy**

When you're finished, your test scene should look similar to the video below:

![[projectile-test-scene-setup.webp]]

### Challenge: Implement Moving Projectile

- [ ] Add an `Update` method to your `Projectile` Script
- [ ] The `Projectile` should rotate to face the **Target**
- [ ] The `Projectile` should move toward the **Target** at `Speed` units per second
- [ ] If the `Projectile` is sufficiently close to the **Target** display a "Hit" message in the console
- [ ] Fix any `NullReferenceExceptions` that you encounter

When you have finished the challenge, it should look similar to the video below:

![[projectile-challenge-completed.webp]]

## Destroying Projectiles
When the **Projectile** has reached its target, it should remove itself from the scene. This can be done using the `Object.Destroy(Object)` method.

- [ ] Read the Friendly Manual: [Unity - Scripting API: Object.Destroy](https://docs.unity3d.com/ScriptReference/Object.Destroy.html)
- [ ] Update your code to call `Object.Destroy` when the `Projectile` has reach its **Target**

**Note**: You should destroy `gameObject` which is the Game Object the `Projectile` component is attached to.

![[destroy-gameobject-1.png]]

- [ ] Enter **Play Mode** to test that your **Projectiles** are removed from the **Hierarchy** when they reach the **Target**

![[verify-projectiles-removed.webp]]

## Applying Projectile

Next, you will add an `ApplyHit(Projectile)` method to your `Health` script that will add `Projectile.Damage`. 

### ApplyHit
- [ ] Open the `Health` script
- [ ] Add a `public void ApplyHit(Projectile)`
- [ ] Increase `Health.Damage` by `Projectile.Damage`

![[apply-hit-damage.png]]

### GetComponentInParent
Before the `Projectile` is destroyed, you must call `Health.ApplyHit` specifying that `this` ``Projectile`` has reached the **Target**. However, because `Target` is a `Transform`, you cannot call the `ApplyHit` method directly.  Furthermore, the `Target` is actually a child of the **Enemy Prefab**. To find the `Health` component attached to the **Parent** object, you can use the `Component.GetComponentInParent` method to find the `Health` component.

- [ ] Read the Friendly Manual: [Unity - Scripting API: Component.GetComponentInParent](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Component.GetComponentInParent.html)
- [ ] Open your `Projectile` Script
- [ ] Update your code to use `Target.GetComponentInParent<Health>()` to retrieve the `Health` component of the `Target`
- [ ] If a `Health` component was found, call `ApplyHit(this)`

![[get-health-apply-hit.png]]

- [ ] Verify that the **Enemy**'s `Damage` property updates properly in your **Test Projectile Scene** 

![[verify-damage-is-updating.webp]]

### Challenge: Destroy the Enemy
Finally, update your **Health** script to destroy the enemy and remove it from the **Scene** if it has taken damage greater than or equal to its `BaseHealth`.

When you have finished, your **Test Projectile Scene** should look similar to the video below:

![[verify-enemy-is-destroyed.webp]]

## Projectile Edge Cases
The test you have created is for the best case scenario. That is, the **Enemy** is destroyed after receiving 2 damage. What happens if there is a 3rd projectile?

- [ ] Add a 3rd **Projectile** to your scene that Targets the **Enemy**
- [ ] Place it in the **Scene** such that all 3 **Projectiles** reach the **Enemy** at different times
- [ ] Enter **Play Mode**, what happens?

Depending on how you implemented your **Projectile**, it may throw a `NullReferenceException` when the **Target** is destroyed. It may also simply stop moving when the **Target** is destroyed. If you check in the **Inspector**, you will see that the **Target** is marked as **Missing**. This is because it was destroyed.

![[missing-target.webp]]

As a developer, you will often need to account for situations that are not ideal but are technically possible during game play. These are often referred to as **Edge Cases** because they exist at the "boundaries" of what is expected. As you continue to develop your skills, you will begin to develop an intuition for **Edge Cases** and be able to anticipate many (but not all) of them.

### Challenge: Fix the Edge Case
There are many possible ways to handle this particular **Edge Case**. One of the simplest solutions is to destroy the **Projectile** if it has no **Target**. 

- [ ] Update your `Projectile` script such that if the `Target` is `null`, the **Projectile** is removed from the **Scene**

When you have successfully implemented this challenge, your scene should act similar to the video below:

![[projectile-challenge-complete.webp]]

## What's Next?
With your **Projectile Prefab** working, it is time to add a script that allows your turrets to fire them.

[[12 - Firing Projectiles]]