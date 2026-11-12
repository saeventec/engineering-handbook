# 1.01.01 How a computer runs a program

> **Tier:** 1 · Core  **Area:** Computer basics  **Status:** ✅ Done

## TL;DR
A computer has three main parts: the **CPU** does the work, **memory (RAM)** holds what is being worked on right now, and **storage** keeps files when the power is off.
"Running a program" means loading its instructions from storage into memory. The CPU then carries them out one at a time, very fast.
Python adds one more step: it turns your code into **bytecode**, and a program called the **interpreter** runs that bytecode.

## Before you start
Nothing, this is a starting point.

## Why it matters
Almost every "why is this slow?" or "why did my data disappear?" question comes back to these three parts.
- Reading a file is far slower than reading a variable.
- Data that only lives in memory is lost when the program stops.
- A program can crash because the computer ran out of memory.

Knowing where your data lives helps you guess what's wrong before you start digging.

## The idea

### The three main parts

| Part | What it does | Kept when power is off? | Speed | Typical size (laptop) |
|---|---|---|---|---|
| **CPU** (processor) | Carries out instructions: math, comparisons, moving data | — | Fastest | — |
| **Memory (RAM)** | Holds the programs and data in use *right now* | No (it's **volatile**) | Fast | 8–64 GB |
| **Storage** (SSD or hard disk) | Keeps files, apps and the operating system | Yes (it's **non-volatile**) | Much slower | 256 GB – several TB |

Think of a chef:
- **Storage** is the pantry. It holds lots of food, but it's a walk away.
- **Memory** is the counter. Smaller, but everything is within reach.
- The **CPU** is the chef's hands, doing the actual work.
- Food on the counter is thrown out at closing time (power off). The pantry keeps its food.

### Memory is a hierarchy
There are more layers than "memory" and "storage". Each layer is **smaller and faster** than the next one:

1. **Registers**: a few tiny slots inside the CPU. The CPU works on values here.
2. **Cache**: small, very fast memory on the CPU chip. It keeps copies of recently used data from RAM.
3. **RAM**: main memory.
4. **Storage**: SSD or hard disk.

Real numbers from one modern (2020s) desktop, to get a feel for it:

| Layer | Size | Time to read |
|---|---|---|
| Register | about 2 KB in total | 0.25 ns |
| L1 cache | 32 KB | 1 ns |
| RAM | 64 GB | 82.5 ns |
| SSD | 2 TB | 0.2 ms (= 200,000 ns) |
| Hard disk | 18 TB | 4.16 ms |

(ns = nanosecond, a billionth of a second. ms = millisecond, a thousandth of a second.)

Reading from an SSD takes about **2,000 times longer** than reading from RAM.
That one fact explains a lot of real-world performance work.

### What the CPU actually does
A CPU only understands **machine code**: instructions stored as numbers, like "add these two values" or "jump to that instruction".
Each CPU family has its own set of instructions, called its **instruction set architecture (ISA)**.
The two you'll meet most:
- **x86-64**: most Windows PCs and many cloud servers.
- **ARM** (arm64): phones, Apple Silicon Macs, and more and more servers.

Machine code built for one ISA doesn't run on the other. This is why some downloads ask you to pick "Intel" or "ARM".

The CPU runs instructions in a loop, called the **fetch–decode–execute cycle**:
1. **Fetch:** read the next instruction from memory. A register called the **program counter** holds its address (its location in memory).
2. **Decode:** work out what the instruction means.
3. **Execute:** do it. This can also change the program counter, to jump somewhere else (that's how `if` and loops work underneath).
4. **Repeat**, billions of times per second.

### What "running a program" means
When you start a program:
1. The **operating system** (OS: Windows, macOS, Linux) reads the program from storage.
2. It loads the program into memory and gives it its own space to work in. A running program is called a **process** (more in [1.01.03](../03-operating-systems-processes-and-threads/), not written yet).
3. The CPU starts running its instructions.
4. When the program ends, the OS frees its memory. Anything not saved to storage is gone.

### How Python fits in
You write Python, not machine code. So who turns it into something the CPU can run? Two kinds of tools do this:
- A **compiler** translates your whole program into machine code *before* it runs (C, Rust and Go work this way).
- An **interpreter** is a program that reads your code and carries it out as it goes.

**Python vs CPython.** "Python" is the *language*: the rules for what valid code looks like. **CPython** is the *program* that runs Python code. It's written in C, hence the name.
When you type `python` in a terminal, you start CPython. Other implementations exist (e.g. PyPy), but CPython is the standard one and the one almost everyone uses.

CPython runs your code in two steps:
1. It **compiles** your `.py` file into **bytecode**: a list of very simple steps, like "load `price`", "add", "return". They're like machine code, but made for CPython, not for your real CPU.
2. Its **interpreter** loop runs that bytecode, one step at a time.

```
your_code.py  →  bytecode  →  CPython interpreter  →  CPU runs the interpreter's machine code
```

**Why compile first?** Source text is slow to work with directly: spaces, comments, brackets, operator order. Translating it once into simple steps lets the interpreter loop run fast. A loop that runs a million times is translated once, not a million times.

**When does it compile?** Every time you run code, just before it runs. It takes a fraction of a second, so you never notice.
- **The file you run** (`python run_program.py`) is compiled in memory each time. Nothing is saved.
- **Files you import** (`import pricing`) are compiled and saved in a `__pycache__` folder as a `.pyc` file. Next time, Python reuses that file. If you change the `.py` file, Python notices and recompiles it.

**So is Python "interpreted"?** Yes, in the sense that matters: your code is never turned into machine code for your CPU. Python still has one quick compile step to bytecode first.
So "interpreted" doesn't mean "reads your text line by line". It means "a program (the interpreter) runs your code, instead of the CPU running it directly".

This extra layer is a big reason Python is slower than C or Rust for heavy number-crunching. It's also why the same `.py` file runs on both x86-64 and ARM: only the interpreter needs to be built for each ISA.

## Example
Save this as `run_program.py` and run it with `python run_program.py` in a terminal (the terminal is covered in [1.02.01](../../02-developer-tools/01-the-terminal-and-the-shell/), not written yet).

```python
import dis
import platform
import sys


def add_tax(price: float, rate: float) -> float:
    return price * (1 + rate)


print(platform.machine())                # the CPU family this machine uses
print(sys.implementation.cache_tag)      # the tag used in .pyc file names
print(add_tax(100.0, 0.2))
dis.dis(add_tax)                         # the bytecode Python made from add_tax
```

Output on an Apple Silicon Mac with Python 3.15:

```
arm64
cpython-315
120.0
  6           RESUME                   0

  7           LOAD_FAST_BORROW         0 (price)
              LOAD_SMALL_INT           1
              LOAD_FAST_BORROW         1 (rate)
              BINARY_OP                0 (+)
              BINARY_OP                5 (*)
              RETURN_VALUE
```

What you're seeing:
- `arm64` is this machine's ISA. On most Windows PCs you'd see `AMD64` or `x86_64`.
- `dis` (short for "disassemble") shows the bytecode for `add_tax`. Each line is one simple step: load `price`, load `1`, load `rate`, add, multiply, return.
- One line of Python became several small instructions. The CPU does the same at its own level: each bytecode step becomes many machine-code instructions inside the interpreter.

Don't memorize these names. Bytecode is an internal detail of CPython and **changes between Python versions**, so your output may look a little different.

Now see the cache. Put `add_tax` in its own file `pricing.py`, then in another file write `import pricing` and run that file.
A new folder appears:

```
__pycache__/
    pricing.cpython-315.pyc
```

`cpython-315` matches the `cache_tag` printed above. It means "compiled by CPython 3.15".

## In real work
- **"It's slow" usually means "it's waiting".** Most slow apps aren't slow because the CPU is busy. They're waiting for storage, a database or the network. Check that first.
- **Keep hot data in memory.** Reading a config file once at startup and keeping it in a variable beats reading it on every request. Caches like Redis ([2.07.05](../../../tier-2-growth/07-databases-deeper/05-caching-with-redis/), not written yet) use this same idea across a whole system.
- **Memory is limited.** Loading a 20 GB log file into a list can crash your program. Read it piece by piece instead. You'll see this in "out of memory" errors and in containers being killed for using too much memory.
- **Save what matters.** If data must survive a restart or crash, write it to storage (a file or a database). Variables vanish when the process ends.
- **ISA shows up in builds.** Docker images and downloaded tools often come in `amd64` and `arm64` versions. A mismatch causes errors like "exec format error".
- **Ignore `__pycache__` in Git.** It's generated, so projects add it to `.gitignore` (covered in [1.02.06](../../02-developer-tools/06-git-basics/), not written yet).

## Common mistakes
- **Thinking memory and storage are the same.** "My laptop has 512 GB of memory" usually means storage. RAM is the much smaller number (like 16 GB).
- **Assuming variables are saved.** They live in RAM and are gone when the program stops. Write to a file or database to keep data.
- **Blaming the CPU first.** Measure before you optimize. Slow code is often waiting on disk or network, not computing.
- **Thinking Python runs on the CPU directly.** The CPU runs the interpreter. The interpreter runs your bytecode.
- **Deleting `__pycache__` to "fix" bugs.** It's safe to delete, but it almost never is the problem. Python recompiles when the source changes.

## Check yourself
1. What are the three main parts of a computer, and which one loses its data when the power goes off?
   <details><summary>Answer</summary>CPU, memory (RAM) and storage. RAM is volatile, so it loses its data. Storage keeps it.</details>
2. Roughly how much slower is reading from an SSD than from RAM?
   <details><summary>Answer</summary>About 2,000 times slower in the example table (0.2 ms vs about 82.5 ns). The exact number varies, but it's thousands of times.</details>
3. What does the program counter do?
   <details><summary>Answer</summary>It holds the address of the next instruction for the CPU to run. Jumps (for `if` and loops) work by changing it.</details>
4. Your Python script runs fine on an Intel laptop and on an ARM Mac, without changes. Why?
   <details><summary>Answer</summary>Python code is turned into bytecode, which isn't tied to any CPU. Only the interpreter is built in machine code, and there's a version of it for each ISA.</details>
5. Your web app reads a 2 MB settings file from disk on every request and is slow. What's a simple fix?
   <details><summary>Answer</summary>Read it once at startup and keep it in memory (a variable), since memory is much faster than storage.</details>

## Q&A
### Q: Can I compile a Python file to a `.pyc` myself and run it?
Yes. `python -m py_compile pricing.py` creates `__pycache__/pricing.cpython-315.pyc`, and `python __pycache__/pricing.cpython-315.pyc` runs it, even without the `.py` file.
(`python -m compileall <folder>` compiles a whole folder.)
- It doesn't run faster. Only loading is faster, because the compile step is skipped.
- It only works with the same Python version (here 3.15).
- It doesn't hide your code: tools like `dis` can read the bytecode back.
- At work you rarely do this by hand. Python manages `__pycache__` for you.

### Q: How do I see the bytecode of a `.py` or `.pyc` file?
- **From a `.py` file:** run `python -m dis pricing.py`. It prints the bytecode for the whole file and every function in it. Numbers on the left are source line numbers. An `__annotate__` block is a helper Python makes for type hints; ignore it.
- **From a `.pyc` file:** it's a 16-byte header (version stamp and freshness info) followed by bytecode packed with `marshal`. Skip the header, unpack, and disassemble:
  ```python
  import dis
  import marshal
  import sys
  from pathlib import Path

  data = Path(sys.argv[1]).read_bytes()
  code = marshal.loads(data[16:])  # skip the 16-byte header
  dis.dis(code)
  ```
  This only works with the Python version that made the file. Only open `.pyc` files you trust: `marshal` isn't safe against malicious data.

## Key takeaways
- **CPU** runs instructions, **RAM** holds what's in use now (lost at power off), **storage** keeps files. Each memory layer is smaller and faster than the next: an SSD is about 2,000× slower than RAM.
- The CPU only runs **machine code** for its **ISA** (x86-64 or ARM), in a fetch–decode–execute loop driven by the **program counter**.
- **Python** is the language; **CPython** is the program that runs it. It compiles your code to **bytecode** (quickly, every run), then its interpreter runs that bytecode.
- Bytecode is tied to the **Python version**, not the ISA. Imported modules are cached as `.pyc` files in `__pycache__`; this speeds up loading, not running.
- See bytecode with `python -m dis file.py`. Slow code is usually *waiting* (disk, network), so keep hot data in memory and save what must survive to storage.

## Sources
- [Python glossary: bytecode, interpreted, virtual machine](https://docs.python.org/3/glossary.html) (checked 2026-11-12)
- [Python docs: `dis`, disassembler for Python bytecode](https://docs.python.org/3/library/dis.html) (checked 2026-11-12)
- [Python tutorial: "Compiled" Python files](https://docs.python.org/3/tutorial/modules.html#compiled-python-files) (checked 2026-11-12)
- [Python docs: `py_compile`, compile Python source files](https://docs.python.org/3/library/py_compile.html) (checked 2026-11-12)
- [Python docs: `marshal`, internal object serialization](https://docs.python.org/3/library/marshal.html) (checked 2026-11-12)
- [PEP 552: Deterministic pycs (the `.pyc` header layout)](https://peps.python.org/pep-0552/) (checked 2026-11-12)
- [Wikipedia: Instruction cycle](https://en.wikipedia.org/wiki/Instruction_cycle) (checked 2026-11-12)
- [Wikipedia: Memory hierarchy (latency table for an AMD Zen 4 system)](https://en.wikipedia.org/wiki/Memory_hierarchy) (checked 2026-11-12)
- [Wikipedia: Machine code](https://en.wikipedia.org/wiki/Machine_code) (checked 2026-11-12)
- Example output: run locally on Python 3.15.2, arm64 (2026-11-12)
