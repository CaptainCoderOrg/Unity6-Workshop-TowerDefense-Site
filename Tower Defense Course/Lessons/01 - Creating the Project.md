## Create the Project
Before starting, you will need to create a new Unity 6 project. The picture below shows the settings you should select when creating the project.
- [ ] Ensure the editor version begins with **6000.0.**
- [ ] Ensure you are using the Universal 3D Core template 
	- [ ] (DO NOT USE **High Definition 3D** you will not be able to publish your project if you choose this setting)
- [ ] Name your project (I recommend naming it Tower Defense)
- [ ] You do not need to connect to **Unity Cloud** or **Unity Version Control** you can unselect these options.
![[UnityHubProjectSettings.png]]

After selecting **Create project** you should see the **Unity Engine** window (similar to the one below). The first time you initialize a project, it may take several minutes depending on the speed of your computer.

![[UnityEngineInitializing.png]]

If all went well, you should see the default Unity project displayed. It should be similar to the image below:

![[DefaultProjectInitialized.png]]

If something doesn't look quite right, you may want to set the **Layout** to the default view. For the majority of this course, the screenshot will be using the default layout.

You can set the default layout from the top menu: **Windows > Layouts > Default**

![[UnitySetDefaultLayout.png]]

## Create a Tower Defense Scene
Before continuing, be sure to create a new **Tower Defense Scene** for your project. If you use the default **Sample Scene** there is a slight chance that it could be overwritten during an import of library / challenge project.

- [ ] In the **Project View**, navigate to **Assets > Scenes**

![[open-scenes-folder.png]]

- [ ] Right click in the **Project View** 
- [ ] Select **Create > Scene > Scene**

![[create-scene.png]]

- [ ] Rename your new Scene (I recommend "TowerDefenseScene")

![[rename-scene.png]]

- [ ] Double click to open your new **Scene**
- [ ] Delete the original `SampleScene` to prevent yourself from accidentally using it.

![[delete-sample-scene.png]]
## What's Next

With your **Tower Defense Scene** created, you're ready to design your map. In the next section, you create a Tile Grid that will be used to create your map

[[02 - Creating a Tile Grid]]