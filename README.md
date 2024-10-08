# Arduino-Lockpicking-Game

## Table of Contents
- [Description](#description)
- [Hardware Setup](#hardware-setup)
- [Software Architecture](#software-architecture)
- [Installation](#installation)
- [Future Improvements](#future-improvements)

## Description

A simple lock picking game developed for Arduino, inspired by lockpicking minigames in games like Skyrim or Oblivion, in which the player must rely on visual and auditory feedback to position the cursor correctly to pick a lock.

### Gameplay
When initialized the game generates a random target position on a 2 dimensional lock. The player, using the joystick to control their pointer's position, must rely on a mixture of visual and auditory feedback to try and locate the randomly generated target. Once they think they have found the target, they can hit the button to attempt to pick the lock, if they are close enough to the target they will pass and keep all their picks, and a new target will be generated. IF they are not close enough then they will break one of their picks and the target will remain. If the player successfully picks three locks, they will win and be shown the amount of time it took them to complete the game in seconds, if however they break all 3 picks then they will lose the game. In either case the game will reset after 10 seconds.
#### Feedback
The game provides both visual and auditory feedback elements, Visually the player will see a representation of a lock on their screen, as well as a pointer visualizing where their joystick is positioned, they will also see a target, which will show the general area in which they need to find the target point, however it will not be centered around the target. Auditorily the player will hear  a buzzing noise when they begin to approach the target point, the buzzing will happen more frequently the closer the player's pointer is to the target.


## Hardware Setup

### Components
- **Arduino Uno**
- **OLED Screen**
- **Joystick Module**
- **Push Button**
- **Buzzer**
- **10kΩ Resistor**
- **Power Source for Arduino**

### Connections
![Hardware Setup Diagram](/assets/Hardware_Setup.svg)

#### **Component Connections:**

- **Joystick**
  - **X-Axis**: Connected to analog pin **A0**.
  - **Y-Axis**: Connected to analog pin **A1**.
  - **VCC**: Connected to **5V** rail.
  - **GND**: Connected to **GND** rail.
  
- **Push Button**
  - **Input Terminal**: Connected to **5V** rail.
  - **Output Terminal**: Connected to digital pin **2**.
  - **Other Terminal**: Connected to **GND** with a pull-down resistor (10kΩ).
  
- **Buzzer**
  - **Positive Terminal**: Connected to digital pin **7**.
  - **Negative Terminal**: Connected to **GND** on the Arduino.
  
- **OLED Screen**
  - **SDA (Data Line)**: Connected to **A4** on the Arduino.
  - **SCL (Clock Line)**: Connected to **A5** on the Arduino.
  - **VCC**: Connected to **3.3V** rail.
  - **GND**: Connected to **GND** rail.

## Software Architecture

The software is structured around a main loop that runs continuously, and calls various functions to determine things about the game state and the player's actions. The software also relies on the library `U8g2lib.h` for graphics, and communication with the OLED screen 

### Main Loop

The `loop()` function continuously runs the game logic. It monitors the player's joystick input, processes button presses, and updates the game state. Depending on the player's actions, it either checks the distance between the player's pointer and the target, updates the display, or plays sounds via the buzzer.

### Key Functions
- `setup()` Initializes the OLED screen, sets pins to the correct modes, and generates  random seed based off of an `analogRead()`
- `checkDistance()` Compares the players pointer position to the target position
- `buttonPress()` Checks if the button was pressed, and if so determines whether to generate a new target or subtract the number of available lockpicks.
- `checkGameState()` Checks if a win condition has been reached, and if so displays the time taken to beat the game before resetting
- `displayGameOver()` If all picks are broken, clears screen, displays Game Over before resetting
- `allPicksBroken()` Returns a bool based on whether there are picks left to play with or not
- `displayPicks()` Draws as many picks as are available


## Installation

After completing the hardware setup, download [LockGame.ino](/code/LockGame.ino) from the assets section. Then open the file in the Arduino IDE, connect your arduino via USB, and upload the file. After this you should be ready to play. Simply power on the device and it will begin.

## Future Improvements
- **UI/UX improvements**: Something like the main menu or controls for choosing when to begin the game, if you'd like to play again etc.
- **Highscores**: Stored highscores to encourage speedy play 
- **Scaling Difficulty**: Each successive attempt could ramp up the difficulty, either requiring more precision or reducing the number of available picks.



