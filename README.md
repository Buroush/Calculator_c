# Simple GTK Calculator in C

This is a basic calculator application built using the GTK library in the C programming language. It provides a graphical user interface for performing arithmetic operations, including addition, subtraction, multiplication, and division. The calculator features a user-friendly interface with numeric buttons, operator buttons (+, -, *, /), a clear button (C), and an equals button (=).

## Key Features

- User-friendly graphical interface.
- Supports basic arithmetic operations.
- Clear button to reset input.
- Error handling for division by zero.
- Right-aligned text entry field.
- Results are displayed with two decimal places.

## Getting Started

To run the calculator on your system, make sure you have the GTK development libraries installed. You can compile the code using GCC or an appropriate compiler for your platform.

### Prerequisites

- GTK development libraries

### Compilation

To compile the code, use the following command:

```bash
gcc -o calculator calculator.c `pkg-config --cflags --libs gtk+-3.0`
