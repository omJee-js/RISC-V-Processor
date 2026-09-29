# RISC-V Processor — SystemVerilog Implementation


A from-scratch RISC-V processor implemented in **SystemVerilog**, supporting the core RISC-V instruction set architecture. The design was functionally validated with algorithmic test programs and extended with **custom instructions** that deliver a **1.6× speedup** over the baseline ISA implementation.

---

## 📋 Overview

This project implements a RISC-V CPU core covering the base instruction set, built and simulated entirely in SystemVerilog using **ModelSim**. Beyond standard ISA compliance, the design explores **microarchitectural customization** — adding application-specific instructions to accelerate common computational patterns without sacrificing correctness.

## ✨ Key Features

- **Core RISC-V ISA support** — arithmetic, logic, memory access, branch, and control-flow instructions
- **Custom accelerator instructions** — extended opcodes designed to speed up common operations, yielding a **1.6× performance improvement** over the baseline core
- **Functional validation via real workloads**, not just isolated instruction tests
- **Modular datapath design** — separable fetch, decode, execute, memory, and writeback stages
- **ModelSim-based simulation environment** for cycle-accurate verification and debugging

## 🏗️ Architecture

```
        ┌────────┐   ┌────────┐   ┌─────────┐   ┌────────┐   ┌───────────┐
        │  IF    │──►│   ID   │──►│   EX    │──►│  MEM   │──►│    WB     │
        │ Fetch  │   │ Decode │   │ Execute │   │ Access │   │ Writeback │
        └────────┘   └────────┘   └─────────┘   └────────┘   └───────────┘
             │             │            │             │             │
             ▼             ▼            ▼             ▼             ▼
        Instruction   Register     ALU / Custom   Data Memory   Register
          Memory        File      Exec Units       Interface    File Update
                                  (incl. custom
                                   accelerated
                                   ops)
```

**Core modules:**
| Module | Responsibility |
|---|---|
| `fetch_unit` | Instruction fetch, PC update logic |
| `decode_unit` | Instruction decode, control signal generation |
| `regfile` | General-purpose register file |
| `alu` | Arithmetic/logic execution, including custom instruction datapaths |
| `mem_stage` | Load/store interface to data memory |
| `writeback` | Result commit to register file |
| `custom_ext_unit` | Hardware for custom accelerated instructions |

*(Update module names to match your actual RTL file structure.)*

## ⚡ Custom Instruction Extensions

To improve performance beyond the baseline ISA, custom instructions were designed and integrated into the pipeline to accelerate frequently repeated operation patterns identified in the test workloads (e.g., comparison-heavy loops, iterative swaps, and index arithmetic).

**Result: 1.6× speedup** over the baseline RISC-V implementation, measured by cycle count across the validation test programs.

*(Consider adding a short table here: instruction name, opcode, operation performed, and where it's used.)*

## 🧪 Validation & Test Programs

Functional correctness and performance were verified in **ModelSim** using representative test programs:

| Test Program | Purpose |
|---|---|
| **Array Maximum** | Validates comparison, branching, and loop control |
| **Fibonacci Sequence** | Validates arithmetic operations and iterative/recursive control flow |
| **Bubble Sort** | Validates memory access patterns, nested loops, and conditional swaps |

Each program was run on both the **baseline** and **custom-instruction-enabled** configurations to confirm functional equivalence and measure the performance gain.

## 🛠️ Tools & Technologies

- **HDL:** SystemVerilog
- **Simulation:** ModelSim
- **ISA:** RISC-V (base integer instruction set + custom extensions)
- **Verification Method:** Directed test programs with cycle-count performance analysis

## 📁 Repository Structure

```
riscv-processor/
├── rtl/                    # Synthesizable RTL source files
│   ├── fetch_unit.sv
│   ├── decode_unit.sv
│   ├── regfile.sv
│   ├── alu.sv
│   ├── mem_stage.sv
│   ├── writeback.sv
│   └── custom_ext_unit.sv
├── tb/                     # Testbenches
│   └── cpu_tb.sv
├── programs/               # Test program assembly/machine code
│   ├── array_max.asm
│   ├── fibonacci.asm
│   └── bubble_sort.asm
├── sim/                    # ModelSim simulation scripts
├── docs/                   # Architecture notes, ISA extension spec
└── README.md
```



## 📈 Future Improvements

- Add pipeline hazard detection and forwarding for higher clock frequency
- Expand ISA coverage (e.g., multiply/divide extension, compressed instructions)
- Add branch prediction to reduce control hazard penalties
- FPGA hardware deployment and validation (beyond simulation)
- Automated regression test suite across all supported instructions

## 👤 Author
Omjee Chauhan
