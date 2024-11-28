With your **Waypoints** set up, it is time to update your Enemy to follow your **Waypoints**.

## High level design idea

* Enemy has a **Target Waypoint** that they move toward
* When the Enemy reaches their **Target** they query the **Waypoint** for the **Next Waypoint**  and update their **Target Waypoint**
* If there is no **Next**, the **Enemy** stops moving

## Vector3.MoveTowards
You can utilize Unity's built in method `Vector3.MoveTowards` to do most of the heavy lifting for the Enemy's movement.

- [ ] Read the Friendly Manual: [Unity - Scripting API: Vector3.MoveTowards](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Vector3.MoveTowards.html)
- [ ] Add a **Target Waypoint** property to your **Enemy Movement** script
- [ ] Be sure to Serialize the property so it can be accessed in the **Inspector**

![[add-waypoint-target.png]]
- [ ] In the **Update** method, call `Vector3.MoveTowards` to update the Enemy's position
	- **Note**: Use Time.deltaTime*Speed as the `maxDistanceDelta`

![[use-vector3-move-towards.png]]

- [ ] In the **Inspector**, set the enemy's **Target Waypoint** to your first waypoint

![[set-first-waypoint.png]]

- [ ] Enter Play Mode and verify that your Enemy moves to the specified **Waypoint**

![[move-to-waypoint.webp]]

While you are in **Play Mode** you can even switch the **Waypoint** to test that when the **Waypoint** is changed, the **Enemy** will move to the new **Target**

![[change-waypoint-in-playmode.webp]]

## Changing Waypoints
You need a way to determine how close the **Enemy** is to their **Target Waypoint**. This can be done using `Vector3.Distance`.

- [ ] Read the Friendly Manual: [Unity - Scripting API: Vector3.Distance](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Vector3.Distance.html)
- [ ] After the **Enemy** has moved, calculate their distance from the **Target Waypoint**
- [ ] If the `distance` is sufficiently close to 0, the Enemy's **Target** updates to the next **Waypoint**

![[calculate-distance.png]]

- [ ] Enter **Play Mode** to verify your **Enemy** moves between each **Waypoint**

![[verify-waypoint-traveler.webp]]

You may have noticed the odd expressions `distance <= 0` and might be asking yourself, "Why are we checking if the distance is less than or equal to 0 and not just equal to 0?". Great question! I'm so glad you asked! As you may already be aware, floating point numbers are approximated values, that is they should not be used for precise calculations (See: [Is floating-point math broken? - Stack Overflow](https://stackoverflow.com/questions/588004/is-floating-point-math-broken)for greater detail).

In our case, it is possible that we may not actually get a value of 0, and instead we want to check if the `distance` is sufficiently close to 0. In Unity, this often done using `Mathf.Epsilon` (which happens to be approximately 0.00001f).

- [ ] Update your code to use `Mathf.Epsilon` in place of 0

![[use-mathf-epsilon.png]]

### Challenge: Fix the NullReferenceException

You may have noticed, when your Enemy reaches the final **Waypoint** an error message appears in the **Unity Console**.

- [ ] Fix the **NullReferenceException**

![[nullreference-exception.png]]

## The Start() Method

Currently, your Enemy begins its journey by moving to your first **Waypoint**. You may have already moved the **Enemy** to start at that position when you enter **Play Mode**. However, it is not guaranteed. One way to fix this, is to use the **Start()** method to move the **Enemy** to their first **Target** before the first game frame.

- [ ] Update your `Start()` method to set the **Enemy**'s initial position to the **Target**'s position.

![[set-enemys-initial-position.png]]
## Challenge: Rotate the Enemy to Face their Target Waypoint
Unity provides a method called `Transform.LookAt` that can be used to make a **Game Object** rotate toward another **Game Object**. You can utilize this, to make your **Enemy** face their **Target Waypoint**.

- [ ] Read the Friendly Manual: [Unity - Scripting API: Transform.LookAt](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Transform.LookAt.html)
- [ ] Remove the **Enemy Rotation** component from your **Enemy**
- [ ] When the **Enemy** changes **Target**s, call the **Transform.LookAt** method to rotate the **Enemy** to face the next **Waypoint**
- [ ] Fix any **NullReferenceExceptions** that occur

When you have successfully completed this challenge, your Enemy should look similar to the one in the video below.

![[challenge-complete.webp]]

## What's Next

With your **Enemy**'s moving, it is time to create an **Enemy Spawner** that will generate additional enemies during game play.