# CPPND: Capstone Snake Game Example

 The code for this repo was inspired by [this](https://codereview.stackexchange.com/questions/212296/snake-game-in-c-with-sdl) excellent StackOverflow post and set of responses.


The Capstone Project provides a chance to integrate what we've learned throughout udacity c++ program. This project is an important part of my portfolio to share with current and future colleagues and employers.

In this project, Snake game is extended, following the principles I have experienced throughout this Nanodegree Program. This project will demonstrate that I can independently create applications using a wide range of C++ features.
SDL library is used in this project.
some of the flags are as following..

<img src="snake_game.gif"/>



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

------ Loops, functions, I/O --------------
The game loop is a while loop that runs continuously in your the and has three steps:

Input: This step handles user input from a keyboard, joystick, game controller, or other input device.

Update: This step uses the input to update the internal state of the game. The game state might include:
        positions of characters in the game world
        the speed, health, or inventory of characters in the game
        how many points have been scored in the game so far
        any other attributes or data in the game
Each part of the game state might be updated independently of the input as well. For example, if a character is moving forward in the game with a given velocity, the update step might change the character's position without any additional input.

Render: This step takes the game state and renders the state to the screen according to fixed rules. For example, a character might be rendered with a particular image or "sprite", or a texture might be applied to the background of the game window.

One major benefit of using this design pattern in a game is that each part of the game loop can be implemented separately in the code. If you want to change the appearance of your game without making major changes to how the game works, you can just update the Rendering code. Similarly, you are free to modify how the gameplay works without changing the rendering or input portion of the code at all.
---------------------------------------------------------------------------------------
------- Object Oriented Programming ----------------
The project code is organized into classes.
Class Structure;The Snake game code consists of four main classes: Game, Snake, Controller, and Renderer
Game Class can be seen as below;  class attributes to hold the data, and class methods to perform tasks.
class Game {
 public:
  Game(std::size_t grid_width, std::size_t grid_height);
  void Run(Controller const &controller, Renderer &renderer,
           std::size_t target_frame_duration);
  int GetScore() const;
  int GetSize() const;

 private:
  Snake snake;
  SDL_Point food;

  std::random_device dev;
  std::mt19937 engine;
  std::uniform_int_distribution<int> random_w;
  std::uniform_int_distribution<int> random_h;

  int score{0};

  void PlaceFood();
  void Update();
};
----------------------------------
All class members that are set to argument values are initialized through member initialization lists.
class Snake {
 public:
  enum class Direction { kUp, kDown, kLeft, kRight };

  Snake(int grid_width, int grid_height)
      : grid_width(grid_width),
        grid_height(grid_height),
        head_x(grid_width / 2),
        head_y(grid_height / 2) {}
 ------------------------------------------
All class member functions document their effects, either through function names, 
comments, or formal documentation. Member functions do not change program state in undocumented ways.
 
  float speed{0.1f};
  int size{1};
  bool alive{true};
  float head_x;
  float head_y;
  std::vector<SDL_Point> body;
  -------------------------------------
Appropriate data and functions are grouped into classes. 
Member data that is subject to an invariant is hidden from the user. (Private definitions provides this) 
State is accessed via member functions.
snake.Update();
 private:
  void UpdateHead();
  void UpdateBody(SDL_Point &current_cell, SDL_Point &prev_cell);
  ------------------------------------------------------------------------------

  



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
