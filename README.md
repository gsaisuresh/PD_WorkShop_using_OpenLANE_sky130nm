# PD_WorkShop_using_OpenLANE_sky130nm
This project is done as part of VLSI Physical Design Work-Shop orgaised by VLSI System Design. In this project a complete RTL to GDSII flow for picorv32a SoC is executed with Openlane using Skywater130nm PDK. OpenLane is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, SPEF-Extractor, CU-GR, Klayout and a number of custom scripts for design exploration and optimization. The flow performs full ASIC implementation steps from RTL all the way down to GDSII.

## Table of Contents
1. [Day-1 Inception of Opensource EDA, OpenLANE and Sky130 PDK](#inception-of-opensource-eda)
   - [How to Talk to computers](#how-to-talk-to-computers)
     - [Introduction to QFN-48 Package, chip, pads, core, die and IPs](#introduction-to-QFN-48)
     - [Introduction to RISC-V](#intoduction-to-riscv)
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
