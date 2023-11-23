
# **PORTS**
URCL supports official ports as well as custom ports specific to a target CPU.

Ports are treated as normal URCL instructions.

|![Tip icon]|*Official ports can be used in URCL programs without having to be defined. They use the definition given here.*|
| - | - |

|![Tip icon]|*Note that the programmer or target CPU can make up their own ports, and these do not have to follow the official documentation.*<br>*In this case the programmer or target CPU should define what is meant by each port if it is not obvious. A simple comment in the code is typically fine if it is not too complex.*|
| - | - |

All the official ports defined in the URCL documentation all have their own port number. The `IN%SUPPORTED` port refers to each port using this port number.

|![Tip icon]|*Beware that if the port number is too large to be represented using the number of bits in the `BITS` header - then the `IN%SUPPORTED` port will not work.*|
| - | - |

Ideally programs should use generic ports where possible as this potentially enables a wider range of target CPUs to run that program.

|![Tip icon]|*Beware that a program using custom ports specific to a target CPU, means that program may not easily be portable to other target CPUs.*|
| - | - |

|![Tip icon]|*Blocking ports mean that the target CPU will wait for the port to finish before continuing execution.<br>This means a `IN%NUMB R1` instruction will stop execution until a number is inputted into register 1.*|
| - | - |

|![Tip icon]|*Non-blocking ports mean that the target CPU will not wait for the port to finish before continuing execution.<br>This means a `IN%KEYBOARD R1` instruction will not stop execution even if the keyboard isn't being used.*|
| - | - |

