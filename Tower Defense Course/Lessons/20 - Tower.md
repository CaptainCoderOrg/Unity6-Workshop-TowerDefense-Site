# Tower
At this point, you have a game scene in which enemies travel along a path and when it reaches the end simply stops. For a player, this is not very exciting and they have little (or no) incentive to try to stop the enemies. In this section, you will add a Tower to your scene that you player will defend from enemies. If enough enemies reach the Tower, the tower will be destroyed.

## Challenge: Create a Tower Prefab
- [ ] Create a new Prefab object and name it Tower
- [ ] Within the Prefab add a child component called `model`
- [ ] Add one or more 3D models to create the visual representation of your Tower

When you have finished you should have a Prefab that looks similar to the image below:

![[tower-prefab.png]]

## Tower Test Scene
Just as you did before with the Projectile Test and the TurretAttack Test, it is easier to test your new Tower component in isolation to know that it works the way you would like before adding it to your main level. 

In this scene you will create a Tower that can withstand 5 points of damage. You will add two enemies to the scene. One enemy will deal 2 damage. The other will deal 3. After both enemies have damaged the tower, it will be destroyed.
### Setup Scene

- [ ] Create a new Scene in your **Test Scenes** folder called "Tower Test Scene"
- [ ] Delete the default Main Camera from the Scene
- [ ] Add a GameCamera Prefab to the Scene
- [ ] Add your Tower Prefab to the Scene
- [ ] Add a Waypoint centered on your Tower (Tower Waypoint)
- [ ] Add a second Waypoint that is a short distance from your tower (Second Waypoint)
- [ ] Set the second Waypoint to go toward the Tower Waypoint
- [ ] Add an Enemy and set its starting Waypoint to Second Waypoint (First Enemy)
- [ ] Add a third Waypoint that is a further distance from your tower (Third Waypoint)
- [ ] Set the third Waypoint to go toward the Tower Waypoint
- [ ] Add an Enemy and set its starting Waypoint to Third Waypoint (Second Enemy)

If all went well, you should have a scene that looks and acts similar to the one in the video below:

![[test-tower-scene 1.webm]]

### Challenge: EnemyAttack MonoBehaviour
Before you can damage the tower, your `Enemy` will need to know how much damage it deals.
- [ ] Create a new **MonoBehaviour** called `EnemyAttack`
- [ ] Add a `int Damage` property
- [ ] Add the `EnemyAttack` component to your `Enemy` prefab
- [ ] In the **Inspector** set **First Enemy**'s `Damage` property to 2
- [ ] In the **Inspector** set **Second Enemy**'s `Damage` property to 3

When you have finished, your **Hierarchy** and **Inspector** should look similar to the video below:

![[enemy-attack-setup.webm]]

### Practice: Add a Collider to your Tower prefab
To be able to detect when an Enemy has collided with your Tower, you will need to add a Collider. I recommend using a Capsule Collider but, depending on the shape of your Tower, you may choose to use a different Collider.

- [ ] Add a child component to your Tower prefab (Tower Collider)
- [ ] Add a Collider to the new child component
- [ ] Adjust the size of the collider to fit your model
- [ ] Set the Collider to be a trigger

When you have finished, your Tower Prefab should look similar to the one in the video below:

![[tower-collider 1.webm]]
## Challenge: TowerCollisionEvents MonoBehaviour
Recall how you implemented the `AreaOfEngagement` **MonoBehaviour** to detect when an enemy moves in range of your turret in [[10 - Rotating Turret]]. 

- [ ] Review [[10 - Rotating Turret#Add a Rigidbody to Area of Effect]]
- [ ] Review [[10 - Rotating Turret#AreaOfEngagement MonoBehaviour]]
- [ ] Review [[10 - Rotating Turret#OnTriggerEnter(Collider)]]
- [ ] Create a new **MonoBehaviour** called `TowerCollisionEvents`
- [ ] Add a property `UnityEvent<EnemyAttack> OnEnemyHit`
- [ ] Add a `void OnTriggerEnter(Collider other)`
- [ ] In `OnTriggerEnter`, use`other.GetComponentInParent<EnemyAttack>()` to get the `EnemyAttack` component.
- [ ] If the component is null, do nothing (return)
- [ ] Otherwise, use `OnEnemyHit.Invoke` to notify listeners of the collision
- [ ] Additionally, add `Debug.Log(other)` to your method so you can verify it works

When you have finished, your prefab and test scene should look and act similar to the video below.

![[testing-collisions.webm]]

### Challenge: TowerController MonoBehaviour

- [ ] Create a `TowerController` **MonoBehaviour**
- [ ] Add a `float BaseHealth` property (set the default value to 5)
- [ ] Add a `float Damage` property (set the default value to 0)
- [ ] Add an `ApplyHit(EnemyAttack attack)` method:
- [ ] Increase `Damage` by `attack.Damage`
- [ ] Destroy `attack.gameObject`
- [ ] If the tower has taken sufficient damage destroy `this.gameObject`
- [ ] Add a `TowerController` component to your **Tower Prefab**
- [ ] Register **TowerController.ApplyHit** as a listener on your **TowerCollisionEvents.OnHit** event
- [ ] Enter **Play Mode** to test your component

If all went well, your **Prefab** and your **Test Scene** should look and act similar to the video below:

![[test-tower-controller.webm]]

### Challenge: Show Game Over

- [ ] Update your `TowerController` **MonoBehaviour**
- [ ] Add a `UnityEvent<TowerController> OnDestroyed` property
- [ ] In `TowerController.ApplyHit`
- [ ] If the tower has taken sufficient damage to be destroyed, use `OnDestroyed.Invoke(this)` to notify any listeners that the tower was destroyed
- [ ] Add a **Label** to your **Test Scene**
- [ ] Update the **Label** to say **Game Over**
- [ ] Position your **Label** in the center of the screen
- [ ] Disable the **Label** so it is not enabled when the scene starts
- [ ] Register your **Label**'s `GameObject.SetActive` method on your **TowerController.OnDestroyed** event to enable the **Label**
- [ ] Enter **Play Mode** to test your event

If all went well, your **Hierarchy** and **Test Scene** should look and act similar to the video below:

![[show-game-over.webm]]

### Challenge: Add a Tower to Your Level

- [ ] Add your **Tower** Prefab to your main level
- [ ] Add a **Game Over** label
- [ ] Test your level

When you've finished, your level should look and act similar to the video below:

![[demo-game-over.webm]]
# What's Next?
At this point, you have a very simple but playable level that is ready for some polish! In the next lesson, you will add a sprinting animation to your Enemy.

[[21 - Animation Basics]]