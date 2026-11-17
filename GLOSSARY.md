# Glossary

Short definitions of terms used in the lessons, in alphabetical order.
Format: `- **Term**: simple definition. → [lesson ID](path)`

<!-- Add a letter heading (e.g. "## A") when its first term is added. -->

## A
- **ASCII**: an old character table with 128 characters (English letters, digits, basic symbols); the first 128 Unicode code points match it. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## B
- **Binary**: counting in base 2, using only 0 and 1; each position is worth twice the one to its right. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)
- **Bit**: the smallest piece of data: 0 or 1. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)
- **BOM (byte order mark)**: an invisible marker some tools put at the start of a text file; in UTF-8 it's the bytes `ef bb bf`. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)
- **Byte**: 8 bits; can hold a number from 0 to 255. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)
- **Bytecode**: simple instructions that Python compiles your code into; the interpreter runs them, not the CPU directly. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## C
- **Cache (CPU)**: small, very fast memory on the CPU chip that keeps copies of recently used data from RAM. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Code point**: the number Unicode gives a character, written like `U+00E9` (é). → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)
- **Compiler**: a program that translates source code into another form (often machine code) before it runs. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Concurrency**: several tasks in progress at once, taking turns; possible on one core. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **Context switch**: the OS saving one thread's state and loading another's, so they can take turns on a core. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **Core**: one independent processing unit inside a CPU; each runs one thread at a time. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **CPU (processor)**: the part of the computer that carries out instructions. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **CPU-bound**: work that's slow because of computing, e.g. resizing images. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **CPython**: the standard Python interpreter, written in C. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## D
- **Decoding**: turning bytes back into text, using an encoding. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## E
- **Encoding**: the rules for turning text (code points) into bytes, e.g. UTF-8. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## F
- **Fetch–decode–execute cycle**: the loop a CPU repeats: read the next instruction, work out what it means, do it. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Float**: a number with a decimal point, stored as a binary fraction; can have tiny rounding errors. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)
- **Free-threaded build**: a separate build of Python without the GIL, so threads can run Python code in parallel. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)

## G
- **GIL (Global Interpreter Lock)**: a lock in standard CPython that lets only one thread run Python code at a time. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)

## H
- **Hexadecimal (hex)**: base 16, digits 0–9 and a–f; one byte is exactly two hex digits (`00`–`ff`). → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## I
- **I/O-bound**: work that's slow because of waiting for the network, disk or a database. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **Instruction set architecture (ISA)**: the set of machine-code instructions a CPU family understands, e.g. x86-64 or ARM. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Interpreter**: a program that reads code and carries it out as it goes. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## K
- **Kernel**: the core of the operating system, with full control of the hardware. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)

## M
- **Machine code**: instructions stored as numbers that a CPU runs directly. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Memory (RAM)**: fast, volatile storage for the programs and data in use right now. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Mojibake**: garbled text caused by decoding bytes with the wrong encoding, e.g. `CafÃ©` for `Café`. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## N
- **Non-volatile**: keeps its data when the power is off (e.g. SSD, hard disk). → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## O
- **Operating system (OS)**: the software that shares the computer's hardware between programs, e.g. Windows, macOS, Linux. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **Overflow**: when a number is too big for the space it's stored in, causing an error or a wrong value. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## P
- **Parallelism**: several tasks running at the exact same moment, on different cores. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **PID (process ID)**: the number the OS uses to identify a process. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **Process**: a running program, with its own private memory given to it by the operating system. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Program counter**: a CPU register holding the address of the next instruction to run. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **.pyc file**: a cached bytecode file Python saves in `__pycache__` so it doesn't recompile unchanged modules. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## R
- **Race condition**: a bug where the result depends on the timing of threads or processes touching the same data. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **Register**: a tiny, fastest storage slot inside the CPU. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## S
- **Scheduler**: the part of the OS that decides which thread runs on which core, and for how long. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)
- **Storage**: non-volatile space (SSD or hard disk) that keeps files when the power is off. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **System call**: a request from a program to the OS kernel, e.g. to open a file or send network data. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)

## T
- **Thread**: one line of execution inside a process; threads of a process share its memory. → [1.01.03](tier-1-core/01-computer-basics/03-operating-systems-processes-and-threads/)

## U
- **Unicode**: the standard that gives every character, symbol and emoji a number (code point). → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)
- **UTF-8**: the most common text encoding; uses 1–4 bytes per character and matches ASCII for English text. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## V
- **Volatile**: loses its data when the power is off (e.g. RAM). → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
