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
   - [Day-1 Lab : Get familiar to open-source EDA tools](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#day-1-lab--get-familiar-to-open-source-eda-tools)
     - [OpenLANE Directory structure](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#openlane-directory-structure)
     - [Design Preparation Step](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#design-preparation-step)
     - [Review files after design prep and run synthesis](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#review-files-after-design-prep-run-synthesis)
     - [Steps to characterize synthesis results](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#steps-to-characterize-synthesis-results)

2. [Day 2 - Good floorplan vs bad floorplan and introduction to library cells](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#day-2---good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
   - [Chip Floor planning considerations](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#chip-floor-planning-considerations)
     - [Utilization factor and aspect ratio](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#utilization-factor-and-aspect-ratio)
     - [Concept of pre-placed cells](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#concept-of-pre-placed-cells)
     - [De-coupling capacitors](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#de-coupling-capacitors)
     - [Power planning](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#power-planning)
     - [Pin placement and logical cell placement blockage](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#pin-placement-and-logical-cell-placement-blockage)
    - [Day-2 Lab : Floorplanning](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#day-2-lab--floorplanning)
      - [Steps to run floorplan using OpenLANE](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#steps-to-run-floorplan-using-openlane)
      - [Review floorplan files and steps to view floorplan](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#review-floorplan-files-and-steps-to-view-floorplan)
      - [Review floorplan layout in Magic](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#review-floorplan-layout-in-magic)
     - [Library Binding and Placement](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#library-binding-and-placement)
       - [Netlist binding and initial place design](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#netlist-binding-and-initial-place-design)
       - [Optimize placement using estimated wire-length and capacitance](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#optimize-placement-using-estimated-wire-length-and-capacitance)
       - [Day-2 Lab : Placement - Congestion aware placement using RePlAce](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#congestion-aware-placement-using-replace)
      - [Cell design and characterization flows](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#cell-design-and-characterization-flows)
        - [Cell Design Flow](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#cell-design-flow) 
        - [Typical characterization flow](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#typical-characterization-flow)
      - [General timing characterization parameters](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#general-timing-characterization-parameters)
        - [Timing threshold definitions](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#timing-threshold-definitions)
        - [Propagation delay and transition time](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#propagation-delay-and-transition-time) 
     

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
We will be working in `openlane_working_dir` inside the working directory there are two directories named as openlane and pdks, we will be working in openlane directory, pdks directory has all the information related to pdk the pdk we use for this workshop is skywater_130nm pdk. 

![1](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/c663631f-ff3d-4dd2-9498-4be46ce5cfa7)

Inside the pdks directory there are 3 directories skywater-pdk, open_pdks, sky130A. skywater-pdk contains all the pdk related files such as timing libraries, .lef files(cell lef and tech lef), etc. open_pdks has set of scripts and files that convert the foundry level pdks to be compatible with opensource EDA tools like magic, netgen. Sky130A is pdk variant which is compatible with opensouce environment. 

![2  ](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/dd9d4691-3139-464a-8424-ba4ef68b1173)

Inside the Sky130A directory there are two directories libs.tech and libs.ref. libs.ref contains all the process specific files such as timing, cell lib etc. libs.tech are those files which are specific to tool.

![3](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/6fa89602-eb15-45fb-bb8e-f504cfe3cdbe)

we would be working on pdk variant `sky130_fd_sc_hd` which means sky130 refers to process name which is sky130nm, fd refers to the foundry name, sc refers to standard cell library files, hd refers to variant of pdk hd stands for high density. 

![4](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/42186708-1326-4999-a2cc-be72bfbaceae)

Now lets see whats inside `sky130_fd_sc_hd` directory.

![5](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/30db3a09-aa90-436e-8dd6-b388ce3f58ff)

We can observe all the technology files such as techlef files which contains the layer information, lib files has timing information for many process corners.  

#### Design Preparation Step

The first lab was to synthesise the RTL code of a picorv32a in the interactive mode using OpenLANE. 
OpenLANE can be invoked by using `docker` command followed by opening an interactive session. flow.tcl is a script that specifies details for openLANE flow. `./flow.cl` which is script tells how flow has to go `-interactive` option tells tools to run step-by-step process.

![1](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/495388b7-362a-42bc-96fd-04f5549c8581)

import the required pacage of openlane using command `package require openlane 0.9`

![1 4](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/ebf16a9a-25b5-41d7-86c9-bc8eddc2ce21)

All the designs that are being run by openLANE are being extracted from the designs directory. 

![2](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/169fa5a9-b4cc-4949-803d-8508e8fb1739)

OpenLANE has close to 30-40 designs, we will be doing for picorv32a 

![3 1](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/e0025ed1-ef37-47a3-819e-8c11a998b75b)
![4](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/59ed49d1-d013-4164-9760-01d2eaf79eee)
![5](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/d3912ccd-dcf4-4efb-b90a-18a65e00053b)

We prepare our design file "picorv32a" with the command `prep -design picorv32a` this merges the tech LEF and cell LEF files and buids a complete directory structure for our run .

![8  prep](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/16a287d2-1c59-44a9-9bba-0461aa55ec1e)

#### Review files after design prep run synthesis

We can observe runs directory is created within the picorv32a folder, which has a directory on the name of cuurent day's date which contains the folder structures required by openLANE. 

![1](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/b9efb298-b308-4278-90bc-89aa449c3596)

![2](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/67887626-8908-45ad-bf2d-9c96e288e7b5)

There is a results folder for each of the stage.

![4](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/8d7ec9f2-5b14-4a2b-9744-2ef87a6904eb)

we run the synthesis of picorv32a design using command `run_synthesis` this will run yosys syntheis and abc. 
OpenLane invokes the following

- `Yosys` - RTL Synthesis and maps to yosys generic cells
- `abc` - Technology mapping with the Skywater130 PDK. Here `sky130_fd_sc_hd` Skywater Foundry produced High density standard cells are used.
- `OpenSTA` - This does the Static Timing Analysis on the netlist generated after synthesis and generated the timing reports 

![8](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/7b012395-5af6-4d90-92c4-017c6cc95fdf)

#### Steps to characterize synthesis results

Calcuation of Flop Ratio:
```
Flop ratio = Number of D Flip flops 
             ______________________
             Total Number of cells
```

![1](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/c291849e-e812-4e2f-b247-79fdd84a3176)

```
Number of cells :  14876 
Number of dfxtp_2 cells : 1613
Flop Ratio : 0.1084
```
Now we check results folder in synthesis step, it should have synthesized netlist.

![2](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/b2c37865-65e9-41dc-b2d4-0278e30dc17b)

we can observe picorv32a.synthesis.v synthesized netlist is created.

![3](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/f34ecaff-c924-4667-9fd0-b889d3b8a427)

The synthesis statistics report can be accessed within the reports directory. The synthesis timing reports are as follows : 

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/0cb00c5e-7f49-47a3-8ea8-c89deddce410)

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/c1c0e76c-008d-4e00-85a6-a8fb6727309d)

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/2ce0b0f8-9f7c-463c-ab57-94f31218a6bd)

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/1f7bdfd3-057c-4d61-bed6-5528a138a7e8)

## Day 2 - Good floorplan vs bad floorplan and introduction to library cells

### Chip Floor planning considerations

#### Utilization factor and aspect ratio

In the physical design flow the first step was to define height and width of core and die which we do in Floor Planning stage. Floor Planning is the process of determing the macro placement, power grid generation and I/O placement. Floor Planning involves Defining the size of chip or block, preplacing macros, IO pads and defining power grid. Two parameters are of importance when it comes to floorplanning are Utilization Factor and Aspect Ratio. They are defines as follows :

- `Utilization factor : (area occupied by netlist) / (total area of core)`
- `Aspect Ratio : (Height of core) / (Width of core)`

A Utilisation Factor of 1 signifies 100% utilisation leaving no place for routing and extra logic. However, In real scenario, the Utilisation Factor will usually be 0.5-0.6 ie., 50 to 60% of the area is used for macros, standard cells and rest is used for routing, extralogic. Likewise, an Aspect ratio of 1 signifies that the chip is square shaped. Any value other than 1 signifies rectanglular chip.

#### Concept of pre-placed cells

Once the Utilisation Factor and Aspect Ratio has been decided, the locations of pre-placed cells need to be defined. Pre-placed cells are IPs which are a piece of complex logic that is reused in design such as Memory, Clock Gating Cell, Comparator, Mux etc. These IP's/Blocks have user defined locations, and hence are placed in chip before automated placement and routing and are called as pre-placed cells. So these cells are placed in such a fashion that the automated PnR tool will not touch the locations of these particular cells. Once their locations are fixed on a floorplan they are fixed and not moved by PnR tool.

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/cc06e755-7a8f-44a9-bf14-6b91099f548c)

#### De-coupling capacitors

De-coupling capacitors are huge capacitors which are completely filled with charge, equivalent voltage acorss decoupling capaciotr is similar to that of voltage across power supply. Pre-placed cells must then be surrounded with decoupling capacitors (decaps). The resistances and capacitances associated with long wire lengths can cause the power supply voltage to drop significantly before reaching the logic circuits. This can lead to the signal value entering into the undefined region, outside the noise margin range. Decaps are huge capacitors charged to power supply voltage and placed close the logic circuit. So role of decoupling capacitor is to decouple the logic circuit from power supply, and whenever switching activity happens decoupling capacitor will send current to logic circuit. In this way decoupling capacitors avoid noise and crosstalk issues and enable the local communication.

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/c0d7d6ad-43dc-444a-963e-52c9a22d88db)

####  Power planning

If we have a single power supply driving all the cells in circuit this can lead to ground bounce and voltage droop issues, and we cannot have decoupling capacitors for each and every block in circuit since it demands more area and area requirements of chip may fail. So, separate horizontal and vertical Vdd and Vss wires have been created forming like a mesh or grid. This creation of a power mesh or power grid like structure is known as power planning.  Now, each cell can tap the required supply from the nearest power net. In this way by creation of an effective power mesh which consists of rails, stripes and power rings the power requirements of all standard cells, macros and other blocks are fulfilled. Power planning is also called as pre-routes because in chip power nets are routed first.

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/ae697305-019f-4bf6-8844-09d4e2931f02)

#### Pin placement and logical cell placement blockage

The connectivity information between the gates is coded using VHDL/Verilog language and is called as netlist. Netlist basically refers to the connectivity of different gates.  The place between the core and die is utilised for placing IO pins. The connectivity information coded in either VHDL or Verilog is used to determine the position of I/O pads of various pins. Then, cell placement blockage is performed so as to differentiate that area from that of the pin area. 

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/2adb902d-7e68-4021-9f55-a2729888c5a2)
![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/c38c4240-9251-417e-9a46-584221f5b177)

### Day-2 Lab : Floorplanning

#### Steps to run floorplan using OpenLANE

Floorplan envrionment variables or switches:
- `FP_CORE_UTIL` - floorplan core utilisation
- `FP_ASPECT_RATIO` - floorplan aspect ratio
- `FP_CORE_MARGIN` - Core to die margin area
- `FP_IO_MODE` - defines pin configurations (1 = equidistant/0 = not equidistant)
- `FP_CORE_VMETAL` - vertical metal layer
- `FP_CORE_HMETAL` - horizontal metal layer

Note: Usually, vertical metal layer and horizontal metal layer values will be 1 more than that specified in the files

#### Review floorplan files and steps to view floorplan

OpenLANE Priority order of files:

1. ```sky130A_sky130_fd_sc_hd_config.tcl```
2. ```conifg.tcl```
3. ```floorplan.tcl``` - System default envrionment variables

floorplan.tcl file is as follows : 

![3  floorplan tcl](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/307159f0-bb93-4330-bc7e-651e1d58dd4d)

config.tcl file is as follows:

![4](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/26215fe8-ac82-4673-b24c-c723a553a885)

sky130A_sky130_fd_sc_hd_config.tcl file is as follows:

![5](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/fba4ab87-c199-449a-81a0-cae98bec23c4)

To run the picorv32a floorplan in openLANE the command is : `run_floorplan`. 

![6  run floorplan](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/e6cf6009-64c2-41a8-bdba-96f0a79c1e77)

Post the floorplan run, a .def file will have been created within the results/floorplan directory. We may review floorplan files by checking the floorplan.tcl. The system defaults will have been overriden by switches set in conifg.tcl and further overriden by switches set in sky130A_sky130_fd_sc_hd_config.tcl

After Succesfull Floorplan The directory with current date is created 

![2](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/67f24a01-b1b5-4e92-b804-1b66001b804a)

The created floorplan def is as follows from this we can calculate the die area as well 

![4](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/f41475bd-b74e-4c68-9f84-5abe931d1793)

#### Review floorplan layout in Magic

To view the floorplan, Magic is invoked after moving to the results/floorplan directory:

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/8b778914-1ce1-4552-9861-d287bdf605f7)

The magic opens the floorplan which is as follows :

![5](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/69626e70-f8c2-4227-a225-dc70e67dcf20)

One can zoom into Magic layout by selecting an area with left and right mouse click followed by pressing "z" key

![6](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/8f6103fa-7328-4d03-a0f6-8e5d3ea257d1)

Component of selection can be quiered and identified using the what command in tkcon window, we can see details such as on which metal layer it is laying on.

![7](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/770a18f5-98cc-4265-b48a-f8ae4cff5fee)
![8](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/97c9e78f-fea0-44a8-9468-69a2b13d874c)

We can view the decap and tap cells by further zooming the layout.

![9](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/0d151b71-d3c1-4864-9c5a-7a9d9cc88ea8)
![10](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/fca8170c-a484-4462-8bda-33badbcede1f)

We can find the details of standard cells at the bottom left most corner of layout, by selecting the component and clicking on S button we can see which component it is.

![11](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/176522ff-2eea-4e69-b3e4-a43e2a55e54b)
![12](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/61279a46-dc92-4b1a-a620-2c542a1b0aa2)
![12 1](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/5923eb0b-00ae-41c2-ab7d-d22c43139e62)

### Library Binding and Placement

#### Netlist binding and initial place design

Library consists of cells with different shapes, sizes, physical information such as width and height of cells, delay information of cells. We need to Bind the netlist with the physical cells i.e., library cells. The timing information of cells is available in .lib files and physical information of cells is available in .lef files. The next step is placement. Once we initial the design, the logic cells in netlist in its physical dimisoins is placed on the floorplan. Next we go for initial placement.

#### Optimize placement using estimated wire-length and capacitance

This is the stage where we estimate wire length and capacitance and based on that insert repeaters. Repeaters are basically buffers that will recondition our original signal, make a new signal which replicates the original signal and send it again. In this way the signal integrity is maintained. 

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/58056f0c-5660-4eb0-b853-f6cf45006550)
![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/da7d0507-916e-496f-8de4-7329b00e206d)
![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/038fac54-17b5-4f45-9e27-1fa1578dddf7)

#### Congestion aware placement using RePlAce

The command to run placement in openLANE flow is `run_placement`

![1](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/7f5c408a-7001-4c3b-a226-6dd36ae92a2a)

The objective of placement is the convergence of overflow value. If overflow value progressively reduces during the placement run it implies that the design will converge and placement will be successful.
Post placement, the design can be viewed on magic within results/placement directory:

To view the placement, Magic is invoked after moving to the results/placements directory:

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/0d4fdc46-f9fe-41cb-990b-ec63ddce02ca)

![3](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/9b4a5b40-f2c2-4ca7-bb39-afe10b2cbb12)
![4 1](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/84d2d47a-37f0-4509-8acc-92e686b5184f)

In OpenLANE flow Power distribution network generation is not a part of the floorplan step. Floorplan does not generate PDN. It is created after post CTS. The steps are - floorplan, placement, CTS and then PDN.

### Cell design and characterization flows

#### Cell Design Flow 

Standard cell design flow involves the following:

- **Inputs**: PDKs, DRC & LVS rules, SPICE models, libraries, user-defined specifications.
- **Design steps**: Circuit design, Layout design (Art of layout - Euler's path and stick diagram), Extraction of parasitics, Characterization (timing, noise, power).
- **Outputs**: CDL (circuit description language), LEF, GDSII, extracted SPICE netlist (.cir), timing, noise and power .lib files

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/34a7afb2-8e67-45de-9665-ccbcc5209073)

#### Typical characterization flow

A typical standard cell characterization flow includes the following steps:

1. Read in the models(model file) and tech files needed for layout
2. Read the extracted spice netlist
3. Define/Recognize the behaviour of the cell
4. Read the subcircuits
5. Attach power sources
6. Apply stimulus to characterization setup
7. Provide necessary output capacitance loads
8. Provide necessary simulation commands
9. Feed in all these inputs from step 1 to 8 in form of a configuration file to the characterization software called as GUNA which will generate Timing, Noise and Power models as output

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/966b0231-8189-46b4-9fe9-5a427a2ad975)

### General timing characterization parameters

#### Timing threshold definitions

Timing Threshold defintions | Value
------------ | -------------
slew_low_rise_thr  | 20% value
slew_high_rise_thr |  80% value
slew_low_fall_thr | 20% value
slew_high_fall_thr | 80% value
in_rise_thr | 50% value
in_fall_thr | 50% value
out_rise_thr | 50% value
out_fall_thr | 50% value

#### Propagation delay and transition time

**Propagation Delay** : the time difference between when the transitional input reaches 50% of its final value and when the output falls 50% of its final value. Poor choice of threshold values lead to negative delay values. 

```
Propagation delay = time(out_fall_thr) - time(in_rise_thr)
```

![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/5befa316-35cc-427f-95f8-889b137f829f)
![image](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/assets/135144937/1d254dc8-c912-40db-88ca-8e9effcbc451)

**transition time** : 
```
Fall transition time: time(slew_high_fall_thr) - time(slew_low_fall_thr)
Rise transition time: time(slew_high_rise_thr) - time(slew_low_rise_thr)
```



