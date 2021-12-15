# Othello
Othello Board Game
This game is Othello, also known as Reversi. The object
of this game is to make sandwiches of your opponents tiles,
flipping them over to your color (which will be black).
These sandwiches can be any thickness, so long as they
are bookended by one existing black tile and one new
black tile.
## RUNNING THE CODE:
 - Run `main` to play.
 - At line 45 of this `main`
   - `debug` activates the pre/post-conditions in each file
   - `reset_settings` resets the game settings in the in-game **"Settings"** screen
 ### FEATURES:
 - Look in settings to change anything you want. These changes are saved permanently in a separate file,
   so if you close the game and reopen, it will be saved.
   - Speed is for the animations.
     - Animations include placing, flipping, and removing
     - Off the right side of the speed slider, you can get "MAX" speed
   - Show Moves will show you all of the possible moves you can make on the board
 - Board sizes from 4x4 to 12x12 are available:
   - 8x8 is recommended (and standard)
   - Bots are slower on larger boards (more possible moves to think about)
 - Bots: Test as much as you like, but each bot typically beats the one below.
   - The lvl 0 bot is different. It chooses a move randomly and won't skip unless forced to.
   - The lvl 10 bot will be a bit slow, but lvl 8 is more skilled than me and will beat you.
 - Undo and Skip can be deactivated (in real life they don't exist)
   - If skip is off, the Bots will avoid skipping unless necessary.
     - If skip is on, Bots will skip if it's strategic, but only a few times in a row before
            getting bored and making a move.
     - If skip is off, it turns back on temporarily if you have no available moves.
   - After "game over", Undo button resets the board.
 - Scorekeepers show current scores
 - Progress bar with animation show current scores and game progress
 - Quit button is always active unless a Bot is thinking.
## FILES
- `main` contains the main loop and other functions.
- `Tile_Class` contains animation classes. This includes `Tile`, which draws the game pieces, `Button`, which draws and holds visual data about the buttons, and `TextBox`, whcih holds display information about text surfaces to be displayed.
- `Board_Class` is self explanatory. The `Board` object holds the state of the board and has functions which access and mutate information about the game state.
- `Bot_Class` has a robot object which can look at a board and make decisions based on what it sees. 
- `Vector_Class` is a subclass of tuple with improved operations for adding/subtracting coordinates and other manipulations.
- `settings.dat` is a `Pickle` file containing a tuple of saved info from the **"Settings"** screen ingame
### MAIN
This file is where the game takes place. Here, all objects are instantiated and the game is played and rendered.

First, functions are defined which do well-defined things like make a move, change the board size, or set the scores. Next, all of the colors, settings, buttons, and text boxes are generated for future reference. Next, the main loop starts. The main loop is separated into event listening and screen display. 

First, pygame listens for clicking events. There are three possible game states: `game_active`, `settings_open`, and the title screen. Collisions are detected depending on the current game state. At all states, we listen for button presses, but during `game_active`, we check if a board click is valid and if legal, we move there.

Last, the display is updated and animations are moved forward by one step. In each of the game states, different objects are rendered and different animations take place.
### TILE_CLASS
This file has three classes which are used for the creating all of the display effects in the game. 
- The `Tile` class holds information about the color, location, shape, and animation state of each tile during gameplay
  - The `Board` holds all information about the actual game, but the tiles are the only thing the player can actually see. 
 There are three animations which morph the dimensions of the tile: Placing, Flipping, and Removal.
- The `Button` class helps to concisely describe and display a clickable button on the screen.
  - The button object hold the dimensions, location, color, text, font, text color, text location, border width of a button on the screen. This would
       otherwise require a bunch of different variables, rectangle objects, and assignments: creating surfaces, rectangles, and several lines of code to render.
- The `TextBox` class is similar to a button but without a rectangle or any clickable functionality.
  - Text boxes to a lot less, but they hold the text rendering surface and the location rectangle in one
       more convenient place, rather than having separate `text_surf` and `text_rect` objects. Also, the `changeText` method is particularly helpful, because this would
       otherwise require constructing brand new objects from scratch
