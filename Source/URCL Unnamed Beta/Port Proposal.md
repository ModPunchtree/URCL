
# **PORTS**
URCL supports official ports as well as custom ports specific to a target CPU.

Ports can be read from or written to using the `IN` or `OUT` instructions as appropriate.

|![Tip icon]|*Official ports can be used in URCL programs without having to be defined. They use the definition given here.*|
| - | - |

|![Tip icon]|*Note that the programmer or target CPU can make up their own ports, and these do not have to follow the official documentation.*<br>*In this case the programmer or target CPU should define what is meant by each port if it is not obvious. A simple comment in the code is typically fine if it is not too complex.*|
| - | - |

All the official ports defined in the URCL documentation all have their own port number. The `%SUPPORTED` port refers to each port using this port number.

|![Tip icon]|*Beware that if the port number is too large to be represented using the number of bits in the `BITS` header - then the `%SUPPORTED` port will not work.*|
| - | - |

Ideally programs should use generic ports where possible as this potentially enables a wider range of target CPUs to run that program.

|![Tip icon]|*Beware that a program using custom ports specific to a target CPU, means that program may not easily be portable to other target CPUs.*|
| - | - |

|**Port Number**|**Port**|**Full Name**|**Port Type**|
| :-: | :-: | :-: | :-: |
|0|%NUMB|Number|Generic|
|1|%TEXT|Text|Generic|
|2|%INT|Integer|Numeric|
|3|%UINT|Unsigned Integer|Numeric|
|4|%BIN|Binary|Numeric|
|5|%HEX|Hexadecimal|Numeric|
|6|%FLOAT|Floating Point|Numeric|
|7|%FIXED|Fixed Point|Numeric|
|8|%RNG|Random Number Generator|Numeric|
|9|%ASCII7|ASCII 7 bit|Text|
|10|%ASCII8|ASCII 8 bit|Text|
|11|%UTF8|UTF-8|Text|
|12|%TEXT_COLOR|Text Colour|Text|
|13|%TEXT_BACKCOLOR|Text Background Colour|Text|
|14|%KEYBOARD|Keyboard|User Input|
|15|%GAMEPAD|Gamepad|User Input|
|16|%MOUSE_X|Mouse X|User Input|
|17|%MOUSE_Y|Mouse Y|User Input|
|18|%MOUSE_POS|Mouse Position|User Input|
|19|%MOUSE_DX|Mouse Delta X|User Input|
|20|%MOUSE_DY|Mouse Delta Y|User Input|
|21|%MOUSE_SPEED|Mouse Speed|User Input|
|22|%MOUSE_BUTTONS|Mouse Buttons|User Input|
|23|%X|X|Graphical|
|24|%Y|Y|Graphical|
|25|%COORD|Coordinate|Graphical|
|26|%COLOR|Colour|Graphical|
|27|%WIDTH|Width|Graphical|
|28|%HEIGHT|Height|Graphical|
|29|%FILL|Fill|Graphical|
|30|%CLEAR|Clear|Graphical|
|31|%FREEZE|Freeze|Graphical|
|32|%UNFREEZE|Unfreeze|Graphical|
|33|%BUFFER|Buffer|Graphical|
|34|%PIXEL|Pixel|Graphical|
|35|%LINE|Line|Graphical|
|36|%BOX|Box|Graphical|
|37|%NOTE|Note|Audio|
|38|%INSTR|Instrument|Audio|
|39|%NLEG|Note Length|Audio|
|40|%VOL|Volume|Audio|
|41|%RUNTIME|Runtime|Temporal|
|42|%WAIT|Wait|Temporal|
|43|%FRAMETIME|Frame Time|Temporal|
|44|%ADDR|Address|Storage|
|45|%BUS|Bus|Storage|
|46|%PAGE|Page|Storage|
|47|%COLORMODE|Colour Mode|Environmental|
|48|%SUPPORTED|Supported|Environmental|
|49|%CLOCKSPEED|Clock Speed|Environmental|
|50|%PROFILE|Profile|Specialised|
|51|%NADDR|Network Address|Specialised|
|52|%NDATA|Network Data|Specialised|

