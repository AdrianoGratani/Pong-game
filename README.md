# Pacman #
## My Code Analysis ##
### Adriano Gratani, 2024 ###

### Description of this Project ###

I chose to write the code to recreate this game when I started my coding journey, to learn more about JavaScript and to grasp a basic understanding of Object-Oriented Programming principles. 

The logic of Pong is quite straight forward, but still, I want to analyse it. Also, even though this game is very famous all over the world, it's worthwile spending few words about its rules. 
- Pong is a 2-D game played by two opponents, in my case on the same device.
- Each opponent controls a paddle. This paddle can be moved only up or down.
- Paddle is used to kick a ball, which moves all over the frame in any direction.
- There is no 'winning' condition: the game stops when one of the players fails to kick the ball towards the opposite direction, and the ball touches his side instead of the paddle surface.
  
### Canvas ###

I used Canvas, a special HTML element used for drawing and animations, which allows to draw graphics via JavaScript. Canvas is perfect to draw 2d games with ease.
- To use Canvas, we declare the html tag, then in the script we get the Canvas element and its context API. This Context is crucial to access the Canvas drawing methods.
- After accessing the context, we set the size of the Canvas, to make it same size as the user screen: the `window` object has `.innerWidth` and `.innerHeight` keys.
- Pixels on the screen are distributed over X and Y axis: Canvas draws and animates every item on the screen calculating the 0 for the X axis from the LEFT of the screen, and the 0 Y axis from the TOP of the screen. Remember this since it can be at first a little counter-intuitive.

### Classes ###

This simple game requires two classes, one for the paddles and the other for the ball. Later, we'll turn these Classes into 'real' object, by creating their Instances.

`Paddle` class:
Paddles are placed on left and right end of the canvas, and move only on the Y axis. One player plays the Paddle on the left, the other plays the Paddle on the right.
The class `Paddle` constructor takes one argument for the position, which is not an object since we only need to move and render each instance over the Y axis.
It has four properties: the aforementioned `position`, `velocity` to orientate the direction of the speed, `width` and `height` for paddle sizing.
Except for the `position`, every other property is set to fallback values.
only two methods are needed: `draw()` and `update()`.
`draw()` uses context API methods to fill the Canvas with chosen color, draw the Paddle shape by calling `.fillRect()` (which takes four arguments: first the instance position over the X-axis, secondd the instance position over the Y-axis, its width and height);
`update()` is called in the animation loop, so it has to call `draw()` and evaluating each paddle velocity according to their position on the screen (to achieve this we need a very simple conditional)

`Ball` class:
This element can move in any direction, and when it collides with one of the paddles should go towards the opposite direction. 
The code for this class consists of FOUR main parts: 1) the constructor, 2) a `draw()` method to draw the instance on the screen, 3) the collision-detector (a function), and lastly 3) the method to update the drawing of this instance on the animation loop. 
Let's see each of these in more detail:

  - the constructor takes two arguments, `position` for the position of the ball frame by frame (we'll update the velocity for each axis to the ball position on the update() function, later on), and `speed = 3`, for the speed of the ball, which is already set to a fallback integer of `3` since we don't need to make this value dynamic. ( Here, we want to keep things simple to understand the vary basics of programming following Object-Oriented-Programming. )
  Inside the scope of the constructor, we initialize `position`, `speed`, but also ball's `width` and `height` and its `velocity`. `velocity` it's basically a vector (an amount of both direction and magnitued), which indicates how fast and in which direction an object is moving. In my case, it's an object with two keys, `x` and `y`, which of them generates a random value based on the followin rule: if `Math.random()` generates an integer which is less than 0, `velocity` will be equal to the negative `speed`.
  - the `draw()` method: now that the constructor is set with all the properties we need for the shape and the movement of the ball, we call the Context API methods to draw the ball on our Canvas. ( VERY IMPORTANT, we only draw the ball, this is not the animation! )
    "Drawing" means assigning color and shape to an element. We use `context.fillStyle()` to set the color to a fallback value of `white`, 
