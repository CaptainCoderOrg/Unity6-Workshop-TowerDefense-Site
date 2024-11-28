In this section, you will create a **Waypoint** script that you will use to define positions in your world for your enemies to move between.
## Creating a Waypoint Prefab

It is possible to create a **Prefab** directly in the **Project** explorer.

- [ ] Navigate to your **Prefabs** folder
- [ ] Right Click
- [ ] Select **Create > Scene > Prefab**
- [ ] Name the **Prefab** "Waypoint"

![[create-prefab-in-project.png]]

![[waypoint-prefab.png]]

- [ ] Double click the **Waypoint** prefab to open it

If all went well, you should be in the **Scenes | Prefab** editor with an Empty Game Object named "Waypoint":

![[waypoint-scene.png]]

To make it easy to know where the **Waypoint** is when you add it to a **Scene**, you can add a 3D Sphere (or another shape if you prefer).

- [ ] In the **Waypoint**'s **Hierarchy**, Right Click
- [ ] Select **3D Object > Sphere**

![[create-sphere.png]]

This will add a child object to the **Waypoint** called **Sphere** that is positioned at the center of the **Waypoint**. You can verify this by ensuring the Transform's position is (0, 0, 0)

![[verify-sphere.png]]

You may have also noticed that the defaults **Sphere** generated comes with 3 additional components that are visible in the **Inspector**.

* Mesh Filter - Used to specify the mesh of this object
* Mesh Renderer - Used to specify how the mesh is rendered
* Sphere Collider - Used by Unity's 3D Physics system to detect collisions

Because the **Waypoint** does not need to collide with other objects, you can safely remove this component.

- [ ] Locate the **Sphere Collider** component in the **Inspector**
- [ ] Click the 3 dots on the top right of the component
- [ ] Select **Remove Component**

![[remove-sphere-collider.png]]

Another way you can exit the **Prefab** editor is by clicking the **Scenes** text that appears in the top left of the **Scene** view.

![[exit-prefab-editor.webp]]

- [ ] Exit the **Prefab** editor and return to your **Scene**
## Adding Waypoints to Your Level

You can add a **Prefab** directly into your **Scene** by dragging it into the **Scene** view.

- [ ] Add a **Waypoint** at the starting point of your path
- [ ] Add a **Waypoint** at each corner of your path
- [ ] Add a **Waypoint** at the end of your path

![[add-waypoints.webp]]

## Grid Snapping

Once again, you might find it difficult to precisely place the objects in the **Scene** view. To help with placement, you can enable **Grid Snapping**.

- [ ] In the **Scene** view, enable the **Grid and Snapping** settings from the **Overlay Menu**

![[grid-and-snapping.png]]

Clicking this button will show the **Grid and Snap** settings at the top of the **Scene View**

![[show-grid-and-snap-settings.webp]]

This menu allows you to specify the size of the **Grid** and allows you to turn on **Snapping**. 

- [ ] Set your **Grid Size** to `0.5`

![[set-grid-snap-size.png]]

- [ ] Enable **Grid Snapping**

![[enable-grid-snapping.png]]

- [ ] Ensure that you have your **Tool Handle** settings are set to **Pivot** and **Global**

![[pivot-position.png]]

With **Grid Snapping** enabled, you should now be able to place your waypoints more precisely on your tile map using the **Move Tool**.

![[move-tool.png]]

- [ ] With **Grid Snapping** enabled, use the **Move Tool** position your **Waypoint**s

![[demonstrate-snap-movement.webp]]

If you're having trouble selecting your **Waypoint**s, you can disable the ability to click your **Tile Grid** elements by hovering to the left of the **Grid** **Game Object** in the **Hierarchy** and clicking the finger icon.

![[disable-grid-clicking.png]]

This will disable your ability to click on that **Game Object** in the **Scene View**. You can re-enable interactions by clicking the finger icon again.

![[disable-grid-clicking.webp]]

## Hiding the Waypoints

Currently, your **Waypoint**s are visible in your **Game View** which means your player will see them during game play. You can test this by Entering **Play Mode**.

![[playmode-shows-waypoints.png]]

