In this lesson, you will create a simple Turret that rotates to face enemies that are nearby.
## Challenge: Create a Turret Prefab
- [ ] Create a new **Prefab** to represent a turret
- [ ] Add a model to the **Prefab** (I will be using the `weapon-ballista` model but you may use any model)
- [ ] Create a new `TurretTarget` MonoBehaviour Script
- [ ] Attach the `TurretTarget` component to your **Turret Prefab**
- [ ] Add a Turret to your **Scene**
- [ ] Adjust the model's, Y position to be slightly above your ground tile. The grass / snow tiles are 0.2 units thick.
- [ ] Add a few instances of your **Turret Prefab** to your scene

If all went well, your Scene should look similar to this:

![[add-turret-to-scene.png]]

## Area of Engagement

Before your turret can rotate to face an enemy, it must be able to detect enemies that are within range. To do this, you will define an **Area of Engagement** using a collider that will track enemies that are within range.

- [ ] Add a **Sphere** to your **Turret**

![[create-spehere.webp]]

- [ ] Rename the **Sphere** (I recommend "**Area of Engagement**")

You can change the range of the Area of Engagement by adjusting the scale
- [ ] Adjust the range of the **Area of Engagement** by adjusting the scale.
	- The scale represents the **diameter** of the **Sphere**. A size of 3 is large enough to hit all 8 surrounding tiles. Feel free to 
	- **Note**: You can click the **constraint** button to change all 3 axes at the same time

![[adjust-scale.webp]]

- [ ] Find the **Sphere Collider** component in the **Inspector**
- [ ] Enable **Is Trigger**
	- In Unity's physics system, trigger colliders allow other objects to pass through them.

![[create-trigger-collider.png]]

### Transparent Material
Currently, your **Area of Engagement** is being drawn as a hideous sphere in both the **Scene** and **Game** views. 

![[hideous-aoe.webp]]

You can create a transparent **Material** that will allow your player to visualize the area of engagement while not preventing them from seeing enemies that pass through.

- [ ] Create a **Materials** folder in your **Assets**
- [ ] Right click in the **Project View**
- [ ] Select **Create > Rendering > Material**

![[create-rendering-material.png]]

- [ ] Name the **Material** (I recommend "Area of Effect Material")
- [ ] Select the **Material**
- [ ] Drag the **Material** on to your **Area of Effect** in the **Prefab** Editor
	- This will change the **Material** in the **Mesh Renderer** component. Alternatively, you could set it directly in the **Inspector**

![[set-aoe-material.png]]

![[assign-aoe-material.webp]]

- [ ] Select the **Area of Effect Material** in the **Project View**
- [ ] In the **Inspector**, set **Surface Type** to **Transparent**

![[transparent-surface-type.png]]

- [ ] Click on the color to the right of **Base Map** to change the color of the **Material** 
	- Be sure to adjust the **Alpha** value so the material is transparent

![[set-aoe-color.webp]]

Adjusting the **Metallic Map** and **Smoothness** property of the **Surface Input** changes how reflective the material appears. To make the material have no "shine" to it, set both of these values to 0.

- [ ] Set the **Metallic Map** and **Smoothness** properties to 0

![[metalic-map-smoothness-0.webp]]

## Modifying the Y Scale
You may have noticed that it is quite difficult to determine which tiles are within the area of engagement in the isometric game view, especially the tiles that are on the far side of the turret.

![[hard-to-tell-tiles.png]]

To help with this, you can modify the Y scale of the **Area of Engagement**. This will make it more obvious where the edge of the collider is located.

- [ ] In the **Prefab Editor**, select your **Area of Engagement**
- [ ] Set the Y Scale to 1
	- You may need to disable your **scale constraint** toggle

![[scale-aoe-y.webp]]

**Note**: The **Sphere Collider** uses the largest of the 3 scales to determine its size. The **Collider**s are shown in the **Scene View** using green lines. You can verify the size of your **Sphere Collider** by clicking on the **Area of Engagement** in the **Hierarchy**.

![[verify-collider-size.webp]]

## Enemy Collider
Before you can detect if an enemy has entered an **Area of Engagement**, you must first add a **Collider** to your **Enemy Prefab**.
### Challenge: Add a Capsule Collider to Your Enemy Prefab
- [ ] Open your **Enemy Prefab** 
- [ ] Add a **Capsule Collider** component to it
- [ ] Make the **Collider** a **Trigger**
- [ ] Adjust the **Capsule Collider**'s size to roughly the size of your enemy
	- You can use the **Edit Collider** button on the **Capsule Collider** component to edit this in the **Prefab View**