## Generic
These are ports that are purposely ambiguously defined. This enables target CPUs to implement these ports in whatever way is optimal for them.

|![Tip icon]|*A target CPU which has a pixel display may choose to print numbers from %NUMB on its screen, but another target CPU with a seven segment display may choose to use that instead to print the same number.*|
| - | - |

|![Tip icon]|*The Generic ports are all blocking. This means that the target CPU will wait for the port to finish before continuing execution.<br>This means a `IN R1 %NUMB` instruction will stop execution until a number is inputted into register 1.*|
| - | - |

|![Tip icon]|*%NUMB typically refers to an unsigned int and %TEXT typically refers to a single ASCII7 char.<br>Beware that different target CPUs may treat these ports differently.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|IN|Register|%NUMB|Inputs an external generic number into a register.|
|IN|Register|%TEXT|Inputs an external generic text character into a register.|

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|OUT|%NUMB|Register or<br>Immediate|Outputs a generic number.|
|OUT|%TEXT|Register or<br>Immediate|Outputs a generic text character.|

## Numeric
These ports are specialised versions of the %NUMB port. They specify what type of number should be inputted/outputted.

|![Tip icon]|*The Numeric ports are all blocking. This means that the target CPU will wait for the port to finish before continuing execution.*|
| - | - |

|![Tip icon]|*The size of an integer is equal to one word on the target CPU.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|IN|Register|%INT|Inputs an external integer into a register.|
|IN|Register|%UINT|Inputs an external unsigned integer into a register.|
|IN|Register|%BIN|Inputs an external base 2 number into a register.|
|IN|Register|%HEX|Inputs an external base 16 into a register.|
|IN|Register|%FLOAT|Inputs an external floating point number into a register.|
|IN|Register|%FIXED|Inputs an external fixed point number into a register.|
|IN|Register|%RNG|Inputs a pseudo random number into a register.|

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|OUT|%INT|Register or<br>Immediate|Outputs an integer.|
|OUT|%UINT|Register or<br>Immediate|Outputs an unsigned integer.|
|OUT|%BIN|Register or<br>Immediate|Outputs a base 2 number.|
|OUT|%HEX|Register or<br>Immediate|Outputs a base 16 number.|
|OUT|%FLOAT|Register or<br>Immediate|Outputs a floating point number.|
|OUT|%FIXED|Register or<br>Immediate|Outputs a fixed point number.|
|OUT|%RNG|Register or<br>Immediate|Sets the seed for generating pseudo random numbers.|

## Text
These ports are specialised versions of the %TEXT port. They specify what type of text character the value should be.

|![Tip icon]|*The Text ports are all blocking. This means that the target CPU will wait for the port to finish before continuing execution.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|IN|Register|%ASCII7|Inputs an external ASCII 7 bit character into a register.|
|IN|Register|%ASCII8|Inputs an external ASCII 8 bit character into a register.|
|IN|Register|%UTF8|Inputs an external UTF-8 character into a register.|
|IN|Register|%TEXT_COLOR|Reads the currently set text colour into a register.|
|IN|Register|%TEXT_BACKCOLOR|Reads the currently set text background colour into a register.|

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|OUT|%ASCII7|Register or<br>Immediate|Outputs a ASCII 7 bit character.|
|OUT|%ASCII8|Register or<br>Immediate|Outputs a ASCII 8 bit character.|
|OUT|%UTF8|Register or<br>Immediate|Outputs a UTF-8 character.|
|OUT|%TEXT_COLOR|Register or<br>Immediate|Sets the text colour.|
|OUT|%TEXT_BACKCOLOR|Register or<br>Immediate|Sets the text background colour.|

## User Input
These are ports which are aimed at reading the user input in real time.

