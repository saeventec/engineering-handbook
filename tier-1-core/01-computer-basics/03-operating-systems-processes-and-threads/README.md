# 1.01.03 Operating systems, processes and threads

> **Tier:** 1 · Core  **Area:** Computer basics  **Status:** 🟡 In progress

## TL;DR
The **operating system (OS)** shares one computer between many programs. Each running program is a **process**, with its own private memory.
Inside a process, one or more **threads** run the code. Threads of the same process share its memory.
The OS switches between them so fast that hundreds of programs seem to run at once, even though each CPU core runs only one thread at a time.

## Before you start
- [1.01.01 How a computer runs a program](../01-how-a-computer-runs-a-program/): CPU, memory, and what a process is.

## Why it matters
Every program you write runs as a process, and every server you deploy runs many of them.
Knowing the difference between processes and threads explains a lot:
- why one crashed program doesn't take down the others,
- why a Python script uses only one core out of 12,
- why "kill the process" fixes a stuck app.

## The idea

### What the operating system does
The OS (Windows, macOS, Linux) sits between programs and the hardware. It:
- **Shares the CPU**: decides which program runs, on which core, and for how long.
- **Shares memory**: gives each program its own area and stops programs reading each other's.
- **Handles files and devices**: disks, network, keyboard, screen.
- **Keeps things safe**: users, permissions, and stopping one program from breaking another.

The core of the OS is the **kernel**: the part that has full control of the hardware.
Your program isn't allowed to touch the disk or network directly. It asks the kernel with a **system call** ("syscall"): "open this file", "send these bytes", "start a new process".
When Python runs `open("orders.csv")`, a system call happens underneath.

### Processes: running programs
A **process** is a program that's running. Open the same app twice and you get two processes.
Each process has:
- a **process ID (PID)**: a number the OS uses to identify it,
- **its own memory**, which other processes can't see or change,
- at least one **thread** running its code,
- a **parent**: the process that started it (your terminal starts `python`, for example).

Because memory is private, processes are **isolated**: if one crashes, the others keep running.
The cost is that they can't simply share variables. To share data, they must send it to each other (through files, pipes, network, a database…).

### Threads: several workers inside one process
A **thread** is one line of execution inside a process: its own program counter (the "next instruction" pointer from [1.01.01](../01-how-a-computer-runs-a-program/)) and its own record of which functions it's in.
A process starts with one thread (the **main thread**) and can start more.

All threads of a process **share its memory**. That makes them cheap to start and easy to share data between.
It's also the danger: two threads changing the same data at the same time can corrupt it. That's a **race condition** ([2.04.02](../../../tier-2-growth/04-concurrency/02-race-conditions-and-locks/), not written yet).

| | Process | Thread |
|---|---|---|
| Memory | Its own, private | Shared with other threads in the same process |
| Cost to start | Higher | Lower |
| If it crashes | Other processes are fine | Can take down the whole process |
| Sharing data | Must send it (pipes, files, network) | Just use the same variables (carefully) |

Analogy: a process is a **restaurant kitchen**, with its own fridge and tools. Threads are **cooks in that kitchen**: they share the fridge, which is fast, but they can bump into each other.
Two different restaurants don't share anything.

### How many programs run at once?
A modern CPU has several **cores**. Each core runs one thread at a time. A laptop might have 8–12 cores but hundreds of processes and thousands of threads.

The OS **scheduler** fixes this by **time slicing**: it lets a thread run for a tiny slice of time, pauses it, and runs another.
Saving one thread's state and loading another's is called a **context switch**. It happens thousands of times per second, so everything looks simultaneous.

Two words you'll hear a lot (covered properly in [2.04.01](../../../tier-2-growth/04-concurrency/01-concurrency-vs-parallelism/), not written yet):
- **Concurrency**: several tasks are in progress at once, taking turns. Possible with one core.
- **Parallelism**: several tasks run at the *exact same moment*, on different cores.