| **Port Number** |     **Port**     |      **Full Name**      | **Port Type** | **Blocking?** |
|:---------------:|:----------------:|:-----------------------:|:-------------:|:-------------:|
|        0        |     OUT%NUMB     |         Number          |   Terminal    |      Yes      |
|        1        |     IN%NUMB      |         Number          |   Terminal    |      Yes      |
|        2        |     OUT%TEXT     |          Text           |   Terminal    |      Yes      |
|        3        |     IN%TEXT      |          Text           |   Terminal    |      Yes      |
|        4        |     OUT%INT      |         Integer         |   Terminal    |      Yes      |
|        5        |      IN%INT      |         Integer         |   Terminal    |      Yes      |
|        6        |     OUT%UINT     |    Unsigned Integer     |   Terminal    |      Yes      |
|        7        |     IN%UINT      |    Unsigned Integer     |   Terminal    |      Yes      |
|        8        |     OUT%BIN      |         Binary          |   Terminal    |      Yes      |
|        9        |      IN%BIN      |         Binary          |   Terminal    |      Yes      |
|       10        |     OUT%HEX      |       Hexadecimal       |   Terminal    |      Yes      |
|       11        |      IN%HEX      |       Hexadecimal       |   Terminal    |      Yes      |
|       12        |    OUT%FLOAT     |     Floating Point      |   Terminal    |      Yes      |
|       13        |     IN%FLOAT     |     Floating Point      |   Terminal    |      Yes      |
|       14        |    OUT%FIXED     |       Fixed Point       |   Terminal    |      Yes      |
|       15        |     IN%FIXED     |       Fixed Point       |   Terminal    |      Yes      |
|       16        |     OUT%RNG      | Random Number Generator |   Numerical   |      Yes      |
|       17        |      IN%RNG      | Random Number Generator |   Numerical   |      Yes      |
|       18        |   IN%KEYBOARD    |        Keyboard         |  User Input   |      No       |
|       19        |   OUT%GAMEPAD    |         Gamepad         |  User Input   |      Yes      |
|       20        |    IN%GAMEPAD    |         Gamepad         |  User Input   |      No       |
|       21        |   OUT%MOUSE_X    |         Mouse X         |  User Input   |      Yes      |
|       22        |    IN%MOUSE_X    |         Mouse X         |  User Input   |      No       |
|       23        |   OUT%MOUSE_Y    |         Mouse Y         |  User Input   |      Yes      |
|       24        |    IN%MOUSE_Y    |         Mouse Y         |  User Input   |      No       |
|       25        |  OUT%MOUSE_POS   |     Mouse Position      |  User Input   |      Yes      |
|       26        |   IN%MOUSE_POS   |     Mouse Position      |  User Input   |      No       |
|       27        |   IN%MOUSE_DX    |      Mouse Delta X      |  User Input   |      No       |
|       28        |   IN%MOUSE_DY    |      Mouse Delta Y      |  User Input   |      No       |
|       29        |  IN%MOUSE_SPEED  |       Mouse Speed       |  User Input   |      No       |
|       30        | IN%MOUSE_BUTTONS |      Mouse Buttons      |  User Input   |      No       |
|       31        |    OUT%WIDTH     |          Width          |   Graphical   |      Yes      |
|       32        |     IN%WIDTH     |          Width          |   Graphical   |      Yes      |
|       33        |    OUT%HEIGHT    |         Height          |   Graphical   |      Yes      |
|       34        |    IN%HEIGHT     |         Height          |   Graphical   |      Yes      |
|       35        |     OUT%FILL     |          Fill           |   Graphical   |      Yes      |
|       36        |    OUT%CLEAR     |          Clear          |   Graphical   |      Yes      |
|       37        |    OUT%FREEZE    |         Freeze          |   Graphical   |      Yes      |
|       38        |   OUT%UNFREEZE   |        Unfreeze         |   Graphical   |      Yes      |
|       39        |    OUT%BUFFER    |         Buffer          |   Graphical   |      Yes      |
|       40        |    IN%BUFFER     |         Buffer          |   Graphical   |      Yes      |
|       41        | OUT%SCREEN_NUMB  |      Screen Number      |   Graphical   |      Yes      |
|       42        | OUT%SCREEN_TEXT  |       Screen Text       |   Graphical   |      Yes      |
|       43        |    OUT%PIXEL     |          Pixel          |   Graphical   |      Yes      |
|       44        |     IN%PIXEL     |          Pixel          |   Graphical   |      Yes      |
|       45        |     OUT%LINE     |          Line           |   Graphical   |      Yes      |
|       46        |     OUT%BOX      |           Box           |   Graphical   |      Yes      |
|       47        |    OUT%SOUND     |          Sound          |     Audio     |      No       |
|       48        |    IN%RUNTIME    |         Runtime         |   Temporal    |      No       |
|       49        |     OUT%WAIT     |          Wait           |   Temporal    |      Yes      |
|       50        |     IN%WAIT      |          Wait           |   Temporal    |      Yes      |
|       51        |   IN%FRAMETIME   |       Frame Time        |   Temporal    |      No       |
|       52        |   OUT%STORAGE    |         Storage         |   External    |      Yes      |
|       53        |    IN%STORAGE    |         Storage         |   External    |      Yes      |
|       54        |   OUT%NETWORK    |         Network         |   External    |      Yes      |
|       55        |    IN%NETWORK    |         Network         |   External    |      Yes      |
|       56        |  OUT%COLORMODE   |       Colour Mode       | Environmental |      Yes      |
|       57        |   IN%COLORMODE   |       Colour Mode       | Environmental |      Yes      |
|       58        |   IN%SUPPORTED   |        Supported        | Environmental |      Yes      |
|       59        |  OUT%CLOCKSPEED  |       Clock Speed       | Environmental |      Yes      |
|       60        |  IN%CLOCKSPEED   |       Clock Speed       | Environmental |      No       |
|       61        |   OUT%PROFILE    |      Port Profile       |  Specialised  |      Yes      |
|       62        |    IN%PROFILE    |      Port Profile       |  Specialised  |      Yes      |

|![Tip icon]|*American spelling must used for port names - to be consistent.*|
| - | - |

## Terminal
These ports are designed to interact with terminal style character displays, rather than pixel displays.

