# CSE-333: System Process Management & Compilation Study

A comprehensive exploration of Unix process management, compilation workflows, and the critical roles of linkers and loaders in modern operating systems.

##  Overview

This repository demonstrates fundamental concepts in systems programming including:
- Unix process creation mechanisms
- Multi-file compilation workflows  
- Linking strategies for modular code
- Dynamic loading and library management
- Automated build systems with Make

##  Quick Start Guide

#### System Requirements

Ensure your development environment includes:
- GCC compiler suite (version 7.0+)
- POSIX-compliant operating system (Linux/Unix/macOS)
- Make utility for build automation

#### Setup Instructions

```bash
# Clone the repository
git clone https://github.com/YasseenAbdelghany/CSE-333.git
cd CSE-333

# Build all examples
make all
```

##  Project Components

### Component 1: Fork-Based Process Creation

**Source File:** `process_creation.c`

Explores Unix process creation through the `fork()` system call, demonstrating parent-child process relationships.

**Key Concepts:**
- Process duplication mechanics
- PID (Process Identifier) management
- Concurrent process execution patterns

**Execution:**
```bash
make process_creation
./process_creation
```

**Sample Output:**
```
Parent process executing. PID: [parent_pid]
Child process executing. PID: [child_pid]
```

### Component 2: Multi-File Linking Example

**Source Files:** `file1.c` + `file2.c`

Illustrates the linker's capability to merge separate compilation units into unified executables.

**Architecture:**
- `file1.c`: Implements the `hello()` function
- `file2.c`: Entry point calling external function

**Build & Execute:**
```bash
make output_program
./output_program
```

**Output:**
```
Hello from file1!
```

### Component 3: Dynamic Loading Exploration

**Source File:** `simple_program.c`

Basic program for examining runtime library loading behavior.

**Usage:**
```bash
make simple_program
./simple_program

# Inspect dynamic dependencies
ldd simple_program
```

**Expected Result:**
```
This is a simple program.
```

##  Build System Commands

| Command | Purpose |
|---------|---------|
| `make all` | Compile all project components |
| `make run` | Execute all programs sequentially |
| `make clean` | Remove generated binaries and artifacts |
| `make process_creation` | Build process creation demo only |
| `make output_program` | Build linker example only |
| `make simple_program` | Build loader example only |

##  Conceptual Deep Dive

### The Linker's Role in Compilation

A linker serves as the bridge between separately compiled code modules, creating a cohesive executable.

**Primary Functions:**

1. **Symbol Resolution**: Maps function/variable references to their implementations across object files
2. **Address Relocation**: Assigns absolute memory addresses to symbols
3. **Library Integration**: Incorporates external library code
4. **Dependency Validation**: Identifies missing or conflicting symbols

**Practical Example**: When compiling our multi-file project, the linker resolves the `hello()` call in `file2.c` by locating its definition in `file1.c`'s object code.

### The Loader's Execution Responsibility  

The loader operates as the OS component responsible for program initialization and execution setup.

**Core Operations:**

1. **Memory Allocation**: Reserves address space for program execution
2. **Code Loading**: Transfers executable content from disk to RAM
3. **Dynamic Library Resolution**: Loads shared libraries at runtime
4. **Environment Setup**: Configures stack, heap, and registers
5. **Transfer Control**: Begins program execution at entry point

**Observation**: Running `ldd simple_program` reveals all shared objects the loader must resolve before execution begins (libc, ld-linux, etc.).

##  Educational Objectives

This project reinforces understanding of:
- Process lifecycle in Unix-like operating systems
- Compilation pipeline stages (preprocessing, compilation, assembly, linking)
- Static vs. dynamic linking trade-offs
- Build automation best practices
- System-level programming in C

##  Development Notes

**Compilation Stages Demonstrated:**
1. **Preprocessing**: Header inclusion and macro expansion
2. **Compilation**: Translation to assembly language
3. **Assembly**: Conversion to machine code (object files)
4. **Linking**: Combining object files into executable
5. **Loading**: Runtime preparation by OS loader

**To examine intermediate stages:**
```bash
# Generate object files only
gcc -c file1.c -o file1.o
gcc -c file2.c -o file2.o

# Link manually
gcc file1.o file2.o -o output_program

# View symbols
nm file1.o
nm file2.o
```

##  Contributing

This is an academic project for CSE-333 coursework. Improvements and suggestions are welcome through standard pull request workflows.

##  License

Released under MIT License. See LICENSE file for complete terms.

---

