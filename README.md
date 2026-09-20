# UVM Labs

A structured, hands-on learning repository for building a complete UVM-based verification environment from the ground up. The labs progress from foundational UVM concepts to advanced verification patterns, including transactions, sequences, drivers, monitors, scoreboards, and Register Abstraction Layer (RAL) modeling.

The goal of this repository is to help engineers and learners understand how a modern verification environment is built and how each UVM component contributes to testbench architecture, stimulus generation, checking, and coverage.

---

## Learning Objectives

By the end of this lab series, you will be able to:

- Build a standard UVM verification environment
- Create and configure UVM test, environment, and top-level components
- Design reusable transactions and sequence classes
- Connect a driver to a DUT using a virtual interface and configuration database
- Implement monitors and scoreboards for functional checks
- Develop top-level and virtual sequences for complex scenarios
- Model DUT registers using the UVM Register Abstraction Layer (RAL)
- Understand how to structure a scalable verification framework for real projects

---

## Repository Structure

```text
UVM_LABS/
├── LAB1_Test_Environment/
├── LAB2_Transaction_Sequence/
├── LAB3_Driver_Interface/
├── LAB4_Monitor_Scoreboard/
├── LAB5_Top_Level_Sequence/
├── LAB6_RAL/
├── README.md
└── docs/                     # Optional: supporting notes, diagrams, and reference material
```

> The exact folder contents may evolve as each lab is implemented. The repository is intended to serve as a guided learning path rather than a single monolithic project.

---

## Why UVM?

UVM is a standardized verification methodology used to create reusable, scalable, and maintainable testbenches for complex digital designs. It provides:

- A reusable component hierarchy for testbench construction
- Standardized stimulus generation through sequences
- Mechanisms for DUT communication using drivers and monitors
- Scoreboarding and checking for functional validation
- Coverage and regression support for large verification flows

This repository teaches these ideas incrementally, starting from the basics and progressing to advanced architecture.

---

## Lab Overview

### Lab 1: Test, Environment & Report Messages

Focus: UVM hierarchy, factory registration, and reporting.

Topics covered:
- `uvm_test`
- `uvm_env`
- `uvm_info`, `uvm_warning`, and `uvm_error`
- build phase vs run phase
- verbosity control

Typical outcomes:
- Successful simulation startup
- Proper hierarchy construction
- Controlled logging and reporting

#### Compile & Simulate

##### QuestaSim
```bash
vlog -sv -timescale 1ns/1ps +incdir+$UVM_HOME LAB1_Test_Environment/*.sv
vsim -c -do "run -all; quit" top
```

##### VCS
```bash
vcs -sverilog -timescale=1ns/1ps -ntb_opts uvm +incdir+$UVM_HOME LAB1_Test_Environment/*.sv
./simv
```

---

### Lab 2: Transaction & Sequence Classes

Focus: Stimulus generation using transactions and sequences.

Topics covered:
- `uvm_sequence_item`
- randomization and constraints
- `uvm_sequence`
- sequencer integration
- factory registration

Typical outcomes:
- Randomized transaction generation
- Reusable sequence logic
- Unified stimulus development

#### Compile & Simulate

##### QuestaSim
```bash
vlog -sv -timescale 1ns/1ps +incdir+$UVM_HOME LAB2_Transaction_Sequence/*.sv
vsim -c -do "run -all; quit" top
```

##### VCS
```bash
vcs -sverilog -timescale=1ns/1ps -ntb_opts uvm +incdir+$UVM_HOME LAB2_Transaction_Sequence/*.sv
./simv
```

---

### Lab 3: Driver and Virtual Interface

Focus: Driving DUT signals with a UVM driver.

Topics covered:
- `uvm_driver`
- handshake and TLM communication
- virtual interface usage
- `uvm_config_db`
- reset sequences

Typical outcomes:
- Driver receives sequence items
- DUT pin-level activity is stimulated correctly
- Reset and protocol flow are controlled

#### Compile & Simulate

##### QuestaSim
```bash
vlog -sv -timescale 1ns/1ps +incdir+$UVM_HOME LAB3_Driver_Interface/*.sv
vsim -c -do "run -all; quit" top
```

##### VCS
```bash
vcs -sverilog -timescale=1ns/1ps -ntb_opts uvm +incdir+$UVM_HOME LAB3_Driver_Interface/*.sv
./simv
```

---

### Lab 4: Monitor & Scoreboard

Focus: Observing DUT behavior and checking expected results.

Topics covered:
- `uvm_monitor`
- analysis ports
- transaction reconstruction
- scoreboard comparison logic
- pass/fail checking

Typical outcomes:
- DUT activity is monitored
- Transactions are reconstructed from signal activity
- Functional checking is automated

#### Compile & Simulate

