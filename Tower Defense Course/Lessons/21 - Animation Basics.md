# Attaching an Animation to your Enemy
Many of the Kenney assets come with predefined animations you can use to add some life to your enemies. In this lesson, I will be showing how to add animations to the `character-zombie`  model but this process should be the same for most of the Kenney character assets.

- [ ] Locate the Kenney model you're using for your enemy in your assets
- [ ] Click the expand button on the model
- [ ] You will see several sub components of the model including several animations

![[locate-animations.webm]]

## Previewing Animations
To make it easier to choose which animations to use, you can preview them in the **Inspector**

- [ ] Select the Kenney model in your assets
- [ ] In the **Inspector**, select the `Animation` tab
- [ ] Find the **Clips** section
- [ ] Select an animation
- [ ] Open the **Preview** tab at the bottom of the inspector
- [ ] Press Play

![[preview-animation.webm]]

## Adding an Animator to your Enemy

- [ ] Open your Enemy Prefab
- [ ] In the **Hierarchy** select your **model**
- [ ] Add an **Animator** component

![[adding-an-animator.webm]]

## Creating an Animator Controller
An animation controller allows you to switch and blend many different animations together during game play. You will need to create one to add to your Enemy's **Animator**

- [ ] Navigate to your **Prefabs/Enemies** folder
- [ ] Right click in the folder
- [ ] Select **Create** > **Animation** > **Animation Controller**
- [ ] I recommend naming your **Animation Controller**  "Enemy Animation Controller"

![[create-animation-controller.webm]]

- [ ] Select your **Enemy/model** in the **Hierarchy**
- [ ] Locate your **Animator**
- [ ] Set the **Animator**'s **Controller** property to be your **Enemy Animation Controller**

![[add-animation-controller.webm]]

## Adding a Sprinting Animation

- [ ] Locate your **Enemy Animation Controller** in the **Project** window 
- [ ] Double click to open it
- [ ] This will open a new window called the **Animator** window

![[open-animator.webm]]

The **Animator** window shows you the different states of animation that your model can be in. By default, it has no animations.

- [ ] Right click in the **Animator** window
- [ ] Select **Create State** > **Empty**
- [ ] This will create a node and the **Entry** node will connect to it

![[create-empty-state.webm]]

- [ ] Select the **New State** in the **Animator Window**
- [ ] In the **Inspector** you can rename the state. 
- [ ] In this section we will add a **Sprint** animation

![[rename-sprint-state.webm]]

- [ ] Select **Sprint** animation node on your **Enemy Animation Controller**
- [ ] In the **Project** window navigate to the appropriate model's **sprint** animation
- [ ] Drag the animation into the **Motion** property of the **Animation Node** in the inspector

![[attach-sprint-animation.webm]]

## Previewing the Animation on your Enemy

- [ ] Open your **Enemy** prefab
- [ ] Select the **model** 
- [ ] From the top menu select **Window** > **Animation** > **Animation**
- [ ] Optionally dock the **Animation** window
- [ ] If all went well, you should be able to click play and see the animation on your prefab

![[previewing-animation-onprefab.webm]]
## Looping the Animation

- [ ] Enter Play Mode to see your animation in action
- [ ] You will notice that the animation plays once and then stops

![[play-once-and-stop.webm]]

- [ ] In the **Animator** window, select the **Sprint** node
- [ ] Double click the **Sprint** node to toggle the inspector between the Node settings and the **Animation** object
- [ ] In the **Inspector** select the **Animation** tab
- [ ] Scroll to the bottom of the **Inspector** to find the **Animation** properties section
- [ ] From the **Source Take** drop down, select **sprint**
- [ ] Set the name of the animation **sprint-loop** (this will make a copy)
- [ ] Click the **Loop Time** check box
- [ ] Click the **Apply** button

![[add-sprint-loop.webm]]

This will create a new animation clip using the `sprint` clip as a base that will loop when it reaches the end.

## Use the sprint-loop clip

- [ ] In the **Animator** window select the **Sprint** node
- [ ] Update the **Motion** to use **sprint-loop**
- [ ] Enter **Play Mode** to test that your animation is looping

![[set-sprint-animation.webm]]

# What's Next?
You have just learned how to add a pre-existing animation to your enemy, in the next section, you will practice creating your own animations.