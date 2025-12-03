# Digital Password-Based Access System (Vivado Project)

This repository contains the EEL 203 Digital Electronics project implemented in Verilog HDL and simulated using Xilinx Vivado. The project is a simple password-based access control system that checks a 12-bit password and keeps track of incorrect attempts. After three wrong attempts, the system activates an alarm (even though the counter used is a mod-4 counter, it effectively counts only three incorrect tries before triggering).

## Project Files

```
DEProject.v                - Main Verilog module
tb_DEProject.v             - Testbench for simulation
schematic.pdf              - Circuit schematic (part 1)
schematic2.pdf             - Circuit schematic (part 2)
EEL 203 Project report.docx
```

## Project Overview

The project implements a basic digital access verification system.
A 12-bit password is given through `PassIn`, and the correct password is stored in `SetPass`. When Enter is pressed, the system checks if both match.

If the password is wrong, the counter increments.
After three consecutive incorrect attempts, the alarm turns on.

Even though a mod-4 counter is used internally, the design logic activates the alarm at count = 3, meaning the user gets only three chances before being locked out.

When the correct password is entered:
- Access is granted
- Counter resets
- Alarm turns off

## Module Description

### 1. DEProject (Main Module)

This module:
- Compares the entered password with the stored one
- Controls the counter
- Outputs `Access`, `Alarm`, and `Count` signals

Password matching is done using bitwise XOR followed by a NOR reduction.

### 2. modN_ctr (Counter Module)

Although it is coded as a parameterized mod-4 counter,
the alarm does not wait for the counter to reach 4.

Instead, the alarm is enabled when:
```
Count == 3
```

So practically:
- 1st wrong attempt → Count = 1
- 2nd wrong attempt → Count = 2
- 3rd wrong attempt → Count = 3 → Alarm ON

The counter resets on a correct password or manual reset.

## Testbench (tb_DEProject.v)

The testbench verifies:
- Reset operation
- Correct password behavior
- Three incorrect attempts and alarm trigger
- System resetting after a correct entry

It uses delays and `$monitor` to show changes in main signals throughout the simulation.

## Schematics

Included PDFs illustrate:
- The password-checking block
- The counter and its control logic

These help visualize how the modules interact.

## Running the Project in Vivado

1. Create a new RTL project in Vivado
2. Add:
   - DEProject.v
   - tb_DEProject.v
3. Run Behavioral Simulation
4. Inspect waveforms for:
   - Count
   - Access
   - Alarm
   - Check signal

## Report

The project report file contains explanations, observations, simulation results, and the final conclusion.


Your Name  
EEL 203 – Digital Electronics Project