### Waiting vs computing
Most work falls into one of two kinds:
- **I/O-bound**: mostly *waiting*, for the network, disk or a database. Example: calling 50 APIs. ("I/O" means input/output.)
- **CPU-bound**: mostly *computing*. Example: resizing 1,000 images.

A thread that's waiting doesn't use the CPU. The OS just runs something else meanwhile.
So for I/O-bound work, many threads help even on one core. For CPU-bound work, only more cores help.

### Python and the GIL
In standard CPython there's a **Global Interpreter Lock (GIL)**: only one thread can run Python code at a time, even on a 12-core machine.
What that means in practice:
- **Threads are fine for I/O-bound work.** A thread that's waiting lets the others run.
- **For CPU-bound work, use processes.** Each process has its own interpreter and its own GIL, so they really run in parallel.

This is changing. Since Python 3.13 there's a separate **free-threaded build** of Python without the GIL. Since 3.14 it's officially supported, but it's still optional and not the default.
Details in [2.01.05 Threads and processes in Python](../../../tier-2-growth/01-python-deeper/05-threads-and-processes-in-python/) (not written yet).

## Example
This script starts 3 threads for "network calls", then 1 extra process. Save it as `processes_and_threads.py` and run it with `python processes_and_threads.py`.

```python
import os
import threading
import time
from concurrent.futures import ProcessPoolExecutor, ThreadPoolExecutor

processed_orders: list[str] = []


def fetch_order(order_id: str) -> str:
    time.sleep(1)  # pretend we're waiting 1 second for a network reply
    processed_orders.append(order_id)
    return f"{order_id} done in thread {threading.current_thread().name}"


def record_in_child(order_id: str) -> int:
    processed_orders.append(order_id)  # changes the CHILD's copy only
    return os.getpid()


if __name__ == "__main__":
    print("my process id:", os.getpid())
    print("CPU cores:", os.cpu_count())

    start = time.perf_counter()
    with ThreadPoolExecutor(max_workers=3) as pool:
        for result in pool.map(fetch_order, ["A-1", "A-2", "A-3"]):
            print(result)
    print(f"3 waits took {time.perf_counter() - start:.1f} s")
    print("shared list after threads:", processed_orders)

    with ProcessPoolExecutor(max_workers=2) as pool:
        child_pid = pool.submit(record_in_child, "B-1").result()
    print("child process id:", child_pid)
    print("list after child process:", processed_orders)
```

Output (your IDs and core count will differ):

```
my process id: 15712
CPU cores: 12
A-1 done in thread ThreadPoolExecutor-0_0
A-2 done in thread ThreadPoolExecutor-0_1
A-3 done in thread ThreadPoolExecutor-0_2
3 waits took 1.0 s
shared list after threads: ['A-1', 'A-2', 'A-3']
child process id: 15714
list after child process: ['A-1', 'A-2', 'A-3']
```

What it shows:
- **Threads overlap waiting.** Three 1-second waits took 1 second in total, not 3. While one thread waits, the others run.
- **Threads share memory.** All three added to the same `processed_orders` list.
- **Processes don't.** The child process has a different PID, and its `append("B-1")` changed only its own copy. The parent's list has no `B-1`.
- **`if __name__ == "__main__":`** is needed when starting processes. The child process imports your file, and this line stops it from running the main code again.
- `ThreadPoolExecutor` and `ProcessPoolExecutor` (from `concurrent.futures`) are the simplest standard ways to run work in threads or processes. A "pool" is a fixed group of workers reused for many tasks.

