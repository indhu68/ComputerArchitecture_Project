# Computer Architecture Projects

This repository contains Computer Architecture coursework projects implemented in C++. The projects cover RISC-V instruction simulation and cache-coherence behavior.

## Repository Contents

```text
.
├── Computer Architecture Homework4/
│   ├── main.cpp
│   ├── instructions.cpp
│   ├── instructions.h
│   ├── output.txt
│   └── Assembly code using RISC V instructions for VADD_C.txt
│
├── part1/
│   ├── main.cpp
│   ├── cache.cpp
│   ├── cache.hpp
│   ├── bus.cpp
│   ├── bus.hpp
│   └── run.bat
│
└── CA_Hw5_2/
    ├── main.c
    ├── cache.h
    └── cache.conf


## Homework 4 — RISC-V Instruction Simulation

### Overview

This project implements a simplified RISC-V processor simulation in C++. It loads a sequence of encoded instructions into simulated RAM, decodes the instructions, and executes them to demonstrate a floating-point array addition workload.

The reference workload adds two arrays of 256 floating-point values:

\[
C[i] = A[i] + B[i], \quad 0 \leq i < 256
\]

### Main Components

- **`main.cpp`** — Initializes simulated memory and registers, loads the instruction sequence, runs the processor simulation, and reports execution statistics.
- **`instructions.cpp` / `instructions.h`** — Provide instruction-decoding functions for supported RISC-V instruction formats, including integer and floating-point formats.
- **`Assembly code using RISC V instructions for VADD_C.txt`** — Contains the reference C workload and an assembly-style implementation of vector/array addition.
- **`output.txt`** — Contains a sample execution output.

### Memory Layout

The simulator defines separate regions for instructions, stack, and the three arrays.

| Region | Address range |
|---|---|
| Instruction memory | `0x0000` – `0x0093` |
| Stack | `0x0200` – `0x02FF` |
| Array A | `0x0400` – `0x07FF` |
| Array B | `0x0800` – `0x0BFF` |
| Array C | `0x0C00` – `0x0FFF` |

Each array contains 256 values, with four bytes allocated per value.

### Build and Run

From the Homework 4 directory, compile the source files:

```bash
g++ -std=c++11 main.cpp instructions.cpp -o homework4
```

Run the executable:

```bash
./homework4
```

On Windows:

```bash
g++ -std=c++11 main.cpp instructions.cpp -o homework4.exe
homework4.exe
```

### Reported Output

The simulator reports execution-related information, including:

- Simulated clock cycles / ticks
- Number of instructions executed
- Calculated CPI (cycles per instruction)
- RAM read/write access count
- Contents of arrays A, B, and C

---

## Homework 5 — Cache and Bus Simulation (Part 1)

### Overview

This project models a small multi-cache system connected through a shared bus. It demonstrates cache reads and writes, cache-line lookup, and state changes based on a simplified MSI/MESI-style coherence approach.

Four cache instances are created and connected to one bus. The program performs sample memory read and write operations and prints the resulting cache contents and state transitions.

### Main Components

- **`main.cpp`** — Creates the bus and four caches, performs sample read/write operations, and prints each cache's final contents.
- **`cache.cpp` / `cache.hpp`** — Implement cache storage, address lookup, reads, writes, and cache-state transitions.
- **`bus.cpp` / `bus.hpp`** — Manage the cache cluster, check whether another cache contains an address, transfer cache-line data, and invalidate other caches when required.
- **`run.bat`** — Windows batch script to compile and run the program.
- **`part1_256.png`** — Image included with the Part 1 project.

### Cache Configuration

The sample program creates four caches using the following constructor arguments:

| Setting | Value |
|---|---:|
| Cache size | 64 bytes |
| Cache-line size | 16 bytes |
| Associativity argument | 1 (direct-mapped) |
| Number of cache entries | 4 per cache |
| Number of cache instances | 4 |

The cache code defines these states:

- **Invalid** — The cache entry does not contain a valid copy.
- **Exclusive** — The cache has a copy that is not currently shared with another cache.
- **Shared** — Multiple caches may hold a copy of the same cache line.
- **Modified** — The cache has modified data.

### Build and Run

From the `part1` directory, compile the source files:

```bash
g++ -std=c++11 main.cpp bus.cpp cache.cpp -o cache_sim
```

Run:

```bash
./cache_sim
```

On Windows, the included batch file can be used:

```bat
run.bat
```

### Demonstrations

The sample operations in `main.cpp` exercise scenarios such as:

- A read miss that obtains a line from memory.
- A read miss that finds a copy in another cache.
- A write that moves a line into the Modified state.
- A write to a Shared line that invalidates copies in other caches.
- Repeated writes to a Modified line.
- Printing the final contents and states of all four caches.

> **Note:** This is a simplified educational simulation. The source includes placeholder memory/cache data and TODO comments; it should not be interpreted as a complete implementation of a production cache-coherence protocol.



## Requirements

- A C++ compiler such as **GCC** or **MinGW-w64**
- A terminal or IDE capable of compiling C/C++ programs
- C++11 support for the supplied C++ projects

## Notes

- Run each project from its own directory, or adjust the compile commands to match your directory structure.
- `output.txt` is a sample output file; actual output may vary because Homework 4 initializes array values using random numbers.
- The Homework 5 Part 1 cache model is intended for demonstrating cache and bus interactions, not for cycle-accurate hardware modeling.