|  **Port**  |     **Operand1**     |                        **Function**                        |
|:----------:|:--------------------:|:----------------------------------------------------------:|
|  OUT%NUMB  | Register / Immediate |           Outputs a generic number to terminal.            |
|  IN%NUMB   |       Register       |     Inputs an external generic number into a register.     |
|  OUT%TEXT  | Register / Immediate |       Outputs a generic text character to terminal.        |
|  IN%TEXT   |       Register       | Inputs an external generic text character into a register. |
|  OUT%INT   | Register / Immediate |              Outputs an integer to terminal.               |
|   IN%INT   |       Register       |             Inputs an integer into a register.             |
|  OUT%UINT  | Register / Immediate |          Outputs an unsigned integer to terminal.          |
|  IN%UINT   |       Register       |        Inputs an unsigned integer into a register.         |
|  OUT%BIN   | Register / Immediate |            Outputs a base 2 number to terminal.            |
|   IN%BIN   |       Register       |          Inputs a base 2 number into a register.           |
|  OUT%HEX   | Register / Immediate |           Outputs a base 16 number to terminal.            |
|   IN%HEX   |       Register       |          Inputs a base 16 number into a register.          |
| OUT%FLOAT  | Register / Immediate |        Outputs a floating point number to terminal.        |
|  IN%FLOAT  |       Register       |      Inputs a floating point number into a register.       |
| OUT%FIXED  | Register / Immediate |         Outputs a fixed point number to terminal.          |
|  IN%FIXED  |       Register       |        Inputs a fixed point number into a register.        |
| OUT%ASCII7 | Register / Immediate |        Outputs a 7 bit ASCII character to terminal.        |
| IN%ASCII7  |       Register       |      Inputs a 7 bit ASCII character into a register.       |
| OUT%ASCII8 | Register / Immediate |        Outputs a 7 bit ASCII character to terminal.        |
| IN%ASCII8  |       Register       |      Inputs a 7 bit ASCII character into a register.       |
|  OUT%UTF8  | Register / Immediate |           Outputs a UTF-8 character to terminal.           |
|  IN%UTF8   |       Register       |         Inputs a UTF-8 character into a register.          |

## Numerical
These ports are used to operate on numbers or do calculations.

| **Port** |     **Operand1**     |                    **Function**                     |
|:--------:|:--------------------:|:---------------------------------------------------:|
| OUT%RNG  | Register / Immediate | Sets the seed for generating pseudo random numbers. |
|  IN%RNG  |       Register       |   Inputs a pseudo random number into a register.    |

## User Input
These are ports which are aimed at reading the user input in real time.

|![Tip icon]|*These ports should be used to capture user input for games or GUIs as they do not stop execution when reading.*|
| - | - |

|     **Port**     |     **Operand1**     |     **Operand2**     |                                                                      **Function**                                                                      |
|:----------------:|:--------------------:|:--------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------:|
|   IN%KEYBOARD    |       Register       |                      | Inputs the current pressed keyboard key (null if none pressed) into a register.<br>Note this does not support pressing multiple keys at the same time. |
|   OUT%GAMEPAD    | Register / Immediate |                      |                                     Sets which gamepad to read from.<br>This allows multiple gamepads to be used.                                      |
|    IN%GAMEPAD    |       Register       |                      |      Inputs a bit field of the current pressed gamepad keys into a register.<br>Note this supports pressing more than one button simultaneously.       |
|   OUT%MOUSE_X    | Register / Immediate |                      |                                                               Sets the mouse x position.                                                               |
|    IN%MOUSE_X    |       Register       |                      |                                                      Inputs the mouse x position into a register.                                                      |
|   OUT%MOUSE_Y    | Register / Immediate |                      |                                                               Sets the mouse y position.                                                               |
|    IN%MOUSE_Y    |       Register       |                      |                                                      Inputs the mouse y position into a register.                                                      |
|  OUT%MOUSE_POS   | Register / Immediate | Register / Immediate |                                          Sets the mouse x position to operand 1 and y position to operand 2.                                           |
|   IN%MOUSE_POS   |       Register       |       Register       |                                  Inputs the mouse x position into operand 1 and the mouse y position into operand 2.                                   |
|   IN%MOUSE_DX    |       Register       |                      |                                                      Inputs the mouse x velocity into a register.                                                      |
|   IN%MOUSE_DY    |       Register       |                      |                                                      Inputs the mouse y velocity into a register.                                                      |
| OUT%MOUSE_SPEED  | Register / Immediate | Register / Immediate |                                  Inputs the mouse x velocity into operand 1 and the mouse y velocity into operand 2.                                   |
| IN%MOUSE_BUTTONS |       Register       |                      |      Inputs a bit field of the current pressed mouse buttons into a register.<br>Note this supports pressing more than one button simultaneously.      |

