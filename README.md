# PD_WorkShop_using_OpenLANE_sky130nm
This project is done as part of VLSI Physical Design Work-Shop orgaised by VLSI System Design. In this project a complete RTL to GDSII flow for picorv32a SoC is executed with Openlane using Skywater130nm PDK. OpenLane is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, SPEF-Extractor, CU-GR, Klayout and a number of custom scripts for design exploration and optimization. The flow performs full ASIC implementation steps from RTL all the way down to GDSII.

## Table of Contents
1. [Day-1 Inception of Opensource EDA, OpenLANE and Sky130 PDK](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#day-1-inception-of-opensource-eda-openlane-and-sky130-pdk)
   - [How to Talk to computers](#how-to-talk-to-computers)
     - [Introduction to QFN48 Package](https://github.com/gsaisuresh/PD_WorkShop_using_OpenLANE_sky130nm/blob/main/README.md#introduction-to-qfn-48-package-chip-pads-core-die-and-ips)
     - [Introduction to RISCV ISA](#intoduction-to-riscv-isa)
     - [From Software Applications to Hardware](#from-software-to-hardware) 
   - [SOC Design & OpenLANE](#soc-design--openlane)
     - [Components of opensource digital ASIC design](#components-of-opensource-digital-asic-design)
     - [Simplified RTL2GDS Flow](#simplified-rtl2gds-flow)
     - [OpenLANE ASIC Flow](#openlane-asic-flow)
   - [Opensource EDA tools](#opensource-eda-tools)
     - [OpenLANE design stages](#openlane-design-stages)
     - [OpenLANE Files](#openlane-files)
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


