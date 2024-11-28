In this section, you will learn how to configure your **Main Camera** to render your game **Isometrically**.

## Isometric Scene View

An isometric camera shows a scene from a tilted angle, so you can see multiple sides of objects at the same time, like the top and two sides of a building. Unlike a regular camera, it doesn’t make things in the distance look smaller, which keeps everything the same size and gives a clean, organized look. It’s often used in games and art to create a clear and detailed view of the world.

By default, the **Scene** view is set to use an **Perspective** camera. This makes things that are further away appear smaller and things that are closer larger. In the top right corner of the **Scene** view, there is an **Orientation Gizmo** that allows you to switch to an **Isometric** view by clicking on the text  "**Persp**". To return to a **Perspective** view, you can click the text "**Iso**".

![[iso-camera-scene-view.webp]]

- [ ] Find the **Orientation Gizmo** in the **Scene** view
- [ ] Change to **Isometric** view
- [ ] Change back to **Perspective** view

You may find it difficult to move the camera in **Isometric** view. To help navigate, you can double click on game objects in the **Hierarchy** to move the camera to that position. Then, rotate the **Scene** view camera by holding the right mouse button and dragging it.

- [ ] Switch to **Isometric** view
- [ ] Double click your **Grid** in the **Hierarchy**
	- This will center the camera on the object
- [ ] Hold down the right mouse button and drag in the **Scene** view to adjust the camera to a slight angle
	- On a track pad, **Right click** is often implemented with a two finger touch
	- On mac, you can hold the **Option** key while dragging to emulate a right click
- [ ] Use the **View Tool** to adjust the camera view port
- [ ] Again, Double click your **Grid** in the **Hierarchy**
	- This time, it will zoom in on that game object
- [ ] Zoom out by scrolling with the mouse wheel (or track pad)

![[moving-iso-camera.webp]]

It will take some practice but, as you continue to use the editor you will become more comfortable with the camera movement.

Another setting that is useful to be aware of is the **Handle Position Pivot Toggle**. This is located in the top left of the **Scene View**. 

![[pivot-setting.png]]