When you're finished, your **Enemy Prefab** should look similar to the image below:

![[add-capsule-collider.png]]

## Add a Rigidbody to Area of Effect
You can use the `Collider.OnTriggerEnter(Collider)` method to detect when a **Collider** has entered a Trigger Collider. However, for the physics system to detect this, at least one of the **Game Object**s must be part of a **Rigidbody**. In this case, you can add a **Rigidbody** to the Area of Effect that is **Kinematic**.

- [ ] Open your **Turret** Prefab
- [ ] Select the **Area of Engagement** from the **Hierarchy**
- [ ] In the **Inspector**, add a **Rigidbody** component
- [ ] Set the **Rigidbody** to be **Kinematic**
	- A **Rigidbody** that is **Kinematic** is unaffected by simulated physics forces.

![[add-kinematic-rigidbody.webp]]


## AreaOfEngagement MonoBehaviour
At this point, everything is ready for you to detect when an **Enemy** has entered the **Area of Engagement** using the `OnTriggerEnter(Collider)` method. 

- [ ] Create an `AreaOfEngagement` **MonoBehaviour** Script
- [ ] In the Turret Prefab, add the component to your **Area of Engagement** object

![[area-of-engagement-component.png]]

### OnTriggerEnter(Collider)

- [ ] Read the Friendly Manual: [Unity - Scripting API: Collider.OnTriggerEnter(Collider)](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Collider.OnTriggerEnter.html)
- [ ] Add a `void OnTriggerEnter(Collider)` to your `AreaOfEngagement` MonoBehaviour
- [ ] Add a `Debug.Log()` to verify that the trigger is working

![[area-of-engagment.png]]

- [ ] Enter **Play Mode** and open the **Console** to verify the Trigger is working

If all went well, your console should look similar to the video below

![[verify-trigger-working.webp]]

### Tracking Enemies
You can use a `List<Transform>` to track the potential targets.

- [ ] Add a `List<Transform> Targets` property to your **Area of Engagement**
	- If you **Serialize** this property, you can view it in the **Inspector**
- In `OnTriggerEnter`, add the entering collider to the `Targets`

![[add-targets.png]]

- [ ] Enter **Play Mode** and verify that the **Target**s are being added to your **Area of Engagement**

If all went well, you should see the **Enemy**'s collider being added to the **Targets** list when they enter the trigger collider.

![[verify-targets-added.webp]]

## Challenge: OnTriggerExit
Next, you will want to make it such that your **Area of Engagement** removes Enemies as they exit the trigger collider.

- [ ] Read the Friendly Manual: [Unity - Scripting API: Collider.OnTriggerExit(Collider)](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Collider.OnTriggerExit.html)
- [ ] Implement `OnTriggerExit(Collider)` such that the collider's transform is removed when the enemy exits the **Area of Engagement**.

If all went well, you should see the collider's being removed from the **Targets** list in the inspector. You may find it useful to increase the size of the Area of Engagement to test this.

![[challenge-remove-transforms.webp]]

## TurretTarget MonoBehaviour
With your **Area of Engagement** script tracking the enemies that are near the **Turret** you can now implement the **TurretTarget** MonoBehaviour to rotate to face one an **Enemy** in the **Targets** list

- [ ] Add a `AreaOfEngagement AreaOfEngagement` property
- [ ] Add a `GameObject Model` property
- [ ] **Serialize** both properties and set them in the **Inspector**

![[turret-target-aoe-model.png]]

- [ ] Set both properties in the **Inspector** to reference the model of the Turret Prefab

![[set-aoe-model-inspector.png]]

### Challenge: Rotate the Model to Face the first Target
- [ ] In `Update`, if `AreaOfEngagement.Targets` is not empty
	- [ ] Call `Model.transform.LookAt` to rotate the model to face the first **Enemy** in **AoE.Targets**

If all went well, you should see your **Turrets** rotating to face enemies as they pass by:

![[rotate-challenge-complete.webp]]

## What's Next
With your turrets successfully tracking the enemies as they pass by, it is time to create a **Projectile** that can be fired at the enemies to destroy them.

