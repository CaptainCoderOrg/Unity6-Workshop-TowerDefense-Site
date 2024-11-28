Before you can design your first level, you will need to create a few more **Prefab**s that will be used on your Grid in place of the empty **Tile**.
## Mini-Lecture
The mini-lecture below provides a high level overview of what you'll learn in this section. Watch the video and take notes. Then, complete the lesson below to apply the concepts from the video. 

**Warning**: It is not recommended to work along side the video as the content is not identical to the lesson.

<iframe width="560" height="315" src="https://www.youtube.com/embed/HqbWWXe45LM?si=vEG6DDuP7stoX5g7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Path Tile Prefab

Start by changing the `Mesh` of a **Tile** in your scene to use the `tile-dirt` mesh.

- [ ] Select a **Tile** in your **Scene**
- [ ] Change the `Mesh` property of the selected tile to `tile-dirt`

![[set-tile-dirt-model.webp]]

This **Game Object** will be the basis for a **Path Tile Prefab.

- [ ] Select the modified **Tile** in the **Inspector**
- [ ] Unpack Completely so it is no longer attached to the **Tile** Prefab
- [ ] Rename the **Game Object**. (I recommend calling it Path Tile)

![[unpack-path-tile.webp]]

- [ ] Drag the **Path Tile** into your **Prefabs** folder to change it to a new **Prefab**

![[create-path-tile-prefab.webp]]

### Practice: Create More Tile Prefabs

Practice unpacking and creating a few more prefabs
- [ ] Create a Tree Tile using the `tile-tree` mesh
- [ ] Create a Rock Tile using the `tile-rock` mesh
- [ ] Create a Crystal Tile using the `tile-crystal` mesh

When you have finished, you should have 5 **Tile Prefabs** that look similar to the ones picture in the image below.

![[create-tiles-challenge.png]]

## Replacing a Prefab

It is possible to swap out a **Prefab** for another quickly in the **Hierarchy** by right clicking on **Prefab** and selecting **Prefab > Replace**.

- [ ] Select a **Tile** you would like to change to a **Path Tile**
- [ ] Right click on it in the **Inspector**
- [ ] Select **Prefab > Replace**
- [ ] Search for and select the **Path Tile** prefab

![[replace-prefab.webp]]

You can also replace a **Prefab** from the **Inspector**.

- [ ] Select a **Tile** you would like to be a path
- [ ] In the **Inspector** click the circle next to the **Prefab** value
- [ ] Search for and select the **Path Tile Prefab**

![[replace-prefab-inspector.webp]]

Changing a **Prefab** from the **Inspector** is particularly useful if you would like to change several **Game Objects** at the same time.

- [ ] Select several **Tile**s that you would like to be a path
	- Hold **Ctrl/Command** while clicking in the **Scene** to add or remove a game object to your selection.
- [ ] In the **Inspector** click the circle next to the **Multiple** value
	- **Note**: The **Prefab** word changes to **Multiple** if you have several objects selected
- [ ] Search for and select the **Path Tile Prefab**

![[replace-multiple-prefabs.webp]]

## Challenge: Design a Map

With everything you've learned so far, it is now time to design a map for your first level! 

- [ ] Your tile grid should be 15x15
	- **Note**: Odd length sides will result in a "center" tile
- [ ] Your level should use at least 5 different types of tiles
- [ ] Your level should have one continuous path from the edge of the map to an "end" location, eventually your Player's tower will be placed here. 
- [ ] Bonus: Share a screenshot of your Map with a friend!

When you're finished, your map might look something like the image below:

![[Example Finished Map.png]]

## What's Next

With a tile grid designed for your game, you are ready to set up the player's view. In the next section, you will configure your editor's Play Mode to optimize your design experience.

[[04 - Play Mode Settings]]