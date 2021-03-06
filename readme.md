## Description
This solution incorporates both parts 1 and 2 from the problem set. I decided to solve the "cloning objects" exercise, as well as incorporate  interactivity with the scene.

The starter code for this project is found on Dr. Dailey's site [1], but this code has been heavily modified to support my own unique solution to the problem. I mostly just kept the original bird generation and structure and used my own logic for doing the rest.

## Instructions
Open the `index.html` file and click "Start Making Birds". You can change the y-axis rotation function as well as the rate of bird generation. You can also move around using keyboard controls. Click "Stop Making Birds" and move around the scene and check out the state of the frozen birds!

## Part 1 - Cloning
I decided to use both a timer and randomization to clone objects. I created a few helper functions:

1) A loop that clones a bird, sets a timeout, then clones another bird
2) Function to randomize color and position of the clone
3) Function to ensure the randomized position stayed within the bounds of the camera's screen. The two functions that do this were taken from the THREE js discussion boards [2].

To actually solve the cloning, after the initial bird is created, I pushed it into an array called `birds` and set up a `currentBird` variable which is initialized to 0. Then, in the cloning function, I clone `birds[currentBird]`. That way, I always clone the last bird generated. Then, I randomly generate position coordinates which are designed to stay within the bounds of the camera's FOV. I also clone the material of the bird so that I can randomly generate each component of an RGB color to set the color of the newly cloned bird. Then, I push the new bird into the array and add it to the scene.

I modified the render code to animate each bird in the array. I loop through the array, and update the birds rotation position. To make it interesting, the `z` component is incremented by `0.02` every time, but the `y` component is dynamic. Essentially, I created a function which can take the index of the bird in the array, and use that index number to generate a dynamic rotation value depending on the index. I first set this function to `(n) => 0.5 / Math.sqrt(n)`. This allows each bird to rotate differently than the others. The first one rotates quickly, but later ones rotate much more slowly.

## Part 2 - Interactivity
I added interactivity in several ways.

1) Allowed the user to define the rotation function for the `y` component of rotation.
2) Allowed the user to define the timeout between bird creations.
3) Allowed the user to navigate the scene with the camera.
4) Allowed the user to start/stop the generation of birds

I accomplished this using a `new Function()` constructor to allow user input to be transformed into executable javascript code. I also allowed the user to input a number of seconds between bird creations which then became set in the timeout function. I also implemented basic navigation using keyboard controls and then updated the camera's position. The start/stop button sets a boolean which gets checked in the timeout/generator function.

I also created a sidebar to show important information to the user. For instance, I allow the user to change things about the bird generation there, and also show the camera position at the bottom. I also put important instructions there so that the user knows how to use the site.

[1] http://srufaculty.sru.edu/david.dailey/cs456/ThreeJS1p.html

[2] https://discourse.threejs.org/t/functions-to-calculate-the-visible-width-height-at-a-given-z-depth-from-a-perspective-camera/269