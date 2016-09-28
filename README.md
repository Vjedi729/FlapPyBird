# Lecture 4: PyGame / Flappy Bird Clone

## How to Run the Code

1. Install Python 2.7.X from [here](https://www.python.org/download/releases/)
2. Install PyGame 1.9.X from [here](http://www.pygame.org/download.shtml)
3. Clone this repository: `git clone https://github.com/cucumbur/FlapPyBird.git` or click `Download ZIP` in right panel and extract it.
4. Run `python flappy.py` from the repo's directory
5. use <kbd>&uarr;</kbd> or <kbd>Space</kbd> key to play and <kbd>Esc</kbd> to close the game.

  (Note: Install pyGame for same version python as above)

  (For x64 windows, get exe [here](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pygame))

## Terminology
- Sprite

## Code Disection
~~~python
def mainGame(movementInfo):
~~~
 the function that contains the main game stuff (of course)
 
 ~~~python
 score = playerIndex = loopIter = 0
 ~~~
 initializing several values to 0. score is obvious. playerIndex is the index of the sprite we use - i.e. are its wings up or down. loopiter keeps track of how many frames have passed so we know how often to make the sprite go to the next stage (flap its wings)
 
 ~~~python
  playerx, playery = int(SCREENWIDTH * 0.2), movementInfo['playery']
 ~~~
 this sets the players horizontal value to the center of the screen, and the vertical value is the default vertical value returned by the welcome function
 
 ~~~python
 def getRandomPipe():
    """returns a randomly generated pipe"""
    # y of gap between upper and lower pipe
    gapY = random.randrange(0, int(BASEY * 0.6 - PIPEGAPSIZE))
    gapY += int(BASEY * 0.2)
    pipeHeight = IMAGES['pipe'][0].get_height()
    pipeX = SCREENWIDTH + 10

    return [
        {'x': pipeX, 'y': gapY - pipeHeight},  # upper pipe
        {'x': pipeX, 'y': gapY + PIPEGAPSIZE}, # lower pipe
    ]
 ~~~
BaseY is the top of the "base", where the ground would normally be. this function calculates a random height within a range with the PIPEGAPSIZE as the size of a gap, and returns those as 2 pairs of coordinates: one for the upper pipe and one for its corresponding lower pipe
 
 ~~~python
     # get 2 new pipes to add to upperPipes lowerPipes list
    newPipe1 = getRandomPipe()
    newPipe2 = getRandomPipe()

    # list of upper pipes
    upperPipes = [
        {'x': SCREENWIDTH + 200, 'y': newPipe1[0]['y']},
        {'x': SCREENWIDTH + 200 + (SCREENWIDTH / 2), 'y': newPipe2[0]['y']},
    ]

    # list of lowerpipe
    lowerPipes = [
        {'x': SCREENWIDTH + 200, 'y': newPipe1[1]['y']},
        {'x': SCREENWIDTH + 200 + (SCREENWIDTH / 2), 'y': newPipe2[1]['y']},
    ]
 ~~~
 Starts off by adding two sets of pipes, with half a screenwidth between them.
 
 ~~~python
 while True:
 ~~~
 This is where the main game loop is
 
 ~~~python
 ~~~