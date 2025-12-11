# Verilog FSM-Controlled LED Shift Register

**Authors:** Christian Lopez & Ashton Char  
**Course:** EE 435  
**Date:** April 26, 2024

## 💡 Project Overview
This project implements a digital system using a **Finite State Machine (FSM)** to control an 8-bit LED shift register. The design follows a modular approach, separating the state control logic from the register shifting logic.

To address the high speed of the system clock, we implemented a **1 Hz strobe signal**. This allows the LED shifting to be visually perceptible, updating the display only once per second.

## 🛠️ Design Structure
The project consists of two main Verilog modules:

### 1. Main Controller (`led_shift.v`)
This module serves as the top-level FSM. It handles:
* **State Management:** Uses **1-Hot Encoding** to switch between states based on button inputs.
* **Strobe Generation:** Creates a 1 Hz boolean flag (`strobe_1hz`) by counting system clock cycles up to a `top_count` parameter.

### 2. Shift Register Logic (`shift_reg.v`)
This module receives the state and strobe signals to drive the LEDs.
* **Input:** Takes an 8-bit sequence from the switches.
* **Output:** Drives the 8-bit LED array.
* **Logic:** Performs circular left or right shifts only when the 1 Hz strobe is asserted.

## 🕹️ Finite State Machine (FSM)
The system utilizes four distinct states:

| State | Function | Control Input |
| :--- | :--- | :--- |
| **CLEAR** | Resets the LED register to 0. (Initial State) | `BTND` |
| **LOAD** | Loads the 8-bit binary pattern from the switches. | `BTNU` |
| **LEFT_SHIFT** | Circularly shifts the bits to the left. | `BTNL` |
| **RIGHT_SHIFT** | Circularly shifts the bits to the right. | `BTNR` |

## 🐛 Implementation Notes & Debugging
During the development process, we encountered and resolved the following issues:

* **Register Assignment:** Initially, the shift logic failed to update the output register because the shifted result was not properly assigned back to the `out` register. This was fixed to ensure persistent storage of the shifted pattern.
* **State Transitions:** We utilized 1-Hot encoding for
