# Advanced-Physical-Design-using-OpenLANE-Sky130
<p align="center">
  <img src="/Images/cover.png">
</p><br>

# Table of contents
- [Day-1- Inception of open source EDA OpenLANE and Sky130](#1-Inception-of-open-source-EDA-OpenLANE-and-Sky130)
    - [1.1 Introduction](#11-Introduction)
    - [1.2 Steps of Digital ASIC Flow](#12-Steps-of-Digital-ASIC-Flow)
    - [1.3 Getting Familiar With OpenLANE and Sky130](#13-Getting-Familiar-With-OpenLANE-and-Sky130)
    
# 1. Inception of open source EDA OpenLANE and Sky130
## 1.1 Introduction
### Chips versus Package
Chips are typically inside a package. Pins of the chips are connected to the package pins via wire bonds. <br>
<p align="center">
  <img src="/Images/pic1.png">
</p><br>
I/O pads are used to communicate with the chip. 

<br><p align="center">
  <img src="/Images/pic2.png">
</p><br>
Typically, components of a chip can be classified into two categories,

 - Foundary IPs
 - Macros 
<br><p align="center">
  <img src="/Images/pic3.png">
</p><br>

### Components of Open-Source Digital ASIC Design
<p align="center">
  <img src="/Images/pic4.png">
</p><br>
<p align="center">
  <img src="/Images/pic5.png">
</p><br>

### What is a PDK?
PDK stands for process Design Kit. PDK is the interface between the Foundary aand the Designers. It is basically a collection of files used to model a fabrication process for the EDA tools used to design an Integrated Circuit (IC) such as, 
 - Process Design Rules - DRC, LVS, PEX
 - Device Models
 - Digital Standard Cell Library
 - I/O Libraries
 - .
 - .
 - .
 
## 1.2 Steps of Digital ASIC Flow

### i. Synthesis
Converts RTL to Circuit out of components from the Standard Cell Library.
<br><p align="center">
  <img src="/Images/pic6.png">
</p><br>
<p align="center">
  <img src="/Images/pic7.png">
</p><br>

### ii. Floorplanning and Power Planning
Floorplanning is broadly classified into 

#### a. Chip Floorplanning

 <p align="center">
  <img src="/Images/pic8.png">
</p><br>

#### b. Macro Floorplanning

 <p align="center">
  <img src="/Images/pic9.png">
</p><br>

#### c. Power Planning

 Power Network is constructed. Typically, chip is powered by multiple VDD and VSS lines. Power lines use upper metal layers as they are comaritively thicker than lower metal lines, thereby offering lesser resistance.
 <p align="center">
  <img src="/Images/pic10.png">
</p><br>

### iii. Placement

 <p align="center">
  <img src="/Images/pic11.png">
</p><br>

### iv. Clock Tree Synthesis 

<p align="center">
  <img src="/Images/pic13.png">
</p><br>

### v. Routing
Routing is usually done in two steps

  - Global Routing : Generates routing guides
  - Detailed Routing : Uses the routing guides to implement the actual wiring.
<p align="center">
  <img src="/Images/pic12.png">
</p><br>
<p align="center">
  <img src="/Images/pic14.png">
</p><br>

### vi. Signoff
 In this step, Physical verifiction is performed, i.e., DRC and LVS. ALso, Timing Verification i.e., Static Timing Analysis (STA) is to verify the clock frequency.
 
## 1.3 Getting Familiar With OpenLANE and Sky130
 
### What is OpenLANE?
OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. It is a tool started for true open source tape-out experience and comes with APACHE version 2.0 . The goal of OpenLANE is to produce clean GDSII without any human intervention. OpenLANE is tuned for Skywater 130nm open-source PDK and can be used to produce hard macros and chips.
<p align="center">
  <img src="/Images/pic15.png">
</p><br>

## Invoking Openlane
To invoke openlane, type the following 
```
cd Desktop/vsdflow/work/tools/openlane_working_dir/OpenLane
make mount
```

Then, type the following command
```
./flow.tcl -interactive
```

Then type 
```
package require openlane 0.9
```