##### QuestaSim
```bash
vlog -sv -timescale 1ns/1ps +incdir+$UVM_HOME LAB4_Monitor_Scoreboard/*.sv
vsim -c -do "run -all; quit" top
```

##### VCS
```bash
vcs -sverilog -timescale=1ns/1ps -ntb_opts uvm +incdir+$UVM_HOME LAB4_Monitor_Scoreboard/*.sv
./simv
```

---

### Lab 5: Top-Level Sequence

Focus: Coordinating multiple scenarios into a structured verification flow.

Topics covered:
- top-level sequence control
- child sequence integration
- sequencing order and scenario generation
- virtual sequence concepts

Typical outcomes:
- Multi-step test scenarios
- Complex verification stimulus sequencing
- Better reuse across tests

#### Compile & Simulate

##### QuestaSim
```bash
vlog -sv -timescale 1ns/1ps +incdir+$UVM_HOME LAB5_Top_Level_Sequence/*.sv
vsim -c -do "run -all; quit" top
```

##### VCS
```bash
vcs -sverilog -timescale=1ns/1ps -ntb_opts uvm +incdir+$UVM_HOME LAB5_Top_Level_Sequence/*.sv
./simv
```

---

### Lab 6: Register Abstraction Layer (RAL)

Focus: Modeling and verifying hardware registers with UVM RAL.

Topics covered:
- register definitions
- address maps
- register blocks
- frontdoor/backdoor access
- prediction and mirror checking

Typical outcomes:
- Register model generation
- Read/write transaction verification
- DUT and model synchronization

#### Compile & Simulate

##### QuestaSim
```bash
vlog -sv -timescale 1ns/1ps +incdir+$UVM_HOME LAB6_RAL/*.sv LAB6_RAL/ral_model/*.sv
vsim -c -do "run -all; quit" top
```

##### VCS
```bash
cd LAB6_RAL
ralgen -t -uvm -top ral_top -dir ral_model
vcs -sverilog -timescale=1ns/1ps -ntb_opts uvm +incdir+$UVM_HOME *.sv ral_model/*.sv
./simv
```

---

## Recommended Learning Path

```text
Lab 1 → UVM Components & Reporting
   ↓
Lab 2 → Transactions & Sequences
   ↓
Lab 3 → Drivers & Virtual Interfaces
   ↓
Lab 4 → Monitors & Scoreboards
   ↓
Lab 5 → Top-Level Sequences
   ↓
Lab 6 → RAL Modeling
   ↓
Final Project → Integrated UVM Verification Environment
```

A sequential flow is recommended. Each lab builds on the previous one and establishes the conventions needed for a realistic verification environment.

---

## Prerequisites

Before starting the labs, you should have:

- Familiarity with SystemVerilog basics
- Basic understanding of digital design and simulation concepts
- A simulator such as VCS, Questa, Xcelium, Riviera, or similar
- Access to the UVM library for your chosen simulator
- Basic familiarity with command-line workflows

---

## Suggested Development Workflow

For each lab:

1. Review the objective and design concept.
2. Implement the UVM class hierarchy required for the lab.
3. Connect the DUT interface or transaction flow as needed.
4. Compile and run the simulation with the chosen tool.
5. Check logs, report messages, and pass/fail results.
6. Extend the lab with additional scenarios for deeper learning.

---

## Example Simulation Command

```bash
vsim -c -do "run -all; quit" top_tb
```

```bash
vcs -sverilog -ntb_opts uvm top_tb.sv
./simv
```

Commands vary by simulator, so adapt them to your local toolchain and project setup.

---

## Suggested Lab Structure

```text
LAB6_RAL/
├── ral_model/
│   ├── reg_pkg.sv
│   ├── reg_block.sv
│   ├── reg_model.sv
│   └── reg_top.sv
├── sequences/
├── tests/
├── tb/
└── README.md
```

This layout is useful for keeping the environment organized as the verification infrastructure grows.

---

## Final Challenge

Once all labs are complete, the final challenge is to integrate them into a single verification environment with:

- UVM testbench components
- reusable transactions and sequences
- driver and monitor agents
- scoreboard validation
- functional coverage
- RAL integration
- configurable test scenarios

This is the point where learners begin to resemble real-world verification engineers, building scalable and maintainable infrastructures.

---

## Resources

Useful references:

- UVM User Guide
- IEEE 1800 SystemVerilog Standard
- Accellera UVM Reference Documentation
- Simulator-specific UVM manuals and examples

---

## Author

Mehul Prajapati

Email: mehul.arvind@signoffsemi.com

This repository was created as a practical learning path for engineers who want to build strong hands-on experience with UVM-based verification environments.

---

## Notes

This repo is designed as an educational progression. It is best used by working through each lab in order, validating behavior in simulation, and reinforcing the concepts through additional custom experiments and extensions.
