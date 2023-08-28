# Bouncing Ball (Redux)

## Overview

The Bouncing Ball (Redux) was a project done by me (Alexander Worley) that allowed for a "ball" sprite to move around the screen of a C64, and if it hit the borders of the screen, it would bounce off and continue moving. The program was made using BASIC's assembly language. Using the starting addresses of various C64 components (also variables, and "mainloop" functions), I was able to create a sprite and make it move through the screen's limited resolution. This file will go over multiple subjects, including sections to explain some of the basic functionalilty of the assembly code (addresses, data list, etc.). It will also go over the purpose of the "mainloop" function and what is nested inside of it, because those are the main components that allow for the entire program to function.

## Sections

### Starting Addresses

In the beginning of the project, there are multiple addresses that are required in order for the system to use certain components in the C64 Hardware, which include:

>$d400 -- start of the SID (Sound Interface Device) chip, a sound chip that provides 4 different waveforms for music and sound effects
>
>$d000 -- start of the VIC-II (Video Interface Chip), a microchip used in the C64 that controls the graphic rountines (characters, sprites, etc.)
>
>$3000 -- the location of the first sprite
>
>$0900 -- location of the sprite data list
>
>$FFD2 -- start of the CHROUT routine, which is used to print an output to the screen
>
>$0801 -- starting location of BASIC's "free" memory space
>
>$1000 -- the starting address for the beginning of the assembly code

### Data List

The sprite data list is used to create a sprite through a series of bytes, which contain 8 bits of 0,1,2,4,8,16,32,64, and 128. All pixels (or bits) add up to 255.

*Note -- the setup of the data list is a "grid" of 24 bits in width, and 21 bits in height.*

### Variables

The two variables that are used in this project are the x and y coordinates of the sprite, coined as "varsx" and "varsy". They are mainly used in this case as "placeholders" for the constant updates of where the sprite is located on the screen. They also help out in the cases of checking the "bounce" of the sprite ball.

### Main Loop

The main loop of the project consists of 3 functions that make up a great portion of the code, which includes:

<ins>bouncecheck</ins>

The purpose of the bouncecheck function is to check the borders of the C64 screen, and if the sprite meets those borders, then it should reverse its current position or "bounce" back.

*Note -- the bounce case has to check both the x position and the y position of the screen seperately, which assembly tells the difference between the coordinates with V (x position) and V+1 (y position).*

<ins>moveball</ins>

The moveball function utilizes the VIC-II chip and variables to increment the sprite by 1 in both directions, which outputs a "move" mechanic to the screen per frame.

<ins>delayloop</ins>

Since the code is in assembly, it can run far faster in-terms of optimization. However, that means the sprite will move at a pace that is hard for the user to notice. So, the delayloop is a function that creates a "delay" in the program's order of operations, simply to allow for a better "pacing" of the sprite's movement.

## Requirements

### Visual Studio Code

Visual Studio Code is a code editor that is built to assist in visual-based debugging and building optimized applications.

*Note -- be sure to have the most recent version of the software, and that your operating system (OS) is either Windows 10 (or later), or OS X 10.11 (or later)*

### VICE

VICE is a program that emulates systems such as the C64. This is needed to run the program file type (.PRG) properly.

*Note -- be sure to know if your computer is either 32-bit or 64-bit. You can most likely find that information in your computer's settings.*

### Turbo Macro Pro x

Turbo Macro Pro x (or TMPx) is a cross-assembler that is used to convert files into different file types. This helps with during the assembly code (.ASM) into the program file type (.PRG) needed to run on VICE.

## Instructions

<ins>Step 1</ins>

Open up Visual Studio Code and start a new terminal (located in the top left-corner). Make sure to have both the assembly file and program file in the file named "TMPx_v1.1.0-STYLE" in order to convert the file properly.

<ins>Step 2</ins>

Go through the file directory in the terminal (on Windows, you can usually use cd followed by ./yourfile/etc) usually until you reach the TMPx file, and input the following line to convert the assembly file into a program:

>TMPX -i alexball1.asm -o alexball2.prg

<ins>Step 3</ins>

Open up VICE and boot up the C64 simulator. Drag and drop the PRG file directly into the VICE application.

Note -- The way the code is written, it should automatically run the program.

<ins>Step 4</ins>

When you are done with the program, press esc to end the program and close VICE.

