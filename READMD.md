# 🛡️ APB Slave IP Design & Verification

## 📖 Overview
This repository contains the RTL design and functional verification of an **APB (Advanced Peripheral Bus) Slave** interface. The APB protocol is part of the AMBA hierarchy, designed for low-bandwidth peripherals where low power consumption and reduced interface complexity are required.

## 🗂️ Repository Structure

| Directory | Description |
| :--- | :--- |
| `rtl/` | Verilog source code for the APB Slave logic. |
| `tb/` | SystemVerilog testbench for protocol and functional verification. |
| `synthesis/` | Logic synthesis scripts and technology-mapped netlist. |
| `sta/` | Timing constraints (`.sdc`) and Static Timing Analysis reports. |
| `AREA/` | Area estimation and reporting for the synthesized design. |
| `HOW_TO_SIMULATE.txt` | Instructions for custom system clock configurations. |
| `README.md` | This document. |

## 🛠️ Design & Verification Flow

### 1. RTL Design Implementation
The design is fully compliant with the AMBA APB specification, supporting the standard three-state operation:
* **IDLE:** The default state for no bus activity.
* **SETUP:** Asserted during the first clock cycle of a transfer (`PSEL` is high).
* **ACCESS:** Asserted during the second cycle to complete data phases (`PENABLE` is high).


### 2. Verification Strategy
A comprehensive SystemVerilog testbench was developed to ensure protocol robustness:
* **Protocol Compliance:** Verifies that the slave responds only when `PSEL` and `PENABLE` follow the correct sequence.
* **Randomized Testing:** Uses randomized address and data patterns to test the slave's internal memory/registers.
* **Wait-State Check:** Validates timing accuracy during both read and write operations.

## ⚙️ User Customization
Users can adapt this IP to different system environments by modifying the frequency parameters:
* **System Clock:** Update the `SYS_CLK_FREQ` parameter in the RTL and TB files (e.g., from `50_000_000` to `100_000_000`).
* **Randomization:** The testbench is designed to handle randomized baud rates and data streams for stress-testing.
* **Simulation:** See `HOW_TO_SIMULATE.txt` for detailed steps on re-running simulations with your own parameters.

## 🔗 Documentation & Professional Connect
For detailed waveform analysis, state machine diagrams, and synthesis reports, please visit:

* **Complete Documentation (LinkedIn):** [Your LinkedIn Post Link Here]
* **LinkedIn Profile:** [Your LinkedIn Profile Link Here]

## 🔮 Future Scope
1. **Wait-State Insertion:** Implementing `PREADY` logic to support slower peripheral devices.
2. **Protection Support:** Upgrading to APB4 to support `PPROT` (Protection) and `PSTRB` (Strobe) signals.
3. **Error Reporting:** Adding `PSLVERR` for invalid address decoding or illegal access types.

---
**Note:** The open-source PDK used for synthesis and timing analysis can be found at the [Open Cell and Free PDK Libraries](https://si2.org/open-cell-and-free-pdk-libraries/) website.
