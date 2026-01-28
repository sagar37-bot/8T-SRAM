# Design and Characterization of a High-Stability 8T SRAM Cell

This repository contains the design, simulation, and performance analysis of an **8-Transistor (8T) SRAM cell** implemented in **90nm CMOS technology**. The design focuses on solving the "Read Disturbance" issue found in conventional 6T SRAM cells by using a decoupled read-port architecture.

## 📌 Project Highlights
- **Technology:** 90nm CMOS (Cadence Virtuoso)
- **Architecture:** 8T (Decoupled Read/Write Ports)
- **Key Achievement:** ~28% higher stability compared to standard 6T SRAM.
- **Tools:** Cadence Virtuoso Schematic Editor, Spectre Simulator, ADE L/XL.

## 🏗️ Circuit Architecture
The 8T cell is divided into three functional blocks:
1. **Storage Core (M1-M4):** Two cross-coupled CMOS inverters forming a bistable latch.
2. **Write Port (M5-M6):** Two NMOS access transistors controlled by the Write Word Line (WWL).
3. **Read Port (M7-M8):** A dedicated 2-transistor read-stack that isolates the storage nodes from the Read Bit Line (RBL), ensuring **Read Disturbance Immunity**.

### Transistor Sizing Strategy
| Transistor Block | Device | W/L Ratio (nm/nm) | Rationale |
| :--- | :--- | :--- | :--- |
| **Pull-Up PMOS** | PM0, PM1 | 400 / 100 | Minimum sized for area; ensures logic '1' restoration. |
| **Pull-Down NMOS** | NM1, NM3 | 200 / 100 | Upsized for strong '0' discharge and improved $\beta$-ratio (~1.45). |
| **Write Access** | NM0, NM2 | 250 / 100 | Optimized for write-ability without compromising hold stability. |
| **Read Port** | NM4, NM5 | 200 / 100 | Sized to provide sufficient read current while limiting leakage. |

## 📊 Performance & Stability Metrics
Simulations were conducted at a nominal **VDD of 1.2V**.

### 1. Static Noise Margin (SNM) Analysis
The stability was verified using the "Butterfly Curve" method (DC Analysis).
- **Hold SNM (HSNM):** 848.5 mV (70% of VDD)
- **Read SNM (RSNM):** 558.3 mV (47% of VDD)
- **Write SNM (WSNM):** 446.8 mV

### 2. Timing & Power
- **Write Delay:** 67.0 ps
- **Read Delay:** 111 ps
- **Static Power (Leakage):** 67.5 nW
- **Energy per Cycle:** 3.88 pJ

## 📈 Simulation Results
- **Butterfly Curve:** The intersection of VTCs confirms a metastable point at **564.5 mV**, indicating high noise tolerance.
- **Transient Analysis:** Confirmed successful Write '1', Write '0', and non-destructive Read operations over a 100ns window.
- **Monte Carlo Simulation:** 200-point statistical analysis confirms **100% yield** for RSNM, proving the design is resilient to process variations.

## 🚀 Why 8T over 6T?
In a standard 6T cell, the storage nodes are directly exposed to the bit-lines during a read, which can accidentally flip the stored bit. This 8T design uses a **Read Buffer**, meaning the data is never "stressed" during a read operation. This makes it a superior choice for high-reliability caches and Compute-In-Memory (CIM) applications.

## Simulation Software
Cadence Virtuoso 90nm PDK
