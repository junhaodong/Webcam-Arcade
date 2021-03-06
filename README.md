Webcam-Arcade
=============
APCS Final Project -- Spring '14  
Junhao Dong & Eric Chen

Games that involve image processing through the webcam.

## Instructions
- Compile using "javac -cp .:libs/\* \*.java" or "javac -cp .;libs/\* \*.java" on Windows machines
- Run the program with "java -cp .:libs/\* Driver" or "java -cp .;libs/\* Driver"
  - It is expected for terminal to default to a no-operation implementation
- Get a distinct color that you wish to track, preferably a light source and cover the entire square in the center. Press any button to begin tracking this color
  - You may press any key besides the following keys to track a new color
- Switch between screens with the following keys:
  - Press **S** to enter the Setup Screen (Default Screen)
  - Press **D** to enter the Draw Screen
  - Press **P** to enter the Pong Screen

__Drawing__
- Once you enter the draw screen, press any key besides 'z' and 'r' to draw a rectangle
- Draw screen supports undo and redo. Press __z__ to undo and __r__ to redo

## Hierarchy and Class Descriptions

__Driver__
- Entrance to the program
- Creates The WebcamPanel, SetupScreen, etc...
- Has a stack of screens
  - peek() the top of the stack and pass down the method paintImage(), which is like a while loop (more like a thread that is constantly updated in the WebcamPanel)

__Screen__
- Interface
- Describes general methods that screens should have. Look into code for more info

__SetupScreen__
- Records the color of the object to be tracked
- Allows the user to test if the color is distinct enough before selecting a different screen

__DrawScreen__
- Allows the user to draw
- Contains a LinkedList of history of commands and a Stack of optional redo commands

__PongScreen__
- Classic Pong game

## Algorithms

__Mean Shift Algorithm__
- Separate colors into RGB (red green blue)
- Find the weighted mean of all the colors in a Rectangle, then move to that mean
  - The weight is given by w = e^(-k*Distance(colorTracked, colorPixel)^2)
  - Credits to cmsoft.com and its color tracking case study

__Undo/Redo in DrawScreen__
- All commands are added to the end of the linkedlist (like a stack, but we need to iterate through the list to draw the rectangles)
- Any undo commands are pushed onto a redo stack
