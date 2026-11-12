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
- **CPU (processor)**: the part of the computer that carries out instructions. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **CPython**: the standard Python interpreter, written in C. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## D
- **Decoding**: turning bytes back into text, using an encoding. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## E
- **Encoding**: the rules for turning text (code points) into bytes, e.g. UTF-8. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## F
- **Fetch–decode–execute cycle**: the loop a CPU repeats: read the next instruction, work out what it means, do it. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Float**: a number with a decimal point, stored as a binary fraction; can have tiny rounding errors. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## H
- **Hexadecimal (hex)**: base 16, digits 0–9 and a–f; one byte is exactly two hex digits (`00`–`ff`). → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## I
- **Instruction set architecture (ISA)**: the set of machine-code instructions a CPU family understands, e.g. x86-64 or ARM. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Interpreter**: a program that reads code and carries it out as it goes. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## M
- **Machine code**: instructions stored as numbers that a CPU runs directly. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Memory (RAM)**: fast, volatile storage for the programs and data in use right now. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Mojibake**: garbled text caused by decoding bytes with the wrong encoding, e.g. `CafÃ©` for `Café`. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## N
- **Non-volatile**: keeps its data when the power is off (e.g. SSD, hard disk). → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## O
- **Overflow**: when a number is too big for the space it's stored in, causing an error or a wrong value. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## P
- **Process**: a running program, with its own memory given to it by the operating system. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **Program counter**: a CPU register holding the address of the next instruction to run. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
- **.pyc file**: a cached bytecode file Python saves in `__pycache__` so it doesn't recompile unchanged modules. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## R
- **Register**: a tiny, fastest storage slot inside the CPU. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## S
- **Storage**: non-volatile space (SSD or hard disk) that keeps files when the power is off. → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)

## U
- **Unicode**: the standard that gives every character, symbol and emoji a number (code point). → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)
- **UTF-8**: the most common text encoding; uses 1–4 bytes per character and matches ASCII for English text. → [1.01.02](tier-1-core/01-computer-basics/02-bits-bytes-and-text/)

## V
- **Volatile**: loses its data when the power is off (e.g. RAM). → [1.01.01](tier-1-core/01-computer-basics/01-how-a-computer-runs-a-program/)
