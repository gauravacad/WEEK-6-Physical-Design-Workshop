# WEEK-6-Physical-Design-Workshop

# 🧠 Lecture Notes: System Software & RISC-V Architecture Overview
---
## 1️⃣ Introduction
- The lecture begins by showing **application software (apps)** used daily.  
- These apps run on **hardware (the chip)** inside devices like laptops.  
- The key question: **“How do applications run on hardware?”**  
- The **Instruction Set Architecture (ISA)** helps bridge this gap.
---
## 2️⃣ The Big Picture: Flow from Software to Hardware
### 📦 System Software Role
- Application software passes through **system software**, which converts it into binary.  
- **Main layers of system software:**
  - **Operating System (OS)**
  - **Compiler**
  - **Assembler**
---
## 3️⃣ Role of Each Component
### 🖥️ Operating System (OS)
- Handles:
  - Memory management  
  - I/O operations  
  - Process scheduling and resource allocation  
- Converts application programs into **assembly language** and finally **binary**.  
- Produces small C/C++/Java functions that are compiled further.
---
### ⚙️ Compiler
- Converts **high-level language (C/C++/Java)** → **machine instructions**.  
- The syntax of instructions depends on the **hardware architecture**:
  - Intel → x86  
  - ARM → ARM ISA  
  - MIPS → MIPS ISA  
  - **RISC-V → RISC-V ISA** (focus of this course)
- Output: **Executable file (.exe)** containing machine instructions.
---
### 🧮 Assembler
- Converts **assembly instructions** → **binary (machine code)**.  
- Output: **Machine language** (logic 1s and 0s).  
- Hardware interprets these binary patterns to perform functions.
---
## 4️⃣ Example: Stopwatch App
Example flow of a simple stopwatch application:
- App (Stopwatch) → OS → C function → Compiler → RISC-V instructions → Assembler → Binary → Hardware.
- Binary patterns determine specific operations (e.g., add, subtract, display output).
- Each binary pattern corresponds to a specific hardware operation (e.g., addition, timing, display).
---

## 5️⃣ Instruction Set Architecture (ISA)
- The **ISA** acts as an **interface between software and hardware**.  
- Defines:
  - The **set of instructions** supported by hardware.  
  - The **syntax, format, and execution behavior** of each instruction.  
- In the RISC-V case, it defines how the CPU interprets and executes instructions.
---
## 6️⃣ Hardware Implementation Path
### 🧩 From ISA to Chip Layout
| Stage | Description |
|--------|-------------|
| **1. Specification (ISA)** | Defines operations like ADD, SUB, etc. |
| **2. RTL Implementation** | Hardware description (VHDL/Verilog) of ISA behavior. |
| **3. Synthesis** | Converts RTL → Gate-level representation (AND, OR, NOT, FFs). |
| **4. Physical Design** | Converts synthesized gates into actual silicon layout. |
---
## 7️⃣ Course Structure
### 🧩 Part 1A: RISC-V Instruction Set Architecture
- Understanding the **ISA concepts**, formats, and core architecture.  
- How software communicates with hardware.
### 🧩 Part 1B: RISC-V Applications
- Focus on practical applications using RISC-V.
### ⚙️ Part 2: RTL Design & Synthesis
- Writing and synthesizing a **RISC-V CPU core** in Verilog/VHDL.
### 🧱 Part 3: Physical Design Implementation
- Converting the synthesized design into a **layout** using **RTL-to-GDSII flow**.
---
## 🏁 Summary
- **Software-to-Hardware Flow:**  
  `App → OS → Compiler → Assembler → Hardware`  
- **RISC-V ISA:**  
  Acts as a **bridge between software and hardware**, defining how instructions are executed.  
- **Course Objective:**  
  Understand → Implement → Synthesize → Physically realize a RISC-V CPU core.
---
> 💡 **Key Takeaway:**  
> Every application you use ultimately becomes a set of binary patterns that your hardware understands through the instruction set
> and the RISC-V ISA defines that language for modern open-source CPUs.
