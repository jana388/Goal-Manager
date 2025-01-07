# Goal-Manager

In this tutorial I will teach you how to make a goal for your game which detects a ball and increases the score. This is suitable for 3D games.

## Prerequisites 

For this tutorial you will need to have **Unity** *(2022.3.46f preferably)* installed as well as the **Microsoft Visual Studio 2022**

This tutorial is a bit more advanced and it is required to be familiar with the basics of Unity and how it works.
I am setting this as a prerequisite since I have already prepared a 3D scene.
In my scene I have set up :
- A platform
- Two players
- Two walls
- Two goals on both sides of the platform



You should have a script for :
- `Player Movement`
- `Ai Movement`
- `Ball Controller`

  ![Screenshot (386)](https://github.com/user-attachments/assets/cf026ac7-6cea-4955-ae94-fc5c8cb3655c)
  > This is what the scene should look like



To actually track a score and have something to connect the Goal Manager with, we need a UI for the **left and right score**

I would also like to set the camera behind one of the players

This is what the scene should look like in the **Game Mode**

![Capture](https://github.com/user-attachments/assets/f272a9cb-fce0-42a7-accb-7085f6a3aec0)

I have set two box colliders on the opposite edges of the platform so they will later be able to indicate a score.
I named the *GoalRight* and *GoalLeft*, but it is totally up to you how you will name the goals

![Capture2](https://github.com/user-attachments/assets/1cfb62e8-1e33-4d42-ad2c-89d9878b12c4)


Make sure the **Box Colliders** are long, so they cover the whole edge of the platform.
Now that we have set the colliders, it is time to add our first script


# Empty Object

We will make a **C# script** in the Project and name it `GameController`

Then we will add an empty object in the Hierarchy and name it also *Game Controller*

This game object will exist in the scene, but will not interact with any object in the game.

We need a component that will be able to track the score
> Why do we need game controllers in a game?
>
> If the game is more complex and we want the game to manage a state, for example, restarting the game
>
> It will also help us handle game events which we will make in the future
>
> Since we want our game to keep track of the score and update the UI when scoring a goal, a game manager is perfect for this case

We can even add a colour to the *Game Manager* in the Inspector like this 

![Screenshot (385)](https://github.com/user-attachments/assets/44182145-f4d8-41b8-ab99-9c88be0d8f5e)

Then we put our script on the Empty object by clicking and dragging the script to the Game Controller object in the Inspector

Open the C# script and we are ready to go

# Coding the Game Controller

Open the Game Controller in Microsoft Visual Studio

Since I am using the *Text Mesh Pro* for my UI, I will have to add `using TMPro` as one of my directives because without it the code for UI could not be classified

Other than that, we are only keeping the `using UnityEngine` directive
![Capture3](https://github.com/user-attachments/assets/2c920588-8fec-4b52-886a-e33936a80b89)

For this script I will not be using `Start` and `Update void`, we will need separate voids that will only be updated when the goal is **triggered**.

Above the `Start void`, I will add two variables for the UI

![Capture4](https://github.com/user-attachments/assets/aae7c94a-de41-44c9-a7cf-3c90e339b70b)

Later on I will add two variables for the scores

![Capture5](https://github.com/user-attachments/assets/372f0819-b36d-4cee-bbf5-62668f014283)

I made two for each score. Both intergers will be private. They will both start at 0. 

> Interger is a number used in Unity that can only be changed in the script
> 
> We will keep it private so it is a fixed number, and no other code can alter its state

Now we need to provide a communication between the Game Controller and Goal Controller *(which I will mention later on)*

![Capture6](https://github.com/user-attachments/assets/8ca7265e-c3b5-42bb-8ce5-d15ad9e2b78d)


> When left goal scores, we want the Goal Controller to inform the Game Controller *ScoreGoalLeft* and the right goal controller to inform the Game Controller *ScoreGoalRight*

Inside each function, we want the score to go up by one

We will do the same for the right one

![Capture7](https://github.com/user-attachments/assets/425ddd6f-b8f4-4e9a-b490-330131ece6a6)

> Only thing we need to watch out for is that when one goal scores (the ball triggers one goal), the other one's score goes up!

Next thing is that we actually want to update the UI when the goal is triggered

![Capture8](https://github.com/user-attachments/assets/c40a999f-3322-407e-971c-1d3236e99e83)


So we figured the score, but if we go back to Unity and start to play the game, we will realise that the ball keeps on moving after one scores the goal. 
What we need to do is reset the ball to its initial position after scoring a goal

That is why we will add a private void which will spawn the ball back to its position after reaching one of the goals

Only thing left to do is to go back to these scripts and add the Invoke for the ball

![Capture10](https://github.com/user-attachments/assets/de9750a8-9949-492e-966a-0241cf61d16d)

> Invoke is a function used to invoke an action with a given delay
> That is why we have to choose a time when we want the ball to be spawned back to the game

# Goal Controller and Events

We will make another script in the Project and name it Goal Controller

> Why are we making another script that is also focusing on the goal and not using Game Controller?
> We are making another script because we want to divide these scripts because Game controller operates on the connections between the UI and the goals, while the Goal controller will be in charge of the events
> Events in Unity help us organise the operations Unity makes and connect different scripts:
> - For instance, in our case, we want the link  the ball with the goal
> - When the ball touches the Box Collider (Goal), we want it to disappear from the game and make it restart the game
> - It is easier to update certain elements in a game

Since we are going to use Events in Unity, we need to classify it

![Capture11](https://github.com/user-attachments/assets/d5076c1c-db44-439c-a5b0-92cacdcc347a)

Other that UnityEvents, we will use Unity...

Now we will add a public variable that will add a Trigger to the goal

![Capture12](https://github.com/user-attachments/assets/10357c92-726a-465a-a75e-29b3531627a0)

We can delete Start and Update void in this script as well, since again, we do not need this code to be updated in every frame, but only when it is triggered by the ball

Instead, we will make a private void that will do this

![Capture13](https://github.com/user-attachments/assets/33eb7d1f-8522-4983-94fd-ad3355d1cede)

This event will link our script to the Ball using the script
This means that when the ball touches the Box Collider, it will be destroyed