|![Tip icon]|*The User Input ports are all non-blocking. This means that the target CPU will not wait for the port to finish before continuing execution.<br>This means a `IN R1 %KEYBOARD` instruction will read the current keyboard state into register 1 without stopping execution.*|
| - | - |

|![Tip icon]|*These ports should be used to capture user input for games or GUIs as they do not stop execution when reading.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Operand3**|**Function**|
| :-: | :-: | :-: | :-: | :-: |
|IN|Register|%KEYBOARD||Inputs the current pressed keyboard key (0 if none pressed) into a register.<br>Note this does not support pressing multiple keys at the same time.|
|IN|Register|%GAMEPAD||Inputs a bit field of the current pressed gamepad keys into a register.<br>Note this supports pressing more than one button simultaneously.|
|IN|Register|%MOUSE_X||Inputs the mouse x position into a register.|
|IN|Register|%MOUSE_Y||Inputs the mouse y position into a register.|
|IN|Register|Register|%MOUSE_POS|Inputs the mouse x position into operand 1 and the mouse y position into operand 2.|
|IN|Register|%MOUSE_DX||Inputs the mouse x velocity into a register.|
|IN|Register|%MOUSE_DY||Inputs the mouse y velocity into a register.|
|IN|Register|%MOUSE_SPEED||Inputs the mouse x velocity into operand 1 and the mouse y velocity into operand 2.|
|IN|Register|%MOUSE_BUTTONS||Inputs a bit field of the current pressed mouse buttons into a register.<br>Note this supports pressing more than one button simultaneously.|

|**Instruction**|**Operand1**|**Operand2**|**Operand3**|**Function**|
| :-: | :-: | :-: | :-: | :-: |
|OUT|%GAMEPAD|Register or<br>Immediate||Sets which gamepad to read from.<br>This allows multiple gamepads to be used.|
|OUT|%MOUSE_X|Register or<br>Immediate||Sets the mouse x position.|
|OUT|%MOUSE_Y|Register or<br>Immediate||Sets the mouse y position.|
|OUT|%MOUSE_POS|Register or<br>Immediate|Register or<br>Immediate|Sets the mouse x position to operand 2 and y position to operand 3.|

## Graphical
These ports are used for drawing simple generic graphics on a pixel screen. If a target CPU supports more types of graphics then they may use their own custom ports to draw them.

|![Tip icon]|*The Graphical ports are all blocking. This means that the target CPU will wait for the port to finish before continuing execution.<br>This means a `OUT %LINE` instruction will wait until the line has been drawn before continuing execution.*|
| - | - |

|![Tip icon]|*American spelling must used for port names - to be consistent.*|
| - | - |

|![Tip icon]|*Beware that using %FILL %PIXEL %LINE and %BOX may change the values of %X and %Y depending on how the target CPU chooses to implement these ports.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Operand3**|**Function**|
| :-: | :-: | :-: | :-: | :-: |
|IN|Register|%X||Reads the current screen x coordinate into a register.|
|IN|Register|%Y||Reads the current screen y coordinate into a register.|
|IN|Register|Register|%COORD|Reads the current screen x coordinate into operand 1 and the current screen y coordinate into operand 2.|
|IN|Register|%COLOR||Reads the colour of the pixel pointed to by `%X` and `%Y` into a register.|
|IN|Register|%WIDTH||Reads the screen width in pixels into a register.|
|IN|Register|%HEIGHT||Reads the screen height in pixels into a register.|
|IN|Register|%BUFFER||Reads the current buffer mode (this can be 0, 1 or 2).|