## In real work
- **Seeing processes.** Task Manager (Windows), Activity Monitor (macOS), or `top` and `ps` in a terminal ([2.03.03](../../../tier-2-growth/03-operating-systems-and-linux/03-linux-for-engineers/), not written yet). You'll look up a PID there and stop a stuck process.
- **Web servers run several processes.** A Python web app usually runs several worker processes, often about one per core, so a slow or crashed request doesn't block the others.
- **Pick the tool by the kind of work.** Calling many APIs → threads (or async, [2.01.06](../../../tier-2-growth/01-python-deeper/06-async-and-await/), not written yet). Heavy computing → processes.
- **Running other programs.** Python's `subprocess.run(["git", "status"])` starts another program as a child process and waits for it.
- **Containers are isolated processes.** A Docker container ([1.12.02](../../12-shipping-software/02-containers-with-docker/), not written yet) is a process with extra walls around it.
- **Shared state needs care.** If threads touch the same data, protect it or avoid sharing it ([2.04.02](../../../tier-2-growth/04-concurrency/02-race-conditions-and-locks/), not written yet).

## Common mistakes
- **Using threads to speed up CPU-heavy Python.** With the GIL, it won't get faster. Use processes (`ProcessPoolExecutor`).
- **Expecting a child process to see your variables.** It has its own memory. Send data in as arguments and get results back as return values.
- **Starting thousands of threads or processes.** Each costs memory, and switching between them costs time. Use a pool with a sensible number of workers.
- **Forgetting `if __name__ == "__main__":`** when using processes. On macOS and Windows this can lead to errors or the main code running again in each child.
- **Thinking "more threads = faster" always.** It only helps while threads are waiting. For computing, the number of cores is the limit.

## Check yourself
1. What's the main difference between a process and a thread?
   <details><summary>Answer</summary>A process has its own private memory. Threads live inside a process and share its memory.</details>
2. Your machine has 8 cores but 400 processes are running. How is that possible?
   <details><summary>Answer</summary>The OS scheduler gives each thread short time slices and switches between them (context switches) very fast. Also, most of them are waiting and don't need the CPU at all.</details>
3. You need to download 200 web pages in Python. Threads or processes? Why?
   <details><summary>Answer</summary>Threads (or async). The work is I/O-bound: mostly waiting. The GIL is released while waiting, so threads overlap the waits.</details>
4. You need to resize 10,000 images in Python, using all cores. Threads or processes?
   <details><summary>Answer</summary>Processes. The work is CPU-bound, and with the GIL only one thread runs Python code at a time. Each process has its own GIL.</details>
5. What is a system call?
   <details><summary>Answer</summary>A request from a program to the OS kernel to do something it isn't allowed to do directly, like opening a file or sending data over the network.</details>

## Q&A
_No questions yet._

## Key takeaways
<!-- Written when the lesson is finished. -->

## Sources
- [Python docs: `threading` (threads, shared memory, GIL note)](https://docs.python.org/3/library/threading.html) (checked 2026-11-18)
- [Python docs: Python support for free threading](https://docs.python.org/3.15/howto/free-threading-python.html) (checked 2026-11-18)
- [PEP 779: Criteria for supported status for free-threaded Python](https://peps.python.org/pep-0779/) (checked 2026-11-18)
- [What's New in Python 3.15](https://docs.python.org/3.15/whatsnew/3.15.html) (checked 2026-11-18)
- [Python glossary: free threading, GIL](https://docs.python.org/3/glossary.html) (checked 2026-11-18)
- [Python docs: `os` (getpid)](https://docs.python.org/3/library/os.html) (checked 2026-11-18)
- [Wikipedia: Process (computing)](https://en.wikipedia.org/wiki/Process_(computing)) (checked 2026-11-18)
- [Wikipedia: Thread (computing)](https://en.wikipedia.org/wiki/Thread_(computing)) (checked 2026-11-18)
- [Wikipedia: Context switch](https://en.wikipedia.org/wiki/Context_switch) (checked 2026-11-18)
- [Wikipedia: System call](https://en.wikipedia.org/wiki/System_call) (checked 2026-11-18)
- [Wikipedia: Kernel (operating system)](https://en.wikipedia.org/wiki/Kernel_(operating_system)) (checked 2026-11-18)
- Example output: run locally on Python 3.15.2, macOS, 12 cores (2026-11-18)
