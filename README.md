# VSD-IAT
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
 ![d1_qfn_package](https://github.com/user-attachments/assets/64a1340c-542b-4870-af11-6a6ca4c9107f)
- **Package**: A case that surrounds the circuit material to protect it from damage and allows for mounting electrical contacts connecting it to the PCB.
- **Die**: A small block of semiconductor material where the circuit is fabricated.
- **Core**: The actual area of the IC where logic resides.
- **Pads**: Interfaces between the internal signals of a chip and external pins, connected via wire bonds.

### Simple Definitions:
- **Package** = Protective case with pins.
- **Die** = Tiny brain of the chip.
- **Core** = The part where the processing happens.
- **Pads** = Connection points between the chip and the outside world.


![m2](https://github.com/user-attachments/assets/cf1fb712-1809-4073-9d9a-4fe97b28f537)

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

![m3](https://github.com/user-attachments/assets/a27c2a94-52aa-43d2-be71-4bfa2dab74e1)

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
![m4](https://github.com/user-attachments/assets/b6480666-85d3-4d62-b45f-f584477f385a)


---

## RTL2GDS OpenLANE ASIC Flow
![m5](https://github.com/user-attachments/assets/c9578d4d-578d-423c-abd7-bc8fbb6b125b)

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
- Custom methodology scripts for design exploration and optimization.
![m6](https://github.com/user-attachments/assets/e49ccb45-8802-44fb-84ff-60984b66acac)

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
![oplean ivoke](https://github.com/user-attachments/assets/ddfa15e6-6f66-4527-9d35-0bbe03ff62d8)
![after](https://github.com/user-attachments/assets/83892b10-8cbc-47e9-ad59-ec5aa3963285)
![cells](https://github.com/user-attachments/assets/75fb7fd0-ec27-4623-ad07-447e3c369adb)
![cell2](https://github.com/user-attachments/assets/bb26c112-ebd4-43a6-8286-b0d8a7a28110)

✅ **Reports on cell usage and flip-flop count**
### 🔢 **Flip-Flop Ratio Calculation**
The flip-flop ratio is the ratio of the number of flip-flops to the total number of cells in the design. It is calculated using the following formula:
#### **Example Calculation:**
For the `picorv32a` design:
- **Number of Flip-Flops** = 1613
- **Total Number of Cells** = 14876
  ![cs](https://github.com/user-attachments/assets/36659b11-d43b-4b36-af4f-4dd2dd6fd253)




