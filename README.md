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
    - [2.1 Chip Floorplanning Considerations](#21-Chip-Floorplanning-Considerations)
   
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
## 2.1 Chip Floorplanning Considerations
### Utilization Factor and Aspect Ratio
<p align="center">
  <img src="/Images/pic22.png">
</p><br>
<p align="center">
  <img src="/Images/pic23.png">
</p><br>
<p align="center">
  <img src="/Images/pic24.png">
</p><br>
<p align="center">
  <img src="/Images/pic25.png">
</p><br>
Typically, chip utilization is around 50% to 70%.

### Preplaced Cells
Preplaced cells, or MACRO’s, are important to enable hierarchical PnR flow. Preplaced cells enable VLSI engineers to granularize a larger design. In floorplanning we define locations and blockages for preplaced cells. Blockages are needed to ensure no standard cells are mapped where the placeplaced cells are located.
<p align="center">
  <img src="/Images/pic26.png">
</p><br>
Here, block 1 and 2 are individually floorplanned and are kept as a blackbox. So, when we need to use the same module multiple times in our design, we can simply place them directly without going through the overhead of floorplanning them individaully. 

<p align="center">
  <img src="/Images/pic27.png">
</p><br>

### Decoupling Capacitor
Decoupling capacitors are placed local to preplaced cells during Floorplanning. Voltage drops associated with interconnect wires can heavily affect our noise margin or put it into an indeterminate state. Decoupling capacitor is a big capacitor located next to the macros to fix this problem. The capacitor will charge up to the power supply voltage over time and it will work as a charge reservoir when a transition is needed by the circuit instead of the charge coming from the power supply. Therefore it “decouples” the circuit from the main supply. The capacitor acts like the power supply.
<p align="center">
  <img src="/Images/pic28.png">
</p><br>

### Power Planning
Power planning during the Floorplanning phase is essential to lower noise in digital circuits attributed to voltage droop and ground bounce. Coupling capacitance is formed between interconnect wires and the substrate which needs to be charged or discharged to represent either logic 1 or logic 0. When a transition occurs on a net, charge associated with coupling capacitors may be dumped to ground. If there are not enough ground taps charge will accumulate at the tap and the ground line will act like a large resistor, raising the ground voltage and lowering our noise margin. To bypass this problem a robust PDN with many power strap taps are needed to lower the resistance associated with the PDN.

### Pin Placement
Pin placement is an essential part of floorplanning to minimize buffering and improve power consumption and timing delays. The goal of pin placement is to use the connectivity information of the HDL netlist to determine where along the I/O ring a specific pin should be placed. In many cases, optimal pin placement will be accompanied with less buffering and therefore less power consumption. After pin placement is formed we need to place logical cell blockages along the I/O ring to discriminate between the core area and I/O area.

## Floorplanning with OpenLANE
The `README.md` file specifies the variables required for each stage. 
<p align="center">
  <img src="/Images/pic29.png">
</p><br>

```
# Variables information
This page describes user-configurable variables and their default values.
## Required variables

|Variable|Description|
|-|-|
| `DESIGN_NAME`   | The name of the top level module of the design        |
| `VERILOG_FILES` | The path of the design's verilog files, space-delimited. |
| `CLOCK_PERIOD`  | The clock period for the design in nanoseconds. |
| `CLOCK_NET` | The name of the net input to root clock buffer used in Clock Tree Synthesis. |
| `CLOCK_PORT`    | The name of the design's clock port used in Static Timing Analysis.   |

## Optional variables

These variables are optional that can be specified in the design configuration file.

### General
|Variable|Description|
|-|-|
| `PDK` | Specifies the process design kit (PDK). <br> (Default: `sky130A` )|
| `STD_CELL_LIBRARY` | Specifies the standard cell library to be used under the specified PDK. <br> (Default: `sky130_fd_sc_hd` )|
| `STD_CELL_LIBRARY_OPT` | Specifies the standard cell library to be used during resizer optimizations. <br> (Default: `$STD_CELL_LIBRARY` )|
| `PDK_ROOT` | Specifies the folder path of the PDK. It searches for a `config.tcl` in `$PDK_ROOT/$PDK/libs.tech/openlane/` directory and at least have one standard cell library config defined in `$PDK_ROOT/$PDK/libs.tech/openlane/$STD_CELL_LIBRARY`. |
| `DIODE_PADDING` | Diode cell padding; increases the width of diode cells during placement checks. <br> (Default: `2` microns -- 2 sites)|
| `MERGED_LEF` | Points to `merged.lef`, which is a merger of various LEF files, including the technology lef, cells lef, any custom lefs, and IO lefs. |
| `NO_SYNTH_CELL_LIST` | Specifies the file that contains the don't-use-cell-list to be excluded from the liberty file during synthesis. If it's not defined, this path is searched `$::env(PDK_ROOT)/$::env(PDK)/libs.tech/openlane/$::env(STD_CELL_LIBRARY)/no_synth.cells` and if it's not found, then the original liberty will be used as is. |
| `DRC_EXCLUDE_CELL_LIST` | Specifies the file that contains the don't-use-cell-list to be excluded from the liberty file during synthesis and timing optimizations. If it's not defined, this path is searched `$::env(PDK_ROOT)/$::env(PDK)/libs.tech/openlane/$::env(STD_CELL_LIBRARY)/drc_exclude.cells` and if it's not found, then the original liberty will be used as is. In other words, `DRC_EXCLUDE_CELL_LIST` contain the only excluded cell list in timing optimizations. |
| `EXTRA_LEFS` | Specifies LEF files of pre-hardened macros to be merged in the design currently getting hardened |
| `EXTRA_GDS_FILES` | Specifies GDS files of pre-hardened macros to be merged in the design currently getting hardened |

### Synthesis

|Variable|Description|
|-|-|
| `SYNTH_BIN` | The yosys binary used in the flow. <br> (Default: `yosys`) |
| `SYNTH_CAP_LOAD` | The capacitive load on the output ports in femtofarads. <br> (Default: `33.5` ff)|
| `SYNTH_MAX_FANOUT`  | The max load that the output ports can drive. <br> (Default: `10` cells) |
| `SYNTH_MAX_TRAN` | The max transition time (slew) from high to low or low to high on cell inputs in ns. Used in synthesis <br> (Default: Calculated at runtime as `10%` of the provided clock period, unless this exceeds a set DEFAULT_MAX_TRAN, in which case it will be used as is). |
| `SYNTH_CLOCK_UNCERTAINITY`  | Specifies a value for the clock uncertainity in the pre-CTS stages. <br> (Default: `0.25`) |
| `SYNTH_CLOCK_TRANSITION`  |  Specifies a value for the clock transition in the pre-CTS stages. <br> (Default: `0.15`) |
| `SYNTH_TIMING_DERATE`  | Specifies a derating factor to multiply the path delays with. It specifies the upper and lower ranges of timing. <br> (Default: `+5%/-5%`) |
| `SYNTH_STRATEGY` | Strategies for abc logic synthesis and technology mapping <br> Possible values are `DELAY/AREA 0-4/0-3`; the first part refers to the optimization target of the synthesis strategy (area vs. delay) and the second one is an index. <br> (Default: `AREA 0`)|
| `SYNTH_BUFFERING` | Enables abc cell buffering <br> Enabled = 1, Disabled = 0 <br> (Default: `1`)|
| `SYNTH_SIZING` | Enables abc cell sizing (instead of buffering) <br> Enabled = 1, Disabled = 0 <br> (Default: `0`)|
| `SYNTH_READ_BLACKBOX_LIB` | A flag that enable reading the full(untrimmed) liberty file as a blackbox for synthesis. Please note that this is not used in technology mapping. This should only be used when trying to preserve gate instances in the rtl of the design.  <br> Enabled = 1, Disabled = 0 <br> (Default: `0`)|
| `SYNTH_NO_FLAT` | A flag that disables flattening the hierarchy during synthesis, only flattening it after synthesis, mapping and optimizations. <br> Enabled = 1, Disabled = 0 <br> (Default: `0`)|
| `SYNTH_SHARE_RESOURCES` | A flag that enables yosys to reduce the number of cells by determining shareable resources and merging them. <br> Enabled = 1, Disabled = 0 <br> (Default: `1`)|
| `SYNTH_ADDER_TYPE` | Adder type to which the $add and $sub operators are mapped to. <br> Possible values are `YOSYS/FA/RCA/CSA`; where `YOSYS` refers to using Yosys internal adder definition, `FA` refers to full-adder structure, `RCA` refers to ripple carry adder structure, and `CSA` refers to carry select adder. <br> (Default: `YOSYS`)|
| `SYNTH_EXTRA_MAPPING_FILE` | Points to extra techmap file for yosys that runs right after yosys `synth` before generic techmap. <br> (Default: `""`)|
| `SYNTH_PARAMETERS` | Space-separated key value pairs to be `chparam`ed in Yosys. In the format `key1=value1 key2=value2` <br> Default: None.  |
| `CLOCK_BUFFER_FANOUT` | Fanout of clock tree buffers. <br> (Default: `16`) |
| `BASE_SDC_FILE` | Specifies the base sdc file to source before running Static Timing Analysis. <br> (Default: `$::env(OPENLANE_ROOT)/scripts/base.sdc`) |
| `VERILOG_INCLUDE_DIRS` | Specifies the verilog includes directories. <br> Optional. |
| `SYNTH_FLAT_TOP` | Specifies whether or not the top level should be flattened during elaboration. 1 = True, 0= False <br> Default: `0`. |
| `IO_PCT` | Specifies the percentage of the clock period used in the input/output delays. Ranges from 0 to 1.0. <br> (Default: `0.2`) |
| `VERILOG_FILES_BLACKBOX` | To point at the blackboxes (the hardened macros). Ideally, this should include all the other verilog files |

### Floorplanning

|Variable|Description|
|-|-|
| `FP_CORE_UTIL`  | The core utilization percentage. <br> (Default: `50` percent)|
| `FP_ASPECT_RATIO`  | The core's aspect ratio (height / width). <br> (Default: `1`)|
| `FP_SIZING`  | Whether to use relative sizing by making use of `FP_CORE_UTIL` or absolute one using `DIE_AREA`. <br> (Default: `"relative"` - accepts "absolute" as well)|
| `DIE_AREA`  | Specific die area to be used in floorplanning. Specified as a 4-corner rectangle "x0 y0 x1 y1". Units in um <br> (Default: unset)|
| `FP_IO_MODE`  | Decides the mode of the random IO placement option. 0=matching mode, 1=random equidistant mode <br> (Default: `1`)|
| `FP_WELLTAP_CELL`  | The name of the welltap cell during welltap insertion. |
| `FP_ENDCAP_CELL`  | The name of the endcap cell during endcap insertion. |
| `FP_PDN_VOFFSET`  | The offset of the vertical power stripes on the metal layer 4 in the power distribution network <br> (Default: `16.32`) |
| `FP_PDN_VPITCH`  | The pitch of the vertical power stripes on the metal layer 4 in the power distribution network <br> (Default: `153.6`) |
| `FP_PDN_HOFFSET`  | The offset of the horizontal power stripes on the metal layer 5 in the power distribution network <br> (Default: `16.65`) |
| `FP_PDN_HPITCH`  | The pitch of the horizontal power stripes on the metal layer 5 in the power distribution network <br> (Default: `153.18`) |
| `FP_PDN_AUTO_ADJUST` | Decides whether or not the flow should attempt to re-adjust the power grid, in order for it to fit inside the core area of the design, if needed. <br> 1=enabled, 0 =disabled (Default: `1`) |
| `FP_TAPCELL_DIST`  | The horizontal distance between two tapcell columns <br> (Default: `14`) |
| `FP_IO_VEXTEND`  |  Extends the vertical io pins outside of the die by the specified units<br> (Default: `-1` Disabled) |
| `FP_IO_HEXTEND`  |  Extends the horizontal io pins outside of the die by the specified units<br> (Default: `-1` Disabled) |
| `FP_IO_VLENGTH`  | The length of the vertical IOs in microns. <br> (Default: `4`) |
| `FP_IO_HLENGTH`  | The length of the horizontal IOs in microns. <br> (Default: `4`) |
| `FP_IO_VTHICKNESS_MULT`  | A multiplier for vertical pin thickness. Base thickness is the pins layer minwidth <br> (Default: `2`) |
| `FP_IO_HTHICKNESS_MULT`  | A multiplier for horizontal pin thickness. Base thickness is the pins layer minwidth <br> (Default: `2`) |
| `FP_IO_UNMATCHED_ERROR`  | Exit on unmatched pins in a provided `FP_PIN_ORDER_CFG` file. 0=Disable 1=Enable. <br> (Default: `1` Enabled) |
| `BOTTOM_MARGIN_MULT`     | The core margin, in multiples of site heights, from the bottom boundary. <br> (Default: `4`) |
| `TOP_MARGIN_MULT`        | The core margin, in multiples of site heights, from the top boundary. <br> (Default: `4`) |
| `LEFT_MARGIN_MULT`       | The core margin, in multiples of site widths, from the left boundary.  <br> (Default: `12`) |
| `RIGHT_MARGIN_MULT`      | The core margin, in multiples of site widths, from the right boundary.   <br> (Default: `12`) |
| `FP_PDN_CORE_RING` | Enables adding a core ring around the design. More details on the control variables in the pdk configurations documentation. 0=Disable 1=Enable. <br> (Default: `0`) |
| `FP_PDN_ENABLE_RAILS` | Enables the creation of rails in the power grid. 0=Disable 1=Enable. <br> (Default: `1`) |
| `FP_PDN_ENABLE_MACROS_GRID` | Enables the connection of macros to the top level power grid. 0=Disable 1=Enable. <br> (Default: `1`) |
| `FP_PDN_MACRO_HOOKS` | Specifies explicit power connections of internal macros to the top level power grid. Comma separated list of macro instance names, power domain vdd and ground net names, and macro vdd and ground pin names: `<instance_name> <vdd_net> <gnd_net> <vdd_pin> <gnd_pin>` |
| `FP_PDN_CHECK_NODES` | Enables checking for unconnected nodes in the power grid. 0=Disable 1=Enable. <br> (Default: `1`) |
| `FP_TAP_HORIZONTAL_HALO` | Specify the horizontal halo size around macros during tap insertion. The value provided is in microns. <br> Default: `10` |
| `FP_TAP_VERTICAL_HALO` | Specify the vertical halo size around macros during tap insertion. The value provided is in microns. <br> Default: set to the value of `FP_TAP_HORIZONTAL_HALO` |
| `FP_PDN_HORIZONTAL_HALO` | Sets the horizontal halo around the macros during power grid insertion. The value provided is in microns. <br> Default: `10` |
| `FP_PDN_VERTICAL_HALO` | Sets the vertical halo around the macros during power grid insertion. The value provided is in microns. <br> Default: set to the value of `FP_PDN_HORIZONTAL_HALO` |
| `DESIGN_IS_CORE` | Controls the layers used in the power grid. Depending on whether the design is the core of the chip or a macro inside the core. 1=Is a Core, 0=Is a Macro <br> (Default: `1`)|
| `FP_PIN_ORDER_CFG` | Points to the pin order configuration file to set the pins in specific directions (S, W, E, N). Check this [file][0] as an example. If not set, then the IO pins will be placed based on one of the other methods depending on the rest of the configurations. <br> (Default: NONE)|
| `FP_CONTEXT_DEF` | Points to the parent DEF file that includes this macro/design and uses this DEF file to determine the best locations for the pins. It must be used with `FP_CONTEXT_LEF`, otherwise it's considered non-existing. If not set, then the IO pins will be placed based on one of the other methods depending on the rest of the configurations. <br> (Default: NONE)|
| `FP_CONTEXT_LEF` | Points to the parent LEF file that includes this macro/design and uses this LEF file to determine the best locations for the pins. It must be used with `FP_CONTEXT_DEF`, otherwise it's considered non-existing. If not set, then the IO pins will be placed based on one of the other methods depending on the rest of the configurations. <br> (Default: NONE)|
| `FP_DEF_TEMPLATE` | Points to the DEF file to be used as a template when running `apply_def_template`. This will be used to exctract pin names, locations, shapes -excluding power and ground pins- as well as the die area and replicate all this information in the `CURRENT_DEF`. |
| `VDD_NETS` | Specifies the power nets/pins to be used when creating the power grid for the design. |
| `GND_NETS` | Specifies the ground nets/pins to be used when creating the power grid for the design. |
| `SYNTH_USE_PG_PINS_DEFINES` | Specifies the power guard used in the verilog source code to specify the power and ground pins. This is used to automatically extract `VDD_NETS` and `GND_NET` variables from the verilog, with the assumption that they will be order `inout vdd1, inout gnd1, inout vdd2, inout gnd2, ...`. |
| `FP_IO_MIN_DISTANCE`  | The minmimum distance between the IOs in microns. <br> (Default: `3`) |
| `FP_PDN_IRDROP` | **Removed: worthless** Enable calculation of power grid IR drop during PDN generation. <br> (Default: `1`)|

#### Deprecated I/O Layer variables
These variables worked initially, but they were too sky130 specific and will be removed. Currently, if you define them in your design, they'll be used, but it's recommended to update your configuration to use `FP_IO_HLAYER` and `FP_IO_VLAYER`, which are defined in the PDK.

|Variable|Description|
|-|-|
| `FP_IO_HMETAL`  | The metal layer on which to place the io pins horizontally (top and bottom of the die). <br>(Default: `4`)|
| `FP_IO_VMETAL`  | The metal layer on which to place the io pins vertically (sides of the die) <br> (Default: `3`)|


### Placement

| Variable      | Description                                                   |
|---------------|---------------------------------------------------------------|
| `PL_TARGET_DENSITY` | The desired placement density of cells. It reflects how spread the cells would be on the core area. 1 = closely dense. 0 = widely spread <br> (Default: `($::env(FP_CORE_UTIL) + 5.0) / 100.0`)|
| `PL_TIME_DRIVEN` | Specifies whether the placer should use time driven placement. 0 = false, 1 = true <br> (Default: `1`)|
| `PL_LIB` | Specifies the library for time driven placement <br> (Default: `LIB_TYPICAL`)|
| `PL_BASIC_PLACEMENT` | Specifies whether the placer should run basic placement or not (by running initial placement, increasing the minimum overflow to 0.9, and limiting the number of iterations to 20). 0 = false, 1 = true <br> (Default: `0`) |
| `PL_SKIP_INITIAL_PLACEMENT` | Specifies whether the placer should run initial placement or not. 0 = false, 1 = true <br> (Default: `0`) |
| `PL_RANDOM_GLB_PLACEMENT` | Specifies whether the placer should run random placement or not. This is useful if the design is tiny (less than 100 cells). 0 = false, 1 = true <br> (Default: `0`) |
| `PL_RANDOM_INITIAL_PLACEMENT` | Specifies whether the placer should run random placement or not followed by replace's initial placement. This is useful if the design is tiny (less than 100 cells). 0 = false, 1 = true <br> (Default: `0`) |
| `PL_ROUTABILITY_DRIVEN` | Specifies whether the placer should use routability driven placement. 0 = false, 1 = true <br> (Default: `1`) |
| `PL_RESIZER_DESIGN_OPTIMIZATIONS` | Specifies whether resizer design optimizations should be performed or not. 0 = false, 1 = true <br> (Default: `1`) |
| `PL_RESIZER_TIMING_OPTIMIZATIONS` | Specifies whether resizer timing optimizations should be performed or not. 0 = false, 1 = true <br> (Default: `1`) |
| `PL_RESIZER_MAX_WIRE_LENGTH` | Specifies the maximum wire length cap used by resizer to insert buffers. If set to 0, no buffers will be inserted. Value in microns. <br> (Default: `0`)|
| `PL_RESIZER_MAX_SLEW_MARGIN` | Specifies a margin for the slews in percentage. <br> (Default: `20`)|
| `PL_RESIZER_MAX_CAP_MARGIN` | Specifies a margin for the capacitances in percentage. <br> (Default: `20`)|
| `PL_RESIZER_HOLD_SLACK_MARGIN` | Specifies a time margin for the slack when fixing hold violations. Normally the resizer will stop when it reaches zero slack. This option allows you to overfix. <br> (Default: `0.1ns`.)|
| `PL_RESIZER_SETUP_SLACK_MARGIN` | Specifies a time margin for the slack when fixing setup violations. <br> (Default: `0.05ns`)|
| `PL_RESIZER_HOLD_MAX_BUFFER_PERCENT` | Specifies a max number of buffers to insert to fix hold violations. This number is calculated as a percentage of the number of instances in the design. <br> (Default: `50`)|
| `PL_RESIZER_SETUP_MAX_BUFFER_PERCENT` | Specifies a max number of buffers to insert to fix setup violations. This number is calculated as a percentage of the number of instances in the design. <br> (Default: `50`)|
| `PL_RESIZER_ALLOW_SETUP_VIOS` | Allows setup violations when fixing hold. <br> (Default: `0`)|
| `LIB_RESIZER_OPT` | Points to the lib file, corresponding to the typical corner, that is used during resizer optimizations. This is copy of `LIB_SYNTH_COMPLETE`. <br> Default: `$::env(synthesis_tmpfiles)/resizer_<library-name>.lib` |
| `DONT_USE_CELLS` | The list of cells to not use during resizer optimizations. <br> Default: the contents of `DRC_EXCLUDE_CELL_LIST`. |
| `PL_ESTIMATE_PARASITICS` | Specifies whether or not to run STA after global placement using OpenROAD's estimate_parasitics -placement and generates reports under `logs/placement`. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `PL_OPTIMIZE_MIRRORING` | Specifies whether or not to run an optimize_mirroring pass whenever detailed placement happens. This pass will mirror the cells whenever possible to optimize the design. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `PL_RESIZER_BUFFER_INPUT_PORTS` | Specifies whether or not to insert buffers on input ports whenever resizer optimizations are run. For this to be used, `PL_RESIZER_DESIGN_OPTIMIZATIONS` must be set to 1. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `PL_RESIZER_BUFFER_OUTPUT_PORTS` | Specifies whether or not to insert buffers on output ports whenever resizer optimizations are run. For this to be used, `PL_RESIZER_DESIGN_OPTIMIZATIONS` must be set to 1. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `PL_RESIZER_REPAIR_TIE_FANOUT` | Specifies whether or not to repair tie cells fanout whenever resizer optimizations are run. For this to be used, `PL_RESIZER_DESIGN_OPTIMIZATIONS` must be set to 1. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `PL_MAX_DISPLACEMENT_X` | Specifies how far an instance can be moved along the X-axis when finding a site where it can be placed during detailed placement. <br> (Default: `500`um) |
| `PL_MAX_DISPLACEMENT_Y` | Specifies how far an instance can be moved along the Y-axis when finding a site where it can be placed during detailed placement. <br> (Default: `100`um) |
| `PL_MACRO_HALO` | Macro placement halo. Format: `{Horizontal} {Vertical}` <br> (Default: `0 0`um). |
| `PL_MACRO_CHANNEL` | Channel widths between macros. Format: `{Horizontal} {Vertical}` <br> (Default: `0 0`um). |
| `MACRO_PLACEMENT_CFG` | Specifies the path a file specifying how openlane should place certain macros |
| `DONT_BUFFER_PORTS` | Semicolon;delimited list of nets from which to remove buffers after placement (but before resizing). <br> (Default: Empty) |

### CTS

|Variable|Description|
|-|-|
| `CTS_TARGET_SKEW` | The target clock skew in picoseconds. <br> (Default: `200`ps)|
| `CLOCK_TREE_SYNTH` | Enable clock tree synthesis. <br> (Default: `1`)|
| `RUN_SIMPLE_CTS` | Runs an alternative simple clock tree synthesis after synthesis instead of TritonCTS. 1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `FILL_INSERTION` | Enables fill cells insertion after cts (if enabled). 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `CTS_TOLERANCE` | An integer value that represents a tradeoff of QoR and runtime. Higher values will produce smaller runtime but worse QoR <br> (Default: `100`) |
| `CTS_SINK_CLUSTERING_SIZE` | Specifies the maximum number of sinks per cluster. <br> (Default: `25`) |
| `CTS_SINK_CLUSTERING_MAX_DIAMETER` | Specifies maximum diameter (in micron) of sink cluster. <br> (Default: `50`) |
| `CTS_REPORT_TIMING` | Specifies whether or not to run STA after clock tree synthesis using OpenROAD's estimate_parasitics -placement and generates reports under `logs/cts`. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `CTS_CLK_MAX_WIRE_LENGTH` | Specifies the maximum wire length on the clock net. Value in microns. <br> (Default: `0`) |
| `CTS_DISABLE_POST_PROCESSING` | Specifies whether or not to disable post cts processing for outlier sinks. <br> (Default: `0`) |
| `CTS_DISTANCE_BETWEEN_BUFFERS` | Specifies the distance (in microns) between buffers when creating the clock tree (Default: `0`) |
| `LIB_CTS` | The liberty file used for CTS. By default, this is the `LIB_SYNTH_COMPLETE` minus the cells with drc errors as specified by the drc exclude list. <br> (Default: `$::env(cts_tmpfiles)/cts.lib`) |

### Routing

> **Note:** All variables previously prefixed GLB_RT_ have had their prefix changed to GRT_.

|Variable|Description|
|-|-|
| `GLOBAL_ROUTER` | Specifies which global router to use. Values: `fastroute`. (`cugr` is deprecated and fastroute will be used instead.) <br> (Default: `fastroute`) |
| `DETAILED_ROUTER` | Specifies which detailed router to use. Values: `tritonroute`. (`drcu`/`tritonroute_or` are both deprecated and tritonroute will be used instead.) <br> (Default: `tritonroute`)|
| `ROUTING_CORES` | Specifies the number of threads to be used in TritonRoute. Can be overriden via environment variable. <br> (Default: `2`) |
| `RT_CLOCK_MIN_LAYER` | The name of lowest layer to be used in routing the clock net. <br> (Default: `RT_MIN_LAYER`)|
| `RT_CLOCK_MAX_LAYER` | The name of highest layer to be used in routing the clock net. <br> (Default: `RT_MAX_LAYER`)|
| `GLB_RESIZER_TIMING_OPTIMIZATIONS` | Specifies whether resizer timing optimizations should be performed after global routing or not. 0 = false, 1 = true <br> (Default: `1`)
| `GLB_RESIZER_MAX_WIRE_LENGTH` | Specifies the maximum wire length cap used by resizer to insert buffers. If set to 0, no buffers will be inserted. Value in microns. <br> (Default: `0`)|
| `GLB_RESIZER_MAX_SLEW_MARGIN` | Specifies a margin for the slews. <br> (Default: `10`)|
| `GLB_RESIZER_MAX_CAP_MARGIN` | Specifies a margin for the capacitances. <br> (Default: `10`)|
| `GLB_RESIZER_HOLD_SLACK_MARGIN` | Specifies a time margin for the slack when fixing hold violations. Normally the resizer will stop when it reaches zero slack. This option allows you to overfix. <br> (Default: `0.05ns`)|
| `GLB_RESIZER_SETUP_SLACK_MARGIN` | Specifies a time margin for the slack when fixing setup violations. <br> (Default: `0.025ns`)|
| `GLB_RESIZER_HOLD_MAX_BUFFER_PERCENT` | Specifies a max number of buffers to insert to fix hold violations. This number is calculated as a percentage of the number of instances in the design. <br> (Default: `50`)|
| `GLB_RESIZER_SETUP_MAX_BUFFER_PERCENT` | Specifies a max number of buffers to insert to fix setup violations. This number is calculated as a percentage of the number of instances in the design. <br> (Default: `50`)|
| `GLB_RESIZER_ALLOW_SETUP_VIOS` | Allows setup violations when fixing hold. <br> (Default: `0`)|
| `GLB_OPTIMIZE_MIRRORING` | Specifies whether or not to run an optimize_mirroring pass whenever detailed placement happens after Routing timing optimization. This pass will mirror the cells whenever possible to optimize the design. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `GRT_ALLOW_CONGESTION` | Allow congestion in the resulting guides. 0 = false, 1 = true <br> (Default: `0`) 
| `GRT_OVERFLOW_ITERS` | The maximum number of iterations waiting for the overflow to reach the desired value. <br> (Default: `50`) |
| `GRT_ANT_ITERS` | The maximum number of iterations for global router repair_antenna. This option is only available in `DIODE_INSERTION_STRATEGY` = `3`. <br> (Default: `3`) |
| `GRT_ESTIMATE_PARASITICS` | Specifies whether or not to run STA after global routing using OpenROAD's estimate_parasitics -global_routing and generates reports under `logs/routing`. 1 = Enabled, 0 = Disabled. <br> (Default: `1`) |
| `GRT_MAX_DIODE_INS_ITERS` | Controls the maximum number of iterations at which re-running Fastroute for diode insertion stops. Each iteration ARC detects the violations and FastRoute fixes them by inserting diodes, then producing the new DEF. The number of antenna violations is compared with the previous iteration and if they are equal or the number is greater the iterations stop and the DEF from the previous iteration is used in the rest of the flow. If the current antenna violations reach zero, the current def will be used and the iterations will not continue. This option is only available in DIODE_INSERTION_STRATEGY = `3`.  <br> (Default: `1`) |
| `GRT_OBS` | Specifies custom obstruction to be added prior to global routing. Comma separated list of layer and coordinates: `layer llx lly urx ury`, where `ll` and `ur` stand for "lower left" and "upper right" respectively.<br> (Example: `li1 0 100 1000 300, met5 0 0 1000 500`)  <br> (Default: unset) |
| `GRT_ADJUSTMENT` | Reduction in the routing capacity of the edges between the cells in the global routing graph. Values range from 0 to 1. <br> 1 = most reduction, 0 = least reduction  <br> (Default: `0.3`)|
| `GRT_MACRO_EXTENSION` | Sets the number of GCells added to the blockages boundaries from macros. A GCell is typically defined in terms of Mx routing tracks. The default GCell size is 15 M3 pitches. <br> (Default: `0`) |
| `DRT_MIN_LAYER` | An optional override to the lowest layer used in detailed routing. For example, in sky130, you may want global routing to avoid li1, but let detailed routing use li1 if it has to. <br> (Default: `RT_MIN_LAYER`)|
| `DRT_MAX_LAYER` | An optional override to the highest layer used in detailed routing. <br> (Default: `RT_MAX_LAYER`)|
| `DRT_OPT_ITERS` | Specifies the maximum number of optimization iterations during Detailed Routing in TritonRoute. <br> (Default: `64`) |
| `ROUTING_OPT_ITERS` |**Removed: Use DRT_OPT_ITERS**: Specifies the maximum number of optimization iterations during Detailed Routing in TritonRoute. <br> (Default: `64`) |
| `GLB_RT_MINLAYER` | **Removed: Use RT_MIN_LAYER**: The number of lowest layer to be used in routing. <br> (Default: `1`)|
| `GLB_RT_MAXLAYER` | **Removed: Use RT_MAX_LAYER**: The number of highest layer to be used in routing. <br> (Default: `6`)|
| `GLB_RT_CLOCK_MINLAYER` | **Removed: Use RT_CLOCK_MIN_LAYER**: The number of lowest layer to be used in routing the clock net. <br> (Default: `GLB_RT_MINLAYER`)|
| `GLB_RT_CLOCK_MAXLAYER` | **Removed: Use RT_CLOCK_MIN_LAYER**: The number of highest layer to be used in routing the clock net. <br> (Default: `GLB_RT_MAXLAYER`)|
| `GLB_RT_L{1/2/3/4/5/6}_ADJUSTMENT` | **Removed: See PDK variable `GLB_RT_LAYER_ADJUSTMENTS` instead**: Reduction in the routing capacity of the edges between the cells in the global routing graph but specific to a metal layer in sky130A. Values ranged from 0 to 1 |
| `GLB_RT_UNIDIRECTIONAL` | **Removed**: Allow unidirectional routing. 0 = false, 1 = true <br> (Default: `1`) |
| `GLB_RT_TILES` | **Removed**: The size of the GCELL used by Fastroute during global routing. <br> (Default: `15`) |

### RC Extraction

|Variable|Description|
|-|-|
| `SPEF_EXTRACTOR` | Specifies which spef extractor to use. Values: `openrcx` or (removed: `def2spef`). <br> (Default: `openrcx`) |
| `RCX_MERGE_VIA_WIRE_RES` | Specifies whether to merge the via resistance with the wire resistance or separate it from the wire resistance. 1 = Merge via resistance, 0 = Separate via resistance <br> (Default: `1`)|
| `SPEF_WIRE_MODEL` | Specifies the wire model used in SPEF extraction. Options are `L` or `Pi`  <br> (Default: `L`) |
| `SPEF_EDGE_CAP_FACTOR` | Specifies the edge capacitance factor used in SPEF extraction. Ranges from 0 to 1 <br> (Default: `1`) |

### Magic
|Variable|Description|
|-|-|
| `MAGIC_PAD` |  A flag to pad the views generated by magic (.mag, .lef, .gds) with one site. 1 = Enabled, 0 = Disabled <br> (Default: `0` )|
| `MAGIC_ZEROIZE_ORIGIN` | A flag to move the layout such that it's origin in the lef generated by magic is 0,0. 1 = Enabled, 0 = Disabled  <br> (Default: `1` )|
| `MAGIC_GENERATE_GDS` | A flag to generate gds view via magic. 1 = Enabled, 0 = Disabled  <br> (Default: `1` )|
| `MAGIC_GENERATE_LEF` | A flag to generate lef view via magic. 1 = Enabled, 0 = Disabled  <br> (Default: `1` )|
| `MAGIC_GENERATE_MAGLEF` | A flag to generate maglef view via magic. 1 = Enabled, 0 = Disabled  <br> (Default: `1` )|
| `MAGIC_WRITE_FULL_LEF` | A flag to specify whether or not the output LEF should include all shapes inside the macro or an abstracted view of the macro lef view via magic. 1 = Full View, 0 = Abstracted View  <br> (Default: `0` )|
| `MAGIC_DRC_USE_GDS` | A flag to choose whether to run the magic DRC checks on GDS or not. If not, then the checks will be done on the DEF/LEF. 1 = GDS, 0 = DEF/LEF  <br> (Default: `1` )|
| `MAGIC_EXT_USE_GDS` | A flag to choose whether to run the magic extractions on GDS or DEF/LEF. If GDS was used Device Level LVS will be run. Otherwise, blackbox LVS will be run. 1 = GDS, 0 = DEF/LEF  <br> (Default: `0` )|
| `MAGIC_INCLUDE_GDS_POINTERS` | A flag to choose whether to include GDS pointers in the generated mag files or not. 1 = Enabled, 0 = Disabled  <br> (Default: `0` )|
| `MAGIC_DISABLE_HIER_GDS` | A flag to disable cif hier and array during GDS-II writing.* 1=Enabled `<so this hier gds will be disabled>`, 0=Disabled `<so this hier gds will be enabled>`. <br> (Default: `1` )|

> * Tim Edwards's Explanation on disabling hier gds: The following is an explanation by Tim Edwards, provided in a slack thread, on how this affects the GDS writing process: "Magic can take a very long time writing out GDS while checking hierarchical interactions in a standard cell layout. If your design is all digital, I recommend using "gds *hier write disable" before "gds write" so that it does not try to resolve hierarchical interactions (since by definition, standard cells are designed to just sit next to each other without creating DRC issues).  That can actually make the difference between a 20 hour GDS write and a 2 minute GDS write.  For a standard cell design that takes up the majority of the user space, a > 24 hour write time (without disabling the hierarchy checks) would not surprise me."

### LVS

|Variable|Description|
|-|-|
| `LVS_INSERT_POWER_PINS` |  Enables power pins insertion before running lvs. 1 = Enabled, 0 = Disabled <br> (Default: `1` )|
| `LVS_CONNECT_BY_LABEL` | Enables connections by label in LVS by skipping `extract unique` in magic extractions. <br> Default: `0` |
| `YOSYS_REWRITE_VERILOG` | Enables yosys to rewrite the verilog before LVS producing a canonical verilog netlist with verbose wire declarations. 1 = Enabled, 0 = Disabled <br> (Default: `0` ) |

### Flow control

|Variable|Description|
|-|-|
| `TEST_MISMATCHES` | Test for mismatches between the OpenLane tool versions and the current environment. `all` tests all mismatches. `tools` tests all except the PDK. `pdk` only tests the PDK. `none` disables the check.<br> (Default: `all`) |
| `QUIT_ON_MISMATCHES` | Whether to halt the flow execution or not if mismatches are found. (Default: `1`) |
| `USE_GPIO_PADS` | Decides whether or not to use the gpio pads in routing by merging their LEF file set in `::env(USE_GPIO_ROUTING_LEF)` and blackboxing their verilog modules set in `::env(GPIO_PADS_VERILOG)`. 1=Enabled, 0=Disabled. <br> (Default: `0`) |
| `LEC_ENABLE` | Enables logic verification using yosys, for comparing each netlist at each stage of the flow with the previous netlist and verifying that they are logically equivalent. Warning: this will increase the runtime significantly. 1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `RUN_DRT` | Enables detailed routing. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `RUN_LVS` | Enables running LVS. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `PRIMARY_SIGNOFF_TOOL` | Determines whether `magic` or `klayout` is the primary signoff tool. <br> (Default: `magic`) |
| `RUN_MAGIC` | Enables running magic and GDSII streaming. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `RUN_MAGIC_DRC` | Enables running magic DRC on GDS-II produced by magic. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `RUN_KLAYOUT` | Enables running Klayout and GDSII streaming. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `RUN_KLAYOUT_DRC` | Enables running Klayout DRC on GDS-II produced by magic. 1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `KLAYOUT_DRC_KLAYOUT_GDS` | Enables running Klayout DRC on GDS-II produced by Klayout. 1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `RUN_KLAYOUT_XOR` | Enables running Klayout XOR on 2 GDS-IIs, the defaults are the one produced by magic vs the one produced by klayout. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `KLAYOUT_XOR_GDS` | If `RUN_KLAYOUT_XOR` is enabled, this will enable producing a GDS output from the XOR along with it's PNG export. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `KLAYOUT_XOR_XML` | If `RUN_KLAYOUT_XOR` is enabled, this will enable producing an XML output from the XOR. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `TAKE_LAYOUT_SCROT` | Enables running Klayout to take a PNG screenshot of the produced layout (currently configured to run on the results of each stage).1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `TAP_DECAP_INSERTION` | Enables tap and decap cells insertion after floorplanning (if enabled) .1 = Enabled, 0 = Disabled <br> (Default: `1`) |
| `DIODE_INSERTION_STRATEGY` | Specifies the insertion strategy of diodes to be used in the flow. 0 = No diode insertion, 1 = Spray diodes, 2 = insert fake diodes and replace them with real diodes if needed. 3= use FastRoute Antenna Avoidance flow, 4 = Use Sylvian's Custom Script for diode insertion on design pins and smartly inserting needed diodes inside the design, 5 = a mix of strategy 2 and 4. <br> (Default: `3`) |
| `WIDEN_SITE` | Specifies the new virtual width of the site to be used in all stages up to diode insertion, then switched back to the original site width. It can be either a factor or an absolute value controlled by `WIDEN_SITE_IS_FACTOR` <br> (Default: `1`) |
| `WIDEN_SITE_IS_FACTOR` | Specifies whether the given `WIDEN_SITE` should be treated as a factor or an absolute value. 0 = absolute, 1 = factor <br> (Default: `1`) |
| `USE_ARC_ANTENNA_CHECK` | Specifies whether to use the openroad ARC antenna checker or magic antenna checker. 0=magic antenna checker, 1=ARC OR antenna checker <br> (Default: `1`)
| `RUN_SPEF_EXTRACTION` | Specifies whether or not to run SPEF extraction on the routed DEF. 1=enabled 0=disabled <br> Default: `1` |
| `GENERATE_FINAL_SUMMARY_REPORT` | Specifies whether or not to generate a final summary report after the run is completed. Check command `generate_final_summary_report`. 1=enabled 0=disabled <br> Default: `1` |
| `RUN_CVC` | Runs CVC on the output spice, which is a Circuit Validity Checker. Voltage aware ERC checker for CDL netlists. Thus, it controls the command `run_lef_cvc`. 1=Enabled, 0=Disabled. <br> Default: `1` |
| `RUN_IRDROP_REPORT` | Creates an IR Drop report using OpenROAD PSM. 1=Enabled, 0=Disabled. <br> Default: `0` |
| `MAGIC_CONVERT_DRC_TO_RDB` | **Removed: Will always run** Specifies whether or not generate a Calibre RDB out of the magic.drc report. Result is saved in `<run_path>/results/magic/`. 1=enabled 0=disabled <br> Default: `1`|

### Checkers

|Variable|Description|
|-|-|
| `CHECK_UNMAPPED_CELLS` | Checks if there are unmapped cells after synthesis and aborts if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `CHECK_ASSIGN_STATEMENTS` | Checks for assign statement in the generated gate level netlist and aborts of any was found.1 = Enabled, 0 = Disabled <br> (Default: `0`)|
| `QUIT_ON_TR_DRC` | Checks for DRC violations after routing and exits the flow if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `QUIT_ON_MAGIC_DRC` | Checks for DRC violations after magic DRC is executed and exits the flow if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `QUIT_ON_ILLEGAL_OVERLAPS` | Checks for illegal overlaps during magic extraction. In some cases, these imply existing undetected shorts in the design. It also exits the flow if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|
| `QUIT_ON_LVS_ERROR` | Checks for LVS errors after netgen LVS is executed and exits the flow if any was found. 1 = Enabled, 0 = Disabled <br> (Default: `1`)|


[0]: ./../designs/spm/pin_order.cfg
```

The parameters for floorplanning can be set by editing the `floorplan.tcl` file shown below. 
<p align="center">
  <img src="/Images/pic30.png">
</p><br>

Also, the parameters can be set in the below specified way
<p align="center">
  <img src="/Images/pic31.png">
</p><br>

```
{
    "DESIGN_NAME": "picorv32",
    "VERILOG_FILES": "dir::src/picorv32a.v",
    "CLOCK_PORT": "clk",
    "CLOCK_NET": "clk",
    "GLB_RESIZER_TIMING_OPTIMIZATIONS": true,
    "CLOCK_PERIOD": 24,
    "pdk::sky130*": {
        "SYNTH_MAX_FANOUT": 6,
        "FP_CORE_UTIL": 35,
        "scl::sky130_fd_sc_ms": {
            "FP_CORE_UTIL": 30
        }
    }
}
```
Now, to run the floorplan, do the following
<p align="center">
  <img src="/Images/pic32.png">
</p><br>

Now, to see the floorplan result, do the following
<p align="center">
  <img src="/Images/pic33.png">
</p><br>
Here, we see that `DIEAREA ( 0 0 ) ( 547910 558630 ) ;` is basically the coordinates, where (0,0) is the lowest leftmost part and ( 547910 558630 ) is the topmost rightmost part. If we divide the above number by 1000, we get the coordinates in micrometers. 
<p align="center">
  <img src="/Images/pic34.png">
</p><br>
