# Pacman #
## Code analysis ##

This game is famous all over the world, but I think it's worthwile to spend few words about the rules and the goals to 'win' the game.
- Pong is a game played by two opponents, in my case on the same device.
- Each opponent controls a paddle. This paddle can be moved only up or down.
- Paddle is used to kick a ball
- 

  
I wrote the code to recreate this game, following Object-Oriented Programming principles. 
The logic is quite straight forward, but still, I think is good to analyse how it works.

### Canvas ###

I used Canvas, a special HTML element which allows to draw graphics via JavaScript. Canvas is perfect to draw 2d games with ease.
- To use Canvas, we declare the html tag, then in the script we get the Canvas element and its context API.
- The context is crucial to use Canvas drawing methods.
- After accessing the context, we set the size of the Canvas, to make it same size of the user screen: the `window` object has `.innerWidth` and `.innerHeight` keys.
- Pixels on the screen are distributed over X and Y axis: Canvas draws and animates every item on the screen calculating the 0 for the X axis from the LEFT of the screen, and the 0 Y axis from the TOP of the screen. Remember this since it can be at first a little counter-intuitive.

### Classes ###

This simple game requires two classes, one for the paddles and the other for the ball.

`Paddle` class:
Paddles are placed on left and right end of the canvas, and move only on the Y axis. One player plays the Paddle on the left, the other plays the Paddle on the right.
The class `Paddle` constructor takes one argument for the position, which is not an object since we only need to move and render each instance over the Y axis.
It has four properties: the aforementioned `position`, `velocity` to orientate the direction of the speed, `width` and `height` for paddle sizing.
Except for the `position`, every other property is set to fallback values.
only two methods are needed: `draw()` and `update()`.
`draw()` uses context API methods to fill the Canvas with chosen color, draw the Paddle shape by calling `.fillRect()` (which takes four arguments: first the instance position over the X-axis, secondd the instance position over the Y-axis, its width and height);
`update()` is called in the animation loop, so it has to call `draw()` and evaluating each paddle velocity according to their position on the screen (to achieve this we need a very simple conditional)
