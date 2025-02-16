# VSD-IAT WORKSHOP

## Table of Contents
- [Course Content](#course-content)
- [Day 1: How to Talk to Computers](#day-1-how-to-talk-to-computers)
- [Day 2: Good Floorplan vs Bad Floorplan](#day-2-good-floorplan-vs-bad-floorplan)

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

### IC Design Terminology
![d1_qfn_package](https://github.com/user-attachments/assets/4215ccd9-0843-45f0-a8ee-87236c106b3b)

#### Key Components:
- **Package**: A case that surrounds the circuit material to protect it from damage and allows for mounting electrical contacts connecting it to the PCB.
- **Die**: A small block of semiconductor material where the circuit is fabricated.
- **Core**: The actual area of the IC where logic resides.
- **Pads**: Interfaces between the internal signals of a chip and external pins, connected via wire bonds.

#### Simple Definitions:
- **Package** = Protective case with pins
- **Die** = Tiny brain of the chip
- **Core** = The part where the processing happens
- **Pads** = Connection points between the chip and the outside world

![m2](https://github.com/user-attachments/assets/e7babab3-aa9a-443f-bf8e-51d33aba24b0)

### Application to Hardware Flow
1. **Operating System (OS)**
   - Manages hardware
   - Provides functions in C, C++, Java, etc.
2. **Compiler**
   - Converts OS functions into hardware-specific instructions
3. **Assembler**
   - Translates instructions into binary (machine language)

### Open-Source ASIC Design Implementation

#### Required Components:
- **RTL Designs**: Register-Transfer Level circuit descriptions
- **EDA Tools**: Electronic Design Automation tools
- **PDK Data**: Process Design Kits

#### Historical Context
- **1979**: Lynn Conway and Carver Mead separated design from fabrication
- Introduced λ-based design rules
- Wrote "Introduction to VLSI Systems"

![m3](https://github.com/user-attachments/assets/0da45d98-ce04-4559-8426-d20a839e54dd)

#### Industry Evolution:
- **Fabless Companies**: Design-focused
- **Pure Play Fabs**: Manufacturing-focused

#### PDK Components:
- Device models
- Technology information
- Design rules
- Digital standard cell libraries
- I/O libraries

### RTL2GDS OpenLANE ASIC Flow
![m5](https://github.com/user-attachments/assets/ed9ff287-2a37-426b-b928-c2a3b99d2a0e)

#### Integrated Tools:
- OpenROAD
- Yosys
- Magic
- Netgen
- Fault
- OpenPhySyn
- CVC
- SPEF-Extractor
- CU-GR
- KLayout

![EDA](https://github.com/user-attachments/assets/ff1296e3-1e50-49a1-83d7-38d24f355c3c)

### Lab Work - Task 1: Running 'picorv32a' Design

#### OpenLANE Configuration Priority:
1. sky130_xxxxx_config.tcl
2. config.tcl
3. Default values

![RUN](https://github.com/user-attachments/assets/d1d838fd-3b07-4998-b16e-e714b70aceb3)

#### Step-by-Step Execution:

1. **Navigate to OpenLANE directory**
```bash
cd openLANE
```

2. **Start Docker environment**
```bash
docker
```

3. **Start OpenLANE interactive mode**
```bash
./flow.tcl -interactive
```

4. **Load OpenLANE package**
```bash
package require openlane 0.9
```

5. **Prepare design**
```bash
prep -design picorv32a
```

6. **Run synthesis**
```bash
run_synthesis
```

#### Generated Outputs:
![oplean ivoke](https://github.com/user-attachments/assets/8ac345de-cbd8-4589-bce7-a5701a0375f3)
![after](https://github.com/user-attachments/assets/caf1d548-d4b8-4ef6-a3db-101c588f1c20)
![cells](https://github.com/user-attachments/assets/9c868fd6-7a3f-4bba-947a-145256a87e33)
![cell2](https://github.com/user-attachments/assets/6868857a-62d8-461f-8601-66b1d3c0ec45)

#### Flip-Flop Ratio Calculation:
- **Number of Flip-Flops**: 1613
- **Total Number of Cells**: 14876

![cs](https://github.com/user-attachments/assets/f2b3a08b-17e8-485b-b8a9-f780cf38deb2)

---

## Day 2: Good Floorplan vs Bad Floorplan

### Introduction to Floorplanning
![day2](https://github.com/user-attachments/assets/13184123-e431-40f9-85ba-92bc1f414b14)
![day2 2](https://github.com/user-attachments/assets/45988e7f-4dba-48dd-a728-49ae54c7cc14)

### Key Concepts:

#### Aspect Ratio
- Ratio of height to width of core area
- Aspect ratio of 1 indicates square shape

#### Utilization Factor
- Ratio of netlist area to core area
- Recommended range: 0.5 to 0.7

#### Preplaced Cells
- Fixed location cells
- Examples: memory blocks, clock gating cells, comparators

#### Decoupling Capacitors
- Used with preplaced cells
- Compensates voltage drop
- Charges to supply voltage

#### Power Planning
- Provides power to all components
- Creates power grid network
- Mitigates voltage droop

### Implementation Steps

1. **Run Floorplan**
```bash
run_floorplan
```

![lab 2 fp 1](https://github.com/user-attachments/assets/3c80b5f4-7821-4533-98c7-8a009a223080)
![fp 2](https://github.com/user-attachments/assets/27a84638-4326-4fb6-a6a0-5ae659dadbe2)
![fp 3](https://github.com/user-attachments/assets/2243289c-cd58-4e24-b5c0-0596d6c8bea2)

2. **Run Placement**
```bash
run_placement
```
```bash
magic -T $PDK/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![fp 4](https://github.com/user-attachments/assets/f3d7d08f-8d7f-4fe1-b24c-c875a0df5bda)

3. **Load Placement in Magic**
```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-02_07-35/results/placement/

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

### Placement Results
![fp 5](https://github.com/user-attachments/assets/136a351f-27d8-4cdb-812a-b31518b264f3)
![fp 5 5](https://github.com/user-attachments/assets/e05e4b74-c9fb-4420-ac43-aa558a4fc532)
