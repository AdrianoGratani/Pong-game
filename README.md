Pacman
My Code Analysis
Adriano Gratani, 2024
Description of this Project
I chose to write the code to recreate this game when I started my coding journey, to learn more about JavaScript and to grasp a basic understanding of Object-Oriented Programming principles.

The logic of Pong is quite straightforward, but still, I want to analyze it. Also, even though this game is very famous all over the world, it's worthwhile to spend a few words about its rules.

Pong is a 2-D game played by two opponents, in my case on the same device.
Each opponent controls a paddle. This paddle can be moved only up or down.
The paddle is used to hit a ball, which moves all over the frame in any direction.
There is no 'winning' condition: the game stops when one of the players fails to hit the ball toward the opposite direction, and the ball touches their side instead of the paddle surface.
Canvas
I used Canvas, a special HTML element used for drawing and animations, which allows drawing graphics via JavaScript. Canvas is perfect for drawing 2D games with ease.

To use Canvas, we declare the HTML tag, then in the script, we get the Canvas element and its context API. This Context is crucial to access the Canvas drawing methods.
After accessing the context, we set the size of the Canvas to make it the same size as the user's screen: the window object has .innerWidth and .innerHeight keys.
Pixels on the screen are distributed over the X and Y axes: Canvas draws and animates every item on the screen by calculating the 0 for the X axis from the LEFT of the screen, and the 0 for the Y axis from the TOP of the screen. Remember this, since it can be a little counterintuitive at first.
Classes
This simple game requires two classes, one for the paddles and the other for the ball. Later, we'll turn these Classes into 'real' objects by creating their Instances.

Paddle class: Paddles are placed on the left and right ends of the canvas and move only on the Y axis. One player plays the paddle on the left, the other plays the paddle on the right. The class Paddle constructor takes one argument for the position, which is not an object since we only need to move and render each instance on the Y axis. It has four properties: the aforementioned position, velocity to orient the direction of the speed, width, and height for paddle sizing. Except for the position, every other property is set to fallback values. Only two methods are needed: draw() and update(). draw() uses context API methods to fill the Canvas with the chosen color, drawing the paddle shape by calling .fillRect() (which takes four arguments: first the instance position on the X-axis, second the instance position on the Y-axis, its width, and height). update() is called in the animation loop, so it has to call draw() and evaluate each paddle's velocity according to its position on the screen (to achieve this, we need a very simple conditional).

Ball class: This element can move in any direction, and when it collides with one of the paddles, it should go toward the opposite direction. The code for this class consists of FOUR main parts: 1) the constructor, 2) a draw() method to draw the instance on the screen, 3) the collision detector (a function), and lastly 4) the method to update the drawing of this instance in the animation loop. Let's see each of these in more detail:

