## Entering Play Mode

Thus far, you have only worked within the **Scene** view without testing how your game will appear to a player. To enter **Play Mode** to see what the player's experience will be, click the Play button at the top center of the Unity Editor window.

![[enter-playmode-button.png]]

Upon entering **Play Mode** you'll notice a few things. First, you likely will see a loading window that will appear for a few seconds (in some cases more minutes!). Then, the editor will automatically switch the the **Game** view. You can tell when you're in **Play Mode** when the play button switches to a "stop" button and is highlighted. Additionally, the editor changes to a slightly darker tint.

You can see each of these changes in the video below:

![[entering-playmode.webp]]

## Editing in Play Mode

A common beginner mistake happens when you modify your scene while you're unintentionally in **Play Mode**. This can result in lost work. The moment you exit **Play Mode** all changes revert back to the state they were in prior to entering **Play Mode**

You can test this by moving your camera while you're in **Play Mode** then exiting **Play Mode**

- [ ] Enter **Play Mode**
- [ ] While in **Play Mode** select your **Main Camera**
- [ ] Move the **Main Camera's** Y position in the **Inspector**
- [ ] Tilt the **Main Camera** down by adjusting the X rotation in the **Inspector**
- [ ] Exit **Play Mode**

You'll notice as soon as you exit **Play Mode** the camera's Transform is restored to it's original values. 

![[editing-in-playmode.webp]]

To help prevent accidentally editing your project in Play Mode, you can change the **Play Mode Tint** to a more obvious color.

### Changing **Play Mode Tint**

 - [ ] First, enter **Play Mode**
 - [ ] From the top menu, select **Edit > Preferences** (on Mac it is **Unity > Preferences**)

![[preferences.png]]

- [ ] In the Preferences window, use the search bar to search for `playmode tint`

![[playmode-tint.png]]

- [ ] Click the color bar adjacent to the `Playmode tint` option on the `Colors` tab 
- [ ] Adjust the color setting. (I personally use yellow)
	- **Note**: If you're in **Play Mode** you can preview what the change will look like

![[changing-playmode-color.webp]]

## Enter Play Mode Settings

Now that you can more easily tell when you are in **Play Mode** you may also want to update your **Play Mode** setting so you can enter **Play Mode** more quickly. Recall, when you enter **Play Mode** you receive a small loading window which says it is "Reloading Domain":

![[reloading-domain.png]]

By default, both the **Scene** and **Domain** are reloaded every time you enter **Play Mode**. There are good reasons to do this, especially for users who are new to Unity. The manual states, "By default Unity reloads the domain on entering Play mode to reset the application state. Resetting state before entering Play mode is often desirable so your application starts up as it would at the beginning of a new build." 

However, it does slow down your iteration speed. Because of this, the Unity Editor provides the option to disable it so long as you invest the effort to implement checks in your code that reset values properly when entering **Play Mode**. You can read more about **Domain Reloading** in the manual here: [Unity - Manual: Enter Play mode with domain reload disabled](https://docs.unity3d.com/6000.0/Documentation/Manual/domain-reloading.html)

### Disabling Domain Reloading

- [ ] From the top menu, select **Edit > Project Settings**
	- **Note**: this is not the same as **Preferences** 

![[project-settings.png]]

- [ ] Select **Editor** from the left menu
- [ ] Scroll to the bottom of the **Editor** settings
- [ ] Find **When entering Play Mode**
- [ ] Change the drop down to **Do not reload Domain or Scene**

![[editor-playmode-settings.png]]

- [ ] Close the **Project Settings** window
- [ ] Enter **Play Mode**

You should notice entering **Play Mode** is now almost instantaneous.

![[instant-playmod.webp]]

## What's Next

Now that you have configured **Play Mode** to work better for you, it is time to set up the game's isometric camera.

[[05 - Creating an Isometric Camera]]