# PD_WorkShop_using_OpenLANE_sky130nm
This project is done as part of VLSI Physical Design Work-Shop organized by VLSI System Design. In this project a complete RTL to GDSII flow for picorv32a SoC is executed with Openlane using Skywater130nm PDK. OpenLane is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, SPEF-Extractor, CU-GR, Klayout and a number of custom scripts for design exploration and optimization. The flow performs full ASIC implementation steps from RTL all the way down to GDSII.

## Table of Contents
1. [Day-1 Inception of Opensource EDA, OpenLANE and Sky130 PDK](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#day-1-inception-of-opensource-eda-openlane-and-sky130-pdk)
   - [How to Talk to computers](#how-to-talk-to-computers)
     - [Introduction to QFN48 Package](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#introduction-to-qfn-48-package-chip-pads-core-die-and-ips)
     - [Introduction to RISCV ISA](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#introduction-to-riscv-isa)
     - [From Software Applications to Hardware](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#from-software-applications-to-hardware) 
   - [SOC Design and OpenLANE](#soc-design-and-openlane)
     - [Introduction to open-source digital asic design](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/tree/main#introduction-to-open-source-digital-asic-design)
     - [Simplified RTL2GDS Flow](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/tree/main#simplified-rtl2gds-flow)
     - [OpenLANE ASIC Design Flow](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#openlane-asic-design-flow)
   - [Day-1 Lab : Get familiar to open-source EDA tools](#opensource-eda-tools)
     - [OpenLANE Directory structure](#openlane-design-stages)
     - [Design Preparation Step](#openlane-files)
     - [Invoking OpenLANE](#invoking-openlane)
     - [Design Preparation Step](#design-preparation-step)
     - [Review of files & Synthesis step](#design-preparation-step#review-of-files-&-synthesis-step)

## Day-1 Inception of Opensource EDA, OpenLANE and Sky130 PDK

### How to Talk to computers

#### Introduction to QFN-48 Package, chip, pads, core, die and IPs

The QFN-48 Package with quad flat no leads looks as follows 

![1](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/225fb7a4-5f55-46c9-9e73-83aeebdcdfa1)

The chip sits at the center of the package and the chip is connected to package using wirebonds 

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/31884276-f9b0-477d-a79c-38240213cba1)

The core of the chip will contain two types of blocks:

- **Foundry IP's**  are the  blocks which requires some amount of intelligent techniques to build which can only be designed by foundries so they are called intellectual properties, some examples of Foundry IP's are ADC,DAC,SRAM and PLL.
- **Macro** are the blocks consisting of pure digital logic compared to IP's which might require some analog parts, example of macros are RISC-V SOC and SPI.

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/612618fb-247a-4aac-8bea-f3e83123b29b)

#### Introduction to RISCV ISA

RISCV-ISA is nothing but the languge of the computers and this is the way we talk to computer. For example a C program has to be run on a particular harware which has a layout(qflow) it should be first compiled to a assembly level language next converted to a machine language program, there is another interface between RISCV Architecture and layout which is a hardware description language, we need to implement these RISCV specifications using some RTL in our case picorv32 cpu core, and finally from RTL to layout which is our standard PnR flow or RTL to GDS flow.

![Screenshot (7444)](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/eec16ed0-85a8-48cd-a8af-2b405c624fa4)

#### From Software Applications to Hardware

Application software enters into a block called as system software, and system software in turn converts the application program into a binary language, these binary numbers which are the output of assembler are fed to hardware. If a user wishes to run a certain application software on a computer, it first enters the OS and corresponding output of OS is in the form of C/C++/Java program which must be converted into instructions by the compliler. The ouput of the compiler is hardware dependent. These instructions go as inputs to the assembler which outputs binary language that the hardware logic in the chip layout can make sense of. According to the bits received, the digital logic consisting of gates performs the function required by the user of the application software.

![Screenshot (7455)](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/b4854ed4-7c6c-48b1-aa8f-01ac6aa47502)

We start from the instruction set, we try to get the specifications of the instruction set,we write a hardware description language of these instructions, we then synthesize it to gate level netlist and this gate level netlist is converted into its respective layout based on the RTL to GDS flow.

![Screenshot (7480)](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/5786c64d-c320-4fef-bb46-1db314129866)

### SOC Design and OpenLANE

#### Introduction to open-source digital asic design

The Digital Application Specific Integrated Circuit (ASIC) design requires three enablers or elements - Resistor Transistor Logic Intellectual Property (RTL IPs), Electronic Design Automation (EDA) Tools and Process Design Kit (PDK) data.

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/73fabc02-084c-4a71-a10d-3ec52a55195e)

Open Souce ASIC design consists of following components :

- **Opensource RTL Designs** : github, librecores, opencores
- **Opensource EDA tools** : Qflow, OpenROAD, OpenLANE
- **Opensource PDK data** : Google + Skywater130 PDK

- **PDK(Process Design Kit)** : A set of data files and documents which serves as the interface between the designer and the fab. This includes standard cell libraries, IO libraries, process design rules (DRC, LVS, etc.) or A collection of files used to model a fabrication process for the EDA tools used to design an IC

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/c881d19b-e12f-4990-aca4-d3a6d932963c)

#### Simplified RTL2GDS Flow

The ASIC flow objective is to convert RTL design to GDSII format used for final layout. The flow is also known as an automated PnR (Place & route). RTL2GDS flow is as follows : 

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/064647c7-4ec1-48a7-94b5-c97449d42826)

- **Synthesis** : The process of converting a Technology independent RTL into a Technology dependent gate level netlist.
- **Floor Planning + Power Planning** : In this step, the rough position of each block on the silicon chip and the shape of each block will be decided,Placement of I/O and macros takes place in this step and silicon area is planned accordingly also a robust power distribution network is created. The power network usually uses the upper metal layer which are thicker than lower layer and thus lower resistance. This lowers the IR drop problem. 
- **Placement** : In this step, the exact position of various sub-blocks will be decided with the objective of maintaining adequate space between various blocks, so that, Vdd and Ground supply lines and the interconnection wires can be routed in such a way that, there will be no clutter, This step consists of 2 stages - Global Placement which is for optimal position of cells for inital congestion analysis and Detailed Placement which has legalized placement of cells and no overlapping of cells.
- **CTS(Clock Tree Synthesis)** : After the completion of floor planning and placement, millions of flip-flops in the complex circuit will be scattered at multiple places on the silicon chip, so that the transmission delays of the clock signal for all the flip-flops will not be the same. The clock will not arrive/reach all the flip-flops at the same time and it is mandatory to make sure that, the clock signal reaches multiple flip-flops with no or minimum skew difference. CTS will ensure that the clock reaches various flip-flops almost at the same time. In the clock tree synthesis process, any one of the standard Tree topology structures such as X-tree, H-tree, I-tree will be implemented in the design with an intention of making the length of all the wires in the clock distribution network equal.
- **Routing** : In this step, interconnecting wires between various blocks will be routed in such a way that, the length of the interconnecting wires will be minimum for meeting the timing requirements and for ensuring that, the chip area will not be increased. Proper routing will also ensure that there are no congestion hotspots in the chip so that, the probability of having faults during the fabrication will be less. The router uses PDK information (thickness, pitch, width,vias) for each metal layer to do the routing. The Sky130 defines 6 routing layers. It do global routing and detailed routing.
- **Signoff** : Involves physical verification checks like DRC, LVS, ERC and timing verification. Design Rule Checking or DRC ensures final layout honors all design rules and Layout versus Schematic or LVS ensures final layout matches the gate level netlist from synthesis phase. Timing verification ensures timing constraints are met.

#### OpenLANE ASIC Design Flow

OpenLANE started as an open source flow for a true open-source tape-out experiment, at efabless we have family of SoC's called as strive and we wanted to have open everything SoC (Open PDK, Open EDA, Open RTL). OpenLANE is tuned for SkyWater-130nm Open PDK and it also supports XFAB180 and GF130G. It has two modes of operation : 

* Autonomous : it performs all of the ASIC flow in one step
* Interactive : It is a step-by-step process to perform every phase of ASIC flow with specific commands.

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/31d5f2c8-de11-4e50-8a91-398a133acf66)

OpenLANE flow consists of several stages. By default all flow steps are run in sequence. Each stage may consist of multiple sub-stages. The flow starts with the design RTL and ends with final layout into GDSII foemat. OpenLANE is based on several open source project such as openROAD, abc, qflow, yosys, Fault and many other. The OpenLANE ASIC flow is as follows.

1. **Synthesis**
    1. `yosys` - Performs RTL synthesis
    2. `abc` - Performs technology mapping
    3. `OpenSTA` - Performs static timing analysis on the resulting netlist to generate timing reports
   
   The flow starts with RTL Synthesis, so the RTL is fed to `yosys` with the design constraints, `yosys` translates the RTL into a logic circuit using generic components, this circuit can be optimized and then mapped into cells from the standard cell library using `abc`. `abc` has to be guided during the optimization, and this guidence comes in the form of abc scripts. OpenLANE comes with several abc scripts, we refer them as synthesis strategies. Different strategies can be used to synthesize for the either the least area or the best timing. To analyse this, synthesis exploration utility generates a report showing the effect on delays/timing/area etc. Also openlane has design exploration utility which generate reports with different metrics to select the best. 
    
2. **DFT Insertion** : After Synthesis comes the dft insertion, which is optional this step uses open-source project Fault to perform Scan Insertion, Automatic Test Pattern Generation (ATPG), Test Pattern Compaction, Fault Coverage and Fault Simultion.

3. **Floorplan and PDN**
    1. `init_fp` - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
    2. `ioplacer` - Places the macro input and output ports
    3. `pdn` - Generates the power distribution network
    4. `tapcell` - Inserts welltap and decap cells in the floorplan
    
   This is done by OpenROAD App for this, In this step the goal is to plan the silicon area and create a robust power distribution network (PDN) to power each of the individual components of the synthesized netlist. 
   
4. **Placement**
    1. `RePLace` - Performs global placement
    2. `Resizer` - Performs optional optimizations on the design
    3. `OpenDP` - Perfroms detailed placement to legalize the globally placed components
   
   Placement is the process of finding a suitable physical location for each cell in the block, it also optimize the design. Placement is performed in two stages : Global Placement and Detail Placement.  In Global Placement the tool determines the approximate location for each cell according to initial timing and congestion constraints, the placed cells donot fall on placement grid and might overlap each other. Detailed placement takes the global placement into consideration and moves the cells to legal locations on the placement grid and eliminate any overlapping of cells.
   
5. **CTS**
    1. `TritonCTS` - Synthesizes the clock distribution network (the clock tree)

   Clock Tree Synteshsis is used to create the effective clock distribution network that is used to deliver the clock to all sequential elements across the chip. The main goal is to create a network with minimal or balanced skew across the sequential blocks of the chip. Some of the popular Clock tree topologies are H-Tree, X-Tree, I-Tree. 
   
6. **Routing**
    1. `FastRoute` - Performs global routing to generate a guide file for the detailed router
    2. `CU-GR` - Another option for performing global routing.
    3. `TritonRoute` - Performs detailed routing
    4. `SPEF-Extractor` - Performs SPEF extraction
7. **GDSII Generation**
    1. `Magic` - Streams out the final GDSII layout file from the routed def
    2. `Klayout` - Streams out the final GDSII layout file from the routed def as a back-up
8. **Checks**
    1. `Magic` - Performs DRC Checks & Antenna Checks
    2. `Klayout` - Performs DRC Checks
    3. `Netgen` - Performs LVS Checks
    4. `CVC` - Performs Circuit Validity Checks

The Skywater 130nm PDK uses 6 metal layers to perform CTS, PDN generation, and interconnect routing.

OpenLane integrated several key open source tools over the execution stages:
- RTL Synthesis, Technology Mapping, and Formal Verification : yosys + abc
- Static Timing Analysis: OpenSTA
- Floor Planning: init_fp, ioPlacer, pdn and tapcell
- Placement: RePLace(Global), Resizer and OpenPhySyn (formerly), and OpenDP (Detailed)
- Clock Tree Synthesis: TritonCTS
- Fill Insertion: OpenDP/filler_placement
- Routing: FastRoute or CU-GR (Global) and TritonRoute(Detailed)
- SPEF Extraction: SPEF-Extractor (formerly), OpenRCX]
- GDSII Streaming out: Magic and Klayout
- DRC Checks: Magic and Klayout
- LVS check: Netgen
- Antenna Checks: Magic
- Circuit Validity Checker: CVC

### Day-1 Lab : Get familiar to open-source EDA tools

#### OpenLANE Directory structure

