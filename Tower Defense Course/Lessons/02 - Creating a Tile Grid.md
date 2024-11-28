## Mini-Lecture
The mini-lecture below provides a high level overview of what you'll learn in this section. Watch the video and take notes. Then, complete the lesson below to apply the concepts from the video. 

**Warning**: It is not recommended to work along side the video as the content is not identical to the lesson.

<iframe width="560" height="315" src="https://www.youtube.com/embed/2rXo9YYaTxA?si=JILtv7LmvA3NJfKQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Importing Assets

- [ ] Download Kenney's Tower Defense Kit: https://kenney.nl/assets/tower-defense-kit
- [ ] Extract the archived **zip** file

![[ExtractFile.png]]

- [ ] Within the extracted folder find the open the **Models** folder and open it
![[find-models.webp]]
- [ ] Import the **FBX format** folder into your **Assets** folder
![[import-fbx-format.webp]]
- [ ] Rename the folder. I recommend calling it **Kenney Tower Defense Kit Models**
![[rename-folder.webp]]

## Adding a Tile to the Scene

- [ ] Navigate to the **Tower Defense Kit Models** in folder in Unity's **Project** explorer

**Note:** You can adjust the size of the preview by using the slider in the bottom right corner of the **Project Explorer** tab.

![[resize-project-preview-size.webp]]

- [ ] Find the `tile` model and drag it into the scene

![[add-tile-fbx-to-scene.webp]]
## Creating a Tile Prefab
Before you add any more tiles to the scene, you should parent the **tile** model and create a Prefab to represent your tile. This will be useful if you decide to change the tile later (and you will).

- [ ] Right click on the `tile` object in the **Hierarchy** and select **Create Empty Parent** this will create a new **Game Object** with the `tile` as a child.

![[create-parent.webp]]

- [ ] Rename the parent object. I recommend calling it `Tile`

Now that you have a `Tile` **Game Object**, that will be the basis of each cell of your map, it is time to turn it into a reusable **Prefab**. To create a **Prefab** from an existing object, drag that object from the **Hierarchy** into your **Project** tab.

- [ ] Drag your `Tile` **Game Object** into your `Assets` folder.

![[create-prefab.webp]]

You'll notice that the **Game Object** in the **Hierarchy** is now appears in blue and has a small arrow `>` on the right side of the **Hierarchy**. This tells you that this **Game Object** is using a **Prefab**.

![[notice-prefab.png]]

**Note**: You should use a **Prefab** any time you plan to use the same **Game Object** in multiple places (e.g., enemies, structures, UI elements). Most projects have many **Prefab**s and as such, it typically makes sense to create a folder to hold them.

- [ ] Create a **Prefabs** folder in your **Assets** folder
- [ ] Move the **Tile** **Prefab** into your **Prefabs** folder

![[create-prefabs-folder.webp]]
## Positioning a Second Tile

For this game, you will need to create a grid of `Tile` **Game Objects** that are aligned perfectly on the X, Y, and Z axis. This can be quite difficult and tedious to do even with just two Tiles! Try it.

- [ ] Add a second **Tile** **Prefab** to your **Hierarchy**
- [ ] Try to align the new **Tile** perfectly on the X, Y, and Z axis with the existing tile so they are adjacent.

![[try-to-align.webp]]

You may have found it very difficult to perfectly align the two tiles, especially using the mouse! One option to align them perfectly is to use the inspector to se them to be exactly 1 unit apart (the tiles happen to be 1 Unity unit on the X and Z axis! LUCKY YOU!)

- [ ] Use the **Inspector** to adjust the **Tile** positions to be perfectly spaced 1 unit apart on the X or Z axis

![[perfect-alignment-with-inspector.webp]]

### Challenge Create a 3 x 3 Grid
Using the above process, can you create a perfectly aligned 3x3 grid of Tiles?
- [ ] Create 9 **Tile** prefabs
- [ ] Move the **Tiles** into a parent object named **Grid**
- [ ] Perfectly align each **Tile** such that they form a 3x3 grid with no overlapping edges and no visible seams

When you are finished, your **Hierarchy** and **Scene** view should look similar to the image below:

![[challenge1-solution.png]]

## Creating a 10x10 Tile Grid

After completing the previous challenge, you might be realizing how difficult, tedious, and painful it is going to be to create a large grid for your game in this manner. When you find yourself performing a repetitive task, it is often beneficial to seek if an automated solution exists and if it does not exists, create one.

In this case, there exists a partially automated solution (later you will create a fully automated solution).

### Using Unity's Linear Spacing Syntax

You will often want to place **Game Objects** at an evenly spaced distance. This can be quickly don by using **Unity's Linear Spacing Syntax**. This allows you to specify a starting position and an ending position for a set of objects and Unity will automagically space the objects between those positions.

- [ ] Create 1 more **Tile** so you have a total of 10 tiles
- [ ] Select all 10 **Tile** objects in the inspector
	- **Note**: You can select multiple objects by holding **Shift** while clicking. This will select all of the objects between the first object clicked and the last object clicked.
	- **Note**: You can add or remove a single object to a selection by holding **Ctrl/Command** and clicking on the object
