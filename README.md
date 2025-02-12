
# VSD-IAT WORKSHOP

## Course Content

### Day 1
- Introduction to IC Design components and terminologies
- Software application to hardware execution
- RTL2GDS OpenLANE ASIC Flow
- Open-source EDA tools familiarization

### Day 2
- Chip floorplanning
- Placement
- Standard cell design
- Standard cell characterization

### Day 3
- 16 Mask CMOS fabrication process
- Design and characterize library cell CMOS inverter

### Day 4
- Introduction and generation of LEF files using Magic tool
- Custom cells in OpenLANE
- Fixing slack violations
- Clock Tree Synthesis (CTS)

### Day 5
- Power distribution network
- Routing
- SPEF extraction
- GDSII

---

## Day 1: How to Talk to Computers

During the physical designing process, you will encounter multiple terminologies. Some key terms are:
 ![d1_qfn_package](https://github.com/user-attachments/assets/4215ccd9-0843-45f0-a8ee-87236c106b3b)

- **Package**: A case that surrounds the circuit material to protect it from damage and allows for mounting electrical contacts connecting it to the PCB.
- **Die**: A small block of semiconductor material where the circuit is fabricated.
- **Core**: The actual area of the IC where logic resides.
- **Pads**: Interfaces between the internal signals of a chip and external pins, connected via wire bonds.

### Simple Definitions:
- **Package** = Protective case with pins.
- **Die** = Tiny brain of the chip.
- **Core** = The part where the processing happens.
- **Pads** = Connection points between the chip and the outside world.


![m2](https://github.com/user-attachments/assets/e7babab3-aa9a-443f-bf8e-51d33aba24b0)

### How Applications Run on Hardware

1. **Operating System (OS)**: Manages hardware and provides functions in C, C++, Java, etc.
2. **Compiler**: Converts OS functions into hardware-specific instructions (e.g., Intel, ARM).
3. **Assembler**: Translates instructions into binary (machine language - 0s and 1s).

---

## Open-Source ASIC Design Implementation

For open-source ASIC design, the following components must be available as open-source:
- **RTL Designs**: Register-Transfer Level (RTL) circuit descriptions.
- **EDA Tools**: Electronic Design Automation tools for design, simulation, and verification.
- **PDK Data**: Process Design Kits for chip fabrication.

### Historical Context
In the early days, IC design and fabrication were controlled by companies like **Intel** and **Texas Instruments (TI)**. This changed in **1979**, when **Lynn Conway** and **Carver Mead** introduced the idea of separating **design** from **fabrication**.

![m3](https://github.com/user-attachments/assets/0da45d98-ce04-4559-8426-d20a839e54dd)

They proposed structured **λ-based design rules** and wrote the first VLSI book, *"Introduction to VLSI Systems"*. This led to two types of companies:

- **Fabless Companies**: Focus only on designing chips.
- **Pure Play Fabs**: Focus only on manufacturing chips.

The interface between designers and fabs is a set of files and documents called **Process Design Kits (PDKs)**, which include:
- Device models
- Technology information
- Design rules
- Digital standard cell libraries
- I/O libraries

### The Challenge with PDKs
PDKs contain proprietary information and were traditionally shared under **NDAs (Non-Disclosure Agreements)**, limiting open innovation.

### The Breakthrough: Open-Source PDK
Google, in collaboration with **SkyWater Technology**, released the first-ever **open-source PDK** for SkyWater’s **130nm process** on **June 30, 2020**. This allowed hobbyists, researchers, and startups to design and fabricate custom chips without NDAs or high costs.

![m4](https://github.com/user-attachments/assets/c0769fcf-6845-4a89-844d-e68a2652a35e)

---

## RTL2GDS OpenLANE ASIC Flow
![m5](https://github.com/user-attachments/assets/ed9ff287-2a37-426b-b928-c2a3b99d2a0e)

**OpenLANE** is an automated **RTL to GDSII** flow. It integrates several open-source tools:
- **OpenROAD**
- **Yosys**
- **Magic**
- **Netgen**
- **Fault**
- **OpenPhySyn**
- **CVC**
- **SPEF-Extractor**
- **CU-GR**
- **KLayout**
![EDA](https://github.com/user-attachments/assets/ff1296e3-1e50-49a1-83d7-38d24f355c3c)

- Custom methodology scripts for design exploration and optimization.
![m6](https://github.com/user-attachments/assets/9e4e6a26-0eff-4e77-882b-2d148867ceb5)

## Section 1: Lab Work - Task 1

### Running 'picorv32a' Design Synthesis using OpenLANE Flow

The OpenLANE flow is an automated RTL-to-GDSII toolchain used for ASIC design. In this lab, we will run synthesis on the `picorv32a` design using OpenLANE and generate the necessary outputs.

---

### 🔹 **Understanding OpenLANE Configuration**
Each design in OpenLANE has specific configuration settings stored in the `config.tcl` file. These configurations define parameters like:
- 🕒 **Clock period**
- 🔌 **Clock port**
- 📜 **Verilog files**

The priority order for OpenLANE settings is:
1️⃣ `sky130_xxxxx_config.tcl` in `OpenLANE/designs/[design]/`
2️⃣ `config.tcl` in `OpenLANE/designs/[design]/`
3️⃣ Default values in `OpenLANE/configuration/`

---
![RUN](https://github.com/user-attachments/assets/d1d838fd-3b07-4998-b16e-e714b70aceb3)


###  **Steps to Run OpenLANE Flow**
To execute the OpenLANE flow for `picorv32a`, follow these steps:

📌 **Step 1:** Navigate to the OpenLANE directory
```bbox
cd openLANE
```
📌 **Step 2:** Start OpenLANE Docker environment
```bbox
docker
```
📌 **Step 3:** Start OpenLANE interactive mode
```bbox
bash-4.2$ ./flow.tcl -interactive
```
📌 **Step 4:** Load OpenLANE package
```bbox
% package require openlane 0.9
```
📌 **Step 5:** Prepare the design
```bbox
% prep -design picorv32a
```
📌 **Step 6:** Run synthesis
```bbox
% run_synthesis
```
📌 **Step 7:** Exit OpenLANE
```bbox
exit
```
📌 **Step 8:** Exit Docker
```bbox
Exit
```

---

### 📊 **Generated Outputs**
Once synthesis is complete, the following outputs will be generated:

![oplean ivoke](https://github.com/user-attachments/assets/8ac345de-cbd8-4589-bce7-a5701a0375f3)
![after](https://github.com/user-attachments/assets/caf1d548-d4b8-4ef6-a3db-101c588f1c20)
![cells](https://github.com/user-attachments/assets/9c868fd6-7a3f-4bba-947a-145256a87e33)
![cell2](https://github.com/user-attachments/assets/6868857a-62d8-461f-8601-66b1d3c0ec45)



✅ **Reports on cell usage and flip-flop count**
### 🔢 **Flip-Flop Ratio Calculation**
The flip-flop ratio is the ratio of the number of flip-flops to the total number of cells in the design. It is calculated using the following formula:
#### **Example Calculation:**
For the `picorv32a` design:
- **Number of Flip-Flops** = 1613
- **Total Number of Cells** = 14876
![cs](https://github.com/user-attachments/assets/f2b3a08b-17e8-485b-b8a9-f780cf38deb2)




