# Pacman #
## Code analysis ##


I wrote the code to recreate this game, following Object-Oriented Programming principles. 
The logic is quite straight forward, but still, I think is good to analyse how it works.

I used Canvas, a special HTML element which allows to draw graphics via JavaScript. Canvas is perfect to draw 2d games with ease.
To use Canvas, we declare the html tag, then in the script we get the Canvas element and its context API.
The context is crucial to use Canvas drawing methods.
After accessing the context, we set the size of the Canvas, to make it same size of the user screen: the `window` object has `.innerWidth` and `.innerHeight` keys.

### Classes ###

This simple game requires two classes, one for the paddles and the other for the ball.
Paddles are placed on left and right end of the canvas, and move only on the Y axis. One player plays the Paddle on the left, the other plays the Paddle on the right.
The class `Paddle` constructor takes one argument for the position, which is not an object since we only need to move and render each instance over the Y axis.
It has four properties: `position`, `velocity` to orientate the direction of the speed, `width` and `height` of the paddle.