The constructor takes two arguments, position for the position of the ball frame by frame (we'll update the velocity for each axis to the ball position in the update() function later on), and speed = 3, for the speed of the ball, which is already set to a fallback value of 3 since we don't need to make this value dynamic. (Here, we want to keep things simple to understand the very basics of programming by following Object-Oriented Programming.) Inside the scope of the constructor, we initialize position, speed, but also the ball's width, height, and its velocity. Velocity is basically a vector (an amount of both direction and magnitude), which indicates how fast and in which direction an object is moving. In my case, it's an object with two keys, x and y, each of which generates a random value based on the following rule: if Math.random() generates an integer that is less than 0, velocity will be equal to the negative speed.
The draw() method: now that the constructor is set with all the properties we need for the shape and movement of the ball, we call the Context API methods to draw the ball on our Canvas. (VERY IMPORTANT, we only draw the ball; this is not the animation!) "Drawing" means assigning color and shape to an element. We use context.fillStyle() to set the color to a fallback value of white, and context.fillRect() to draw the shape using the properties taken from the Constructor: this.position on both axes, width, and height.
ballCollisionLogic(): the core of the game, where things get really interesting. This function sets:
Three objects to store the location of any type of boundary and
What happens when the ball collides against paddles or the boundaries of the screen.
The losing conditionals. Let's see each of them. 1)
One object for the boundaries of the ball (ballSide).
One object for the boundaries of the canvas (canvasBoundaries).
The last object for the boundaries of each paddle (paddle). (Canvas measures in pixels, from LEFT (0) to RIGHT (canvas size) for the X-axis, and from TOP to BOTTOM for the Y-axis. If we add (depending on which side) width and height to the position of each instance, we get their boundaries.)
Having set these three objects, we have all the data to control the logic of the game: preventing the ball from overflowing outside the Canvas, and making it bounce against the boundary of each paddle.
Using IF statements, we control the behavior of the ball:
If the velocity on the X axis is greater than 0 (which means the ball is moving toward the right side of the screen), we access another IF statement to verify the location of the ball by accessing the three objects previously declared inside the IF condition statement. If the coordinates of the right boundary of the ball are greater than the left boundary of the right paddle, and the bottom coordinates of the ball are not lower than the top of the right paddle, it means that A COLLISION JUST HAPPENED. If this is true, set the velocity on the X-axis to its opposite.
Basically, the same logic is applied if the ball collides with the left paddle or with the top or bottom of the Canvas.
If the ball's left-boundary coordinates are lower than the left-side boundary of the Canvas, it means that the left paddle missed the ball, failing to prevent the ball from touching its side. The player loses the game, and the game immediately stops by breaking from the animation loop.
The same logic is applied if the right paddle loses the game.
Instances
We set the Canvas, the Class for the Paddle and for the Ball, methods to draw each class, and the logic to detect collisions. Now it's time to create the instances of the classes in order to make our game real.

We initialize three variables, one for each paddle and one for the ball, assigning position properties for both X and Y axes as arguments for the constructor.
The Animation Loop
Having created each instance, we can render all the elements of the game on our Canvas.

We use requestAnimationFrame() from the DOM window object to generate an infinite loop: for every frame, we call the .update() method of each instance. Their shapes will get re-rendered and every new frame will clear the previous one.
Lastly, the losing condition should stop the loop using a return statement.
Event Listeners
Each user has two keys, one to move the paddle up and the other to move it down.

We need to add an EventListener to the window object.
We want to monitor four keys, so we use a switch statement that takes the event.key as an argument (= the key pressed that triggered the event listener, now we can access this object in this switch). Based on each case, we set a different behavior: i.e. if the user presses 'w', the eventListener keydown is triggered, which triggers a callback function to the switch statement. If the event.key value equals the one of the w case, the speed of the left paddle will be negative = the paddle will move upwards.
The same logic is applied for all other cases.




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
    "Drawing" means assigning color and shape to an element. We use `context.fillStyle()` to set the color to a fallback value of `white`, and `context.fillRect()` to draw the shape using the properties taken from the Constructor: `this.position` on both axis, `width` and `height`.
  - `ballCollisionLogic()`: the core of the game, here things get really interesting. this function sets:
  - 1) three objects to store the location of any type of boundary and
  - 2) what happens when ball collides against paddles or the boundaries of the screen:
  - 3) losing conditionals.
  Let's see each of them.
       1) 
      - one object for the boundaries of the ball (`ballSide`);
      - one object for the boundaries of the canvas (`canvaBoundaries`);
      - last object for the boundaries of each paddle (`paddle`);
    ( Canvas measures in pixel, from LEFT (0) to RIGHT (canvas size) for the x-axis, and from TOP to BOTTOM for the y-axis. If we add (depending on which side) width and height  to the position of each instance, we get their boundaries. )
      - Having set these three objects, we have all the data to control the logic of the game: preventing the ball to overflow outside the Canvas, and to make it bounce against the boundary of each paddle.
       2)
      - using IF statements we control the behaviour of the Ball:
          - if the velocity on the x axis is greater than 0 (which means: Ball is moving towards right side of the screen), we access another IF statement to verify the location of the ball accessing the three object previously declared, inside the if condition statement. If the cohordinates of the right boundaries of the ball are greater than the left boundaries of the right paddle, and the bottom cohordinates of the ball are not lower than top of the right paddle, it means that A COLLISION JUST HAPPENED.
            If this is true, set the velocity on the x-axis to its opposite.
          - Basically, the same logic is applied in case the ball collides with the left paddle, or with the top or bottom of the Canvas.
       3) 
          - if the ball left-boundary cohordinates are lower than the left-side boundary of the Canvas, means that the left paddle missed the ball, failing to prevent the ball from touching its side. The player loses the game, and the game immediately stops by breaking from the animation loop.
          - same logic is applied in case the right paddle loses the game.

### Instances ###
  We set the Canvas, the Class for the Paddle and for the Ball, methods to draw each class and the logic to detect collision. Now it's time to create the instances of the classes in order to make our game real.
  - we initialize three variables, one for each paddle and one for the ball, assigning `position` properties for both x and y axis, as arguments for the constructor.

### The Animation Loop ###
  Having created each instance, we can render all the elemnts of the game on our Canvas.
  - we use the `requestAnimationFrame()` from the DOM `window` object, to generate an infinite loop: for every frame we call `.update()` method of each instance. Their shapes will get rerendered and every new frame will clear the previous one.
  - Lastly, the losing condition should stop the loop using a `return` statement.

### Event Listeners ###

  Each user has two keys, one for move the paddle up, the other to move down.
  -  We need to add an EventListener to the `window` object. 
      - we want to monitor four keys, so we use a `switch` statements which takes the `event.key` as argument ( = the key pressed triggered the event listener, now we can access this object in this switch). Based on each case, we set a different behaviour: i.e. if the user presses 'w', the eventLIstener `keydown` is triggered which  triggers a callback function to the switch statement. If the `event.key` value equals the one of the `w` case, the speed of the left paddle will be negative = the paddle will move upwards.
      - same logic is applied for all other cases.
