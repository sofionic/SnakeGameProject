# CPPND: Capstone Snake Game Example

 The code for this repo was inspired by [this](https://codereview.stackexchange.com/questions/212296/snake-game-in-c-with-sdl) excellent StackOverflow post and set of responses.

<img src="snake_game.gif"/>

The Capstone Project provides a chance to integrate what we've learned throughout udacity c++ program. This project is an important part of my portfolio to share with current and future colleagues and employers.

In this project, Snake game is extended, following the principles I have experienced throughout this Nanodegree Program. This project will demonstrate that I can independently create applications using a wide range of C++ features.
SDL library is used in this project.
some of the flags are as following..
// triggers the program that controls 
    // your graphics hardware and sets flags 
    Uint32 render_flags = SDL_RENDERER_ACCELERATED; 
  
    // creates a renderer to render our images 
    SDL_Renderer* rend = SDL_CreateRenderer(win, -1, render_flags); 
  
    // creates a surface to load an image into the main memory 
    SDL_Surface* surface; 
  
    // please provide a path for your image 
    surface = IMG_Load("path"); 
  
    // loads image to our graphics hardware memory. 
    SDL_Texture* tex = SDL_CreateTextureFromSurface(rend, surface); 
  
    // clears main-memory 
    SDL_FreeSurface(surface); 
  
    // let us control our image position 
    // so that we can move it with our keyboard. 
    SDL_Rect dest; 
  
    // connects our texture with dest to control position 
    SDL_QueryTexture(tex, NULL, NULL, &dest.w, &dest.h); 
    --------------------------------------------
    https://www.geeksforgeeks.org/sdl-library-in-c-c-with-examples/
    --------------------------------------------

    -----------------------------------------------------------------------------------------
    The Snake game code consists of four main classes: Game, Snake, Controller, and Renderer. The image above shows how the code functions:

    To begin, main creates a Controller, a Game, and a Renderer object. Game stores a Snake object as part of the state.
    main calls Game::Run to start the game loop.

The next videos walk through each of the files in the Snake game repository in more detail.
main.cpp

This is the entrypoint for the program. The main function in this file sets variables such as the window height and width and the number of frames per second at which the game will be played. The main also creates Renderer, Controller, and Game objects, and calls the Game::Run method to start the game loop.
---------------------------------------------------------------------------------------------

---------------------------------------------------------------------------------------------
snake.h and snake.cpp

These files define the Snake class which contains attributes to keep track of the Snake speed, size, and location. Additionally, there are methods to update the snake state, which are called from the Game::Update method. The Snake head and body are treated separately; the head is stored using float coordinates, and the body is stored using a vector of int cell coordinates. The Snake::UpdateHead method updates the head location using the snake's speed. If the head has passed into a new cell, then the body is updated with the Snake::UpdateBody.
---------------------------------------------------------------------------------------------

---------------------------------------------------------------------------------------------
game.h and game.cpp

These files define the Game class and the game loop: Game::Run. The Game class stores the state of the game, including an instance of a Snake object, the game score, and the location of "food" in the game. Aside from the game loop, the Game class also contains methods to update the state of the game (Game::Update), get the size of the snake, get the total score in the game, and place new food in the game if the food has been eaten by the snake.
---------------------------------------------------------------------------------------------

---------------------------------------------------------------------------------------------
render.h and render.cpp

These files define the Renderer class which uses the SDL library to render the game to the screen. The Renderer class constructor creates the SDL window and an SDL renderer object that can draw in the window. The Renderer::Render method draws the food and the snake in the window using the SDL renderer.
---------------------------------------------------------------------------------------------

---------------------------------------------------------------------------------------------
controller.h and controller.cpp
These files define the Controller class. This class handles keyboard input using the SDL libary, and it sets the snake's direction based on the input.
---------------------------------------------------------------------------------------------

------------- Link for SDL -------------
https://wiki.libsdl.org/APIByCategory
----------------------------------------
## Dependencies for Running Locally
* cmake >= 3.7
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* SDL2 >= 2.0
  * All installation instructions can be found [here](https://wiki.libsdl.org/Installation)
  * Note that for Linux, an `apt` or `apt-get` installation is preferred to building from source.
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./SnakeGame`.