By default, this is set to **Pivot** but it is often useful to set it to **Center**. This adjusts the "pivot" point when interacting with an object. This can be useful when you want to move an object by its center point (or find an object's center point).

![[pivot-setting.webp]]

## Setting Up an Isometric Game Camera

Next, you will set up your game's **Main Camera** to render in an **Isometric** view.

To help configure the **Main Camera's** view, you can enable a **Camera** preview in the **Scene** view. You can find the **Cameras** toggle on menu that is docked in the bottom left of the **Scene View**.

- [ ] Locate the **Cameras** toggle and enable it

![[camera-preview-setting.png]]

If all went well, you should now see a **Cameras** window that shows the **Main Camera**'s current view (by default, this appears in the bottom right of the **Scene** view).

![[camera-preview-setting-2.png]]

Currently, your main camera is likely aimed directly across your map (or your map may not be visible at all). To help with this, you will center your grid in your game world.

- [ ] Set your **Tile Grid**'s Transform Position to (0, 0, 0)

![[center-grid.webp]]

Next, adjust your Camera to be centered in your game world slightly above your Grid.

- [ ] Set your **Main Camera**'s Transform Position to (0, 1, 0)

![[center-camera.webp]]

You may have noticed a few things that feel a bit off:

1. The camera is showing in a **Perspective View** rather than an **Isometric** view
2. The camera is positioned above the corner of your map rather than the center

### Orthographic Projection

To achieve an **Isometric** feel within a 3D game, you can set the **Projection** mode of your camera to **Orthographic**.

- [ ] Select your **Main Camera** in the **Hierarchy** 
- [ ] In the **Inspector** find the **Camera Component**
- [ ] Within the **Camera Component** expand the **Projection** settings
- [ ] Set the **Perspective** to **Orthographic**

![[camera-orthographic-projection.webp]]

You'll notice after you change to an **Orthographic** projection, that the camera preview in the **Scene** view changes from a pyramid shape to a rectangular view port. You can adjust the size of the rectangle by changing the **Size** property in the **Projection** settings.

- [ ] Set the **Size** of the **Orthographic Projection** to 8

![[orthographic-size.webp]]

This property represents the height of the view port for this camera's projection. More specifically, how many units from the center of the rectangle to the top and bottom edge. That is to say, with a size of 8, the view port has a height of 16. This size will allow your 15x15 tile grid to fit centered on the screen.

To achieve 2.5D isometric feel, you can adjust the camera's position to center on the grid and rotation of your camera to be at an angle

- [ ] Set your **Main Camera**'s Transform Position to (0, 0, 0)
- [ ] Set your **Main Camera**'s Transform Rotation to (22.5, 45, 0)
	- Other good options are (30, 45, 0) and (37.5, 45, 0)

![[rotate-camera.webp]]

It is hard to see in the **Main Camera** preview, but the camera is still centered on the corner of your map that is positioned at (0, 0, 0). Additionally, a small portion of that corner is now missing in the camera view!

If you switch to the **Game** view, it is much more obvious

- [ ] Switch to the **Game View** tab

![[missing-corner.png]]

## Centering the Grid

Currently, your Grid's Transform is set to (0, 0, 0). However, if you set the **Handle Position Toggle** to the **Pivot**, you will notice that the Tile objects within are positioned from (0 to 14) in both the X and Z directions. This is useful for quickly identifying their location within the Grid.

At this point, it would be difficult to reposition all of the children objects directly. However, you can create a new "Position Pivot" object that will help you reposition all of the tiles.

- [ ] Create a new Game Object that is a child of the **Grid**
- [ ] Name the new Game Object "Position Pivot"

![[position-pivot.png]]

Next, move the "Position Pivot" so it is in the center of the Grid. Because you know the grid is 15x15, you can set the X position to 15/2 and the Z position to 15/2.

- [ ] Set the Position Pivot Transform Position to (15/2, 0, 15/2)
	- You'll notice that the math expression is evaluated resulting in the position (7.5, 0, 7.5)

![[set-position-pivot.webp]]

By reparenting all of the tiles within the "Position Pivot", their positions will now be relative to the "Position Pivot" which is centered. This allows you to move them relative to their center.

- [ ] Move all of the rows to be children of the "Position Pivot"
- [ ] Set the Position Pivot's Transform Position to (0.5, 0, 0.5)
	- This will move the center tile to the middle of your world. The 0.5 accounts for the size of the tile being 1 unit in size on both the X and Z axis.

![[center-all-tiles-with-pivot.webp]]

You can verify that the tiles are now centered within the **Grid** by switching the **Tool Handle Position** to **Pivot** and double clicking the **Grid**. The camera will move to the center of your map.

## Fixing the Clipping Planes

Now that you have centered your grid in your world view, it may be more obvious why only part of your tile grid is being displayed in the **Main Camera**. In this case, you can only see the top half of the grid!

If you select the **Main Camera** in the **Scene View**, you'll see the issue more clearly.

- [ ] Select the **Main Camera** in the **Hierarchy** while in the **Scene View**

Notice, the rectangle view port of the camera preview is bisecting your grid. This is related to centering the camera directly on your tile grid. By default, an **Orthographic Projection** will only display elements in front of it. This is called the **Near Clipping Plane**. You can adjust this setting to change the size of the **Clipping Plane** to start behind the camera in the **Projection** settings.

- [ ] In the inspector, find the **Clipping Planes** setting in the **Projection** settings of your **Camera**
- [ ] Set the **Near Clipping Plane** to -50
- [ ] Set the **Far Clipping Plane** to 50

![[adjust-clipping-plane.webp]]

The **Clipping Plane** is used to specify how far in the game world this camera searches for game objects to be rendered. When the **Near Clipping Plane** was set to 3, the camera was not rendering anything that was behind the position of the camera.

## Developing for an Aspect Ratio / Resolution

You may have noticed that within the **Game View** your game looks pixelated. This is likely caused by the **Game View** scaling to 1.3x (or higher). You may have also noticed that you cannot adjust the scale below 1.3x! This is due to a setting that is enabled for "Low Resolution Aspect Ratios". You can disable this setting in the **Aspect** drop down of the **Game View**.

- [ ] Switch to the **Game View** tab
- [ ] Select the **Aspect** drop down (by default this says **Free Aspect**)
- [ ] Disable the "Low Resolution Aspect Ratios" setting

![[disable-low-aspect-ratios.webp]]

You should now be able to set the Scale to 1x.
### Aspect Ratio

Aspect ratio refers to the proportional relationship between the width and height of a display or image, expressed as a ratio like 16:9 or 4:3. In Unity, aspect ratio is important because it determines how your game looks on different devices, ensuring that graphics and UI elements aren't stretched or cropped.

By default, Unity starts in **Free Aspect** this means your camera's resolution is the size of your **Game View** tab's view. You can also enforce an **Aspect Ratio** or specific resolution by changing the **Aspect** in the **Game View**.

- [ ] Select the **Game View** tab
- [ ] Set the **Aspect** to "Full HD (1920x1080)"
- [ ] Resize the **Game View** tab

![[set-hd-resolution.webp]]
You'll now notice that the elements within the **Game View** will begin to scale with the size of the view port. This is because the game camera will now force the specified resolution / aspect ratio.

The majority of desktop and TV screens use a 16:9 aspect ratio. If you are developing for mobile devices, you will need to take more care to ensure the game functions properly for more aspect ratios. For this project, we will use a 16:9 ratio.

- [ ] Set the **Aspect** to **16:9**
## Isometric Camera Challenge
Whew! That was a lot of work. The best way to learn and retain something is to practice it. Before continuing to the next lesson, why not see if you can set up an Isometric Camera again in the [[Isometric Camera Challenge]]?

If you get stuck or need help, you can refer back to this lesson. Best of luck!

## What's Next

With your Game Camera set up, you are ready it is time to create your game's mechanics. In the next lesson, you will learn how to create a simple enemy that moves within your world.

[[06 - Adding an Enemy]]