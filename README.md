
# FIFO (First-In First-Out) Buffer – Verilog Implementation

## 📘 Overview

This project implements a parameterized **FIFO (First-In First-Out) buffer** in **Verilog**, complete with a **testbench** and support for:

- Push and Pop operations
- Full and Empty detection
- Overrun and Underrun flags
- Threshold-based trigger signal
- Internal memory monitoring

The design simulates in **Xilinx Vivado** and is suitable for FPGA or ASIC integration.

---

## 📁 Directory Structure

```
fifo_project/
│
├── fifo_top.v       # Top-level FIFO module
├── fifo_tb.v        # Testbench
├── README.md        # Project documentation
```

---

## 🔧 Features

- **Depth**: 16 elements  
- **Width**: 8-bit data  
- **Flags**:  
  - `full`  
  - `empty`  
  - `overrun`  
  - `underrun`  
  - `thre_trigger` (threshold reached)
- Internal memory (`mem[0:15]`) and `waddr` tracking

---

## 🚀 Getting Started

### 🛠 Requirements

- [Xilinx Vivado](https://www.xilinx.com/products/design-tools/vivado.html)
- Basic knowledge of Verilog/SystemVerilog

### 🔬 Simulation Steps

1. Open Vivado and create a new simulation project.
2. Add `fifo_top.v` and `fifo_tb.v` to your project.
3. Set `fifo_tb` as the **top module** for simulation.
4. Launch simulation.

---

## 📊 Waveform Tips

To view internal signals like memory (`mem`) and write pointer (`waddr`):

### Option 1: GUI

- Expand `fifo_top` instance in simulation.
- Right-click on `mem` → Expand → Select `mem[0]` to `mem[15]` → **Add to Wave Window**.
- Also add `waddr`.

### Option 2: TCL (Recommended)

Open the TCL console and paste:

```tcl
for {set i 0} {$i < 16} {incr i} {
    add_wave -radix hex sim:/fifo_tb/dut_fifo/mem\[$i\]
}
add_wave sim:/fifo_tb/dut_fifo/waddr
```

---

## 🧪 Testbench Behavior

The testbench performs:

1. FIFO reset
2. 20 write cycles with random data
3. 20 read cycles
4. Observes flag behavior (overrun/underrun/threshold)

---

## 📌 Signals

| Signal         | Direction | Description                        |
|----------------|-----------|------------------------------------|
| `clk`          | input     | Clock signal                       |
| `rst`          | input     | Synchronous reset                  |
| `en`           | input     | Enable signal                      |
| `push_in`      | input     | Push request                       |
| `pop_in`       | input     | Pop request                        |
| `din[7:0]`     | input     | Input data                         |
| `dout[7:0]`    | output    | Output data                        |
| `empty`        | output    | FIFO is empty                      |
| `full`         | output    | FIFO is full                       |
| `overrun`      | output    | Push attempted on full FIFO        |
| `underrun`     | output    | Pop attempted on empty FIFO        |
| `threshold[3:0]` | input   | Threshold level                    |
| `thre_trigger` | output    | High when `waddr >= threshold`     |

---

## ✅ License

This project is open-source and free to use under the [MIT License](https://opensource.org/licenses/MIT).

---

## 👨‍💻 Author

Created by: Reyansh Gahlot 
Date: June 17, 2025
