#  Snake Game on AVR Microcontroller with 2x16 LCD Display

This README provides instructions on how to build a stable snake game on an AVR microcontroller, featuring a 2x16 LCD display while consuming only 12.8% of memory.

## Hardware:

- AVR Microcontroller: ATmega32
- LCD Module: LM016L (2 x 16)
- Compiler/IDE: Microchip

## Features:

- Minimal RAM usage
- Stable LCD display with consistent lighting

## Getting Started:

### Problems and solution:

One challenge addressed in this project is how to design a snake game that occupies only 256 bytes of memory while utilizing a display resolution of 1600 pixels. The solution involves representing the snake's body without relying on the coordinates of each pixel on the LCD. Instead, an array (`uint8_t snake_body[32][8]`) is used. Each segment of the LCD is simulated with an array of 8 bytes, corresponding to the 5x8 pixel font of the LCD. By drawing the snake using individual bits within this array and sending the resulting pattern to the LCD, the snake's movements can be displayed efficiently.

Another challenge tackled in this project involves ensuring a stable screen display for the snake game. Due to the limited number of character generator RAM (CGRAM) slots available (only 8), the screen tends to flicker when updating the snake's movements. To address this issue, instead of storing each part of the snake's body in CGRAM, which would lead to repetitive patterns as the snake grows, a mapping technique is employed.

Before sending the snake's body to the LCD, a mapping array (map[32]) is created. Each index of the array corresponds to a segment of the LCD, and the value stored represents the pattern in CGRAM. For example, `map[0] = 1` means that segment 0 on the LCD corresponds to the pattern stored in CGRAM slot 1. This mapping reduces the number of communications between the LCD and the microcontroller during each step of the snake's movement, ensuring a stable display.

 
