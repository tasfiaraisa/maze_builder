# Maze Builder & Runner — FPGA-Based Game

An interactive, two-player maze game developed in **C** for the **DE1-SoC FPGA platform**, using the **Nios II processor**, memory-mapped I/O, PS/2 keyboard input, and VGA graphics.

The game combines maze construction and navigation with hardware-level programming, custom rendering, collision detection, and interactive gameplay.

## Overview

Maze Builder & Runner consists of two gameplay phases:

**Maze Builder:** The first player designs a maze by placing walls and obstacles, creating a path that the second player must navigate.

**Maze Runner:** The second player attempts to navigate the maze while avoiding walls and traps to reach the destination.

The game includes scoring, collision detection, and different trap mechanics to make navigation more challenging.

## Features

- **Two-player gameplay:** Separate maze-building and maze-running phases.
- **Interactive maze construction:** Place walls, obstacles, and traps using hardware inputs.
- **Collision detection:** Prevent invalid player movements through maze boundaries and walls.
- **Trap mechanics:** Gameplay includes traps that affect player movement.
- **VGA graphics:** Custom graphics rendered directly through a pixel buffer.
- **Double buffering:** Uses two frame buffers to support smoother display updates.
- **Scoring system:** Tracks game outcomes and displays results.
- **Hardware interaction:** Uses memory-mapped input/output and PS/2 keyboard controls.

## Technology Stack

| Category | Technology |
|---|---|
| Programming language | C |
| Processor architecture | Nios II |
| Hardware platform | DE1-SoC FPGA |
| Graphics | VGA pixel buffer |
| Input | PS/2 keyboard, FPGA switches |
| Hardware interfacing | Memory-Mapped I/O |
| Debugging & simulation | CPUlator |

## System Architecture

```text
          PS/2 Keyboard       FPGA Switches
                 |                  |
                 +---------+--------+
                           |
                           v
                  Memory-Mapped I/O
                           |
                           v
                    Nios II CPU
                           |
                 Game Logic in C
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
     Maze Grid        Player Logic      Game State
     & Walls          & Collision       & Scoring
          |                |                |
          +----------------+----------------+
                           |
                           v
                    VGA Rendering
                           |
                           v
                  Pixel Frame Buffers
                           |
                           v
                     VGA Display
```

## Implementation Details

### 1. Maze Representation and Game Logic

The game maintains a two-dimensional maze array to represent the maze layout and its elements.

The application tracks player positions, maze boundaries, walls, traps, and game state using C data structures and global variables.

Dedicated functions handle maze initialization, placement of elements, movement, collision checks, and rendering.

### 2. Hardware Input

The application interacts with hardware through memory-mapped registers.

Switch input and PS/2 keyboard input are processed to control maze construction and player movement.

This approach provides direct communication between the application and the FPGA's peripherals without relying on a conventional desktop operating system.

### 3. VGA Graphics and Double Buffering

Graphics are rendered using pixel-level drawing functions that write to a frame buffer.

The implementation uses two pixel buffers and display synchronization to manage frame updates.

This allows the application to prepare graphics in one buffer while another buffer is used for display, reducing visible rendering artifacts.

### 4. Player Movement and Collision Detection

Player movement is processed according to input direction and the current maze configuration.

The game checks the maze state to determine whether movement is valid and whether the player has encountered an obstacle or trap.

### 5. Trap Mechanics and Scoring

The game incorporates multiple trap behaviors that affect navigation and gameplay progression.

It also maintains scoring variables for both players and uses the game state to determine and display the outcome.

## Debugging with CPUlator

During development, I used [CPUlator — Nios II System Simulator](https://cpulator.01xz.net/) to test and debug the program.

CPUlator provides a simulated Nios II environment for inspecting program execution and working with supported memory-mapped peripherals.

Using CPUlator helped with debugging the game's logic and hardware-oriented interactions before or alongside testing on the physical FPGA platform.

## Screenshots and Demonstration

*Gameplay screenshots and a demonstration video will be added here.*

## What I Learned

This project strengthened my understanding of:

- Bare-metal programming and direct hardware interaction
- Memory-mapped I/O and peripheral control
- Graphics rendering using pixel buffers
- Double buffering and display synchronization
- Game-state management and collision detection
- Debugging embedded software with processor simulation tools

## Future Improvements

Potential extensions include additional maze layouts, more complex obstacles, and improvements to the user interface and gameplay experience.

## Source Code

The game is implemented primarily in `mazeBuilderGame.c`.

The project demonstrates embedded software development using C, hardware peripherals, and low-level graphics programming on an FPGA-based system.
