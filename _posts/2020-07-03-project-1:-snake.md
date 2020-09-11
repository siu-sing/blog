---
layout: post
title: "Classic Snake with JavaScript, HTML and CSS"
excerpt_separator:  <!--more-->
categories: 
    - Projects
---

The first project of SEI-23 involves us putting what we've learnt in the first 3 weeks of the course to use in a simple game.

Personally, I definitely lean towards programming work that requires more algorithmic thinking, breaking down bigger problems into logical chunks and building the solutions back up to create "magic".

Shortlisted a few games: Snake, Tetris, Solitaire, Minesweeper, GuitarHero(ish), Flappybird

I would imagine Snake, Tetris and Minesweeper would require some kind of intense math behind the scenes so they were pretty attractive as project 1. Ultimately for nostalgia, I decided on Snake since I used to play that a lot on my first Nokia 3310, and I would actually want to play it now.

- Game: [Snake](https://siu-sing.github.io/snake/)
- Code: [GitHub Snake Repo](https://github.com/siu-sing/snake)

## The Plan
So originally the idea was to just rebuild the classic snake game on html/css/js. But due to some unforeseen drama in my class, we had an additional week (total 2) to work on the project (the original timeline was < 1 week). 

After completing the basic snake in the first week and consulting with the TAs, I decided I had time to embark on a second version - Battle Snakes.

Turns out there are a number of multiplayer snake games out there (check out [slither.io](http://slither.io/)). I decided to add multiplayer snakes to the game, but instead of human players I attempted to build an AI Snake.

## Implementation

Full implementation details are well documented on the [ReadMe](https://github.com/siu-sing/snake) page in the Snake repo. I will be picking out some key parts to share here.

![Classic]({{site.baseurl}}/assets/classic.gif "Classic")
*Classic Snake*

In summary, for Classic Snake
 - Game screen is an N by N grid and refreshes itself every 100ms
 - At each refresh, conditions for snake death/growth are checked before being "re-drawn" on the screen in its new position
 - Player snake's direction can be updated dynamically by arrow keys

![Battle]({{site.baseurl}}/assets/battle.gif "Battle")
*Battle Snake*

 For Battle Snakes, in addition to above
- AI Snake's behaviour is similar to the default snake
- AI Snake's direction is automatically determined by the program and its always directed towards its fruit/target
- AI Snake respawns 4s after death
- Program also additionally checks for collision between Snakes

Fruits and Snakes were implemented as classes, with `AISnake` extending the `Snake` class with additional methods for auto navigation.

By far the most challenging part of this project was to implement the `autoMove()` method, which determines the best `direction` to set for the AI snake given the current state of the board.

The original intent was to allow the AI snake to make random turns on the board, which would be trivial to implement by updating the `direction` with a random (and valid) value for each refresh interval. 

However, upon further consideration, random turns could result in very erratic movements, which will need to be handled by "smoothing" the randomness of the suggested direction. Other edge cases will also need to be considered - e.g. How to get the snake out of the corner of the game board? How to avoid collision with itself?

In order to solve this in a more generic way, I started to think about how to replicate the AI snake to mimic human player behaviour i.e. make turns that will direct it towards a predetermined destination (fruit). The fruit itself would reappear at random locations, which caters for the randomness that we want. 

We will need to consider the relative position of the fruit with respect to the snake head position (and direction) at every refresh interval, and decide if a change in direction is required, and if so, which direction to give.

### AI Snake of 1 unit length

To start, we consider an AI Snake with length of 1 unit (i.e. a single unit moving on the board), heading **east** with the fruit at **North-East** of its current position. 

At some point when the snake is in _vertical_ alignment with the fruit we will need to give it a new direction `n` and leave it to head towards the fruit successfully. 

Consider the same situation except the snake is moving north, and at some point when the snake is in _horizontal_ alignment with the fruit, we will need to give it a new direction `e`.

Finally, if the snake is facing away (`s` or `w`) from the fruit, we'll need to set a direction (`e` or `n`) respectively to reorient the snake towards the target.

The psuedo code to cater for above will look like this:
```
//Psuedocode to handle first condition
At ever refresh interval,
IF fruit is N-E with respect to snake
    IF snake is moving E
        IF snake is vertically aligned with fruit
            SET direction to N
        ELSE continue travelling E
    ELSEIF snake is travelling N
        IF snake is horizontally aligned with fruit
            SET direction to E
        ELSE continue travelling N
    ELSEIF snake is travelling S
        SET direction to E
    ELSEIF snake is travelling W
        SET direction to N
```
Given the basic 2-dimensional game board we will only need to replicate this logic symmetrically 4 ways - fruit relative positions at NE, NW, SE and SW. Code snippet [here](https://github.com/siu-sing/snake/blob/18f58e965f7775392d359dc69cfe199346dd1cad/script.js#L362-L434).

This also solves the problem of getting the snake to escape from the edges of the game board because fruits are only generated within the playable area - i.e. AI snake will only be directed within the game board.

### AI Snake of more than 1 unit length

However, as the AI snake grows in length, and given the randomness of fruit respawn, snake would inadvertently run into itself. 

We would need an additional check if we know that the snake is about to run into itself. But which direction should we give the snake it its about to run into itself. 

In the most basic case, we would want to prevent the snake from entering a death trap (i.e. turning towards an area enclosed by its own body without a way to escape). For this, we will need to turn the snake in the opposite direction of the segment of the body it will be heading towards.

The following psuedo code handles this:
```
//Psuedocode to avoid self collision
IF the suggestedDirection will result with self collision
    IF snake is moving E
        IF segment of snake to be collided with has direction S
            SET direction N //to prevent death traps
        ELSE IF ... //vice versa

```
Again, this would be replicated symmetrically in 4 directions. Code snippet [here](https://github.com/siu-sing/snake/blob/18f58e965f7775392d359dc69cfe199346dd1cad/script.js#L437-L476).

The resulting movement would look something like this:

<img src="{{site.baseurl}}/assets/autoMove.gif" width="350"> 
*autoMove() function*

### Other non-trivial functions (WIP)
- Generating random fruit
- Touch display

## Future Work (?)
- Improve AI Snake capabilities
    - More defensive and able to avoid player snake
    - More offensive and able to trap player snake
    - Multiple AI snakes simultaneously
    - Random respawn location
- Dynamic resizing of game area during game play
- Use swipes instead of touches for mobile/touch screen support. Some friends mentioned that their thumbs were in the way of the screen.
- More exciting animation on deaths, kills

## Post Mortem / Lessons Learnt
- Diving into developing the backend algorithms are great fun but without considering front-end interactions/displays at the same time, it will be hard to showcase the full result of your work
- Work in sprints and carefully choose features to develop in each sprint that will create a minimally functioning product at the end of each sprint. This will ensure all parts of the program (both front and back end) would be kept in line.
- Use git branching judiciously. As I moved along my "sprint" cycles, I was hopping from different parts of the program from DOM manipulation, to AI snake logic, to CSS/HTML. There were times where I had to undo/revert/checkpoint since my edits resulted in other functioning parts breaking. Especially when closer to the project deadline, I had to make sure I was working on a branch other than master.