|**Instruction**|**Operand1**|**Operand2**|**Operand3**|**Operand4**|**Operand5**|**Operand6**|**Function**|
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|OUT|%X|Register or<br>Immediate|||||Sets the current screen x coordinate.|
|OUT|%Y|Register or<br>Immediate|||||Sets the current screen y coordinate.|
|OUT|%COORD|Register or<br>Immediate|Register or<br>Immediate||||Sets the current screen coordinate to operand 2 (x coordinate) and operand 3 (y coordinate).|
|OUT|%COLOR|Register or<br>Immediate|||||Draws a pixel at the position pointed to by `%X` and `%Y` using the colour given by operand 2.|
|OUT|%WIDTH|Register or<br>Immediate|||||Sets the screen width.<br>Beware that target CPUs outside of emulators are unlikely to be able to support more than one size.|
|OUT|%HEIGHT|Register or<br>Immediate|||||Sets the screen height.<br>Beware that target CPUs outside of emulators are unlikely to be able to support more than one size.|
|OUT|%FILL|Register or<br>Immediate|||||Fills the entire screen with the colour given by operand 2.|
|OUT|%CLEAR||||||Clears the screen.|
|OUT|%FREEZE||||||Freezes the visible part of the screen.<br>Reading and writing to the screen still works but does not visually update the screen.|
|OUT|%UNFREEZE||||||Unfreezes the visible part of the screen.<br>The visual screen now shows what the screen contains.|
|OUT|%BUFFER|Register or<br>Immediate|||||Sets the buffer mode.<br>Setting to 0 unfreezes the visible screen.<br>Setting to 1 freezes the visible screen, then clears the screen.<br>Setting to 2 unfreezes the visible screen, then it freezes the visible screen again.|
|OUT|%PIXEL|Register or<br>Immediate|Register or<br>Immediate|Register or<br>Immediate|||Draws a pixel at the position pointed to by operand 2 (x coordinate) and operand 3 (y coordinate) using the colour given by operand 4.|
|OUT|%LINE|Register or<br>Immediate|Register or<br>Immediate|Register or<br>Immediate|Register or<br>Immediate|Register or<br>Immediate|Draws a line between the position pointed to by operand 2 (first x coordinate) and operand 3 (first y coordinate), and operand 4 (second x coordinate) and operand 5 (second y coordinate) using the colour given by operand 6.|
|OUT|%BOX|Register or<br>Immediate|Register or<br>Immediate|Register or<br>Immediate|Register or<br>Immediate|Register or<br>Immediate|Draws a filled box (non-rotated rectangle) between the position pointed to by operand 2 (first x coordinate) and operand 3 (first y coordinate), and operand 4 (second x coordinate) and operand 5 (second y coordinate) using the colour given by operand 6.|

## Audio
These ports are used for playing simple audio tones. If a target CPU supports more types of audio then they may use their own custom ports to play them.

|![Tip icon]|*The Audio ports are all non-blocking. This means that the target CPU will not wait for the port to finish before continuing execution.*|
| - | - |

|![Tip icon]|*Beware that target CPUs which are being simulated on another system (such as a Minecraft CPU or a CPU running on a logic sim program) might not be able to accurately measure time for correctly playing audio.<br>This due to the simulation potentially running at inconsistent or unpredictable speeds.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|IN|Register|%NOTE|Inputs the value most recently outputted to the %NOTE port into a register.|
|IN|Register|%INSTR|Inputs the value most recently outputted to the %INSTR port into a register.|
|IN|Register|%NLEG|Inputs the value most recently outputted to the %NLEG port into a register.|
|IN|Register|%VOL|Reads the current volume level into a register.|

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|OUT|%NOTE|Register or<br>Immediate|Sets the pitch.|
|OUT|%INSTR|Register or<br>Immediate|Sets the instrument.|
|OUT|%NLEG|Register or<br>Immediate|Plays a sound for the length specified by operand 2.|
|OUT|%VOL|Register or<br>Immediate|Sets the volume.|

## Temporal
These ports interact with time or the speed of the target CPU.

|![Tip icon]|*The %RUNTIME and %FRAMETIME ports are non-blocking. This means that the target CPU will not wait for the port to finish before continuing execution.*|
| - | - |

|![Tip icon]|*The %WAIT port is blocking. This means that the target CPU will wait for the port to finish before continuing execution.*|
| - | - |

