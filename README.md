# 🛡️ APB Slave IP: RTL-to-STA Implementation Flow

## 📖 Overview
This repository documents the complete implementation flow of an **APB (Advanced Peripheral Bus) Slave** interface. The project covers the entire ASIC design cycle—from **RTL Design** and **Functional Verification** to **Logic Synthesis** and **Static Timing Analysis (STA)**—using a fully open-source toolchain.

## 🗂️ Repository Structure

| Directory | Description |
| :--- | :--- |
| `rtl/` | Verilog source code for the APB Slave logic. |
| `tb/` | SystemVerilog testbench for protocol and functional verification. |
| `synthesis/` | Yosys scripts, technology-mapped netlist, and **Area reports**. |
| `sta/` | Timing constraints (`.sdc`), OpenSTA scripts, and **Performance reports**. |
| `AREA/` | Detailed area estimation and cell utilization data. |
| `HOW_TO_SIMULATE.txt` | Instructions for user-defined clock and randomization settings. |
| `README.md` | This document. |

## 🛠️ Implementation Flow & Tools

### 1. Design & Functional Verification
* **Logic:** Compliant with AMBA APB protocol (IDLE, SETUP, and ACCESS states).
* **Simulation Environment:** EDA Playground.
* **Live Demo:** [Check the Simulation on EDA Playground](https://www.edaplayground.com/x/s7kR) 

### 2. Logic Synthesis (RTL to Netlist)
* **Tool:** **Yosys Open-Source Synthesis Suite**.
* **Work Performed:** Converted RTL into a technology-mapped netlist.
* **Area Analysis:** Performed area estimation to determine gate count and hardware overhead. Reports are available in the `synthesis/` and `AREA/` folders.

### 3. Static Timing Analysis (STA)
* **Tool:** **OpenSTA**.
* **Goal:** Verified the performance of the synthesized netlist.
* **Metrics:** Calculated Setup and Hold slacks and identified the maximum operating frequency ($F_{max}$) under the specified constraints.



## ⚙️ How to Replicate the Project

Detailed guidance for replicating each stage of this project is provided within the respective directories:

### 🚀 Synthesis & Area Reporting
Navigate to the `synthesis/` folder. Use the provided command scripts to run Yosys:
```bash
# Example command to run synthesis:
yosys -s synthesis/synthesis_script.ys