One way you could hide the **Waypoint**s would be to disable the **Mesh Renderer**. (Don't do this)

![[disable-mesh-renderer.webp]]

However, it is very convenient to be able to see the **Waypoint**s in the **Scene** view so we can adjust them.

Another option is to tell our **Main Camera** to ignore rendering them. This can be done by setting adding the **Waypoint**s to a special rendering layer and then updating the **Main Camera**'s **Culling Mask** to ignore that layer.
### Creating a Waypoint Layer
- [ ] Open your Project Settings
	- From the top menu **Edit > Project Settings**
- [ ] Select the **Tags and Layers** tab on the left

![[tags-and-layers.png]]

- [ ] Verify you're editing the **Layers** drop down
- [ ] Select Layer 6
- [ ] Enter the name "Waypoint"

![[specify-waypoint-layer.png]]

- [ ] Close the **Project Settings** Window

### Specifying the Waypoint Layer

In the **Inspector** you can see and modify the layer of a **Game Object**.

![[where-is-layer.png]]

- [ ] Select a **Waypoint** from your **Hierarchy**
	- Alternatively you could open it in **Prefab** mode
- [ ] Set the **Layer** to **Waypoint** 
- [ ] When prompted select "**Yes, Change Children**"
	- This will set the layer of all children objects to the selected layer

![[change-children.png]]

- [ ] If you are not editing in **Prefab** mode, don't forget to apply the **Override**

### Camera the Culling Mask

Culling refers to the process of determining which objects in a scene are not visible to the camera and excluding them from rendering to improve performance. Next, you will update the **Main Camera**'s **Culling Mask** to exclude the **Waypoint** layer.

- [ ] Select the **Main Camera**
- [ ] In the **Inspector** locate the **Camera** components **Rendering** settings

![[culling-mask-settings.png]]

By default, the camera's **Culling Mask** will render everything. 

- [ ] Select the Drop Down and unselect the **Waypoint** layer

You can verify that the camera is no longer rendering your **Waypoint**s by entering the **Game View**.

![[verify-waypoints-hidden.webp]]

## Waypoint Component

With your Waypoints placed on your map, it is now time to make them aware of their order. You can accomplish this by creating a Waypoint component that knows which **Waypoint** comes next in the sequence.

- [ ] Create a **Waypoint** MonoBehaviour
- [ ] Delete the Start and Update methods from the template, you won't need them
- [ ] Add a **Waypoint** property called **Next**
	- Remember to use good programming practices and us a `private set`
- [ ] Serialize the **Next** property using the `[field: SerializeField]` attribute


![[waypoint-component.png]]

### Practice

Can you remember how to add your new component to your **Waypoint** prefab? If you're having trouble, you can review how you added the **EnemyMovement** component in [[06 - Adding an Enemy]]

- [ ] Add the **Waypoint** component to your **Waypoint** Prefab
- [ ] Verify that each **Waypoint** object in your scene has the component

![[verify-waypoints.webp]]

## Set the Waypoint Sequence in the **Inspector**

By creating a **Next** property that has the type **Waypoint** , you have made it possible to specify the **Next** property of each **Waypoint** in the **Inspector**.

- [ ] Select your starting **Waypoint** Game Object from the **Hierarchy**
- [ ] In the **Inspector** click the small circle next to the **Next** property
- [ ] Select the second **Waypoint** Game Object from the list

**Note**: If you click the object in the **Next** field, it will highlight in the **Hierarchy**. If you double-click the object in the **Next** field, it will select that object.

![[set-next-on-first-waypoint.webp]]

You can also set the an object property in the **Inspector** by dragging a game object into the property field.

![[set-waypoint-dragging.webp]]

Sometimes this can be challenging to do because you can accidentally click the object you're trying to drag, changing the selected object in the **Inspector**. To help with this, you can open a new inspector window for a specific game object by **Right Clicking** on it and select **Properties**.

![[properties-window.webp]]

### Practice

Test out each of the methods for setting the **Next** for each of your **Waypoints** property to figure out which one works best for you. You should leave the final **Waypoint**'s **Next** property as **None**. You will use this to signal to the **Enemy** that it has reached the end of the path.

## Organizing the **Hierarchy**

Depending on the number of **Waypoints** you have created, your **Hierarchy** might be feeling a bit crowded. To help with this, create an **Empty Parent** that contains all of the **Waypoint**s as children object.

When you're finished, your **Hierarchy** should look similar to the image below:

![[organize-waypoints.png]]

## Drawing the Waypoint Path in the Scene View

While setting each of the **Next** properties, you may have sensed that this process could be error prone. That is, it is easy to set the wrong **Waypoint**. To help with this, you can use the **OnDrawGizmos** and **OnDrawGizmosSelected** methods to draw additional information in the **Scene View**.

### OnDrawGizmosSelected

The **OnDrawGizmosSelect** method is used to draw information in the **Scene View** when a **Game Object** is selected. 

- [ ] Read the Friendly Manual
	- [Unity - Scripting API: MonoBehaviour.OnDrawGizmosSelected()](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/MonoBehaviour.OnDrawGizmosSelected.html)
	- [Unity - Scripting API: Handles](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Handles.html)
- [ ] Add `using UnityEditor;` to your `using` statements
	- **Note**: This will allow you to access the **Handles** API
- [ ] Add the **void OnDrawGizmosSelected()** to your **Waypoint** script
	- **Note**: Spelling and casing must match exactly
- [ ] Set the **Handles.color** property to **Color.red**
- [ ] Use the **Handles.DrawLine** method to draw a line between the **Waypoint** and its **Next**

![[drawing-red-line-on-selected.png]]
With your new gizmo in place, you can now more easily verify that your **Waypoint**s are connected properly:

![[view-gizmo-line.webp]]

### Null Check

You most likely encountered **NullReferenceException** when you selected your final **Waypoint**. This is because the **Next** property is set to **None**. For class objects, this is the equivalent to a `null` value. To prevent this, you should add a **null** check to your code that exists your method early if `Next == null`.

![[null-check.png]]

### Using OnDrawGizmos

If you prefer, you can also use the **OnDrawGizmos** method which is executed in the **Scene View** even when the **Game Object** is not selected.

- [ ] Rename your **OnDrawGizmosSelected** method to **OnDrawGizmos**

![[on-draw-gizmos.png]]

In the **Scene View** verify your path is correct

![[view-all-gizmo-lines.webp]]


## Binary Waypoint Challenge

It is important to review what you've learned in this lesson and apply it in a new context. Before continuing, I encourage you to attempt the [[Binary Waypoint Challenge]] in which you will be challenged to create a new script to accommodate splitting paths.

![[binary-waypoint-connections.png]]

## What's Next

With your **Waypoints** set up, it is now time to update your **Enemy Movement** script to move between each **Waypoint**.
