# Advanced-Physical-Design-using-OpenLANE-Sky130
<p align="center">
  <img src="/Images/cover.png">
</p><br>

# Table of contents
- [Day-1- Inception of open source EDA OpenLANE and Sky130](#1-Inception-of-open-source-EDA-OpenLANE-and-Sky130)
    - [1.1 Introduction](#11-Introduction)
    - [1.2 Steps of Digital ASIC Flow](#12-Steps-of-Digital-ASIC-Flow)
    - [1.3 Getting Familiar With OpenLANE and Sky130](#13-Getting-Familiar-With-OpenLANE-and-Sky130)
- [Day-2- Good Floorplan vs Bad Floorplan and Introduction to Library Cells](#2-Good-Floorplan-vs-Bad-Floorplan-and-Introduction-to-Library-Cells)
   
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
To prep the design for openlane, type the following command
```
prep -design picorv32a
```
<p align="center">
  <img src="/Images/pic16.png">
</p><br>

Open a new terminal and type the commands
```
cd Desktop/vsdflow/work/tools/openlane_working_dir/OpenLane/designs/picorv32a/runs
ls -ltr
```
<p align="center">
  <img src="/Images/pic17.png">
</p><br>

Once we run `prep` command, a new `RUN_2022.08.14_11.31.00` folder is created. 
<p align="center">
  <img src="/Images/pic18.png">
</p><br>
This config.tcl shows all the default parameters considered by the run. Whereas, cmds.log keeps a track of all the commands we have typed. The folder reports contains reports on synthesis, floorplanning, ......, etc. All these folders are still empty as we have not run any of the commands.

The next step is to run synthesis. So, type the following command in openlane.
```
run_synthesis
```
<p align="center">
  <img src="/Images/pic20.png">
</p><br>
On running synthesis, the reports are created in the location `Desktop/vsdflow/work/tools/openlane_working_dir/OpenLane/designs/picorv32a/runs/RUN_2022.08.14_11.31.00/reports/synthesis`
<p align="center">
  <img src="/Images/pic19.png">
</p><br>
The statistics of the design are as follows

```
24. Printing statistics.

=== picorv32 ===

   Number of wires:               9379
   Number of wire bits:           9761
   Number of public wires:        1512
   Number of public wire bits:    1894
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:               9659
     sky130_fd_sc_hd__a2111o_2       1
     sky130_fd_sc_hd__a211o_2       68
     sky130_fd_sc_hd__a211oi_2      11
     sky130_fd_sc_hd__a21bo_2       17
     sky130_fd_sc_hd__a21boi_2       6
     sky130_fd_sc_hd__a21o_2       263
     sky130_fd_sc_hd__a21oi_2      117
     sky130_fd_sc_hd__a221o_2      119
     sky130_fd_sc_hd__a22o_2       155
     sky130_fd_sc_hd__a22oi_2        2
     sky130_fd_sc_hd__a2bb2o_2      22
     sky130_fd_sc_hd__a311o_2       35
     sky130_fd_sc_hd__a311oi_2       1
     sky130_fd_sc_hd__a31o_2        80
     sky130_fd_sc_hd__a31oi_2        7
     sky130_fd_sc_hd__a32o_2       108
     sky130_fd_sc_hd__a41o_2         3
     sky130_fd_sc_hd__and2_2       218
     sky130_fd_sc_hd__and2b_2       29
     sky130_fd_sc_hd__and3_2       110
     sky130_fd_sc_hd__and3b_2       41
     sky130_fd_sc_hd__and4_2        44
     sky130_fd_sc_hd__and4b_2        1
     sky130_fd_sc_hd__buf_1       2613
     sky130_fd_sc_hd__buf_2         18
     sky130_fd_sc_hd__conb_1       106
     sky130_fd_sc_hd__dfxtp_2     1596
     sky130_fd_sc_hd__inv_2         69
     sky130_fd_sc_hd__mux2_1         1
     sky130_fd_sc_hd__mux2_2      1629
     sky130_fd_sc_hd__mux4_2       440
     sky130_fd_sc_hd__nand2_2      229
     sky130_fd_sc_hd__nand2b_2       1
     sky130_fd_sc_hd__nand3_2       13
     sky130_fd_sc_hd__nand3b_2       4
     sky130_fd_sc_hd__nand4_2        2
     sky130_fd_sc_hd__nor2_2       226
     sky130_fd_sc_hd__nor2b_2        1
     sky130_fd_sc_hd__nor3_2        13
     sky130_fd_sc_hd__nor3b_2        3
     sky130_fd_sc_hd__nor4_2         4
     sky130_fd_sc_hd__nor4b_2        2
     sky130_fd_sc_hd__o2111a_2       4
     sky130_fd_sc_hd__o2111ai_2      4
     sky130_fd_sc_hd__o211a_2       94
     sky130_fd_sc_hd__o211ai_2       5
     sky130_fd_sc_hd__o21a_2       203
     sky130_fd_sc_hd__o21ai_2      118
     sky130_fd_sc_hd__o21ba_2        9
     sky130_fd_sc_hd__o21bai_2       4
     sky130_fd_sc_hd__o221a_2       67
     sky130_fd_sc_hd__o22a_2        45
     sky130_fd_sc_hd__o2bb2a_2       6
     sky130_fd_sc_hd__o311a_2        5
     sky130_fd_sc_hd__o31a_2        15
     sky130_fd_sc_hd__o31ai_2        8
     sky130_fd_sc_hd__o32a_2         3
     sky130_fd_sc_hd__o32ai_2        1
     sky130_fd_sc_hd__o41a_2         2
     sky130_fd_sc_hd__or2_2        385
     sky130_fd_sc_hd__or2b_2        23
     sky130_fd_sc_hd__or3_2         49
     sky130_fd_sc_hd__or3b_2        19
     sky130_fd_sc_hd__or4_2         33
     sky130_fd_sc_hd__or4b_2         5
     sky130_fd_sc_hd__xnor2_2       86
     sky130_fd_sc_hd__xor2_2        38

   Chip area for module '\picorv32': 100880.502400
```

Whereas, the results of the synthesis, i.e., the synthesized netlist can be found in the results folder under the name `picorv32.v`.
<p align="center">
  <img src="/Images/pic21.png">
</p><br>

# 2. Good Floorplan vs Bad Floorplan and Introduction to Library Cells 
