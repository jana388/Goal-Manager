# Goal-Manager

In this tutorial I will teach you how to make a goal for your game which detects a ball and increases the score. This is suitable for 3D games.
## Prerequisites 

For this tutorial you will need to have Unity 2022.3.46f installed as well as the Microsoft Editor 2022.
It is a bit more advanced tutorial so I suggest not following it if not previously using Unity.
You should know how to navigate through Unity, and know how to make a movement script for the ball and the player. It would also be ideal if you knew how to make a UI for the left and right score.

Having done this, you should be ready for setting up the goals

![Capture](https://github.com/user-attachments/assets/f272a9cb-fce0-42a7-accb-7085f6a3aec0)

This is what my scene looks like right now.
I have set the players as cubes on both edges of the platform and placed the ball in the middle. I also placed two other cubes to block the ball from leaving the platform. However, the goals would be empty where the ball can leave the platforms.

![Capture2](https://github.com/user-attachments/assets/1cfb62e8-1e33-4d42-ad2c-89d9878b12c4)

I have set two box colliders on the opposite edges of the platform so they will later be able to indicate a score.
I named the *GoalRight* and *GoalLeft*, but it is totally up to you how you will name the goals

Make sure the **Box Colliders** are long, so they cover the whole edge of the platform.
Now that we have set the colliders, it is time to add our first script

# Empty Object

We will make a **C# script** in the Project and name it *GameController*
Then 
We will add an empty object in the Hierarchy and name it Game Controller

This game object will exist in the scene, but will not interact with any object in the game.

we need a component that will be able to track the score

We can even add a colour to it in the Inspector like this 

![Screenshot (385)](https://github.com/user-attachments/assets/44182145-f4d8-41b8-ab99-9c88be0d8f5e)

Then we put our script on the Empty object by clicking and dragging

and we are ready to code.

# Coding the Game Controller

Open the Game Controller in Mictrosoft Editor
Since I am using the Text Mesh pro for my Ui, I am using the ... for it because without it the code could not be classified.
Other than that, we are only using Unitys ...
![Capture3](https://github.com/user-attachments/assets/2c920588-8fec-4b52-886a-e33936a80b89)

For this script I will not be using Start and Update void, because we will only need separate voids that will only be updated when the goal is triggered.
But before that, I will add two variables for the Ui

![Capture4](https://github.com/user-attachments/assets/aae7c94a-de41-44c9-a7cf-3c90e339b70b)

Later on I will add two variables for the scores

![Capture5](https://github.com/user-attachments/assets/372f0819-b36d-4cee-bbf5-62668f014283)

I made two for each score. Both intergers will be private. They will both start at 0. 
> Interger is a number used in Unity that can only be changed in the script
> We will keep it private so it is a fixed number, and no other code can alter its state

Now we need to provide a communication between the Goal and the Game Controller

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

# Goal Event