**Repository:** YasseenAbdelghany/CSE-333  
**Academic Context:** Systems Programming Fundamentals  
**Lab Assignment:** Process Management & Compilation Mechanisms# Lab-5 Assignment: Process Management and Compilation

This repository contains C code examples demonstrating process creation, the role of linkers and loaders, along with a Makefile for compilation.

## Table of Contents

- [About](#about)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
- [Code Examples](#code-examples)
  - [Exercise 1: Process Creation with fork()](#exercise-1-process-creation-with-fork)
  - [Exercise 5: Linker Demonstration](#exercise-5-linker-demonstration)
  - [Exercise 6: Loader Demonstration](#exercise-6-loader-demonstration)
- [Understanding Linkers and Loaders](#understanding-linkers-and-loaders)
  - [What is a Linker?](#what-is-a-linker)
  - [What is a Loader?](#what-is-a-loader)
- [Building and Running](#building-and-running)
- [License](#license)

## About

This project is part of Lab-5 coursework focusing on:
- Process creation in C using the `fork()` system call
- Understanding the compilation process
- The role of linkers in combining object files
- The role of loaders in executing programs
- Creating Makefiles for automated compilation

## Getting Started

### Prerequisites

To compile and run these programs, you need:
- **GCC (GNU Compiler Collection)**: Required to compile C programs
- **Linux/Unix environment**: The programs use POSIX system calls

Install GCC on Ubuntu/Debian:
```bash
sudo apt install gcc
```

### Installation

1. Clone this repository:
```bash
git clone https://github.com/Homd11/assignment2.git
cd assignment2
```

2. Compile all programs:
```bash
make all
```

## Usage

### Compile all programs
```bash
make all
```

### Run all programs
```bash
make run
```

### Clean compiled files
```bash
make clean
```

### Compile individual programs
```bash
# Process creation example
make process_creation

# Linker example
make output_program

# Loader example
make simple_program
```

## Code Examples

### Exercise 1: Process Creation with fork()

**File:** `process_creation.c`

This program demonstrates how to create a new process using the `fork()` system call.

**What it does:**
- Creates a child process using `fork()`
- The parent and child processes both print their Process IDs (PIDs)
- Demonstrates concurrent execution of parent and child processes

**Run:**
```bash
./process_creation
```

**Expected Output:**
```
This is the parent process. PID: [parent_pid]
This is the child process. PID: [child_pid]
```

### Exercise 5: Linker Demonstration

**Files:** `file1.c`, `file2.c`

This example shows how the linker combines multiple source files into a single executable.

**What it does:**
- `file1.c` defines a `hello()` function
- `file2.c` contains the `main()` function that calls `hello()`
- The linker resolves the function call and creates the final executable

**Run:**
```bash
./output_program
```

**Expected Output:**
```
Hello from file1!
```

### Exercise 6: Loader Demonstration

**File:** `simple_program.c`

A simple program used to demonstrate the loader's role in loading dynamic libraries.

**What it does:**
- Prints a simple message
- Can be inspected with `ldd` to see which libraries the loader loads

**Run:**
```bash
./simple_program
ldd simple_program
```

**Expected Output:**
```
This is a simple program.
```

The `ldd` command will show the dynamic libraries loaded by the loader.

## Understanding Linkers and Loaders

### What is a Linker?

The **linker** is a program that combines one or more object files into a single executable.

**Key responsibilities:**
1. **Symbol Resolution**: Connects function calls to their definitions across different files
2. **Relocation**: Assigns final memory addresses to code and data
3. **Library Linking**: Links external libraries to the program
4. **Error Detection**: Reports undefined or duplicate symbols

**Example:** In the linker demonstration, `file1.c` and `file2.c` are compiled separately into object files, then the linker combines them and resolves the `hello()` function reference.

### What is a Loader?

The **loader** is part of the operating system that loads programs into memory and prepares them for execution.

**Key responsibilities:**
1. **Program Loading**: Reads the executable and loads it into memory
2. **Dynamic Linking**: Loads shared libraries required by the program
3. **Relocation**: Adjusts addresses for the program's actual load location
4. **Initialization**: Sets up the runtime environment and starts execution

**Example:** When running `./simple_program`, the loader loads the executable and dynamic libraries (libc, etc.) into memory before execution begins.

## Building and Running

### Compile all programs:
```bash
make all
```

### Run programs individually:
```bash
./process_creation
./output_program
./simple_program
```

### View dynamic libraries:
```bash
ldd simple_program
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Author:** Lab-5 Assignment  
**Course:** Operating Systems / Systems Programming  
**Purpose:** Educational demonstration of process management and compilation
