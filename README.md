# GD50-angry-birds
*Angry Birds*


Lecture Slides: [Lecture 6](https://github.com/jazorhe/GD50-angry-birds/blob/main/lecture6.pdf)

<img src="img/title.png" width="700">


### Overview
-   [Our Goal](#our-goal)
-   [Lecture Notes](#lecture-notes)
-   [Assignment](#assignment)
-   [Submission](#submission)
-   [Useful Links](#useful-links)


<br>

## Our Goal

<img src="img/our-goal.png" width="700">


## Lecture Notes
**Topics**:
-   [Box2d](#box2d)
-   [Mouse Input](#mouse-input)


**Related Links**:
-   <https://love2d.org/wiki/love.physics>
-   <https://love2d.org/wiki/Tutorial:Physics>
-   <http://www.iforce2d.net/b2dtut/introduction>


### Box2d
####The World:
-   Performs all physics calculations on all "Bodies" it holds a reference to.
-   Possesses a gravity value that affects every Body in the scene in addition to each Body's own characterstics.
-   `love.physics.newWorld(gravX, gravY, [sleep])`: Creates a new World object to simulate physics, as provided by BoxeD, with gravX and gravY for global gravity and an optional sleep parameter to allow non-moving Bodies in our world to sleep (to not have their physics calculated when they're completely still, for performance gains)


####Bodies:
-   Abstract containers that manage position and velocity
-   Can be manipulated via forces (or just raw positional assignment) to bring about physical behaviour when updated by the `world`
-   `love.physics.newBody(world, x, y, type)`: Creates a new Body in our `world` at x and y, with type being what kind of physical body it it ('static', 'dynamic' or 'kinematic', which we will explore)


####Fixtures:
-   The individual components of Bodies that possess physical characteristics to influence Bodies' movements.
-   Attach shapes to Bodies, influencing collision.
-   Have densities, frictional characteristics, restitution (bounciness), and more
-   `love.physics.newCircleShape(radius)`
-   `love.physics.newRectangleShape(width, height)`
-   `love.physics.newEdgeShape(x, y, width, height)`
-   `love.physics.newChainShape(loop, x1, y1, x2...)`
-   `love.physics.newPolygonShape(x1, y1, x2, y2...)`
-   `love.physics.newFixture(body, shape)`: Creates a new Fixture for a given body, attaching the shape to it relative to the center, influencing it for the `world`'s collision detection.


#### Implementation:
-   Definition:

    ```lua
    -- new Box2D "world" which will run all of our physics calculations
    world = love.physics.newWorld(0, 300)

    -- body that stores velocity and position and all fixtures
    boxBody = love.physics.newBody(world, VIRTUAL_WIDTH / 2, VIRTUAL_HEIGHT / 2, 'static')

    -- shape that we will attach using a fixture to our body for collision detection
    boxShape = love.physics.newRectangleShape(10, 10)

    -- fixture that attaches a shape to our body
    boxFixture = love.physics.newFixture(boxBody, boxShape)
    ```

-   Rendering:

    ```lua
    -- draw a polygon shape by getting the world points for our body, using the box shape's
    -- definition as a reference
    love.graphics.polygon('fill', boxBody:getWorldPoints(boxShape:getPoints()))
    ```


### Mouse Input
-   `love.mousepressed(x, y, key)`: Callback that executes whenever the user clicks a mouse button; has access to the X and Y of th emouse press, as well as the particular "key" (or mouse button).
-   `love.mousereleased(x, y, key)`: The opposite of `love.mousepressed`, which is fired whenever we release a mouse key in our scene; also takes in the coordinates of the release and the key that was released.
-   Similar Implementation with the keyboard with a `wasPresed` table to store all pressed and released keys (however, my implementation with the match 3 game is also valid)

### Other Notes
#### Collision Callback
-   <https://love2d.org/wiki/Tutorial:PhysicsCollisionCallbacks>


-   Destroying Bodies
-   Multiple fixtures in a body
-   Remove from a table in reverse index order
-   Keep Data Driven Design in mind
-   Potential Expanded Features:
    -   More shapes (arbitrary thanks to polygons)
    -   Compound obstacles (see pulley, motor, and weld joints, plus more)
    -   Levels defined as tables
    -   Birds (aliens) with different shooting mechanics, like explosions
    -   Different obstacle materials with varying densities


<br>

## Assignment
### Objectives
-   [ ] [**Code Reading**](#code-reading)Read and understand all of the Legend of Zelda source code from Lecture 5.
    -   [ ] [`main.lua`](#mainlua)
    -   [ ] [`Dependencies.lua`, `constants.lua` and `Util.lua`](#dependenciesluaconstantslua-and-utillua)
    -   [ ] [`Background.lua`](#backgroundlua)
    -   [ ] [`Alien.lua`, `AlienLaunchMarker.lua` and `Obstacle.lua`](#alienlua-alienlaunchmakerlua-and-obstaclelua)
    -   [ ] [`StateMachine and States`](#statemachine-and-states)


-   [ ] [**Triple Aliens**](#task): Implement it such that when the player presses the space bar after they’ve launched an `Alien` (and it hasn’t hit anything yet), split the `Alien` into three Aliens that all behave just like the base `Alien`.


<br>

### Code Reading
#### `main.lua`
#### `Dependencies.lua`, `constants.lua` and `Util.lua`
#### `Background.lua`
#### `Alien.lua`, `AlienLaunchMarker.lua` and `Obstacle.lua`
#### `StateMachine and States`

### Triple Aliens
*Implement it such that when the player presses the space bar after they’ve launched an `Alien` (and it hasn’t hit anything yet), split the `Alien` into three `Alien`s that all behave just like the base `Alien`. The code for actually launching the `Alien` exists in `AlienLaunchMarker`, and we could naively implement most, if not all, of this code in the same class, since the `Alien` in question we want to split off is a field of this class. However, because we want to only allow splitting before we’ve hit anything, we need a flag that will get triggered whenever this `Alien` collides with anything else, so we’ll likely want the logic for this in the `Level` itself here, since that is where we pass in the collision callbacks via `World:setCallbacks()`. The center `Alien` doesn’t really need to be modified for the splitting process; really, all we need to do is spawn two new `Alien`s at the right angle and velocity so that it appears we’ve turned the single `Alien` into three, one above and one below. For this, you’ll need to take linear velocity into consideration. Additionally, be aware that the `Alien` we want to launch has the `userData` of the string “Player”, as opposed to the `Alien` we want to kill, which has just the `userData` of “`Alien`”. Lastly, be sure that the launch marker doesn’t reset until all of the `Alien`s we fling have slowed to nearly being still, not just the one `Alien` we normally check. In all, you should have all of the pieces at this point you need in order to make this happen; best of luck!*

**The update needs to do the following**:
**How I achieved**:
**Challenge myself**:


## Submission


## Useful Links
-   Framework: [LÖVE2d](https://love2d.org/wiki/love)
-   Graphical Module: [Push Module for Lua](https://github.com/Ulydev/push)
-   Timer Module: [Lua Knife](https://github.com/airstruck/knife)
-   Physics Module: [Box2d](https://box2d.org/)
-   Fonts: [Dafont.com](https://www.dafont.com/)
-   Freely Available Game Assets: [Open Game Art](https://opengameart.org/)
-   Sound Effects: [Bfxr Sound Effect Generator](https://www.bfxr.net/)
-   Markdown Guides:
    -   [Embed youtube to markdown, GitLab, GitHub](http://embedyoutube.org/)
    -   [GitHub: Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
    -   [Markdown Emoji Cheatsheet](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md)