|![Tip icon]|*Beware that target CPUs which are being simulated on another system (such as a Minecraft CPU or a CPU running on a logic sim program) might not be able to accurately measure time.<br>This due to the simulation potentially running at inconsistent or unpredictable speeds.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|IN|Register|%RUNTIME|Inputs the time the URCL program has been running for into a register.|
|IN|Register|%WAIT|Waits until the wait period is done, then writes 1 into a register.|
|IN|Register|%FRAMETIME|Inputs the time since the screen was last updated into a register.|

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|OUT|%WAIT|Register or<br>Immediate|Sets the wait period to the value of operand 2.|

## Storage
The Storage ports control external mass storage devices.

|![Tip icon]|*The Storage ports are all blocking. This means that the target CPU will wait for the port to finish before continuing execution.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|IN|Register|%ADDR|Inputs the value most recently outputted to the %ADDR port into a register.|
|IN|Register|%BUS|Inputs the data found in the external storage device at the address in the %ADDR port and on the page number in the %PAGE port into a register.|
|IN|Register|%PAGE|Inputs the value most recently outputted to the %PAGE port into a register.|

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|OUT|%ADDR|Register or<br>Immediate|Sets the address of the external storage device.|
|OUT|%BUS|Register or<br>Immediate|Writes the value in operand 2 to the external storage device address in the %ADDR port on the page in the %PAGE port.|
|OUT|%PAGE|Register or<br>Immediate|Sets the page number of the external storage device.|

## Environmental
These are ports which control the execution environment of the URCL program on the target CPU.

|![Tip icon]|*The %CLOCKSPEED port is non-blocking. This means that the target CPU will not wait for the port to finish before continuing execution.*|
| - | - |

|![Tip icon]|*The %COLORMODE and %SUPPORTED ports are blocking. This means that the target CPU will wait for the port to finish before continuing execution.*|
| - | - |

|![Tip icon]|*Trying to change the %COLORMODE on a target CPU which does not have a pixel screen will not work.<br>So before using one of these ports - make sure the target CPU supports it.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|IN|Register|%COLORMODE|Reads the current screen colour mode into a register.|
|IN|Register|%SUPPORTED|Returns 1 if the queried port number is supported. Else it returns 0.|
|IN|Register|%CLOCKSPEED|Reads the current clock speed into a register.|

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|OUT|%COLORMODE|Register or<br>Immediate|Sets the screen colour mode.|
|OUT|%SUPPORTED|Register or<br>Immediate|Sets the port number to query if it is supported.|
|OUT|%CLOCKSPEED|Register or<br>Immediate|Sets the clock speed.|

Specialised:  
These are uncommonly used ports which have a specific purpose.

|![Tip icon]|*The Specialised ports are entirely dependent on the target CPU to define if they are blocking or non-blocking.<br>Before using these ports, make sure you know exactly how the target CPU will interpret these.*|
| - | - |

|![Tip icon]|*Some of the Specialised ports are blocking and others are non-blocking.<br>The description for each port specifies which if it is blocking or non-blocking.*|
| - | - |

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|IN|Register|%PROFILE|Inputs the current port profile into a register.<br>The port profile is used to support multiple versions of the same port. Such as having multiple screens which need their own %X %Y ports.<br>This port is blocking.|
|IN|Register|%NADDR|Reads the current network address into a register.<br>This port is blocking.|
|IN|Register|%NDATA|Reads network data into a register.<br>This port is blocking.|

|**Instruction**|**Operand1**|**Operand2**|**Function**|
| :-: | :-: | :-: | :-: |
|OUT|%PROFILE|Register or<br>Immediate|Sets the port profile.<br>This port is blocking.|
|OUT|%NADDR|Register or<br>Immediate|Sets the network address.<br>This port is blocking.|
|OUT|%NDATA|Register or<br>Immediate|Sends network data.<br>This port is blocking.|

[Tip icon]: Tip_Icon.png