## Graphical
These ports are used for drawing simple generic graphics on a pixel screen. If a target CPU supports more types of graphics then they may use their own custom ports to draw them.

|    **Port**     |     **Operand1**     |     **Operand2**     |     **Operand3**     |     **Operand4**     |     **Operand5**     |                                                                                                                         **Function**                                                                                                                          |
|:---------------:|:--------------------:|:--------------------:|:--------------------:|:--------------------:|:--------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|    OUT%WIDTH    | Register / Immediate |                      |                      |                      |                      |                                                                 Sets the screen width.<br>Beware that target CPUs outside of emulators are unlikely to be able to support more than one size.                                                                 |
|    IN%WIDTH     |       Register       |                      |                      |                      |                      |                                                                                                       Reads the screen width in pixels into a register.                                                                                                       |
|   OUT%HEIGHT    | Register / Immediate |                      |                      |                      |                      |                                                                Sets the screen height.<br>Beware that target CPUs outside of emulators are unlikely to be able to support more than one size.                                                                 |
|    IN%HEIGHT    |       Register       |                      |                      |                      |                      |                                                                                                      Reads the screen height in pixels into a register.                                                                                                       |
|    OUT%FILL     | Register / Immediate |                      |                      |                      |                      |                                                                                                  Fills the entire screen with the colour given by operand 1.                                                                                                  |
|    OUT%CLEAR    |                      |                      |                      |                      |                      |                                                                                                                      Clears the screen.                                                                                                                       |
|   OUT%FREEZE    |                      |                      |                      |                      |                      |                                                               Freezes the visible part of the screen.<br>Reading and writing to the screen still works but does not visually update the screen.                                                               |
|  OUT%UNFREEZE   |                      |                      |                      |                      |                      |                                                                              Unfreezes the visible part of the screen.<br>The visual screen now shows what the screen contains.                                                                               |
|   OUT%BUFFER    | Register / Immediate |                      |                      |                      |                      |                Sets the buffer mode.<br>Setting to 0 unfreezes the visible screen.<br>Setting to 1 freezes the visible screen, then clears the screen.<br>Setting to 2 unfreezes the visible screen, then it freezes the visible screen again.                |
|    IN%BUFFER    |       Register       |                      |                      |                      |                      |                                                                                                    Reads the current buffer mode (this can be 0, 1 or 2).                                                                                                     |
| OUT%SCREEN_NUMB | Register / Immediate | Register / Immediate | Register / Immediate | Register / Immediate | Register / Immediate |                    Draws a generic number given by operand 5 at the position pointed to by operand 1 (x coordinate) and operand 2 (y coordinate), using the foreground colour given by operand 3 and background colour given by operand 4.                    |
| OUT%SCREEN_TEXT | Register / Immediate | Register / Immediate | Register / Immediate | Register / Immediate | Register / Immediate |                Draws a generic text character given by operand 5 at the position pointed to by operand 1 (x coordinate) and operand 2 (y coordinate), using the foreground colour given by operand 3 and background colour given by operand 4.                |
|    OUT%PIXEL    | Register / Immediate | Register / Immediate | Register / Immediate |                      |                      |                                                            Draws a pixel at the position pointed to by operand 1 (x coordinate) and operand 2 (y coordinate) using the colour given by operand 3.                                                             |
|    IN%PIXEL     |       Register       | Register / Immediate | Register / Immediate |                      |                      |                                                                       Reads the colour of the pixel pointed to by operand 2 (x coordinate) and operand 3 (y coordinate) into operand 1.                                                                       |
|    OUT%LINE     | Register / Immediate | Register / Immediate | Register / Immediate | Register / Immediate | Register / Immediate |                Draws a line between the position pointed to by operand 1 (first x coordinate) and operand 2 (first y coordinate), and operand 3 (second x coordinate) and operand 4 (second y coordinate) using the colour given by operand 5.                |
|     OUT%BOX     | Register / Immediate | Register / Immediate | Register / Immediate | Register / Immediate |       Register       | Draws a filled box (non-rotated rectangle) between the position pointed to by operand 1 (first x coordinate) and operand 2 (first y coordinate), and operand 3 (second x coordinate) and operand 4 (second y coordinate) using the colour given by operand 5. |

