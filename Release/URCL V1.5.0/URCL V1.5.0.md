![URCL Logo.](URCL_Logo.png)![File icon for .urcl files.](URCL_File_Icon.png)

# **URCL V1.5.0**
**OFFICIAL DOCUMENTATION**

**Written by Ben Aitken (Mod Punchtree) – 17<sup>th</sup> Nov 2023**

# <a name="_toc112787800"></a>**ABSTRACT**

|![Tip icon]|*URCL stands for: Universal Reduced Computer Language*|
| - | - |

URCL is a simple universal intermediate language. It is designed to be as similar as possible to common RISC assembly in order to make it as easy as possible to translate to any specific assembly language. This documentation will go into greater depth than the old Google Sheet documentation.

# <a name="_toc112787801"></a>**CONTENTS**
* [Abstract](#_toc112787800)
* [Contents](#_toc112787801)
* [Introduction](#_toc112787802)
    * [Links](#_toc112787803)
* [Overview](#_toc112787804)
    * [Source Files](#_toc112787805)
        * [URCL Source Files](#_toc112787806)
    * [General Syntax](#_toc112787807)
        * [General Layout](#_toc112787808)
        * [Prefixes](#_toc112787809)
        * [Comments](#_toc112787810)
        * [Macros](#_toc112787811)
        * [Numbers](#_toc112787812)
        * [Relative Numbers](#_toc112787813)
        * [Defined Immediate Values](#_toc112787814)
        * [ASCII Characters](#_toc112787815)
        * [Whitespace](#_toc112787816)
    * [Zero Register](#_toc112787817)
    * [Program Counter](#_toc112787818)
    * [Headers](#_toc112787819)
        * [CPU Word Length](#_toc112787820)
        * [Minimum Number of Registers](#_toc112787821)
        * [Minimum Heap Space](#_toc112787822)
        * [Instruction Storage Architecture](#_toc112787823)
        * [Minimum Stack Size](#_toc112787824)
    * [Define Words](#_toc112787825)
        * [Define Word Definition](#_toc112787826)
        * [Define Word Usage](#_toc112787827)
    * [Labels](#_toc112787828)
        * [Label Definition](#_toc112787829)
        * [Label Usage](#_toc112787830)
    * [Memory Map](#_toc112787831)
        * [Heap](#_toc112787832)
        * [Stack](#_toc112787833)
        * [Stack Pointer](#_toc112787834)
* [Instructions](#_toc112787835)
    * [Core Instructions](#_toc112787836)
        * [ADD](#_toc112787837)
        * [RSH](#_toc112787838)
        * [LOD](#_toc112787839)
        * [STR](#_toc112787840)
        * [BGE](#_toc112787841)
        * [NOR](#_toc112787842)
        * [IMM](#_toc112787843)
    * [Basic Instructions](#_toc112787844)
        * [ADD](#_toc112787845)
        * [RSH](#_toc112787846)
        * [LOD](#_toc112787847)
        * [STR](#_toc112787848)
        * [BGE](#_toc112787849)
        * [NOR](#_toc112787850)
        * [SUB](#_toc112787851)
        * [JMP](#_toc112787852)
        * [MOV](#_toc112787853)
        * [NOP](#_toc112787854)
        * [IMM](#_toc112787855)
        * [LSH](#_toc112787856)
        * [INC](#_toc112787857)
        * [DEC](#_toc112787858)
        * [NEG](#_toc112787859)
        * [AND](#_toc112787860)
        * [OR](#_toc112787861)
        * [NOT](#_toc112787862)
        * [XNOR](#_toc112787863)
        * [XOR](#_toc112787864)
        * [NAND](#_toc112787865)
        * [BRL](#_toc112787866)
        * [BRG](#_toc112787867)
        * [BRE](#_toc112787868)
        * [BNE](#_toc112787869)
        * [BOD](#_toc112787870)
        * [BEV](#_toc112787871)
        * [BLE](#_toc112787872)
        * [BRZ](#_toc112787873)
        * [BNZ](#_toc112787874)
        * [BRN](#_toc112787875)
        * [BRP](#_toc112787876)
        * [PSH](#_toc112787877)
        * [POP](#_toc112787878)
        * [CAL](#_toc112787879)
        * [RET](#_toc112787880)
        * [HLT](#_toc112787881)
        * [CPY](#_toc112787882)
        * [BRC](#_toc112787883)
        * [BNC](#_toc112787884)
    * [Complex Instructions](#_toc112787885)
        * [MLT](#_toc112787886)
        * [DIV](#_toc112787887)
        * [MOD](#_toc112787888)
        * [BSR](#_toc112787889)
        * [BSL](#_toc112787890)
        * [SRS](#_toc112787891)
        * [BSS](#_toc112787892)
        * [SETE](#_toc112787893)
        * [SETNE](#_toc112787894)
        * [SETG](#_toc112787895)
        * [SETL](#_toc112787896)
        * [SETGE](#_toc112787897)
        * [SETLE](#_toc112787898)
        * [SETC](#_toc112787899)
        * [SETNC](#_toc112787900)
        * [LLOD](#_toc112787901)
        * [LSTR](#_toc112787902)
        * [SDIV](#_toc112787903)
        * [SBRL](#_toc112787904)
        * [SBRG](#_toc112787905)
        * [SBLE](#_toc112787906)
        * [SBGE](#_toc112787907)
        * [SSETL](#_toc112787908)
        * [SSETG](#_toc112787909)
        * [SSETLE](#_toc112787910)
        * [SSETGE](#_toc112787911)
        * [ABS](#_toc112787912)
    * [I/O Instructions](#_toc112787913)
        * [IN](#_toc112787914)
        * [OUT](#_toc112787915)
* [Instruction Translations](#_toc112787916)
    * [Basic Instruction Translations](#_toc112787917)
        * [ADD](#_toc112787918)
        * [RSH](#_toc112787919)
        * [LOD](#_toc112787920)
        * [STR](#_toc112787921)
        * [BGE](#_toc112787922)
        * [NOR](#_toc112787923)
        * [SUB](#_toc112787924)
        * [JMP](#_toc112787925)
        * [MOV](#_toc112787926)
        * [NOP](#_toc112787927)
        * [IMM](#_toc112787928)
        * [LSH](#_toc112787929)
        * [INC](#_toc112787930)
        * [DEC](#_toc112787931)
        * [NEG](#_toc112787932)
        * [AND](#_toc112787933)
        * [OR](#_toc112787934)
        * [NOT](#_toc112787935)
        * [XNOR](#_toc112787936)
        * [XOR](#_toc112787937)
        * [NAND](#_toc112787938)
        * [BRL](#_toc112787939)
        * [BRG](#_toc112787940)
        * [BRE](#_toc112787941)
        * [BNE](#_toc112787942)
        * [BOD](#_toc112787943)
        * [BEV](#_toc112787944)
        * [BLE](#_toc112787945)
        * [BRZ](#_toc112787946)
        * [BNZ](#_toc112787947)
        * [BRN](#_toc112787948)
        * [BRP](#_toc112787949)
        * [PSH](#_toc112787950)
        * [POP](#_toc112787951)
        * [CAL](#_toc112787952)
        * [RET](#_toc112787953)
        * [HLT](#_toc112787954)
        * [CPY](#_toc112787955)
        * [BRC](#_toc112787956)
        * [BNC](#_toc112787957)
    * [Complex Instruction Translations](#_toc112787958)
        * [MLT](#_toc112787959)
        * [DIV](#_toc112787960)
        * [MOD](#_toc112787961)
        * [BSR](#_toc112787962)
        * [BSL](#_toc112787963)
        * [SRS](#_toc112787964)
        * [BSS](#_toc112787965)
        * [SETE](#_toc112787966)
        * [SETNE](#_toc112787967)
        * [SETG](#_toc112787968)
        * [SETL](#_toc112787969)
        * [SETGE](#_toc112787970)
        * [SETLE](#_toc112787971)
        * [SETC](#_toc112787972)
        * [SETNC](#_toc112787973)
        * [LLOD](#_toc112787974)
        * [LSTR](#_toc112787975)
        * [SDIV](#_toc112787976)
        * [SBRL](#_toc112787977)
        * [SBRG](#_toc112787978)
        * [SBLE](#_toc112787979)
        * [SBGE](#_toc112787980)
        * [SSETL](#_toc112787981)
        * [SSETG](#_toc112787982)
        * [SSETLE](#_toc112787983)
        * [SSETGE](#_toc112787984)
        * [ABS](#_toc112787985)
* [Ports](#_toc112787986)
* [Code Faults](#_toc112787987)
    * [Pre-Runtime Faults](#_toc112787988)
        * [Invalid Number of Operands](#_toc112787989)
        * [Invalid Operand Types](#_toc112787990)
        * [Unrecognised Identifier](#_toc112787991)
        * [Unsupported Number of Registers](#_toc112787992)
        * [Unsupported Heap Size](#_toc112787993)
        * [Unsupported Stack Size](#_toc112787994)
        * [Invalid Label Name](#_toc112787995)
        * [Duplicate Label Definition](#_toc112787996)
    * [Runtime Faults](#_toc112787997)
        * [Non-Instruction Execution](#_toc112787998)
        * [Stack Underflow](#_toc112787999)
        * [Stack Overflow](#_toc112788000)
        * [Invalid RAM Location](#_toc112788001)
* [Interpreting URCL](#_toc112788002)
    * [Bitwise Representation](#_toc112788003)
* [Example Programs](#_toc112788004)
    * [Simple Fibonacci](#_toc112788005)
    * [FizzBuzz](#_toc112788006)
    * [Bubble Sort](#_toc112788007)
* [Acknowledgements](#_toc112788008)
    * [Biggest Contributors](#_toc112788009)

# <a name="_toc112787802"></a>**INTRODUCTION**
URCL first started with Minecraft CPUs and has also been called Universal Redstone Computer Language. However, applications for URCL are not limited to only Minecraft, as it can be applied to a wide range of CPUs with any ISA (Instruction Set Architecture).

CPUs which are compatible with URCL can make use of the tools built for URCL. These tools include emulators and high-level language compilers. Programs which are written in URCL can also be shared between any other URCL compatible CPU regardless of the ISAs of the CPUs.
## <a name="_toc112787803"></a>**Links**
**URCL Official Documentation Repository:**

<https://github.com/ModPunchtree/URCL>

|![Tip icon]|*Go here to find the most up to date version of the official URCL documentation.*|
| - | - |

**URCL Discord:**  
<https://discord.gg/Nv8jzWg5j8>

**URCX Emulator:**  
<https://github.com/BramOtte/urcl-explorer>

|![Tip icon]|*This is a URCL emulator that runs directly in the browser.*|
| - | - |

# <a name="_toc112787804"></a>**OVERVIEW**
## <a name="_toc112787805"></a>**Source Files**
### <a name="_toc112787806"></a>***URCL Source Files***
All URCL code should be contained in “.urcl” files. These are plain text files. The name of the file can be any string of letters, numbers, and underscore.

|![Tip icon]|*To edit URCL code it is recommended that VSCode is used along with the “URCL & B Syntax Highlighter” extension by RedCMD on the VSCode marketplace.*|
| - | - |

|![Tip icon]|*To directly emulate URCL code it is recommended that the URCX Emulator by Bram is used.*<br>*URCX can be found here: [https://github.com/BramOtte/urcl-explorer](https://github.com/BramOtte/urcl-explorer)*<br>*Or it can be accessed using the URCX discord bot in the #urcl-bot channel in the URCL Discord server.*|
| - | - |

## <a name="_toc112787807"></a>**General Syntax**
### <a name="_toc112787808"></a>***General Layout***
All URCL instructions contain an Identifier as well as Sources and a Destination. The Identifier is simply the name of the instruction. Sources specify where data should be fetched from, and the Destination specifies where the result of the instruction should be written to.

URCL instructions generally follow a three operand format. This means that there are three or fewer operands in each instruction.

In written form, the instructions take the format:

    Identifier Destination Source1 Source2

For example:

    ADD R1 R2 R3

|![Tip icon]|*Add the contents of register 2 to the contents of register 3. Then write result into register 1.*|
| - | - |

All URCL instructions are atomic and are fully self-contained.

Atomic means that instructions are executed one at a time sequentially, and the next instruction does not start until the previous has finished.

Self-contained means that each instruction can be executed without any external information outside of the sources specified by the instruction itself. This means that the exact same instruction will always do the exact same thing regardless of the current state of the CPU.

URCL instructions are designed to be translated one at a time into the target CPU’s assembly.

This means that any URCL program can be translated easily, provided each instruction has an equivalent translation on the target CPU.

|![Tip icon]|*URCL uses a load-store architecture.*<br>*Which means that values must be loaded from the RAM into the registers in order to be used. Then the results may be stored back into the RAM.*|
| - | - |

### <a name="_toc112787809"></a>***Prefixes***
There are prefixes for general purpose registers, memory, labels, relative numbers, and ports.

#### *Registers*
Registers are prefixed with either `R` or `$`.

For example:  
`R1` or `$1` refer to general purpose register 1.

#### *Memory*
Memory locations are prefixed with either `M` or `#`.

For example:  
`M0` or `#0` refer to memory location 0.

|![Tip icon]|*Note that “memory” here does not refer to the entire RAM space, it only refers to the Heap which is later described in the Memory Map section.*|
| - | - |

|![Tip icon]|*If memory locations are used in an instruction which is not LOD, STR, LLOD or LSTR then it gets translated to an immediate value which points to that memory location.*|
| - | - |

#### *Labels*
Labels are prefixed with **`.`**.

For example:  
`.test` refers to the label called “test”.

#### *Relative Numbers*
Relative Numbers are prefixed with `~+` or `~-`.

For example:  
`~+2` is a relative number that is positive 2.

#### *Ports*
Ports are prefixed with `%`. For example:

`%TEXT` refers to a port called “TEXT”

### <a name="_toc112787810"></a>***Comments***
Comments in URCL are the same as comments in C. Line comments are denoted using `//`. Multi-line comments are denoted using `/*` and `*/`.

For example:

    // this comment is a line comment.

    /*
    this comment
    is a multi-line
    comment.
    */

### <a name="_toc112787811"></a>***Macros***
All macros are prepended with `@`.

For example:

    @DEFINE TEST 2

|![Tip icon]|*Individual macros are not defined in URCL as they are completely up to the particular URCL interpreter to define. This is to enable different interpreters to define macros to suit their own needs.*|
| - | - |

### <a name="_toc112787812"></a>***Numbers***
Numbers that have no prefix are in base 10, such as a number used as an immediate value. For example:

`IMM R1 5` in this example the `5` is being used as an immediate value and it has no prefix so it will be interpreted as being in base 10.

Base 16 and base 2 numbers can also be used but they must be prepended with 0x and 0b respectively. For example:

`IMM R1 0x5` the `0x5` will be interpreted as a base 16 value.

`IMM R1 0b101` the `0b101` will be interpreted as a base 2 value.

|![Tip icon]|*The example instruction in the previous 3 examples all load an immediate value of 5, into register 1.*|
| - | - |

Base 8 numbers are prefixed with 0o. Numbers that are prefixed with 0 will be treated as base 10 numbers.

|![Tip icon]|*Base 8 numbers are rarely used, so check they are supported by the target before using them.*|
| - | - |

### <a name="_toc112787813"></a>***Relative Numbers***
Relative numbers are used to specify the address of an instruction, relative to the current instruction. These are values are prefixed with a `~+` or a `~-`. For example:

`JMP ~+5` the `~+5` refers to the URCL instruction 5 ahead of the current instruction.

|![Tip icon]|*A relative value of `~+0` or `~-0` refers to the address of the current instruction.*|
| - | - |

|![Tip icon]|*Relative values must be converted into labels before being translated.*|
| - | - |

### <a name="_toc112787814"></a>***Defined Immediate Values***
Defined immediate values are values which are directly translated into an immediate value before translating the URCL code into the target assembly. All defined immediate values are prepended with a `@`.

The following table contains all the defined immediate values:

|**Defined Immediate Value**|**Full Name**|**Value**|
| :-: | :-: | :-: |
|`@BITS`|Bits|Equal to the value of the BITS header|
|`@MINREG`|Minimum registers|Equal to the value of the MINREG header|
|`@MINHEAP`|Minimum heap|Equal to the value of the MINHEAP header|
|`@MINSTACK`|Minimum stack|Equal to the value of the MINSTACK header|
|`@HEAP`|Heap|Equal to the maximum size of the heap (where the stack is empty, and the heap occupies all available space in the RAM)Note this is specific to the target CPU instead of the URCL program|
|`@MSB`|Most significant bit|Equal to a binary value with only the most significant bit active (128 in an 8 bit program)|
|`@SMSB`|Signed most significant bit|Equal to a binary value with only the second most significant bit active (64 in an 8 bit program)|
|`@MAX`|Maximum|Equal to a binary value with all bits active (255 in an 8 bit program)|
|`@SMAX`|Signed maximum|Equal to a binary value with all bits active except the most significant bit (127 in an 8 bit program)|
|`@UHALF`|Upper half|Equal to a binary value with all bits greater than or equal to 2BITS2 active (240 in an 8 bit program)|
|`@LHALF`|Lower half|Equal to a binary value with all bits less than 2BITS2 active (15 in an 8 bit program)|

|![Tip icon]|*For odd number bit widths, the Lower half will contain the middle bit and the Upper half will not.*|
| - | - |

### <a name="_toc112787815"></a>***ASCII Characters***
ASCII Characters In the code must enclosed using `'`. These characters are directly translated into an immediate value (based on 7 bit ASCII) before being translated from URCL code into the target assembly.

For example:  
`'C'` would become an immediate value of 67.  
`'5'` would become an immediate value of 53.

When translating characters into immediate values, refer to:  
<https://montcs.bloomu.edu/Information/Encodings/ascii-7.html>

### <a name="_toc112787816"></a>***Whitespace***
All groups of spaces in URCL are treated as a single space. This means that multiple spaces can be used, and code can be indented however much the programmer wants while still being valid.

However, newlines are important as these mark where one instruction ends and the next begins. This means that multiple instructions cannot be put on the same line. Empty lines will be ignored though, meaning the programmer can have as many empty lines in between their instructions as they like.

|![Tip icon]|*The whitespace should be used to make the code as legible as possible.*|
| - | - |

## <a name="_toc112787817"></a>**Zero Register**
The zero register is a register that cannot be overwritten and always reads 0. The zero register is referred to in the same way as any other general purpose register. So, `R0` and `$0` both refer to register zero.

If the zero register is specified as a source operand to in an instruction, then it is the same as using an immediate value of zero.

If the zero register is specified as the destination operand in an instruction, then the output of the instruction is simply discarded.

|![Tip icon]|*In most circumstances it is advisable that the zero register is never used as a destination as this is the same as doing nothing in most instructions.*|
| - | - |

## <a name="_toc112787818"></a>**Program Counter**
The program counter is a register that points to the beginning of the current instruction. The program counter in URCL can be read from in the exact same way that any other general purpose register is read.

The program counter is referred to using `PC`. For example:

`PSH PC` this pushes the value currently in the program counter onto the stack.

|![Tip icon]|*Reading or writing to the program counter directly should be avoided, if possible, as some target CPUs may struggle to translate this code if the program counter cannot be accessed directly.* |
| - | - |

## <a name="_toc112787819"></a>**Headers**
Headers contain information which tells the URCL interpreter the required specific parameters for running a program. The headers can also allow you to see if a program is compatible with a target CPU.

### <a name="_toc112787820"></a>***CPU Word Length***
URCL assumes that the target CPU uses the same word length for everything. This means that an 8 bit CPU can have a maximum of 256 memory locations, 256 general purpose registers and any value larger than 8 bits in the code would be truncated to make it 8 bits.

The word length is specified on a per-program basis, this means that every URCL program must specify the word length it runs at. This is done using the `BITS` header. For example:

`BITS == 8` this specifies that the word length must be exactly 8 bits for this program.

`BITS >= 8` this specifies that the word length can be 8 or more bits.

`BITS <= 8` this specifies that the word length can be 8 or fewer bits.

|![Tip icon]|*Most programs will only run at a single word length, so >= and <= are rarely used outside of libraries.*|
| - | - |

|![Tip icon]|*If the BITS header is missing, then the program should be assumed to be 8 bit.*|
| - | - |

|![Tip icon]|*If the BITS header is missing the “==” or “>=” or “<=” then it is assumed to be “==”.*<br>*So “BITS 8” is the same as “BITS == 8”.*|
| - | - |

### <a name="_toc112787821"></a>***Minimum Number of Registers***
The number of registers that can be used in URCL is fixed and each program needs to specify the minimum number of general purpose registers it requires. This is done using the MINREG header. 

For example:  
`MINREG 4` this specifies that this program requires a minimum of 4 general purpose registers which means that any CPU at least 4 general purpose registers can run the program (provided it meets all other requirements).

|![Tip icon]|*If the MINREG header is missing, then the assumed value is 8.*|
| - | - |

### <a name="_toc112787822"></a>***Minimum Heap Space***
The minimum number of words of heap space a program needs is specified using the `MINHEAP` header.

For example:  
`MINHEAP 16` this specifies that this program needs 16 words of heap space to run.

|![Tip icon]|*Note that the Heap does not refer to the entire RAM space. The Heap is described in more detail in the Memory Map section.*|
| - | - |

|![Tip icon]|*If the MINHEAP header is missing, then the assumed value is 16.*|
| - | - |

### <a name="_toc112787823"></a>***Instruction Storage Architecture***
There are two ways that instructions can be stored on a target CPU. The instructions can be stored in the same RAM space that the program runs in (for example von Neumann architecture) or the instructions can be stored in a separate space which cannot be accessed while the program is running (for example Harvard architecture).

URCL programs which store data inside of the instructions will only work if the instructions are stored in the same space that the program is running in. So, it is important that programs specify which storage architecture they require. This is done using the `RUN` header.

For example:  
`RUN RAM` specifies that the instructions are stored in the same space the program runs in.  
`RUN ROM` specifies that the instructions are not stored in the same space the program runs in.

|![Tip icon]|*If the RUN header is missing, then the assumed value is RUN ROM.*|
| - | - |

### <a name="_toc112787824"></a>***Minimum Stack Size***
Programs can specify the minimum number of words that the stack must be able to hold in order to run a program. This is done using the `MINSTACK` header. For example:

`MINSTACK 32` specifies that the stack must be able to hold at least 32 values to run this program.

|![Tip icon]|*If the MINSTACK header is missing, then the assumed value is 8.*|
| - | - |

|![Tip icon]|*The stack is explained further in the Memory Map section.*|
| - | - |

|![Tip icon]|*Headers can be located anywhere within a program, but they should be at the very top to make it clearer to anyone reading the code.*|
| - | - |

## <a name="_toc112787825"></a>**Define Words**
Define words are predefined values that exist inside of the RAM/ROM space where the URCL program is stored. In both RUN RAM and RUN ROM programs these values can freely be read and written to in the same way as any other value in the heap.

These are useful for storing predefined arrays, strings, or lookup tables within a URCL program.

### <a name="_toc112787826"></a>***Define Word Definition***
Defined words are created by writing `DW` followed by a value. The value must be able to fit in a single word (so, the value must be between 0 and 255 in an 8 bit program).

For example:

    DW 0x45

This defines a value of “0x45” directly inside of the URCL program.

Arrays of values can also be defined by writing `DW` followed by an array of values enclosed with square braces `[` and `]`.

For example:

    DW [0 1 2 3]

This defines 4 sequential values. The first is 0, the second is 1, the third is 2 and the final value is 3.

The above example is identical to:

    DW 0
    DW 1
    DW 2
    DW 3

Where each value inside of the array is a single, separate defined value.

|![Tip icon]|*Note that the order the values in the array are defined, starts with the first item in the array. The order must not be changed when translating to the target.*|
| - | - |

|![Tip icon]|*Defined values that are in series (such as an array) must be stored in adjacent RAM address values in the target CPU. This is so that any value in the array can be accessed by adding its index to the address of the first value.*|
| - | - |

### <a name="_toc112787827"></a>***Define Word Usage***
Defined words can be pointed to using relative values or labels.

For example:

    .test2
        DW 0x45

The label “test2” points to the defined value of “0x45”.

Values inside of an array can be accessed by adding the array index to the address value of the first item in the array.

For example:

    .test3
        DW 0
        DW 1

The second defined value (1) can be accessed by adding 1 the “test3” label, then reading/writing to that address. So:

    LLOD R1 .test3 1

This will load the value located at the address value pointed to by “test3” plus one, into register one.
## <a name="_toc112787828"></a>**Labels**
Labels point towards a particular memory or instruction location. Labels in URCL work similar to labels in most assembly languages.
### <a name="_toc112787829"></a>***Label Definition***
Labels are defined by writing `.` followed by the name of the label on a line. That label then points to the instruction or data contained in the next line. The label name must be unique and can be made of string of letters, numbers and underscore.

For example:

    .test
        ADD R1 R2 R3

This defines the label “test”, and this label points to the instruction: `ADD R1 R2 R3`.

Labels can also point to data that is stored inside of the instructions as defined values.

For example:

    .test2
        DW 0x45

This defines the label “test2”, and this points to the defined value “0x45” which is located inside of the instructions.

|![Tip icon]|*DW means “Define Word” and it is used to put one word of data into the instructions.*|
| - | - |

|![Tip icon]|*Since DW values are located in the instructions there is a risk of executing these as instructions. This should be avoided as this can cause undefined behaviour in the target CPU.*<br>*This particular fault is defined as “Non-Instruction Execution”.*|
| - | - |

### <a name="_toc112787830"></a>***Label Usage***
Once defined, labels can be used in the code as source operands. They act the same as immediate values as a label is simply an immediate value which points to the address it was defined at. For example:

`JMP .test` which branches to the location of the label “test”.

|![Tip icon]|*Labels are converted to immediate values after being translated to the target CPUs assembly code.*<br>*This means that they can be translated in the exact same way as an immediate value would.*|
| - | - |

`ADD R1 .test 1` which adds 1 to the location of the label “test”.

|![Tip icon]|*Since the size of the instructions on the target CPU can be bigger than one word, adding 1 to a label which points at an instruction does not make that label point to the next instruction.*<br>*Labels can only be added to or subtracted from if that label points to DW values as these are guaranteed to occupy 1 word per value, regardless of the target CPU.*|
| - | - |

## <a name="_toc112787831"></a>**Memory Map**
![URCL memory map for the working RAM.](Memory_Map.png)

- Normal memory values should be prepended with `M` or `#`.
- Normal memory values do not use an absolute RAM address, instead they are relative to the start of the Heap.
- M0 points to the start of the Heap.
- If a memory address is specified without being prepended with `M` or `#` then it will be treated as an absolute address.
- The stack pointer must be stored in a dedicated general purpose register.

The RAM layout depends on the instruction storage architecture specified using the RUN header.
### <a name="_toc112787832"></a>***Heap***
The heap either starts at location zero in a RUN ROM program or it starts at the first available location after the space that the program itself occupies in a RUN RAM program. Then the heap in both cases expands upwards.

The Heap is where M and # prepended values go.

|![Tip icon]|*There is no limit to the size of the Heap, other than the total size of the RAM.*|
| - | - |

The literal RAM address of M or # prepended values in a RUN RAM program requires an offset to be added. The offset is equal to the location of M0. So, the location of MX is M0 + X which applies to any memory address.

|![Tip icon]|*Knowing the location of M0 is important when translating URCL to the target CPU’s assembly.*|
| - | - |

### <a name="_toc112787833"></a>***Stack***
The stack always starts at the top of the RAM (the highest address value) and expands downwards. This is a LIFO stack.

|![Tip icon]|*There is no limit to the size of the Stack, other than the total size of the RAM.*|
| - | - |

|![Tip icon]|*While the Heap and Stack can be any size, they must **never** cross over each other. If they crossed over each other, they would overwrite each other.*<br>*This particular fault is defined as “Stack Overflow”.*|
| - | - |

### <a name="_toc112787834"></a>***Stack Pointer***
The stack pointer points to the final item on the stack, rather than the next available space. When an item is added to the stack the stack pointer is decremented by 1, and when an item is removed from the stack the stack pointer is incremented by 1.

The stack pointer in URCL must be stored in a dedicated general purpose register. This means it can be read and written to in the same way as any other register. To specify the stack pointer register, `SP` is used. For example:

`MOV R1 SP` this instruction reads from the stack pointer register.

|![Tip icon]|*Modifying the stack pointer directly is potentially dangerous as it can become out of sync to the stack. So, avoid doing this if it is not necessary.*|
| - | - |

# <a name="_toc112787835"></a>**INSTRUCTIONS**

|![Tip icon]|*This section will define all the instructions within URCL*|
| - | - |

There are two main categories of instructions. These are “Basic” and “Complex”. There are also “Core” instructions which are a specific subset of the Basic instructions which are the minimum instructions required for a CPU to be 100% compatible with URCL.

All Complex instructions can be translated to Basic instructions and all Basic instructions can be translated to Core instructions. This means that if a target CPU can translate the Core instructions it can translate all URCL instructions.

Note that all instructions are unsigned, unless otherwise stated.
## <a name="_toc112787836"></a>**Core Instructions**

|![Tip icon]|*A CPU must be able to translate all these instructions to be 100% compatible with URCL*|
| - | - |

There are 7 Core instructions.
### <a name="_toc112787837"></a>***ADD***
#### *Full Name*
Add
#### *Description*
The ADD instruction adds two values together, then it stores the result in a register.

|![Tip icon]|*The input values must be registers in the core instructions.*|
| - | - |

#### *Operands*
ADD requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>ADD R1 R2 R3</pre>|
#### *Code Examples*
    ADD R1 R1 R2

This instruction adds the value in register 1 to the value in register 2, then it stores the result into register 1.

### <a name="_toc112787838"></a>***RSH***
#### *Full Name*
Right shift
#### *Description*
The RSH instruction does a bitwise right shift of a value, then it stores the result in a register.

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

|![Tip icon]|*The lowest bit is shifted out and is lost in this instruction.*<br>*So, if the lowest bit is important, then save it before right shifting.*|
| - | - |

|![Tip icon]|*Note that this is non-cyclic.*|
| - | - |

#### *Operands*
RSH requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>RSH R1 R2</pre>|
#### *Code Examples*
    RSH R1 R1

This instruction right shifts the value in register 1, then it stores the result into register 1.
### <a name="_toc112787839"></a>***LOD***
#### *Full Name*
Load
#### *Description*
The LOD instruction copies a value from the RAM at a specified address into a register.
#### *Operands*
LOD requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register (Pointer)|<pre>LOD R1 R2</pre>|
#### *Code Examples*
    LOD R1 R1

This instruction copies the RAM value addressed by the value in register 1, then it stores the result into register 1.
### <a name="_toc112787840"></a>***STR***
#### *Full Name*
Store
#### *Description*
The STR instruction copies a value into the RAM at a specified address.
#### *Operands*
STR requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register (Pointer)|Register|<pre>STR R1 R2</pre>|
#### *Code Examples*
    STR R1 R1

This instruction copies the value in register 1 into the RAM value addressed by the value in register 1.
### <a name="_toc112787841"></a>***BGE***
#### *Full Name*
Branch if greater than or equal to
#### *Description*
The BGE instruction branches to a specified address if one value is greater than or equal to another value.

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
BGE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>BGE R1 R2 R3</pre>|
#### *Code Examples*
    BGE R1 R3 R2

This instruction branches to the instruction pointed to by the value in register 1 if the value in register 3 is greater than or equal to the value in register 2.
### <a name="_toc112787842"></a>***NOR***
#### *Full Name*
Bitwise NOR
#### *Description*
The NOR instruction does a bitwise NOR of two values, then it stores the result in a register.
#### *Operands*
NOR requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>NOR R1 R2 R3</pre>|
#### *Code Examples*
    NOR R1 R1 R2

This instruction does a bitwise NOR of the value in register 1 and the value in register 2, then it stores the result into register 1.
### <a name="_toc112787843"></a>***IMM***
#### *Full Name*
Immediate
#### *Description*
The IMM instruction copies an immediate value into a register.
#### *Operands*
IMM requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Immediate|<pre>IMM R1 6</pre>|
#### *Code Examples*
    IMM R3 5

This instruction copies the immediate value 5 and stores it into register 3.
## <a name="_toc112787844"></a>**Basic Instructions**
These are relatively simple instructions that can be translated into core instructions if needed.
### <a name="_toc112787845"></a>***ADD***
#### *Full Name*
Add
#### *Description*
The ADD instruction adds two values together, then it stores the result in a register.

|![Tip icon]|*The input values can be either registers or immediate values.*|
| - | - |

#### *Operands*
ADD requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>ADD R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>ADD R1 R2 1</pre>|
|Register|Immediate|Register|<pre>ADD R1 1 R3</pre>|
|Register|Immediate|Immediate|<pre>ADD R1 1 2</pre>|
#### *Code Examples*
    ADD R3 3 5

This instruction adds the immediate value of 3 to the immediate value of 5 and stores the result (8) into register 3.

    ADD R1 R1 R2

This instruction adds the value in register 1 to the value in register 2, then it stores the result into register 1.
### <a name="_toc112787846"></a>***RSH***
#### *Full Name*
Right shift
#### *Description*
The RSH instruction does a bitwise right shift of a value, then it stores the result in a register.

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

|![Tip icon]|*The lowest bit is shifted out and is lost in this instruction.*<br>*So, if the lowest bit is important, then save it before right shifting.*|
| - | - |

|![Tip icon]|*Note that this is non-cyclic.*|
| - | - |

#### *Operands*
RSH requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>RSH R1 R2</pre>|
|Register|Immediate|<pre>RSH R1 1</pre>|
#### *Code Examples*
    RSH R3 3

This instruction right shifts the immediate value of 3 and stores the result (1) into register 3.

    RSH R1 R1

This instruction right shifts the value in register 1, then it stores the result into register 1.
### <a name="_toc112787847"></a>***LOD***
#### *Full Name*
Load
#### *Description*
The LOD instruction copies a value from the RAM at a specified address into a register.
#### *Operands*
LOD requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|RAM Address (Relative)|<pre>LOD R1 M2</pre>|
|Register|RAM Address (Literal)|<pre>LOD R1 1</pre>|
|Register|Register (Pointer)|<pre>LOD R1 R2</pre>|
|Program Counter|RAM Address (Relative)|<pre>LOD PC M2</pre>|
|Program Counter|RAM Address (Literal)|<pre>LOD PC 1</pre>|
|Program Counter|Register (Pointer)|<pre>LOD PC R2</pre>|

|![Tip icon]|*Loading directly into the program counter should be avoided if possible. This is because it may be hard to translate to some target CPUs which cannot access their program counter directly.*|
| - | - |

#### *Code Examples*
    LOD R3 3

This instruction copies the RAM value addressed by an immediate value of 3 and stores the result into register 3.

    LOD R1 R1

This instruction copies the RAM value addressed by the value in register 1, then it stores the result into register 1.
### <a name="_toc112787848"></a>***STR***
#### *Full Name*
Store
#### *Description*
The STR instruction copies a value into the RAM at a specified address.
#### *Operands*
STR requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|RAM Address (Relative)|Register|<pre>STR M2 R1</pre>|
|RAM Address (Literal)|Register|<pre>STR 1 R1</pre>|
|Register (Pointer)|Register|<pre>STR R1 R2</pre>|
|RAM Address (Relative)|Immediate|<pre>STR M2 5</pre>|
|RAM Address (Literal)|Immediate|<pre>STR 1 5</pre>|
|Register (Pointer)|Immediate|<pre>STR R1 5</pre>|
#### *Code Examples*
    STR 3 R3

This instruction copies the value in register 3 into the RAM value addressed by an immediate value of 3.

    STR R1 R1

This instruction copies the value in register 1 into the RAM value addressed by the value in register 1.
### <a name="_toc112787849"></a>***BGE***
#### *Full Name*
Branch if greater than or equal to
#### *Description*
The BGE instruction branches to a specified address if one value is greater than or equal to another value.

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
BGE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>BGE .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>BGE .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>BGE .foo 1 R3</pre>|
|Register|Register|Register|<pre>BGE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BGE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BGE R1 1 R3</pre>|
#### *Code Examples*
    BGE .foo R1 5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is greater than or equal to the immediate value of 5.

    BGE R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is greater than or equal to the value in register 2.
### <a name="_toc112787850"></a>***NOR***
#### *Full Name*
Bitwise NOR
#### *Description*
The NOR instruction does a bitwise NOR of two values, then it stores the result in a register.
#### *Operands*
NOR requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>NOR R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>NOR R1 R2 1</pre>|
|Register|Immediate|Register|<pre>NOR R1 1 R3</pre>|
#### *Code Examples*
    NOR R3 3 R2

This instruction does a bitwise NOR of the immediate value of 3 and the value in register 2 and stores the result into register 3.

    NOR R1 R1 R2

This instruction does a bitwise NOR of the value in register 1 and the value in register 2, then it stores the result into register 1.
### <a name="_toc112787851"></a>***SUB***
#### *Full Name*
Subtract
#### *Description*
The SUB instruction subtracts one values from another, then it stores the result in a register.
#### *Operands*
SUB requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SUB R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SUB R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SUB R1 1 R3</pre>|
|Register|Immediate|Immediate|<pre>SUB R1 1 2</pre>|
#### *Code Examples*
    SUB R3 3 5

This instruction subtracts the immediate value of 3 from the immediate value of 5 and stores the result (-2 in 2’s complement) into register 3.

|![Tip icon]|*Negative numbers will use 2’s complement. So, -2 on an 8 bit CPU would be the equivalent of 254.*|
| - | - |

    SUB R1 R1 R2

This instruction subtracts the value in register 1 from the value in register 2, then it stores the result into register 1.
### <a name="_toc112787852"></a>***JMP***
#### *Full Name*
Jump
#### *Description*
The JMP instruction branches to a specified value.
#### *Operands*
JMP requires 1 operand.

|**Destination**|**Example**|
| :-: | :-: |
|Immediate|<pre>JMP 5</pre>|
|Register|<pre>JMP R1</pre>|
#### *Code Examples*
    JMP .test

This instruction jumps to the instruction addressed by the label “test”.

    JMP R1

This instruction jumps to the instruction addressed by the value in register 1.
### <a name="_toc112787853"></a>***MOV***
#### *Full Name*
Move
#### *Description*
The MOV instruction copies a value into a register.
#### *Operands*
MOV requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>MOV R1 R2</pre>|
|Register|Immediate|<pre>MOV R1 .foo</pre>|
#### *Code Examples*
    MOV R1 R2

This instruction copies the value in register 2, then it stores it into register 1.

    MOV R3 M5

This instruction copies the address of memory location 5 (as an immediate value) and stores it into register 3.

|![Tip icon]|*Note that if a memory address is used in a location where an immediate would normally go, it is converted into an immediate value which points to the address of that memory location.*<br>*So, the M5 here is converted to the literal RAM address of memory location 5 in the Heap.*|
| - | - |

### <a name="_toc112787854"></a>***NOP***
#### *Full Name*
No operation
#### *Description*
The NOP instruction does nothing.

|![Tip icon]|*NOP should never be used in the majority of URCL programs since there is no point to making the target CPU do nothing if every instruction is atomic.*<br>*Note that there are no read before write hazards in URCL and branching occurs instantly.*|
| - | - |

#### *Operands*
NOP requires 0 operands.
#### *Code Examples*
    NOP

This instruction does nothing.
### <a name="_toc112787855"></a>***IMM***
#### *Full Name*
Immediate
#### *Description*
The IMM instruction copies an immediate value into a register.
#### *Operands*
IMM requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Immediate|<pre>IMM R1 6</pre>|
#### *Code Examples*
    IMM R3 5

This instruction copies the immediate value 5 and stores it into register 3.

|![Tip icon]|*Since MOV also accepts immediates, MOV can always be used in place of IMM.*<br>*But using IMM when loading immediates is preferred as it makes the code clearer to the reader.*<br>*MOV allows immediates because this makes compiling to URCL a little easier.*|
| - | - |

### <a name="_toc112787856"></a>***LSH***
#### *Full Name*
Left shift
#### *Description*
The LSH instruction does a bitwise left shift of a value, then it stores the result in a register.

|![Tip icon]|*The uppermost bit is shifted out and is lost in this instruction.*<br>*So, if the uppermost bit is important then save it before left shifting.*|
| - | - |

|![Tip icon]|*Note that this is non-cyclic.*|
| - | - |

#### *Operands*
LSH requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>LSH R1 R2</pre>|
|Register|Immediate|<pre>LSH R1 1</pre>|
#### *Code Examples*
    LSH R3 3

This instruction left shifts the immediate value of 3 and stores the result (6) into register 3.

    LSH R1 R1

This instruction left shifts the value in register 1, then it stores the result into register 1.
### <a name="_toc112787857"></a>***INC***
#### *Full Name*
Increment
#### *Description*
The INC instruction adds 1 to a value then stores the result into a register.
#### *Operands*
INC requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>INC R1 R2</pre>|
|Register|Immediate|<pre>INC R1 .foo</pre>|
#### *Code Examples*
    INC R1 R2

This instruction adds 1 to the value in register 2, then it stores it into register 1.

    INC R3 .foo

This instruction adds 1 to the address of the label “foo” and stores it into register 3.

|![Tip icon]|*Since the size of the instructions on the target CPU can be bigger than one word, adding 1 to a label which points at an instruction does not make that label point to the next instruction.*<br>*Labels should only be added to or subtracted from if that label points to DW values as these are guaranteed to occupy 1 word per value regardless of the target CPU.*|
| - | - |

### <a name="_toc112787858"></a>***DEC***
#### *Full Name*
Decrement
#### *Description*
The DEC instruction subtracts 1 from a value then stores the result into a register.
#### *Operands*
DEC requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>DEC R1 R2</pre>|
|Register|Immediate|<pre>DEC R1 .foo</pre>|
#### *Code Examples*
    DEC R1 R2

This instruction subtracts 1 from the value in register 2, then it stores it into register 1.

    DEC R3 .foo

This instruction subtracts 1 from the address of the label “foo” and stores it into register 3.
### <a name="_toc112787859"></a>***NEG***
#### *Full Name*
Negate
#### *Description*
The NEG instruction calculates the negation of the value, interpreted as 2's compliment, then stores the result into a register.
#### *Operands*
NEG requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>NEG R1 R2</pre>|
|Register|Immediate|<pre>NEG R1 5</pre>|
#### *Code Examples*
    NEG R1 R2

This instruction calculates the 2’s complement of the value in register 2 and stores the result into register 1.

    NEG R3 5

This instruction calculates the 2’s complement of the immediate value 5 and stores the result (-5) into register 3.
### <a name="_toc112787860"></a>***AND***
#### *Full Name*
Bitwise AND
#### *Description*
The AND instruction does a bitwise AND of two values, then it stores the result in a register.
#### *Operands*
AND requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>AND R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>AND R1 R2 1</pre>|
|Register|Immediate|Register|<pre>AND R1 1 R3</pre>|
#### *Code Examples*
    AND R3 3 R2

This instruction does a bitwise AND of the immediate value of 3 and the value in register 2 and stores the result into register 3.

    AND R1 R1 R2

This instruction does a bitwise AND of the value in register 1 and the value in register 2, then it stores the result into register 1.
### <a name="_toc112787861"></a>***OR***
#### *Full Name*
Bitwise OR
#### *Description*
The OR instruction does a bitwise OR of two values, then it stores the result in a register.
#### *Operands*
OR requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>OR R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>OR R1 R2 1</pre>|
|Register|Immediate|Register|<pre>OR R1 1 R3</pre>|
#### *Code Examples*
    OR R3 3 R2

This instruction does a bitwise OR of the immediate value of 3 and the value in register 2 and stores the result into register 3.

    OR R1 R1 R2

This instruction does a bitwise OR of the value in register 1 and the value in register 2, then it stores the result into register 1.
### <a name="_toc112787862"></a>***NOT***
#### *Full Name*
Bitwise NOT
#### *Description*
The NOT instruction does a bitwise NOT of a value, then it stores the result in a register.
#### *Operands*
NOT requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>NOT R1 R2</pre>|
|Register|Immediate|<pre>NOT R1 1</pre>|
#### *Code Examples*
    NOT R1 R1

This instruction does a bitwise NOT of the value in register 1, then it stores the result into register 1.

    NOT R3 3

This instruction does a bitwise NOT of the immediate value of 3 and stores the result into register 3.

|![Tip icon]|*On an 8 bit CPU the result of NOT of 3 would be 252.*|
| - | - |

### <a name="_toc112787863"></a>***XNOR***
#### *Full Name*
Bitwise XNOR
#### *Description*
The XNOR instruction does a bitwise XNOR of two values, then it stores the result in a register.
#### *Operands*
XNOR requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>XNOR R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>XNOR R1 R2 1</pre>|
|Register|Immediate|Register|<pre>XNOR R1 1 R3</pre>|
#### *Code Examples*
    XNOR R3 3 R2

This instruction does a bitwise XNOR of the immediate value 3 and the value in register 2 and stores the result into register 3.

    XNOR R1 R1 R2

This instruction does a bitwise XNOR of the value in register 1 and the value in register 2, then it stores the result into register 1.
### <a name="_toc112787864"></a>***XOR***
#### *Full Name*
Bitwise XOR
#### *Description*
The XOR instruction does a bitwise XOR of two values, then it stores the result in a register.
#### *Operands*
XOR requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>XOR R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>XOR R1 R2 1</pre>|
|Register|Immediate|Register|<pre>XOR R1 1 R3</pre>|
#### *Code Examples*
    XOR R3 3 R2

This instruction does a bitwise XOR of the immediate value 3 and the value in register 2 and stores the result into register 3.

    XOR R1 R1 R2

This instruction does a bitwise XOR of the value in register 1 and the value in register 2, then it stores the result into register 1.
### <a name="_toc112787865"></a>***NAND***
#### *Full Name*
Bitwise NAND
#### *Description*
The NAND instruction does a bitwise NAND of two values, then it stores the result in a register.
#### *Operands*
NAND requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>NAND R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>NAND R1 R2 1</pre>|
|Register|Immediate|Register|<pre>NAND R1 1 R3</pre>|
#### *Code Examples*
    NAND R3 3 R2

This instruction does a bitwise NAND of the immediate value of 3 and the value in register 2 and stores the result into register 3.

    NAND R1 R1 R2

This instruction does a bitwise NAND of the value in register 1 and the value in register 2, then it stores the result into register 1.
### <a name="_toc112787866"></a>***BRL***
#### *Full Name*
Branch if less than
#### *Description*
The BRL instruction branches to a specified address if one value is less than another value.

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
BRL requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>BRL .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>BRL .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>BRL .foo 1 R3</pre>|
|Register|Register|Register|<pre>BRL R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BRL R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BRL R1 1 R3</pre>|
#### *Code Examples*
    BRL .foo R1 5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is less than the immediate value of 5.

    BRL R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is less than the value in register 2.
### <a name="_toc112787867"></a>***BRG***
#### *Full Name*
Branch if greater than
#### *Description*
The BRG instruction branches to a specified address if one value is less than another value.

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
BRG requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>BRG .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>BRG .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>BRG .foo 1 R3</pre>|
|Register|Register|Register|<pre>BRG R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BRG R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BRG R1 1 R3</pre>|
#### *Code Examples*
    BRG .foo R1 5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is greater than the immediate value of 5.

    BRG R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is greater than the value in register 2.
### <a name="_toc112787868"></a>***BRE***
#### *Full Name*
Branch if equal to
#### *Description*
The BRE instruction branches to a specified address if one value is equal to another value.
#### *Operands*
BRE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>BRE .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>BRE .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>BRE .foo 1 R3</pre>|
|Register|Register|Register|<pre>BRE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BRE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BRE R1 1 R3</pre>|
#### *Code Examples*
    BRE .foo R1 5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is equal to the immediate value of 5.

    BRE R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is equal to the value in register 2.
### <a name="_toc112787869"></a>***BNE***
#### *Full Name*
Branch if not equal to
#### *Description*
The BNE instruction branches to a specified address if one value is not equal to another value.
#### *Operands*
BNE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>BNE .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>BNE .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>BNE .foo 1 R3</pre>|
|Register|Register|Register|<pre>BNE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BNE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BNE R1 1 R3</pre>|
#### *Code Examples*
    BNE .foo R1 5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is not equal to the immediate value of 5.

    BNE R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is not equal to the value in register 2.
### <a name="_toc112787870"></a>***BOD***
#### *Full Name*
Branch if odd
#### *Description*
The BOD instruction branches to a specified address if a value is odd.

|![Tip icon]|*A value is odd if the lowest bit is active.*|
| - | - |

#### *Operands*
BOD requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Immediate|Register|<pre>BOD .foo R2</pre>|
|Register|Register|<pre>BOD R1 R2</pre>|
#### *Code Examples*
    BOD .foo R1

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is odd.

    BOD R1 R2

This instruction branches to the instruction pointed to by the value in register 1 if the value in register 2 is odd.
### <a name="_toc112787871"></a>***BEV***
#### *Full Name*
Branch if even
#### *Description*
The BEV instruction branches to a specified address if a value is even.

|![Tip icon]|*A value is even if the lowest bit is not active.*|
| - | - |

#### *Operands*
BEV requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Immediate|Register|<pre>BEV .foo R2</pre>|
|Register|Register|<pre>BEV R1 R2</pre>|
#### *Code Examples*
    BEV .foo R1

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is even.

    BEV R1 R2

This instruction branches to the instruction pointed to by the value in register 1 if the value in register 2 is even.
### <a name="_toc112787872"></a>***BLE***
#### *Full Name*
Branch if less than or equal to
#### *Description*
The BLE instruction branches to a specified address if one value is less than or equal to another value.

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
BLE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>BLE .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>BLE .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>BLE .foo 1 R3</pre>|
|Register|Register|Register|<pre>BLE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BLE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BLE R1 1 R3</pre>|
#### *Code Examples*
    BLE .foo R1 5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is less than or equal to the immediate value of 5.

    BLE R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is less than or equal to the value in register 2.
### <a name="_toc112787873"></a>***BRZ***
#### *Full Name*
Branch if zero
#### *Description*
The BRZ instruction branches to a specified address if a value is equal to zero.
#### *Operands*
BRZ requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Immediate|Register|<pre>BRZ .foo R2</pre>|
|Register|Register|<pre>BRZ R1 R2</pre>|
#### *Code Examples*
    BRZ .foo R1

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is equal to zero.

    BRZ R1 R2

This instruction branches to the instruction pointed to by the value in register 1 if the value in register 2 is equal to zero.
### <a name="_toc112787874"></a>***BNZ***
#### *Full Name*
Branch if not zero
#### *Description*
The BNZ instruction branches to a specified address if a value is not equal to zero.
#### *Operands*
BNZ requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Immediate|Register|<pre>BNZ .foo R2</pre>|
|Register|Register|<pre>BNZ R1 R2</pre>|
#### *Code Examples*
    BNZ .foo R1

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is not equal to zero.

    BNZ R1 R2

This instruction branches to the instruction pointed to by the value in register 1 if the value in register 2 is not equal to zero.
### <a name="_toc112787875"></a>***BRN***
#### *Full Name*
Branch if negative
#### *Description*
The BRN instruction branches to a specified address if a value is negative.

|![Tip icon]|*This is signed.*|
| - | - |

|![Tip icon]|*A value is negative if the highest bit is active. (2’s complement)*|
| - | - |

#### *Operands*
BRN requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Immediate|Register|<pre>BRN .foo R2</pre>|
|Register|Register|<pre>BRN R1 R2</pre>|
#### *Code Examples*
    BRN .foo R1

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is negative.

    BRN R1 R2

This instruction branches to the instruction pointed to by the value in register 1 if the value in register 2 is negative.
### <a name="_toc112787876"></a>***BRP***
#### *Full Name*
Branch if positive
#### *Description*
The BRP instruction branches to a specified address if a value is positive or zero.

|![Tip icon]|*This is signed.*|
| - | - |

|![Tip icon]|*A value is positive if the highest bit is not active. (2’s complement)*|
| - | - |

#### *Operands*
BRP requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Immediate|Register|<pre>BRP .foo R2</pre>|
|Register|Register|<pre>BRP R1 R2</pre>|
#### *Code Examples*
    BRP .foo R1

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is positive.

    BRP R1 R2

This instruction branches to the instruction pointed to by the value in register 1 if the value in register 2 is positive.
### <a name="_toc112787877"></a>***PSH***
#### *Full Name*
Push
#### *Description*
The PSH instruction pushes a value onto the stack.

|![Tip icon]|*Since the stack pointer points to the topmost filled value in the stack, the stack pointer is first decremented before writing to the location it points to. This happens automatically in the PSH instruction.*|
| - | - |

#### *Operands*
PSH requires 1 operand.

|**Source1**|**Example**|
| :-: | :-: |
|Register|<pre>PSH R1</pre>|
|Immediate|<pre>PSH 5</pre>|
#### *Code Examples*
    PSH R1

This instruction pushes the value in register 1 onto the stack.

    PSH .test

This instruction pushes the address of the label “test” onto the stack.
### <a name="_toc112787878"></a>***POP***
#### *Full Name*
Pop
#### *Description*
The POP instruction pops a value from the stack into a register.

|![Tip icon]|*Since the stack pointer points to the topmost filled value in the stack, the value at the location where the stack pointer points is first read before incrementing the stack pointer. This happens automatically in the POP instruction.*|
| - | - |

#### *Operands*
POP requires 1 operand.

|**Destination**|**Example**|
| :-: | :-: |
|Register|<pre>POP R1</pre>|
#### *Code Examples*
    POP R1

This instruction pops from the stack into register 1.
### <a name="_toc112787879"></a>***CAL***
#### *Full Name*
Call
#### *Description*
The CAL instruction pushes the address of the next instruction onto the stack then it branches to a specific address.

|![Tip icon]|*This is used to branch to subroutines.*|
| - | - |

|![Tip icon]|*The address pushed onto the stack is the return address.*|
| - | - |

#### *Operands*
CAL requires 1 operand.

|**Source1**|**Example**|
| :-: | :-: |
|Immediate|CAL .test|
|Register|<pre>CAL R1</pre>|
#### *Code Examples*
    CAL .test

This instruction pushes the address of the next instruction onto the stack then it branches to the instruction pointed to by the label “test”.

    CAL R1

This instruction pushes the address of the next instruction onto the stack then it branches to the instruction pointed to by the value in register 1.
### <a name="_toc112787880"></a>***RET***
#### *Full Name*
Return
#### *Description*
The RET instruction pops a value from the stack then it branches to that value.

|![Tip icon]|*The value at the top of the stack must be a valid address of an instruction for RET to work.*<br>*Otherwise, a “Non-Instruction Execution” fault may occur.*|
| - | - |

#### *Operands*
RET requires 0 operands.
#### *Code Examples*
    RET

This instruction pops a value from the stack then it branches to that value.
### <a name="_toc112787881"></a>***HLT***
#### *Full Name*
Halt
#### *Description*
The HLT instruction halts execution.

|![Tip icon]|*This marks the end of a program.*|
| - | - |

|![Tip icon]|*Once halted, the target CPU will need to be manually reset to run again.*|
| - | - |

#### *Operands*
HLT requires 0 operands.
#### *Code Examples*
    HLT

This instruction halts the target CPU.
### <a name="_toc112787882"></a>***CPY***
#### *Full Name*
Copy
#### *Description*
The CPY instruction copies a value from the RAM at a specified address into another RAM location at another specified address.
#### *Operands*
CPY requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|RAM Address (Relative)|RAM Address (Relative)|<pre>CPY M1 M2</pre>|
|RAM Address (Relative)|RAM Address (Literal)|<pre>CPY M1 1</pre>|
|RAM Address (Relative)|Register (Pointer)|<pre>CPY M1 R2</pre>|
|RAM Address (Literal)|RAM Address (Relative)|<pre>CPY 1 M2</pre>|
|RAM Address (Literal)|RAM Address (Literal)|<pre>CPY 1 1</pre>|
|RAM Address (Literal)|Register (Pointer)|<pre>CPY 1 R2</pre>|
|Register|RAM Address (Relative)|<pre>CPY R1 M2</pre>|
|Register|RAM Address (Literal)|<pre>CPY R1 1</pre>|
|Register|Register (Pointer)|<pre>CPY R1 R2</pre>|

|![Tip icon]|*This instruction should be used when moving values around in the RAM.*<br>*This instruction allows for potentially shorter or faster translations than that of the equivalent LOD followed by a STR instruction.*|
| - | - |

#### *Code Examples*
    CPY M3 3

This instruction copies the RAM value addressed by an immediate value of 3 and stores the result into memory location 3.

    CPY R2 R1

This instruction copies the RAM value addressed by the value in register 1, then stores it into the RAM value addressed by the value in register 2.
### <a name="_toc112787883"></a>***BRC***
#### *Full Name*
Branch if carry
#### *Description*
The BRC instruction branches to a specified address if one value added to another value activates the carry flag.

|![Tip icon]|*Note that the results of the addition in this instruction are not kept.*|
| - | - |

#### *Operands*
BRC requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>BRC .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>BRC .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>BRC .foo 1 R3</pre>|
|Register|Register|Register|<pre>BRC R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BRC R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BRC R1 1 R3</pre>|
#### *Code Examples*
    BRC .foo R1 5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 added to the immediate value of 5 activates the carry flag.

    BRC R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 added to the value in register 2 activates the carry flag.
### <a name="_toc112787884"></a>***BNC***
#### *Full Name*
Branch if no carry
#### *Description*
The BNC instruction branches to a specified address if one value added to another value does not activate the carry flag.

|![Tip icon]|*Note that the results of the addition in this instruction are not kept.*|
| - | - |

#### *Operands*
BNC requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>BNC .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>BNC .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>BNC .foo 1 R3</pre>|
|Register|Register|Register|<pre>BNC R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BNC R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BNC R1 1 R3</pre>|
#### *Code Examples*
    BNC .foo R1 5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 added to the immediate value of 5 does not activate the carry flag.

    BNC R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 added to the value in register 2 does not activate the carry flag.
## <a name="_toc112787885"></a>**Complex Instructions**
These are instructions which are typically more difficult to translate directly to a target CPU’s assembly. These instructions can be translated into equivalent Basic and Core instructions if they cannot be directly translated.

There are 17 complex instructions.
### <a name="_toc112787886"></a>***MLT***
#### *Full Name*
Multiply
#### *Description*
The MLT instruction multiplies two values together, then it stores the result in a register.
#### *Operands*
MLT requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>MLT R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>MLT R1 R2 1</pre>|
|Register|Immediate|Register|<pre>MLT R1 1 R3</pre>|
#### *Code Examples*
    MLT R3 3 R2

This instruction multiplies the immediate value of 3 with the value in register 2 and stores the result into register 3.

    MLT R1 R1 R2

This instruction multiplies the value in register 1 with the value in register 2, then it stores the result into register 1.
### <a name="_toc112787887"></a>***DIV***
#### *Full Name*
Division
#### *Description*
The DIV instruction divides one value by another, then it stores the result in a register.

|![Tip icon]|*This is integer division. So, the result is rounded down (towards zero) to the nearest integer.*|
| - | - |

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
DIV requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>DIV R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>DIV R1 R2 1</pre>|
|Register|Immediate|Register|<pre>DIV R1 1 R3</pre>|
#### *Code Examples*
    DIV R3 5 R2

This instruction divides the immediate value of 5 by the value in register 2 and stores the result into register 3.

    DIV R1 R1 R2

This instruction divides the value in register 1 by the value in register 2, then it stores the result into register 1.
### <a name="_toc112787888"></a>***MOD***
#### *Full Name*
Modulus
#### *Description*
The MOD instruction calculates the remainder left after one value is divided by another, then it stores the result in a register.

|![Tip icon]|*This uses integer division. So, the dividend is rounded down (towards zero) to the nearest integer, leaving the remainder as the result.*|
| - | - |

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
MOD requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>MOD R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>MOD R1 R2 1</pre>|
|Register|Immediate|Register|<pre>MOD R1 1 R3</pre>|
#### *Code Examples*
    MOD R3 5 R2

This instruction calculates the remainder left after the immediate value of 5 is divided by the value in register 2 and stores the result into register 3.

    MOD R1 R1 R2

This instruction calculates the remainder left after the value in register 1 is divided by the value in register 2, then it stores the result into register 1.
### <a name="_toc112787889"></a>***BSR***
#### *Full Name*
Barrel shift right
#### *Description*
The BSR instruction does a specific number of bitwise right shifts of a value, then it stores the result in a register.

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

|![Tip icon]|*The bits that are shifted out in this instruction are lost.*<br>*So, if those bits are important, save them before shifting.*|
| - | - |

|![Tip icon]|*Note that this is non-cyclic.*|
| - | - |

#### *Operands*
BSR requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>BSR R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BSR R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BSR R1 1 R3</pre>|
#### *Code Examples*
    BSR R3 3 R2

This instruction right shifts the immediate value of 3 a number of times, this number is the value in register 2. Then it stores the result into register 3.

    BSR R1 R1 R2

This instruction right shifts the value in register 1 a number of times, this number is the value in register 2. Then it stores the result into register 1.
### <a name="_toc112787890"></a>***BSL***
#### *Full Name*
Barrel shift left
#### *Description*
The BSL instruction does a specific number of bitwise left shifts of a value, then it stores the result in a register.

|![Tip icon]|*The bits that are shifted out in this instruction are lost.*<br>*So, if those bits are important, save them before shifting.*|
| - | - |

|![Tip icon]|*Note that this is non-cyclic.*|
| - | - |

#### *Operands*
BSL requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>BSL R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BSL R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BSL R1 1 R3</pre>|
#### *Code Examples*
    BSL R3 3 R2

This instruction left shifts the immediate value of 3 a number of times, this number is the value in register 2. Then it stores the result into register 3.

    BSL R1 R1 R2

This instruction left shifts the value in register 1 a number of times, this number is the value in register 2. Then it stores the result into register 1.
### <a name="_toc112787891"></a>***SRS***
#### *Full Name*
Signed right shift
#### *Description*
The SRS instruction does a signed right shift of a value, then it stores the result in a register.

|![Tip icon]|*Note that this is signed.*|
| - | - |

|![Tip icon]|*The lowest bit is shifted out and is lost in this instruction.*<br>*So, if the lowest bit is important, then save it before right shifting.*|
| - | - |

|![Tip icon]|*The sign bit (uppermost bit) is extended in this instruction.*|
| - | - |

|![Tip icon]|*Note that this is non-cyclic.*|
| - | - |
#### *Operands*
SRS requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>SRS R1 R2</pre>|
|Register|Immediate|<pre>SRS R1 1</pre>|
#### *Code Examples*
    SRS R1 R1

This instruction does a signed right shift of the value in register 1, then it stores the result into register 1.

    SRS R3 3

This instruction does a signed right shift of the immediate value of 3 and stores the result into register 3.
### <a name="_toc112787892"></a>***BSS***
#### *Full Name*
Barrel shift right signed
#### *Description*
The BSS instruction does a specific number of signed right shifts of a value, then it stores the result in a register.

|![Tip icon]|*Note that this is signed.*|
| - | - |

|![Tip icon]|*The bits that are shifted out in this instruction are lost.*<br>*So, if those bits are important, save them before shifting.*|
| - | - |

|![Tip icon]|*Note that this is non-cyclic.*|
| - | - |

#### *Operands*
BSS requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>BSS R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>BSS R1 R2 1</pre>|
|Register|Immediate|Register|<pre>BSS R1 1 R3</pre>|
#### *Code Examples*
    BSS R3 3 R2

This instruction does a signed right shift of the immediate value of 3 a number of times, this number is the value in register 2. Then it stores the result into register 3.

    BSS R1 R1 R2

This instruction does a signed right shift of the value in register 1 a number of times, this number is the value in register 2. Then it stores the result into register 1.
### <a name="_toc112787893"></a>***SETE***
#### *Full Name*
Set if equal to
#### *Description*
The SETE instruction sets a register to all 1’s in binary if one value is equal to another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

#### *Operands*
SETE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SETE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SETE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SETE R1 1 R3</pre>|
#### *Code Examples*
    SETE R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is equal to the immediate value of 5, otherwise it will write 0 into register 2.

    SETE R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is equal to the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787894"></a>***SETNE***
#### *Full Name*
Set if not equal to
#### *Description*
The SETNE instruction sets a register to all 1’s in binary if one value is not equal to another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

#### *Operands*
SETNE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SETNE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SETNE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SETNE R1 1 R3</pre>|
#### *Code Examples*
    SETNE R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is not equal to the immediate value of 5, otherwise it will write 0 into register 2.

    SETNE R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is not equal to the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787895"></a>***SETG***
#### *Full Name*
Set if greater than
#### *Description*
The SETG instruction sets a register to all 1’s in binary if one value is greater than another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
SETG requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SETG R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SETG R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SETG R1 1 R3</pre>|
#### *Code Examples*
    SETG R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is greater than the immediate value of 5, otherwise it will write 0 into register 2.

    SETG R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is greater than the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787896"></a>***SETL***
#### *Full Name*
Set if less than
#### *Description*
The SETL instruction sets a register to all 1’s in binary if one value is less than another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
SETL requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SETL R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SETL R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SETL R1 1 R3</pre>|
#### *Code Examples*
    SETL R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is less than the immediate value of 5, otherwise it will write 0 into register 2.

    SETL R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is less than the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787897"></a>***SETGE***
#### *Full Name*
Set if greater than or equal to
#### *Description*
The SETGE instruction sets a register to all 1’s in binary if one value is greater than another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
SETGE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SETGE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SETGE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SETGE R1 1 R3</pre>|
#### *Code Examples*
    SETGE R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is greater than or equal to the immediate value of 5, otherwise it will write 0 into register 2.

    SETGE R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is greater than or equal to the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787898"></a>***SETLE***
#### *Full Name*
Set if less than or equal to
#### *Description*
The SETLE instruction sets a register to all 1’s in binary if one value is greater than another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

|![Tip icon]|*Note that this is unsigned.*|
| - | - |

#### *Operands*
SETLE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SETLE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SETLE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SETLE R1 1 R3</pre>|
#### *Code Examples*
    SETLE R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is less than or equal to the immediate value of 5, otherwise it will write 0 into register 2.

    SETLE R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is less than or equal to the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787899"></a>***SETC***
#### *Full Name*
Set if carry
#### *Description*
The SETC instruction sets a register to all 1’s in binary if one value added to another value activates the carry flag, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

|![Tip icon]|*Note that the result of the addition is not kept.*|
| - | - |

#### *Operands*
SETC requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SETC R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SETC R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SETC R1 1 R3</pre>|
#### *Code Examples*
    SETC R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 added to the immediate value of 5 activates the carry flag, otherwise it will write 0 into register 2.

    SETC R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 added to the value in register 2 activates the carry flag, otherwise it will write 0 into register 1.
### <a name="_toc112787900"></a>***SETNC***
#### *Full Name*
Set if no carry
#### *Description*
The SETNC instruction sets a register to all 1’s in binary if one value added to another value does not activate the carry flag, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

|![Tip icon]|*Note that the result of the addition is not kept.*|
| - | - |

#### *Operands*
SETNC requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SETNC R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SETNC R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SETNC R1 1 R3</pre>|
#### *Code Examples*
    SETNC R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 added to the immediate value of 5 does not activate the carry flag, otherwise it will write 0 into register 2.

    SETNC R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 added to the value in register 2 does not activate the carry flag, otherwise it will write 0 into register 1.
### <a name="_toc112787901"></a>***LLOD***
#### *Full Name*
List load
#### *Description*
The LLOD instruction copies a value from the RAM at a specified address + offset into a register.
#### *Operands*
LLOD requires 3 operands.

|**Destination**|**Source1 (Base)**|**Source2 (Offset)**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>LLOD R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>LLOD R1 R2 1</pre>|
|Register|Immediate|Register|<pre>LLOD R1 1 R3</pre>|
|Register|Immediate|Immediate|<pre>LLOD R1 .foo 2</pre>|
#### *Code Examples*
    LLOD R3 .foo 5

This instruction copies a value from the RAM at a specific address. This address is the address of the label “foo” added to the offset of an immediate value of 5. Then it stores the result into register 3.

    LLOD R1 R1 R2

This instruction copies a value from the RAM at a specific address. This address is the value in register 1 added to the value in register 2. Then it stores the result into register 1.
### <a name="_toc112787902"></a>***LSTR***
#### *Full Name*
List store
#### *Description*
The LSTR instruction writes a value into the RAM at a specified address + offset.
#### *Operands*
LSTR requires 3 operands.

|**Destination (Base)**|**Source1 (Offset)**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>LSTR R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>LSTR R1 R2 1</pre>|
|Register|Immediate|Register|<pre>LSTR R1 1 R3</pre>|
|Register|Immediate|Immediate|<pre>LSTR R1 1 2</pre>|
|Immediate|Register|Register|<pre>LSTR .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>LSTR .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>LSTR .foo 2 R3</pre>|
|Immediate|Immediate|Immediate|<pre>LSTR .foo 2 1</pre>|
#### *Code Examples*
    LSTR .foo 5 R3

This instruction writes the value in register 3 into the RAM at a specific address. This address is the address of the label “foo” added to an immediate value of 5.

    LSTR R1 R2 R3

This instruction writes the value in register 3 into the RAM at a specific address. This address is the value in register 1 added to the value in register 3.
### <a name="_toc112787903"></a>***SDIV***
#### *Full Name*
Signed division
#### *Description*
The SDIV instruction divides one signed value by another, then it stores the signed result in a register.

|![Tip icon]|*This is integer division. So, the result is rounded towards zero (down if result is positive, up if the result is negative) to the nearest integer.*|
| - | - |

#### *Operands*
SDIV requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SDIV R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SDIV R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SDIV R1 1 R3</pre>|
#### *Code Examples*
    SDIV R3 -5 R2

This instruction divides the immediate value of -5 by the value in register 2 and stores the result into register 3.

    SDIV R1 R1 R2

This instruction divides the value in register 1 by the value in register 2, then it stores the result into register 1.
### <a name="_toc112787904"></a>***SBRL***
#### *Full Name*
Signed branch if less than
#### *Description*
The SBRL instruction branches to a specified address if one signed value is less than another value.
#### *Operands*
SBRL requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>SBRL .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>SBRL .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>SBRL .foo 1 R3</pre>|
|Register|Register|Register|<pre>SBRL R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SBRL R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SBRL R1 1 R3</pre>|
#### *Code Examples*
    SBRL .foo R1 -5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is less than the immediate value of -5.

    SBRL R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is less than the value in register 2.
### <a name="_toc112787905"></a>***SBRG***
#### *Full Name*
Signed branch if greater than
#### *Description*
The SBRG instruction branches to a specified address if one value is less than another value.
#### *Operands*
SBRG requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>SBRG .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>SBRG .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>SBRG .foo 1 R3</pre>|
|Register|Register|Register|<pre>SBRG R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SBRG R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SBRG R1 1 R3</pre>|
#### *Code Examples*
    SBRG .foo R1 -5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is greater than the immediate value of -5.

    SBRG R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is greater than the value in register 2.
### <a name="_toc112787906"></a>***SBLE***
#### *Full Name*
Signed branch if less than or equal to
#### *Description*
The SBLE instruction branches to a specified address if one signed value is less than or equal to another value.
#### *Operands*
SBLE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>SBLE .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>SBLE .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>SBLE .foo 1 R3</pre>|
|Register|Register|Register|<pre>SBLE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SBLE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SBLE R1 1 R3</pre>|
#### *Code Examples*
    SBLE .foo R1 -5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is less than or equal to the immediate value of -5.

    SBLE R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is less than or equal to the value in register 2.
### <a name="_toc112787907"></a>***SBGE***
#### *Full Name*
Signed branch if greater than or equal to
#### *Description*
The SBGE instruction branches to a specified address if one value is greater than or equal to another value.
#### *Operands*
SBGE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Immediate|Register|Register|<pre>SBGE .foo R2 R3</pre>|
|Immediate|Register|Immediate|<pre>SBGE .foo R2 1</pre>|
|Immediate|Immediate|Register|<pre>SBGE .foo 1 R3</pre>|
|Register|Register|Register|<pre>SBGE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SBGE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SBGE R1 1 R3</pre>|
#### *Code Examples*
    SBGE .foo R1 -5

This instruction branches to the instruction pointed to by the label “foo” if the value in register 1 is greater than or equal to the immediate value of -5.

    SBGE R1 5 R2

This instruction branches to the instruction pointed to by the value in register 1 if the immediate value of 5 is greater than or equal to the value in register 2.
### <a name="_toc112787908"></a>***SSETL***
#### *Full Name*
Signed set if less than
#### *Description*
The SSETL instruction sets a register to all 1’s in binary if one signed value is less than another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

#### *Operands*
SSETL requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SSETL R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SSETL R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SSETL R1 1 R3</pre>|
#### *Code Examples*
    SSETL R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is less than the immediate value of 5, otherwise it will write 0 into register 2.

    SSETL R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is less than the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787909"></a>***SSETG***
#### *Full Name*
Signed set if greater than
#### *Description*
The SSETG instruction sets a register to all 1’s in binary if one signed value is greater than another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

#### *Operands*
SSETG requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SSETG R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SSETG R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SSETG R1 1 R3</pre>|
#### *Code Examples*
    SSETG R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is greater than the immediate value of 5, otherwise it will write 0 into register 2.

    SSETG R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is greater than the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787910"></a>***SSETLE***
#### *Full Name*
Signed set if less than or equal to
#### *Description*
The SSETLE instruction sets a register to all 1’s in binary if one signed value is greater than another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

#### *Operands*
SSETLE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SSETLE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SSETLE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SSETLE R1 1 R3</pre>|
#### *Code Examples*
    SSETLE R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is less than or equal to the immediate value of 5, otherwise it will write 0 into register 2.

    SSETLE R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is less than or equal to the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787911"></a>***SSETGE***
#### *Full Name*
Signed set if greater than or equal to
#### *Description*
The SSETGE instruction sets a register to all 1’s in binary if one value is greater than another value, otherwise it sets that register to 0.

|![Tip icon]|*All 1’s in binary on an 8 bit CPU is 255.*|
| - | - |

#### *Operands*
SSETGE requires 3 operands.

|**Destination**|**Source1**|**Source2**|**Example**|
| :-: | :-: | :-: | :-: |
|Register|Register|Register|<pre>SSETGE R1 R2 R3</pre>|
|Register|Register|Immediate|<pre>SSETGE R1 R2 1</pre>|
|Register|Immediate|Register|<pre>SSETGE R1 1 R3</pre>|
#### *Code Examples*
    SSETGE R2 R1 5

This instruction will write all 1’s into register 2 if the value in register 1 is greater than or equal to the immediate value of 5, otherwise it will write 0 into register 2.

    SSETGE R1 R1 R2

This instruction will write all 1’s into register 1 if the value in register 1 is greater than or equal to the value in register 2, otherwise it will write 0 into register 1.
### <a name="_toc112787912"></a>***ABS***
#### *Full Name*
Absolute value
#### *Description*
The ABS instruction calculates the twos complement of a value if that value is negative (defined by the topmost bit being active), or if the value is positive then it returns that value. The result is then stored into a register.
#### *Operands*
ABS requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Register|<pre>ABS R1 R2</pre>|
|Register|Immediate|<pre>ABS R1 -5</pre>|
#### *Code Examples*
    ABS R1 R2

This instruction calculates the absolute value of the number in register 2 and stores the result into register 1.

    ABS R3 -5

This instruction calculates the absolute value of the immediate value -5 and stores the result (5) into register 3.
## <a name="_toc112787913"></a>**I/O Instructions**
These instructions cannot be translated into other instructions and must be directly translated in order to be ran on the target CPU.

There are 2 I/O instructions.
### <a name="_toc112787914"></a>***IN***
#### *Full Name*
In
#### *Description*
The IN instruction reads the value on a particular port and writes it into a register.

|![Tip icon]|*Specific ports are defined in the Ports section.*|
| - | - |

|![Tip icon]|*Note that ports can also be made up and do not have to follow the official documentation.*<br>*In this case the programmer should define what is meant by each port if it is not obvious. A simple comment in the code is usually fine.*|
| - | - |

#### *Operands*
IN requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Register|Port|<pre>IN R1 %RNG</pre>|
#### *Code Examples*
    IN R1 %RNG

This instruction reads from the port “RNG” (which is defined in the port documentation as a random number generator) and the result is written into register 1.

    IN R2 %7SEG

This instruction reads from the port “7SEG” (which is **not** defined in the port documentation so it should be defined somewhere by the programmer), and the result is written into register 2.
### <a name="_toc112787915"></a>***OUT***
#### *Full Name*
Out
#### *Description*
The OUT instruction reads a value and outputs the result into a specific port.

|![Tip icon]|*Specific ports are defined in the Ports section.*|
| - | - |

|![Tip icon]|*Note that ports can also be made up and do not have to follow the official documentation.*<br>*In this case the programmer should define what is meant by each port if it is not obvious. A simple comment in the code is usually fine.*|
| - | - |

#### *Operands*
OUT requires 2 operands.

|**Destination**|**Source1**|**Example**|
| :-: | :-: | :-: |
|Port|Register|<pre>OUT %RNG R1</pre>|
|Port|Immediate|<pre>OUT %RNG 5</pre>|
#### *Code Examples*
    OUT %RNG R1

This instruction reads the value in register 1 and writes it into the port “RNG” (which is defined in the port documentation as a random number generator).

    OUT %7SEG 5

This instruction takes the immediate value 5 and writes it into port “7SEG” (which is **not** defined in the port documentation so it should be defined somewhere by the programmer).
# <a name="_toc112787916"></a>**INSTRUCTION TRANSLATIONS**
All Basic instructions can be translated into Core instructions and all Complex instructions can be translated into Basic and Core instructions.

This section covers the translations for each instruction.

|![Tip icon]|*In this section “\<A\>” refers to the first operand, “\<B\>” refers to the second operand and “\<C\>” refers to the third operand.*|
| - | - |

|![Tip icon]|*There are multiple translations for different operands. Each with specific conditions where that translation is valid.*<br>*So, of the translations where the conditions are met, the shortest translation should be used.*|
| - | - |

|![Tip icon]|*All relative values must be converted into labels before translating.*<br>*This is to prevent relative values from being broken as the translations are usually longer than one instruction.*|
| - | - |

|![Tip icon]|*Beware that most of the Basic translations require temporary registers.*<br>*Ensure the target CPU has enough temporary registers available before converting.*|
| - | - |

## <a name="_toc112787917"></a>**Basic Instruction Translations**
### <a name="_toc112787918"></a>***ADD***

|**Operand 1 \<A\>**|**Operand 2 \<B\>**|**Operand 3 \<C\>**|**Condition**|**Translation**|
| :-: | :-: | :-: | :-: | :-: |
|Register|Register|Register|Any|None|
|Register|Register|Immediate|A temporary register is required|<pre>IMM \<tempREG\> \<C\><br>ADD \<A\> \<B\> \<tempREG\></pre>|
|Register|Immediate|Register|A temporary register is required|<pre>IMM \<tempREG\> \<B\><br>ADD \<A\> \<tempREG\> \<C\></pre>|
|Register|Immediate|Immediate|Two temporary registers are required|<pre>IMM \<tempREG1\> \<B\><br>IMM \<tempREG2\> \<C\><br>ADD \<A\> \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787919"></a>***RSH***

|**Operand 1 \<A\>**|**Operand 2 \<B\>**|**Condition**|**Translation**|
| :-: | :-: | :-: | :-: |
|Register|Register|Any|None|
|Register|Immediate|A temporary register is required|<pre>IMM \<tempREG\> \<B\><br>RSH \<A\> \<tempREG\></pre>|
### <a name="_toc112787920"></a>***LOD***

|**Operand 1 \<A\>**|**Operand 2 \<B\>**|**Condition**|**Translation**|
| :-: | :-: | :-: | :-: |
|Register|Register|Any|None|
|Register|Immediate|A temporary register is required|<pre>IMM \<tempREG\> \<B\><br>LOD \<A\> \<tempREG\></pre>|
|PC|Register|A temporary register is required|<pre>LOD \<tempREG\> \<B\><br>JMP \<tempREG\></pre>|
|PC|Immediate|A temporary register is required|<pre>LOD \<tempREG\> \<B\><br>JMP \<tempREG\></pre>|
### <a name="_toc112787921"></a>***STR***

|**Operand 1 \<A\>**|**Operand 2 \<B\>**|**Condition**|**Translation**|
| :-: | :-: | :-: | :-: |
|Register|Register|Any|None|
|Register|Immediate|A temporary register is required|<pre>IMM \<tempREG\> \<A\><br>STR \<tempREG\> \<B\></pre>|
|Immediate|Register|A temporary register is required|<pre>IMM \<tempREG\> \<B\><br>STR \<A\> \<tempREG\></pre>|
|Immediate|Immediate|Two temporary registers are required|<pre>IMM \<tempREG1\> \<A\><br>IMM \<tempREG2\> \<B\><br>STR \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787922"></a>***BGE***

|**Operand 1 \<A\>**|**Operand 2 \<B\>**|**Operand 3 \<C\>**|**Condition**|**Translation**|
| :-: | :-: | :-: | :-: | :-: |
|Register|Register|Register|Any|None|
|Register|Register|Immediate|A temporary register is required|<pre>IMM \<tempREG\> \<C\><br>BGE \<A\> \<B\> \<tempREG\></pre>|
|Register|Immediate|Register|A temporary register is required|<pre>IMM \<tempREG\> \<B\><br>BGE \<A\> \<tempREG\> \<C\></pre>|
|Immediate|Register|Register|A temporary register is required|<pre>IMM \<tempREG\> \<A\><br>BGE \<tempREG\> \<B\> \<C\></pre>|
|Immediate|Register|Immediate|Two temporary registers are required|<pre>IMM \<tempREG1\> \<A\><br>IMM \<tempREG2\> \<C\><br>BGE \<tempREG1\> \<B\> \<tempREG2\></pre>|
|Immediate|Immediate|Register|Two temporary registers are required|<pre>IMM \<tempREG1\> \<A\><br>IMM \<tempREG2\> \<B\><br>BGE \<tempREG1\> \<tempREG2\> \<C\></pre>|
### <a name="_toc112787923"></a>***NOR***

|**Operand 1 \<A\>**|**Operand 2 \<B\>**|**Operand 3 \<C\>**|**Condition**|**Translation**|
| :-: | :-: | :-: | :-: | :-: |
|Register|Register|Register|Any|None|
|Register|Register|Immediate|A temporary register is required|<pre>IMM \<tempREG\> \<C\><br>NOR \<A\> \<B\> \<tempREG\></pre>|
|Register|Immediate|Register|A temporary register is required|<pre>IMM \<tempREG\> \<B\><br>NOR \<A\> \<tempREG\> \<C\></pre>|
### <a name="_toc112787924"></a>***SUB***

|![Tip icon]|*If the Operand types are not specified, then the translation applies to all possible combinations of operand types.*|
| - | - |

|**Condition**|**Translation**|
| :-: | :-: |
|\<B\> is the same as \<C\>|<pre>MOV \<A\> R0</pre>|
|\<A\> is different to \<B\>|<pre>NOT \<A\> \<C\><br>ADD \<A\> \<A\> \<B\><br>INC \<A\> \<A\></pre>|
|\<A\> is different to \<C\><br>and<br>\<C\> is a register|<pre>NOT \<C\> \<C\><br>ADD \<A\> \<B\> \<C\><br>INC \<A\> \<A\><br>NOT \<C\> \<C\></pre>|
|\<A\> is not R1|<pre>PSH R1<br>NOT R1 \<C\><br>ADD \<A\> \<B\> R1<br>INC \<A\> \<A\><br>POP R1</pre>|
|\<A\> is not R2|<pre>PSH R2<br>NOT R1 \<C\><br>ADD \<A\> \<B\> R1<br>INC \<A\> \<A\><br>POP R2</pre>|
### <a name="_toc112787925"></a>***JMP***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE \<A\> R0 R0</pre>|
### <a name="_toc112787926"></a>***MOV***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>ADD \<A\> \<B\> R0</pre>|
### <a name="_toc112787927"></a>***NOP***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>MOV R0 R0</pre>|
### <a name="_toc112787928"></a>***IMM***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>ADD \<A\> \<B\> R0</pre>|
### <a name="_toc112787929"></a>***LSH***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>ADD \<A\> \<B\> \<B\></pre>|
### <a name="_toc112787930"></a>***INC***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>ADD \<A\> \<B\> 1</pre>|
### <a name="_toc112787931"></a>***DEC***

|**Condition**|**Translation**|
| :-: | :-: |
|X is equal to an immediate value which has all its bits active. (255 in 8 bit)|ADD \<A\> \<B\> X|

|![Tip icon]|*Some of the translations include instructions that are in the same category as the original instruction.*<br>*If this is the case, then the code will need further translation if the goal is to lower the tier of instructions.*|
| - | - |

### <a name="_toc112787932"></a>***NEG***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>NOT \<A\> \<B\><br>INC \<A\> \<A\></pre>|
### <a name="_toc112787933"></a>***AND***

|**Condition**|**Translation**|
| :-: | :-: |
|\<B\> is the same as \<C\>|<pre>MOV \<C\> \<A\></pre>|
|\<A\> is different to \<C\><br>and<br>\<C\> is a register|<pre>NOT \<A\> \<B\><br>NOT \<C\> \<C\><br>NOR \<A\> \<A\> \<C\><br>NOT \<C\> \<C\></pre>|
|\<A\> is different to \<B\><br>and<br>\<B\> is a register|<pre>NOT \<B\> \<B\><br>NOT \<A\> \<C\><br>NOR \<A\> \<A\> \<B\><br>NOT \<B\> \<B\></pre>|
|\<A\> is different to R1 or R2|<pre>PSH R1<br>PSH R2<br>NOT R1 \<B\><br>NOT R2 \<C\><br>NOR \<A\> R1 R2<br>POP R2<br>POP R1</pre>|
|\<A\> is different to R3 or R4|<pre>PSH R3<br>PSH R4<br>NOT R3 \<B\><br>NOT R4 \<C\><br>NOR \<A\> R3 R4<br>POP R4<br>POP R3</pre>|
### <a name="_toc112787934"></a>***OR***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>NOR \<A\> \<B\> \<C\><br>NOT \<A\> \<A\></pre>|
### <a name="_toc112787935"></a>***NOT***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>NOR \<A\> \<B\> R0</pre>|
### <a name="_toc112787936"></a>***XNOR***

|**Condition**|**Translation**|
| :-: | :-: |
|\<B\> is the same as \<C\>|<pre>IMM \<A\> @MAX</pre>|
|\<A\> is different to R1|<pre>AND \<A\> \<B\> \<C\><br>PSH R1<br>NOR R1 \<B\> \<C\><br>NOR \<A\> \<A\> R1<br>POP R1<br>NOT \<A\> \<A\></pre>|
|\<A\> is different to R2|<pre>AND \<A\> \<B\> \<C\><br>PSH R2<br>NOR R1 \<B\> \<C\><br>NOR \<A\> \<A\> R2<br>POP R2<br>NOT \<A\> \<A\></pre>|
### <a name="_toc112787937"></a>***XOR***

|**Condition**|**Translation**|
| :-: | :-: |
|\<B\> is the same as \<C\>|<pre>MOV \<A\> R0</pre>|
|\<A\> is different to R1|<pre>AND \<A\> \<B\> \<C\><br>PSH R1<br>NOR R1 \<B\> \<C\><br>NOR \<A\> \<A\> R1<br>POP R1</pre>|
|\<A\> is different to R2|<pre>AND \<A\> \<B\> \<C\><br>PSH R2<br>NOR R1 \<B\> \<C\><br>NOR \<A\> \<A\> R2<br>POP R2</pre>|
### <a name="_toc112787938"></a>***NAND***

|**Condition**|**Translation**|
| :-: | :-: |
|\<B\> is the same as \<C\>|<pre>NOT \<A\> \<B\></pre>|
|\<A\> is different to \<C\><br>and<br>\<C\> is a register|<pre>NOT \<A\> \<B\><br>NOT \<C\> \<C\><br>NOR \<A\> \<A\> \<C\><br>NOT \<C\> \<C\><br>NOT \<A\> \<A\></pre>|
|\<A\> is different to \<B\><br>and<br>\<B\> is a register|<pre>NOT \<B\> \<B\><br>NOT \<A\> \<C\><br>NOR \<A\> \<A\> \<B\><br>NOT \<B\> \<B\><br>NOT \<A\> \<A\></pre>|
|\<A\> is different to R1|<pre>PSH R1<br>NOT R1 \<B\><br>NOT \<A\> \<C\><br>NOR \<A\> \<A\> R1<br>POP R1<br>NOT \<A\> \<A\></pre>|
|\<A\> is different to R2|<pre>PSH R2<br>NOT R1 \<B\><br>NOT \<A\> \<C\><br>NOR \<A\> \<A\> R2<br>POP R2<br>NOT \<A\> \<A\></pre>|
### <a name="_toc112787939"></a>***BRL***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE ~+2 \<B\> \<C\><br>JMP \<A\></pre>|
### <a name="_toc112787940"></a>***BRG***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE ~+2 \<C\> \<B\><br>JMP \<A\></pre>|
### <a name="_toc112787941"></a>***BRE***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE ~+2 \<B\> \<C\><br>JMP ~+4<br>BGE ~+2 \<C\> \<B\><br>JMP ~+2<br>JMP \<A\></pre>|
### <a name="_toc112787942"></a>***BNE***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE ~+2 \<B\> \<C\><br>JMP +2<br>BGE ~+2 \<C\> \<B\><br>JMP \<A\></pre>|
### <a name="_toc112787943"></a>***BOD***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>PSH R1<br>AND R1 \<B\> 1<br>BGE ~+2 R1 1<br>JMP ~+3<br>POP R1<br>JMP \<A\></pre>|
### <a name="_toc112787944"></a>***BEV***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>PSH R1<br>AND R1 \<B\> 1<br>BGE ~+2 R1 1<br>JMP \<A\><br>POP R1</pre>|
### <a name="_toc112787945"></a>***BLE***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE \<A\> \<C\> \<B\></pre>|
### <a name="_toc112787946"></a>***BRZ***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE ~+2 \<B\> 1<br>JMP \<A\></pre>|
### <a name="_toc112787947"></a>***BNZ***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE \<A\> \<B\> 1</pre>|
### <a name="_toc112787948"></a>***BRN***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE \<A\> \<B\> @MSB</pre>|
### <a name="_toc112787949"></a>***BRP***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>BGE ~+2 \<B\> @MSB<br>JMP \<A\></pre>|
### <a name="_toc112787950"></a>***PSH***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>DEC SP SP<br>STR SP \<A\></pre>|
### <a name="_toc112787951"></a>***POP***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>LOD \<A\> SP<br>INC SP SP</pre>|
### <a name="_toc112787952"></a>***CAL***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>PSH ~+2<br>JMP \<A\></pre>|
### <a name="_toc112787953"></a>***RET***

|**Condition**|**Translation**|
| :-: | :-: |
|A temporary register is required|<pre>POP \<tempREG\><br>JMP \<tempREG\></pre>|
|A temporary RAM location is required|<pre>PSH R1<br>INC SP SP<br>LOD R1 SP<br>STR \<tempRAM\> R1<br>DEC SP SP<br>POP R1<br>INC SP SP<br>LOD PC \<tempRAM\></pre>|
|Program must be support DW values|<pre>PSH R1<br>INC SP SP<br>LOD R1 SP<br>STR ~+5 R1<br>DEC SP SP<br>POP R1<br>INC SP SP<br>LOD PC ~+1<br>DW 0</pre>|
### <a name="_toc112787954"></a>***HLT***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>JMP ~+0</pre>|
### <a name="_toc112787955"></a>***CPY***

|**Condition**|**Translation**|
| :-: | :-: |
|A temporary register is required|<pre>LOD \<tempREG\> \<B\><br>STR \<A\> \<tempREG\></pre>|
|\<A\> is different to R1|<pre>PSH R1<br>LOD R1 \<B\><br>STR \<A\> R1<br>POP R1</pre>|
|\<A\> is different to R2|<pre>PSH R2<br>LOD R2 \<B\><br>STR \<A\> R2<br>POP R2</pre>|
### <a name="_toc112787956"></a>***BRC***

|**Condition**|**Translation**|
| :-: | :-: |
|A temporary register is required|<pre>ADD \<tempREG\> \<B\> \<C\><br>BRL \<A\> \<tempREG\> \<B\><br>BRL \<A\> \<tempREG\> \<C\></pre>|
|A temporary RAM location is required<br>and<br>\<A\> is different to R1<br>and<br>\<B\> is different to R1<br>and<br>\<C\> is different to R1|<pre>PSH R1<br>ADD R1 \<B\> \<C\><br>STR \<tempRAM\> \<A\><br>BRL ~+3 R1 \<B\><br>BRL ~+2 R1 \<C\><br>STR \<tempRAM\> ~+3<br>POP R1<br>LOD PC \<tempRAM\></pre>|
|A temporary RAM location is required<br>and<br>\<A\> is different to R2<br>and<br>\<B\> is different to R2<br>and<br>\<C\> is different to R2|<pre>PSH R2<br>ADD R2 \<B\> \<C\><br>STR \<tempRAM\> \<A\><br>BRL ~+3 R2 \<B\><br>BRL ~+2 R2 \<C\><br>STR \<tempRAM\> ~+3<br>POP R2<br>LOD PC \<tempRAM\></pre>|
|A temporary RAM location is required<br>and<br>\<A\> is different to R3<br>and<br>\<B\> is different to R3<br>and<br>\<C\> is different to R3|<pre>PSH R3<br>ADD R3 \<B\> \<C\><br>STR \<tempRAM\> \<A\><br>BRL ~+3 R3 \<B\><br>BRL ~+2 R3 \<C\><br>STR \<tempRAM\> ~+3<br>POP R3<br>LOD PC \<tempRAM\></pre>|
|A temporary RAM location is required<br>and<br>\<A\> is different to R4<br>and<br>\<B\> is different to R4<br>and<br>\<C\> is different to R4|<pre>PSH R4<br>ADD R4 \<B\> \<C\><br>STR \<tempRAM\> \<A\><br>BRL ~+3 R4 \<B\><br>BRL ~+2 R4 \<C\><br>STR \<tempRAM\> ~+3<br>POP R4<br>LOD PC \<tempRAM\></pre>|
### <a name="_toc112787957"></a>***BNC***

|**Condition**|**Translation**|
| :-: | :-: |
|A temporary register is required|<pre>LOD \<tempREG\> \<B\><br>STR \<A\> \<tempREG\></pre>|
|A temporary RAM location is required<br>and<br>\<A\> is different to R1<br>and<br>\<B\> is different to R1<br>and<br>\<C\> is different to R1|<pre>PSH R1<br>ADD R1 \<B\> \<C\><br>STR \<tempRAM\> ~+6<br>BRL ~+3 R1 \<B\><br>BRL ~+2 R1 \<C\><br>STR \<tempRAM\> \<A\><br>POP R1<br>LOD PC \<tempRAM\></pre>|
|A temporary RAM location is required<br>and<br>\<A\> is different to R2<br>and<br>\<B\> is different to R2<br>and<br>\<C\> is different to R2|<pre>PSH R2<br>ADD R2 \<B\> \<C\><br>STR \<tempRAM\> ~+6<br>BRL ~+3 R2 \<B\><br>BRL ~+2 R2 \<C\><br>STR \<tempRAM\> \<A\><br>POP R2<br>LOD PC \<tempRAM\></pre>|
|A temporary RAM location is required<br>and<br>\<A\> is different to R3<br>and<br>\<B\> is different to R3<br>and<br>\<C\> is different to R3|<pre>PSH R3<br>ADD R3 \<B\> \<C\><br>STR \<tempRAM\> ~+6<br>BRL ~+3 R3 \<B\><br>BRL ~+2 R3 \<C\><br>STR \<tempRAM\> \<A\><br>POP R3<br>LOD PC \<tempRAM\></pre>|
|A temporary RAM location is required<br>and<br>\<A\> is different to R4<br>and<br>\<B\> is different to R4<br>and<br>\<C\> is different to R4|<pre>PSH R4<br>ADD R4 \<B\> \<C\><br>STR \<tempRAM\> ~+6<br>BRL ~+3 R4 \<B\><br>BRL ~+2 R4 \<C\><br>STR \<tempRAM\> \<A\><br>POP R4<br>LOD PC \<tempRAM\></pre>|
## <a name="_toc112787958"></a>**Complex Instruction Translations**
### <a name="_toc112787959"></a>***MLT***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|\<A\> is different to R1<br>and<br>\<A\> is different to R2|Shift and Add|<pre>PSH R1<br>PSH R2<br>MOV R1 \<B\><br>MOV R2 \<C\><br>MOV \<A\> R0<br>BEV ~+2 R2<br>ADD \<A\> \<A\> R1<br>RSH R2 R2<br>LSH R1 R1<br>BNZ ~-4 R2<br>POP R2<br>POP R1</pre>|
|\<A\> is different to R3 <br>and<br>\<A\> is different to R4|Shift and Add|<pre>PSH R3<br>PSH R4<br>MOV R3 \<B\><br>MOV R4 \<C\><br>MOV \<A\> R0<br>BEV ~+2 R4<br>ADD \<A\> \<A\> R3<br>RSH R4 R4<br>LSH R3 R3<br>BNZ ~-4 R4<br>POP R4<br>POP R3</pre>|
|\<A\> is different to R1 <br>and<br>\<A\> is different to R2|Repeated Addition|<pre>PSH R1<br>PSH R2<br>MOV R1 \<C\><br>MOV R2 \<B\><br>MOV \<A\> R0<br>BRZ ~+4 \<C\><br>DEC R1 R1<br>ADD \<A\> \<A\> R2<br>BNZ ~-2 R1<br>POP R2<br>POP R1</pre>|
|\<A\> is different to R3<br>and<br>\<A\> is different to R4|Repeated Addition|<pre>PSH R3<br>PSH R4<br>MOV R3 \<C\><br>MOV R4 \<B\><br>MOV \<A\> R0 <br>BRZ ~+4 \<C\><br>DEC R3 R3<br>ADD \<A\> \<A\> R4<br>BNZ ~-2 R3<br>POP R4<br>POP R3</pre>|
### <a name="_toc112787960"></a>***DIV***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|\<A\> is different to R1<br>and<br>\<A\> is different to \<C\>|Repeated Subtraction|<pre>BRL ~+9 \<B\> \<C\><br>PSH R1<br>MOV R1 \<B\><br>MOV \<A\> R0<br>INC \<A\> \<A\><br>SUB R1 R1 \<C\><br>BGE ~-2 R1 \<C\><br>POP R1<br>JMP ~+2<br>MOV \<A\> R0</pre>|
|\<A\> is different to R2<br>and<br>\<A\> is different to \<C\>|Repeated Subtraction|<pre>BRL ~+9 \<B\> \<C\><br>PSH R2<br>MOV R2 \<B\><br>MOV \<A\> R0<br>INC \<A\> \<A\><br>SUB R2 R2 \<C\><br>BGE ~-2 R2 \<C\><br>POP R2<br>JMP ~+2<br>MOV \<A\> R0</pre>|
|\<A\> is different to R1<br>and<br>\<A\> is different to R2|Repeated Subtraction|<pre>BRL ~+13 \<B\> \<C\><br>PSH R1<br>PSH R2<br>MOV R1 \<B\><br>MOV R2 \<C\><br>MOV \<A\> R0<br>INC \<A\> \<A\><br>SUB R1 R1 R2<br>BGE ~-2 R1 R2<br>POP R2<br>POP R1<br>JMP ~+2<br>MOV \<A\> R0</pre>|
|\<A\> is different to R3<br>and<br>\<A\> is different to R4|Repeated Subtraction|<pre>BRL ~+13 \<B\> \<C\><br>PSH R3<br>PSH R4<br>MOV R3 \<B\><br>MOV R4 \<C\><br>MOV \<A\> R0<br>INC \<A\> \<A\><br>SUB R3 R3 R4<br>BGE ~-2 R3 R4<br>POP R4<br>POP R3<br>JMP ~+2<br>MOV \<A\> R0</pre>|
### <a name="_toc112787961"></a>***MOD***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|\<A\> is different to \<C\>|Repeated Subtraction|<pre>MOV \<A\> \<B\><br>BRL ~+3 \<A\> \<C\><br>SUB \<A\> \<A\> \<C\><br>JMP ~-2</pre>|
|\<A\> is different to R1<br>and<br>\<B\> is different to R1|Repeated Subtraction|<pre>PSH R1<br>MOV R1 \<C\><br>MOV \<A\> \<B\><br>BRL ~+3 \<B\> R1<br>SUB \<A\> \<A\> R1<br>JMP ~-2<br>POP R1</pre>|
|\<A\> is different to R2<br>and<br>\<B\> is different to R2|Repeated Subtraction|<pre>PSH R2<br>MOV R2 \<C\><br>MOV \<A\> \<B\><br>BRL ~+3 \<A\> R2<br>SUB \<A\> \<A\> R2<br>JMP ~-2<br>POP R2</pre>|
|\<A\> is different to R3<br>and<br>\<B\> is different to R3|Repeated Subtraction|<pre>PSH R3<br>MOV R3 \<C\><br>MOV \<A\> \<B\><br>BRL ~+3 \<A\> R3<br>SUB \<A\> \<A\> R3<br>JMP ~-2<br>POP R3</pre>|
### <a name="_toc112787962"></a>***BSR***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|\<A\> is different to R1<br>and<br>\<B\> is different to R1||PSH R1<br>MOV R1 \<C\><br>MOV \<A\> \<B\><br>BRZ ~+4 R1<br>RSH \<A\> \<A\><br>DEC R1 R1<br>JMP ~-3<br>POP R1|
|\<A\> is different to R2<br>and<br>\<B\> is different to R2||PSH R2<br>MOV R2 \<C\><br>MOV \<A\> \<B\><br>BRZ ~+4 R2<br>RSH \<A\> \<A\><br>DEC R2 R2<br>JMP ~-3<br>POP R2|
|\<A\> is different to R3<br>and<br>\<B\> is different to R3||PSH R3<br>MOV R3 \<C\><br>MOV \<A\> \<B\><br>BRZ ~+4 R3<br>RSH \<A\> \<A\><br>DEC R3 R3<br>JMP ~-3<br>POP R3|
### <a name="_toc112787963"></a>***BSL***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|\<A\> is different to R1<br>and<br>\<B\> is different to R1||<pre>PSH R1<br>MOV R1 \<C\><br>MOV \<A\> \<B\><br>BRZ ~+~4 R1<br>LSH \<A\> \<A\><br>DEC R1 R1<br>JMP ~-3<br>POP R1</pre>|
|\<A\> is different to R2<br>and<br>\<B\> is different to R2||<pre>PSH R2<br>MOV R2 \<C\><br>MOV \<A\> \<B\><br>BRZ ~+4 R2<br>LSH \<A\> \<A\><br>DEC R2 R2<br>JMP ~-3<br>POP R2</pre>|
|\<A\> is different to R3<br>and<br>\<B\> is different to R3||<pre>PSH R3<br>MOV R3 \<C\><br>MOV \<A\> \<B\><br>BRZ ~+4 R3<br>LSH \<A\> \<A\><br>DEC R3 R3<br>JMP ~-3<br>POP R3</pre>|
### <a name="_toc112787964"></a>***SRS***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Any||<pre>BRN ~+3 \<B\><br>RSH \<A\> \<B\><br>JMP ~+3<br>RSH \<A\> \<B\><br>ADD \<A\> \<A\> @MSB</pre>|
### <a name="_toc112787965"></a>***BSS***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|\<A\> is different to R1<br>and<br>\<B\> is different to R1||<pre>PSH R1<br>MOV R1 \<C\><br>MOV \<A\> \<B\><br>BRZ ~+4 R1<br>SRS \<A\> \<A\><br>DEC R1 R1<br>JMP ~-3<br>POP R1</pre>|
|\<A\> is different to R2<br>and<br>\<B\> is different to R2||<pre>PSH R2<br>MOV R2 \<C\><br>MOV \<A\> \<B\><br>BRZ ~+4 R2<br>SRS \<A\> \<A\><br>DEC R2 R2<br>JMP ~-3<br>POP R2</pre>|
|\<A\> is different to R3<br>and<br>\<B\> is different to R3||<pre>PSH R3<br>MOV R3 \<C\><br>MOV \<A\> \<B\><br>BRZ ~+4 R3<br>SRS \<A\> \<A\><br>DEC R3 R3<br>JMP ~-3<br>POP R3</pre>|
### <a name="_toc112787966"></a>***SETE***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Any||<pre>BRE ~+3 \<B\> \<C\><br>MOV \<A\> R0<br>JMP ~+2<br>IMM \<A\> -1</pre>|
### <a name="_toc112787967"></a>***SETNE***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Any||<pre>BNE ~+3 \<B\> \<C\><br>MOV \<A\> R0<br>JMP ~+2<br>IMM \<A\> -1</pre>|
### <a name="_toc112787968"></a>***SETG***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Any||<pre>BRG ~+3 \<B\> \<C\><br>MOV \<A\> R0<br>JMP ~+2<br>IMM \<A\> -1</pre>|
### <a name="_toc112787969"></a>***SETL***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Any||<pre>BRL ~+3 \<B\> \<C\><br>MOV \<A\> R0<br>JMP ~+2<br>IMM \<A\> -1</pre>|
### <a name="_toc112787970"></a>***SETGE***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Any||<pre>BGE ~+3 \<B\> \<C\><br>MOV \<A\> R0<br>JMP ~+2<br>IMM \<A\> -1</pre>|
### <a name="_toc112787971"></a>***SETLE***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Any||<pre>BLE ~+3 \<B\> \<C\><br>MOV \<A\> R0<br>JMP ~+2<br>IMM \<A\> -1</pre>|
### <a name="_toc112787972"></a>***SETC***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|A temporary register is required||<pre>MOV \<tempREG\> \<B\><br>BRG +2 \<B\> \<C\><br>MOV \<tempREG\> \<C\><br>ADD \<A\> \<B\> \<C\><br>SETL \<A\> \<A\> \<tempREG\></pre>|
|\<A\> is different to R1<br>and<br>\<B\> is different to R1<br>and<br>\<C\> is different to R1||<pre>PSH R1<br>MOV R1 \<B\><br>BRG ~+2 \<B\> \<C\><br>MOV R1 \<C\><br>ADD \<A\> \<B\> \<C\><br>SETL \<A\> \<A\> R1<br>POP R1</pre>|
|\<A\> is different to R2<br>and<br>\<B\> is different to R2<br>and<br>\<C\> is different to R2||<pre>PSH R2<br>MOV R2 \<B\><br>BRG ~+2 \<B\> \<C\><br>MOV R2 \<C\><br>ADD \<A\> \<B\> \<C\><br>SETL \<A\> \<A\> R2<br>POP R2</pre>|
|\<A\> is different to R3<br>and<br>\<B\> is different to R3<br>and<br>\<C\> is different to R3||<pre>PSH R3<br>MOV R3 \<B\><br>BRG ~+2 \<B\> \<C\><br>MOV R3 \<C\><br>ADD \<A\> \<B\> \<C\><br>SETL \<A\> \<A\> R3<br>POP R3</pre>|
|\<A\> is different to R4<br>and<br>\<B\> is different to R4<br>and<br>\<C\> is different to R4||<pre>PSH R4<br>MOV R4 \<B\><br>BRG ~+2 \<B\> \<C\><br>MOV R4 \<C\><br>ADD \<A\> \<B\> \<C\><br>SETL \<A\> \<A\> R4<br>POP R4</pre>|
### <a name="_toc112787973"></a>***SETNC***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|A temporary register is required||<pre>MOV \<tempREG\> \<B\><br>BRG ~+2 \<B\> \<C\><br>MOV \<tempREG\> \<C\><br>ADD \<A\> \<B\> \<C\><br>SETGE \<A\> \<A\> \<tempREG\></pre>|
|\<A\> is different to R1<br>and<br>\<B\> is different to R1<br>and<br>\<C\> is different to R1||<pre>PSH R1<br>MOV R1 \<B\><br>BRG ~+2 \<B\> \<C\><br>MOV R1 \<C\><br>ADD \<A\> \<B\> \<C\><br>SETGE \<A\> \<A\> R1<br>POP R1</pre>|
|\<A\> is different to R2<br>and<br>\<B\> is different to R2<br>and<br>\<C\> is different to R2||<pre>PSH R2<br>MOV R2 \<B\><br>BRG ~+2 \<B\> \<C\><br>MOV R2 \<C\><br>ADD \<A\> \<B\> \<C\><br>SETGE \<A\> \<A\> R2<br>POP R2</pre>|
|\<A\> is different to R3<br>and<br>\<B\> is different to R3<br>and<br>\<C\> is different to R3||<pre>PSH R3<br>MOV R3 \<B\><br>BRG ~+2 \<B\> \<C\><br>MOV R3 \<C\><br>ADD \<A\> \<B\> \<C\><br>SETGE \<A\> \<A\> R3<br>POP R3</pre>|
|\<A\> is different to R4<br>and<br>\<B\> is different to R4<br>and<br>\<C\> is different to R4||<pre>PSH R4<br>MOV R4 \<B\><br>BRG ~+2 \<B\> \<C\><br>MOV R4 \<C\><br>ADD \<A\> \<B\> \<C\><br>SETGE \<A\> \<A\> R4<br>POP R4</pre>|

### <a name="_toc112787974"></a>***LLOD***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Any||<pre>ADD \<A\> \<B\> \<C\><br>LOD \<A\> \<A\></pre>|
### <a name="_toc112787975"></a>***LSTR***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|A temporary register is required||<pre>ADD \<tempREG\> \<A\> \<B\><br>STR \<C\> \<tempREG\></pre>|
|\<C\> is different to R1||<pre>PSH R1<br>ADD R1 \<A\> \<B\><br>STR \<C\> R1<br>POP R1</pre>|
|\<C\> is different to R2||<pre>PSH R2<br>ADD R1 \<A\> \<B\><br>STR \<C\> R2<br>POP R2</pre>|
### <a name="_toc112787976"></a>***SDIV***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Three temporary registers are required||<pre>IMM \<tempREG1\> 0<br>MOV \<tempREG2\> \<B\><br>BRP ~+3 \<B\><br>NEG \<tempREG2\> \<B\><br>IMM \<tempREG1\> @MSB<br>MOV \<tempREG3\> \<C\><br>BRP ~+3 \<C\><br>NEG \<tempREG3\> \<C\><br>ADD \<tempREG1\> \<tempREG1\> @MSB<br>DIV \<A\> \<tempREG2\> \<tempREG3\><br>BRP ~+2 \<A\><br>NEG \<A\> \<A\></pre>|
### <a name="_toc112787977"></a>***SBRL***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Two temporary registers are required||<pre>MOV \<tempREG1\> \<B\><br>BRP ~+2 \<B\><br>ADD \<tempREG1\> \<B\> @MSB<br>MOV \<tempREG2\> \<C\><br>BRP ~+2 \<C\><br>ADD \<tempREG2\> \<C\> @MSB<br>BRL \<A\> \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787978"></a>***SBRG***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Two temporary registers are required||<pre>MOV \<tempREG1\> \<B\><br>BRP ~+2 \<B\><br>ADD \<tempREG1\> \<B\> @MSB<br>MOV \<tempREG2\> \<C\><br>BRP ~+2 \<C\><br>ADD \<tempREG2\> \<C\> @MSB<br>BRG \<A\> \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787979"></a>***SBLE***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Two temporary registers are required||<pre>MOV \<tempREG1\> \<B\><br>BRP ~+2 \<B\><br>ADD \<tempREG1\> \<B\> @MSB<br>MOV \<tempREG2\> \<C\><br>BRP ~+2 \<C\><br>ADD \<tempREG2\> \<C\> @MSB<br>SBLE \<A\> \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787980"></a>***SBGE***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Two temporary registers are required||<pre>MOV \<tempREG1\> \<B\><br>BRP ~+2 \<B\><br>ADD \<tempREG1\> \<B\> @MSB<br>MOV \<tempREG2\> \<C\><br>BRP ~+2 \<C\><br>ADD \<tempREG2\> \<C\> @MSB<br>SBGE \<A\> \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787981"></a>***SSETL***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Two temporary registers are required||<pre>MOV \<tempREG1\> \<B\><br>BRP ~+2 \<B\><br>ADD \<tempREG1\> \<B\> @MSB<br>MOV \<tempREG2\> \<C\><br>BRP ~+2 \<C\><br>ADD \<tempREG2\> \<C\> @MSB<br>SETL \<A\> \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787982"></a>***SSETG***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Two temporary registers are required||<pre>MOV \<tempREG1\> \<B\><br>BRP ~+2 \<B\><br>ADD \<tempREG1\> \<B\> @MSB<br>MOV \<tempREG2\> \<C\><br>BRP ~+2 \<C\><br>ADD \<tempREG2\> \<C\> @MSB<br>SETG \<A\> \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787983"></a>***SSETLE***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Two temporary registers are required||<pre>MOV \<tempREG1\> \<B\><br>BRP ~+2 \<B\><br>ADD \<tempREG1\> \<B\> @MSB<br>MOV \<tempREG2\> \<C\><br>BRP ~+2 \<C\><br>ADD \<tempREG2\> \<C\> @MSB<br>SETLE \<A\> \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787984"></a>***SSETGE***

|**Condition**|**Extra Information**|**Translation**|
| :-: | :-: | :-: |
|Two temporary registers are required||<pre>MOV \<tempREG1\> \<B\><br>BRP ~+2 \<B\><br>ADD \<tempREG1\> \<B\> @MSB<br>MOV \<tempREG2\> \<C\><br>BRP ~+2 \<C\><br>ADD \<tempREG2\> \<C\> @MSB<br>SETGE \<A\> \<tempREG1\> \<tempREG2\></pre>|
### <a name="_toc112787985"></a>***ABS***

|**Condition**|**Translation**|
| :-: | :-: |
|Any|<pre>MOV \<A\> \<B\><br>BRP ~+2 \<A\><br>NEG \<A\> \<A\></pre>|
# <a name="_toc112787986"></a>**PORTS**
There are 64 official ports.

The word length of the value of each port is equal to the word length of the CPU.

Ports can be written to or read from using the I/O instructions as appropriate.

|![Tip icon]|*Official ports can be used in URCL programs without having to be defined. They use the definition given here.*|
| - | - |

|![Tip icon]|*Note that the programmer can make up any ports and these do not have to follow the official documentation.*<br>*In this case the programmer should define what is meant by each port if it is not obvious. A simple comment in the code is usually fine if it is not too complex.*|
| - | - |

<table><tr><th colspan="1" valign="bottom"><B>Type</b></th><th colspan="1" valign="bottom"><B>Port Number</b></th><th colspan="1" valign="bottom"><B>Alias (Port Name)</b></th><th colspan="1" valign="bottom"><B>Full Name</b></th><th colspan="1" valign="bottom"><B>Input Notes/Usage</b></th><th colspan="1" valign="bottom"><B>Output Notes/Usage</b></th><th colspan="1" valign="bottom"><B>Valid Inputs</b></th></tr>
<tr><td colspan="1" rowspan="8">General</td><td colspan="1">0</td><td colspan="1">%CPUBUS</td><td colspan="1">CPU Bus</td><td colspan="1"></td><td colspan="1"></td><td colspan="1">Number</td></tr>
<tr><td colspan="1">1</td><td colspan="1">%TEXT</td><td colspan="1">Text IO</td><td colspan="1">Generic text input</td><td colspan="1">Generic text output</td><td colspan="1">Number, Character</td></tr>
<tr><td colspan="1">2</td><td colspan="1">%NUMB</td><td colspan="1">Numeric IO</td><td colspan="1">Generic number input</td><td colspan="1">Generic number output</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">3</td><td colspan="1"></td><td colspan="1">Reserved</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">4</td><td colspan="1"></td><td colspan="1">Reserved</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">5</td><td colspan="1">%SUPPORTED</td><td colspan="1">Port Supported</td><td colspan="1">Returns 0 if the port does not exist</td><td colspan="1">Sets value to return if it does exist, this can be handled by a compiler if the CPU does not support it</td><td colspan="1">Number, Port Alias</td></tr>
<tr><td colspan="1">6</td><td colspan="1">%SPECIAL</td><td colspan="1">Special</td><td colspan="1">User Defined</td><td colspan="1">User Defined</td><td colspan="1"></td></tr>
<tr><td colspan="1">7</td><td colspan="1">%PROFILE</td><td colspan="1">Profile</td><td colspan="1">Tells current Profile</td><td colspan="1">Sets Profile</td><td colspan="1">Number</td></tr>
<tr><td colspan="1" rowspan="8">Graphics</td><td colspan="1">8</td><td colspan="1">%X</td><td colspan="1">Display X</td><td colspan="1">Tells display width</td><td colspan="1">Sets X Vertex</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">9</td><td colspan="1">%Y</td><td colspan="1">Display Y</td><td colspan="1">Tells display height</td><td colspan="1">Sets Y Vertex</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">10</td><td colspan="1">%COLOR or %COLOUR</td><td colspan="1">Colour</td><td colspan="1">Reads colour at %X, %Y into a register (from the currently writeable part of the screen)</td><td colspan="1">Draws a pixel of the specified colour at %X, %Y (on the currently writeable part of the screen)</td><td colspan="1">Colour</td></tr>
<tr><td colspan="1">11</td><td colspan="1">%BUFFER</td><td colspan="1">Display Buffer</td><td colspan="1">Reads buffer state</td><td colspan="1">0 copies buffer to display, and disables it,1 enables writing to the buffer and locks the screen from being updated2 disables, then reenables the buffer which updates the screen to the buffer, but the buffer remains enabled</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">12</td><td colspan="1">%FREEZE</td><td colspan="1">Freeze</td><td colspan="1">Freezes screen</td><td colspan="1">Freezes the visible part of the screen.Reading and writing to the screen still works but does not visually update the screen.</td><td colspan="1">Any</td></tr>
<tr><td colspan="1">13</td><td colspan="1">%UNFREEZE</td><td colspan="1">Unfreeze</td><td colspan="1">Unfreezes screen</td><td colspan="1">Unfreezes the visible part of the screen.The visual screen now shows what the screen contains.</td><td colspan="1">Any</td></tr>
<tr><td colspan="1">14</td><td colspan="1">%CLEAR</td><td colspan="1">Clear</td><td colspan="1">Clears screen</td><td colspan="1">Clears the screen.This does not unfreeze the screen if it is frozen.</td><td colspan="1">Any</td></tr>
<tr><td colspan="1">15</td><td colspan="1">%GSPECIAL</td><td colspan="1">Graphics Special</td><td colspan="1">User Defined</td><td colspan="1">User Defined</td><td colspan="1"></td></tr>
<tr><td colspan="1" rowspan="8">Text</td><td colspan="1">16</td><td colspan="1">%ASCII8</td><td colspan="1">8-Bit ASCII</td><td colspan="1">Takes in an 8-Bit Ascii character</td><td colspan="1">Displays an 8-bit ascii character</td><td colspan="1">Number, Character</td></tr>
<tr><td colspan="1">17</td><td colspan="1">%CHAR5</td><td colspan="1">5-Bit Char</td><td colspan="1">Takes in a 5-bit character</td><td colspan="1">Displays a 5 bit character</td><td colspan="1">Number, Character</td></tr>
<tr><td colspan="1">18</td><td colspan="1">%CHAR6</td><td colspan="1">6-Bit Char</td><td colspan="1">Takes in a 6-bit character</td><td colspan="1">Displays a 6 bit character</td><td colspan="1">Number, Character</td></tr>
<tr><td colspan="1">19</td><td colspan="1">%ASCII7</td><td colspan="1">7-Bit ASCII</td><td colspan="1">Takes in a 7-Bit ASCII character</td><td colspan="1">Displays a 7-bit ascii character</td><td colspan="1">Number, Character</td></tr>
<tr><td colspan="1">20</td><td colspan="1">%UTF8</td><td colspan="1">UTF-8</td><td colspan="1">Takes in a UTF-8 character (1-4 bytes)</td><td colspan="1">Displays a UTF-8 character</td><td colspan="1">Number, Character</td></tr>
<tr><td colspan="1">21</td><td colspan="1"></td><td colspan="1">Reserved</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">22</td><td colspan="1"></td><td colspan="1">Reserved</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">23</td><td colspan="1">%TSPECIAL</td><td colspan="1">Text Special</td><td colspan="1">User Defined</td><td colspan="1">User Defined</td><td colspan="1"></td></tr>
<tr><td colspan="1" rowspan="8">Numbers</td><td colspan="1">24</td><td colspan="1">%INT</td><td colspan="1">Signed Integer</td><td colspan="1">Takes in a signed integer</td><td colspan="1">Displays a signed integer</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">25</td><td colspan="1">%UINT</td><td colspan="1">Unsigned Integer</td><td colspan="1">Takes in an unsigned integer</td><td colspan="1">Displays an unsigned integer</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">26</td><td colspan="1">%BIN</td><td colspan="1">Binary</td><td colspan="1">Takes in a binary number</td><td colspan="1">Displays a binary number</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">27</td><td colspan="1">%HEX</td><td colspan="1">Hexadecimal</td><td colspan="1">Takes in a hexadecimal number</td><td colspan="1">Displays a hexadecimal number</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">28</td><td colspan="1">%FLOAT</td><td colspan="1">Floating Point Number</td><td colspan="1">Takes in a floating-point number</td><td colspan="1">Displays a floating-point number</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">29</td><td colspan="1">%FIXED</td><td colspan="1">Fixed Point Number</td><td colspan="1">Takes in a fixed-point number</td><td colspan="1">Displays a fixed-point number</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">30</td><td colspan="1"></td><td colspan="1">Reserved</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">31</td><td colspan="1">%N-SPECIAL</td><td colspan="1">Numbers Special</td><td colspan="1">User Defined</td><td colspan="1">User Defined</td><td colspan="1"></td></tr>
<tr><td colspan="1" rowspan="8">Storage</td><td colspan="1">32</td><td colspan="1">%ADDR</td><td colspan="1">Address</td><td colspan="1">Tells address</td><td colspan="1">Sets address</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">33</td><td colspan="1">%BUS</td><td colspan="1">Bus</td><td colspan="1">Reads the data at the address</td><td colspan="1">Writes data to that address</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">34</td><td colspan="1">%PAGE</td><td colspan="1">Page</td><td colspan="1">Reads the page number</td><td colspan="1">Sets the page number</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">35</td><td colspan="1"></td><td colspan="1">Reserved</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">36</td><td colspan="1"></td><td colspan="1">Reserved</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">37</td><td colspan="1"></td><td colspan="1">Reserved</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">38</td><td colspan="1"></td><td colspan="1">Reserved</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">39</td><td colspan="1">%SSPECIAL</td><td colspan="1">Storage Special</td><td colspan="1">User Defined</td><td colspan="1">User Defined</td><td colspan="1"></td></tr>
<tr><td colspan="1" rowspan="8">Miscellaneous</td><td colspan="1">40</td><td colspan="1">%RNG</td><td colspan="1">RNG Device</td><td colspan="1">Reads a random number</td><td colspan="1">Sets a seed or device specific</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">41</td><td colspan="1">%NOTE</td><td colspan="1">Note</td><td colspan="1">Reads sound device pitch</td><td colspan="1">Sets sound device pitch</td><td colspan="1">Number, Note</td></tr>
<tr><td colspan="1">42</td><td colspan="1">%INSTR</td><td colspan="1">Instrument</td><td colspan="1">Reads sound device instrument</td><td colspan="1">Sets sound device instrument</td><td colspan="1">Number, Instrument</td></tr>
<tr><td colspan="1">43</td><td colspan="1">%NLEG</td><td colspan="1">Note length</td><td colspan="1">Device specific</td><td colspan="1">Sets sound device note length and plays that note (in tenths?)</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">44</td><td colspan="1">%WAIT</td><td colspan="1">Wait</td><td colspan="1">Returns 1 after the wait period</td><td colspan="1">Sets wait period (in tenths of seconds)</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">45</td><td colspan="1">%NADDR</td><td colspan="1">Network Address</td><td colspan="1">Reads the current address</td><td colspan="1">Sets the network address</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">46</td><td colspan="1">%DATA</td><td colspan="1">Network Data</td><td colspan="1">Reads network data</td><td colspan="1">Sends network data</td><td colspan="1">Number</td></tr>
<tr><td colspan="1">47</td><td colspan="1">%MSPECIAL</td><td colspan="1">Miscellaneous Special</td><td colspan="1">User Defined</td><td colspan="1">User Defined</td><td colspan="1"></td></tr>
<tr><td colspan="1" rowspan="16">User defined</td><td colspan="1">48</td><td colspan="1">%UD1</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">49</td><td colspan="1">%UD2</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">50</td><td colspan="1">%UD3</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">51</td><td colspan="1">%UD4</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">52</td><td colspan="1">%UD5</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">53</td><td colspan="1">%UD6</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">54</td><td colspan="1">%UD7</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">55</td><td colspan="1">%UD8</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">56</td><td colspan="1">%UD9</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">57</td><td colspan="1">%UD10</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">58</td><td colspan="1">%UD11</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">59</td><td colspan="1">%UD12</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">60</td><td colspan="1">%UD13</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">61</td><td colspan="1">%UD14</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">62</td><td colspan="1">%UD15</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
<tr><td colspan="1">63</td><td colspan="1">%UD16</td><td colspan="1">User Defined</td><td colspan="1"></td><td colspan="1"></td><td colspan="1"></td></tr>
</table>

# <a name="_toc112787987"></a>**CODE FAULTS**

|![Tip icon]|*This section contains most common faults and the most likely causes as well as possible solutions.*|
| - | - |

Faults within the code can be detected using a URCL emulator.

It is important to test for and fix these faults before deploying the code onto a target CPU. The code is unable to detect these errors itself when deployed.
## <a name="_toc112787988"></a>**Pre-Runtime Faults**
These are faults which can be detected before running the code.

|![Tip icon]|*These faults can be detected by static analysis before execution, such as part of a generic URCL code optimiser.*|
| - | - |

### <a name="_toc112787989"></a>***Invalid Number of Operands***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|Too many operands were given for an instruction.|Rewrite the instruction in question, making sure that the number of operands match the expected value given in the Instruction section.|
|Too few operands were given for an instruction.|Rewrite the instruction in question, making sure that the number of operands match the expected value given in the Instruction section.|

### <a name="_toc112787990"></a>***Invalid Operand Types***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|The types of operands that were given for an instruction are not in the valid operand types which are listed in the Instruction section.|Rewrite the instruction in question, making sure that the types are valid as per the operand type tables provided in the Instruction section.|
### <a name="_toc112787991"></a>***Unrecognised Identifier***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|Invalid instruction name.|Rewrite the instruction in question, making sure that the name is spelt exactly as given in the Instruction section.|
|Invalid operand name.|Rewrite the instruction in question, making sure that the operands have the correct prefix if required. These are specified in the Prefix section.|
|Comment that has not be marked as a comment.|Add `//` or `/*` and `*/` as appropriate to the comment.|
|Invalid header name.|Rewrite the header in question, making sure that the name is spelt exactly as given in the Header section.|
|Label without prefix.|Add the prefix `.` on to the label in question.|
### <a name="_toc112787992"></a>***Unsupported Number of Registers***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|The value of MINREG is higher than 2 to the power of CPU Word Length. (256 on an 8 bit CPU)|Lower the number of registers the program requires by using the Heap and Stack or increase the word length. This may require rewriting large parts of the program.|
|The program uses a register which is larger than the value set in the MINREG header.|Increase the value of the MINREG header to match the minimum required by the program.|
### <a name="_toc112787993"></a>***Unsupported Heap Size***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|The value of MINHEAP is higher than 2 to the power of CPU Word Length. (256 on an 8 bit CPU)|Lower the number of words of heap the program requires or increase the word length. This may require rewriting large parts of the program.|
### <a name="_toc112787994"></a>***Unsupported Stack Size***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|The value of MINSTACK is higher than 2 to the power of CPU Word Length. (256 on an 8 bit CPU)|Lower the number of stack values the program requires or increase the word length. This may require rewriting large parts of the program.|

### <a name="_toc112787995"></a>***Invalid Label Name***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|Label name contains invalid characters.|Rename the label in question, making sure that the label name consists of only letters, numbers, and underscore.|
### <a name="_toc112787996"></a>***Duplicate Label Definition***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|The same label is defined multiple times.|Remove or rename one of the label definitions. Each label should only be defined once.|
## <a name="_toc112787997"></a>**Runtime Faults**
These are faults which can only be detected by running the code.
### <a name="_toc112787998"></a>***Non-Instruction Execution***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|Branched to a value which does not point towards an instruction.|Rewrite the code in question to make sure the branch address always points to a valid instruction.|
|A non-instruction pointer is loaded into the program counter.|Rewrite the code in question to make sure the load target always points to a valid instruction.|
|The program fails to branch around DW values.|Add JMP instructions to branch around the DW value or move the DW values elsewhere in the program.|
### <a name="_toc112787999"></a>***Stack Underflow***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|Popping from the stack while it is empty.|Rewrite code to ensure the POP instruction is only called when there are values on the stack.|
|The stack pointer lost sync with the actual size of the stack.|Avoid editing the stack pointer directly in the code as this can cause it to be desynced if not handled properly.|
### <a name="_toc112788000"></a>***Stack Overflow***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|The stack overlaps the heap.|Rewrite code to ensure the heap and stack do not get too big or increase the values of the MINHEAP and MINSTACK headers.|
|The stack pointer lost sync with the actual size of the stack.|Avoid editing the stack pointer directly in the code as this can cause it to be desynced if not handled properly.|
### <a name="_toc112788001"></a>***Invalid RAM Location***

|**Potential Cause**|**Potential Fix**|
| :-: | :-: |
|Attempted to write to a RAM location which does not exist.|Rewrite code to ensure that invalid RAM addresses are not written to or increase the value of the MINHEAP header to include that RAM address.|
|Attempted to read from a RAM location which does not exist.|Rewrite code to ensure that invalid RAM addresses are not read from or increase the value of the MINHEAP header to include that RAM address.|
# <a name="_toc112788002"></a>**INTERPRETING URCL**
Due to how simple it is to translate from URCL to a target CPU’s assembly, it is possible to store the raw URCL code on the target CPU and get the CPU to interpret and translate the code itself during execution.

This is a lot slower than running compiled code but can offer some advantages, such as being able to modify the instructions more easily during execution.
## <a name="_toc112788003"></a>**Bitwise Representation**
There are several different ways to represent URCL code, some of which are given here.

Each operand requires one full word length, and the operand type must be stored separately.

There are only two types that an operand can be, and the exact pair of types depend on the instruction. This means that the operand type can be represented using a single bit for each operand.

There are 59 URCL instructions. This means that 6 bits are required to be able to represent them all.

|![Tip icon]|*To represent just the Core instructions, only 3 bits are required.*|
| - | - |

This means that 1 to 5 words are required to represent each instruction.

The first 1 or 2 words represent the instruction and the operand types. Then the remaining 0 to 3 words represent the number of operands.

On an 8 bit CPU this could look like:

|**8 Bit (All instructions + Separate Types)**|**Bitwise Representation**|**Key**|
| :-: | :-: | :-: |
|First Word|AAAAAA XX|A = InstructionX = Unused|
|Second Word|BCD XXXXX|B = First operand typeC = Second operand typeD = Third operand type|
|Third Word|EEEEEEEE|E = First Operand|
|Fourth Word|FFFFFFFF|F = Second Operand|
|Fifth Word|GGGGGGGG|G = Third Operand|

|![Tip icon]|*Each letter represents 1 bit within each word.*|
| - | - |

A 4 Byte version can be done with 8 bits which has fewer unused bits, but only if the number of instructions is cut down to 32. This means that all the Complex and some of Basic instructions must be removed to make it work with only 5 bits for the instruction:

|**8 Bit (Cut down to 4 Bytes + Separate Types)**|**Bitwise Representation**|**Key**|
| :-: | :-: | :-: |
|First Word|AAAAA BCD|A = InstructionB = First operand typeC = Second operand typeD = Third operand type|
|Second Word|EEEEEEEE|E = First Operand|
|Third Word|FFFFFFFF|F = Second Operand|
|Fourth Word|GGGGGGGG|G = Third Operand|

Since there are only 159 possible combinations of instructions and operand types, the operand types can be combined with the instructions to fit in one byte. This will, however, make it harder to interpret the instruction.

So, on an 8 bit CPU it could look like:

|**8 Bit (Cut down to 4 Bytes + Combined Types)**|**Bitwise Representation**|**Key**|
| :-: | :-: | :-: |
|First Word|AAAAAAAA|A = Instruction and Types|
|Second Word|BBBBBBBB|B = First Operand|
|Third Word|CCCCCCCC|C = Second Operand|
|Fourth Word|DDDDDDDD|D = Third Operand|

On a 16 bit CPU it could look like:

|**16 Bit (All instructions)**|**Bitwise Representation**|**Key**|
| :-: | :-: | :-: |
|First Word|AAAAAA BCD XXXXXXX|A = InstructionB = First operand typeC = Second operand typeD = Third operand typeX = Unused|
|Second Word|EEEEEEEEEEEEEEEE|E = First Operand|
|Third Word|FFFFFFFFFFFFFFFF|F = Second Operand|
|Fourth Word|GGGGGGGGGGGGGGGG|G = Third Operand|

Lastly, on a 4 bit CPU if the only the Core and a couple of the Basic instructions were kept, it could look like:

|**4 Bit (Cut down to 4 bits)**|**Bitwise Representation**|**Key**|
| :-: | :-: | :-: |
|First Word|AAAA|A = Instruction|
|Second Word|BCD X|B = First operand typeC = Second operand typeD = Third operand typeX = Unused|
|Third Word|EEEE|E = First Operand|
|Fourth Word|FFFF|F = Second Operand|
|Fifth Word|GGGG|G = Third Operand|

# <a name="_toc112788004"></a>**EXAMPLE PROGRAMS**
## <a name="_toc112788005"></a>**Simple Fibonacci**
    BITS 8
    MINREG 2
    MINHEAP 0
    MINSTACK 0
    RUN ROM

    IMM R1 0
    IMM R2 1
    .loop
        ADD R1 R1 R2
        ADD R2 R1 R2
        JMP .loop

|![Tip icon]|*This program has no escape condition so it will keep going forever.*|
| - | - |

|![Tip icon]|*This program does not output the answers.*|
| - | - |

## <a name="_toc112788006"></a>**FizzBuzz**
    BITS == 8
    MINREG 4
    MINHEAP 0
    MINSTACK 0
    RUN ROM

    .setup
        IMM R1 0        // current value = 0
        IMM R2 3        // fizz counter = 3
        IMM R3 5        // buzz counter = 5

    .loop
        OUT %TEXT '\n'   // draw a new line character to the char display
        INC R1 R1
        IMM R4 0        // R4 is used to tell if fizz activated
        DEC R2 R2
        BRZ .fizz R2    // branch to .fizz if fizz counter == 0

    .return
        DEC R3 R3
        BRZ .buzz R3    // branch to .buzz if buzz counter == 0
        BNZ .loop R4    // branch to .loop if R4 != 0
        OUT %TEXT R1    // draw current value to the char display
        JMP .loop

    .fizz
        IMM R4 1        // R4 = 1
        OUT %TEXT 'F'   // draw "FIZZ" on the char display
        OUT %TEXT 'I'
        OUT %TEXT 'Z'
        OUT %TEXT 'Z'
        IMM R2 3        // fizz counter = 3
        JMP .return

    .buzz
        OUT %TEXT 'B'   // draw "BUZZ" on the char display
        OUT %TEXT 'U'
        OUT %TEXT 'Z'
        OUT %TEXT 'Z'
        IMM R3 5        // buzz counter = 5
        JMP .loop

|![Tip icon]|*This program starts at 1 and it increments this value once per loop. It prints out “FIZZ” if the value is divisible by 3, “BUZZ” if the value is divisible by 5, “FIZZBUZZ” if the value is divisible by both 3 and 5 or the original value if not divisible by 3 or 5.*|
| - | - |

|![Tip icon]|*This program has no escape condition so it will keep going forever.*|
| - | - |

## <a name="_toc112788007"></a>**Bubble Sort**
    BITS == 8
    MINREG 5
    MINHEAP 5
    MINSTACK 0
    RUN ROM

    .setup
        MOV R2 R0                      // R2 = list pointer
    .rng
        IN R1 %RNG                 // R1 = random number
        STR R2 R1
        INC R2 R2
        OUT %TEXT '\n'
        OUT %TEXT R1
        BNE .rng R2 5              // stop when 5 numbers have been generated
    .main
        MOV R5 R0                      // R5 = switch check
        DEC R3 R0                      // R3 = low pointer
        MOV R4 R0                      // R4 = high pointer
    .loop
        INC R3 R3                  // R3 += 1
        INC R4 R4                  // R4 += 1
        LOD R1 R3                  // R1 = low value
        LOD R2 R4                  // R2 = high value
        BRL .switch R2 R1          // go to .switch if high less than low
        BNE .loop R4 4             // branch to .loop if not at end of list
        BRE .main R5 1             // loop again if any switches occurred
    .out
        MOV R1 R0                  // R1 = pointer for printing outputs
        .outLoop
            LOD R2 R1
            OUT %TEXT '\n'
            OUT %TEXT R2
            INC R1 R1
            BNE .outLoop R1 5      // loop until all 5 values are printed
        HLT
    .switch
        IMM R5 1                   // set switch check
        STR R3 R2
        STR R4 R1
        BNE .loop R4 4             // branch to .loop if not at end of list
        JMP .main                  // loop again

|![Tip icon]|*This program generates a list of 5 random numbers and prints them. Then it sorts the numbers using a bubble sort algorithm, afterwards it prints the sorted list.*|
| - | - |

More example programs can be found in the URCL Discord which is linked in the Links section.
# <a name="_toc112788008"></a>**ACKNOWLEDGEMENTS**
URCL would not have been possible without all of the URCL community contributing towards it. The community has contributed by voting on every part of the language, testing the language on real CPUs, creating tools such as emulators and compilers, writing many URCL programs and more.
## <a name="_toc112788009"></a>**Biggest Contributors**

|**Name (If they wish to give it)**|**Discord Username / Minecraft Username**|**Contributions**|
| :-: | :-: | :-: |
|Ben Aitken|Mod Punchtree / ModPunchtree|- One of the original founders of URCL<br>- Created the Flagless fork of URCL<br>- Managed the Google Sheet documentation for both Main URCL and Flagless<br>- Ran URCL on both the MPU6 and MPU7<br>- Hosted polls<br>- Made several emulators<br>- Made a B to URCL compiler<br>- Made a generic URCL code optimiser<br>- Made a Discord bot so the emulator and compiler are more easily accessible<br>- Created and maintained this formal URCL documentation|
||Haku / |- Created a tool to translate URCL into target CPU’s assembly<br>- Created a URCL emulator|
||Kuggo / Kuggo|- One of the original founders of URCL<br>- Began working on math and string libraries<br>- Hosted a poll|
||Lucida Dragon / |- Created FlapStacks and URCL.NET<br>- Created a URCL highlight extension for VSCode<br>- Created a Discord bot|
||Big Gay Lady / IAmLesbian|- One of the original founders of URCL<br>- Managed the URCL discord<br>- Hosted polls<br>- Created the URCL logo|
||Verlio\_H / |- One of the original founders of URCL<br>- Created URCL OS<br>- Made the current ports documentation<br>- Created the complex numbers library|
||Tuke / |- Created URCL OS<br>- Made the current ports documentation<br>- Created a compiler|
||sammyuri / sammyuri|- Ran URCL on several of their CPUs|
||GLS / GamingLiamStudios|- Tried to make a C to URCL compiler|
||Qwerasd / |- Made a URCL emulator|
||Tape / TapeDispenser69|- Made a URCL emulator in scratch<br>- Tried to make an OS<br>- Whined about the existence of Flagless URCL|
||Bram / |- Created URCX Emulator<br>- Created the URCX discord bot|
||RedCMP / RedCMD|- Created a URCL highlight extension for VSCode|

[Tip icon]: Tip_Icon.png