- [ ] Set all of the **Tile**s positions to 0, 0, 0 in the inspector.
- [ ] In the X Position editor, type **L(0, 9)**

![[linear-on-10-objects.webp]]

At this point, you should have 10 **Tile** objects spaced perfectly in a single row. Next, you need to create 10 rows that are evenly spaced.

- [ ] Select your 10 **Tile**s and put them into an **Empty Parent Object**
- [ ] Rename the parent (I recommend calling it a row)
- [ ] Duplicate your row such that you have 10 rows
	- **Note:** Ctrl+D/Command+D will duplicate the selected **Game Object** 
- [ ] Use **Linear Spacing Syntax** to place the rows evenly on the Z axis between 0 and 9

![[linear-on-z-axis.webp]]

## Changing the Tile Prefab's Model

Earlier in the lesson, you created a **Tile** **Prefab**. One of the major benefits of using a **Prefab** is the ability to change all **Game Objects** that use that **Prefab** throughout your project by modifying the original.

Double clicking on a **Prefab** asset in the **Project** explorer will open it in the **Scene** tab where it can be edited. You can exit the **Prefab** editor by clicking the `<` near the top of the **Hierarchy**. 

![[open-prefab-editor.webp]]

- [ ] Open your **Tile** **Prefab**

You may have noticed that the `tile` model you previously added to the `Tile` object is a prefab! Recall that you can easily identify prefab game objects by their blue color in the **Inspector**.

Some times, it is useful to unpack a prefab object to separate it from the parent **Prefab**. This can be done by right clicking on the **Game Object** in the **Hierarchy** and selecting **Prefab > Unpack**. When you do this, it disconnects it from the prefab such that it won't update if the original prefab changes. Because some of your **Tile**s will use different models, you will want disconnect the **tile** **Prefab** to allow the model to be changed.

- [ ] Completely Unpack the `tile` object
- [ ] Rename the `tile` object to be more generalized (I recommend `model`)

![[unpack-tile-model.webp]]

With the child object renamed, you can verify that all of your **Tile** **Prefab**s have changed exiting the **Prefab Scene** and opening your **Tile** objects.

- [ ] Verify that your **Prefab**s have updated

![[verify-prefab-update.webp]]

You will often want to make changes to a single instance of a **Prefab**. For example, you will want to change some of your tiles to use a different model. This can be done by editing the **Game Object** directly in the **Scene** view's **Hierarchy / Inspector**.

In this case, you want to adjust some of your **Tile**s to use a different **mesh**. This can be set on the `model` **Game Object**'s `Mesh Filter`. In the **Inspector** you can click the small circle next to the `Mesh` field to see all `mesh` assets in your project that can be set.

- [ ] Select a **Tile** in your **Scene**
- [ ] Select the **model** child **Game Object**
- [ ] Update the `Mesh` of the `model` **Game Object** to be `tile-dirt`

![[set-tile-dirt-model.webp]]

By clicking the `>` button to the right of a **Prefab** in the **Hierarchy**, you can edit a **Prefab** in the **Scene** view. When you do this, all elements in the **Scene** view that are not apart of the selected object will be shown in grey scale indicating that you cannot interact with them in the **Hierarchy**.

- [ ] Select a **Tile** in the **Inspector**
- [ ] Click the `>` button to enter the **Prefab** editor within the **Scene**

![[enter-prefab-scene-editor.webp]]

While editing the **Tile Prefab** while in the **Scene** view, you can observe the changes live.

- [ ] Change the **Tile Prefab's** the `Mesh` property to be `snow-tile`
- [ ] Exit the **Prefab** editor

![[change-to-snow-tile.webp]]

One thing to note is that the **Prefab** that you previously modified in the **Hierarchy** did not change. This is because the `Mesh` property has been overridden. You can see all **Overrides** for a **Game Object** in the **Inspector** by selecting the **Overrides** drop down. Additionally, if you can **Revert** those changes to the **Prefab**'s current setting or **Apply** those changes to the **Prefab** to propagate the change throughout your project.

- [ ] Select the **Tile** that is different
- [ ] In the **Inspector** find the **Overrides** drop down
- [ ] Select **Apply All** to change all of the **Tile Prefabs** to use the dirt mesh


![[apply-overrides-inspector.webp]]

### Practice
Practice editing prefabs by setting the **Tile Prefab** to use a different mesh using each of the methods described above
- [ ] Edit the **Prefab** directly
- [ ] Edit a **Tile** using the **Scene** prefab editor
- [ ] Modify a **Tile** then **Apply** the **Override** to all prefabs

Before continuing, update your **Tile Prefab** to use the `tile` mesh. This particular **Prefab** will be used as an empty tile where the player can build a structure.

## What's Next

In the next section, you will create several more **Prefabs** that you will use to build a more detailed map

[[03 - Creating Additional Tile Prefabs]]