## Audio
These ports are used for interacting with audio. If a target CPU supports more types of audio then they may use their own custom ports to play/listen to them.

|![Tip icon]|*Beware that target CPUs which are being simulated on another system (such as a Minecraft CPU or a CPU running inside a logic sim program) might not be able to accurately measure time for correctly playing audio.<br>This due to the simulation potentially running at inconsistent or unpredictable speeds.*|
| - | - |

| **Port**  |     **Operand1**     |     **Operand2**     |     **Operand3**     |     **Operand4**     |                                                            **Function**                                                            |
|:---------:|:--------------------:|:--------------------:|:--------------------:|:--------------------:|:----------------------------------------------------------------------------------------------------------------------------------:|
| OUT%SOUND | Register / Immediate | Register / Immediate | Register / Immediate | Register / Immediate | Plays a sound using the instrument given by operand 1, the volume by operand 2, the pitch by operand 3 and the length by operand 4 |

## Temporal
These ports interact with time or the speed of the target CPU.

|![Tip icon]|*Beware that target CPUs which are being simulated on another system (such as a Minecraft CPU or a CPU running inside a logic sim program) might not be able to accurately measure time.<br>This due to the simulation potentially running at inconsistent or unpredictable speeds.*|
| - | - |

|   **Port**   |     **Operand1**     |                              **Function**                              |
|:------------:|:--------------------:|:----------------------------------------------------------------------:|
|  IN%RUNTIME  |       Register       | Inputs the time the URCL program has been running for into a register. |
|   OUT%WAIT   | Register / Immediate |            Sets the wait period to the value of operand 1.             |
|   IN%WAIT    |       Register       |  Waits until the wait period is done, then writes 1 into a register.   |
| IN%FRAMETIME |       Register       |   Inputs the time since the screen was last updated into a register.   |

## External
These ports interact with devices outside of the machine running the URCL program.

|  **Port**   |     **Operand1**     |     **Operand2**     |     **Operand3**     |                                                                  **Function**                                                                   |
|:-----------:|:--------------------:|:--------------------:|:--------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------:|
| OUT%STORAGE | Register / Immediate | Register / Immediate | Register / Immediate |          Writes the data in operand 3 to the external storage device on the page given by operand 1 at the address given by operand 2.          |
| IN%STORAGE  |       Register       | Register / Immediate | Register / Immediate | Inputs the data found in an external storage device on the page number given by operand 2 and at the address given by operand 3 into operand 1. |
| OUT%NETWORK | Register / Immediate | Register / Immediate |                      |                                     Writes the data in operand 2 to the network address given by operand 1.                                     |
| IN%NETWORK  |       Register       | Register / Immediate |                      |                         Inputs the data found on the network at the network address given by operand 2 into operand 1.                          |

## Environmental
These are ports which control the execution environment of the URCL program on the target CPU.

|![Tip icon]|*Trying to change the %COLORMODE on a target CPU which does not have a pixel screen will not work.<br>So before using one of these ports - make sure the target CPU supports it.*|
| - | - |

|    **Port**    |     **Operand1**     |                             **Function**                              |
|:--------------:|:--------------------:|:---------------------------------------------------------------------:|
| OUT%COLORMODE  | Register / Immediate |                     Sets the screen colour mode.                      |
|  IN%COLORMODE  |       Register       |         Reads the current screen colour mode into a register.         |
| OUT%SUPPORTED  | Register / Immediate |           Sets the port number to query if it is supported.           |
|  IN%SUPPORTED  |       Register       | Returns 1 if the queried port number is supported. Else it returns 0. |
| OUT%CLOCKSPEED | Register / Immediate |                         Sets the clock speed.                         |
| IN%CLOCKSPEED  |       Register       |            Reads the current clock speed into a register.             |

## Specialised
These are uncommonly used ports which have a specific purpose.

|  **Port**   |     **Operand1**     |                                                        **Function**                                                         |
|:-----------:|:--------------------:|:---------------------------------------------------------------------------------------------------------------------------:|
| OUT%PROFILE | Register / Immediate |                                                   Sets the port profile.                                                    |
| IN%PROFILE  |       Register       | Inputs the current port profile into a register.<br>The port profile is used to support multiple versions of the same port. |

[Tip icon]: Tip_Icon.png
