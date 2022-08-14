# Advanced-Physical-Design-using-OpenLANE-Sky130
<p align="center">
  <img src="/Images/cover.png">
</p><br>

# Table of contents
- [Day-1- Inception of open source EDA OpenLANE and Sky130](#1-Inception-of-open-source-EDA-OpenLANE-and-Sky130)
    - [1.1 Introduction](#11-Introduction)
    
# 1. Inception of open source EDA OpenLANE and Sky130
## 1.1 Introduction
### Chips versus Package
Chips are typically inside a package. Pins of the chips are connected to the package pins via wire bonds.
<p align="center">
  <img src="/Images/pic1.png">
</p><br>
I/O pabd are used to communicate with the chip. 
<p align="center">
  <img src="/Images/pic2.png">
</p><br>
Typically, components of a chip can be classified into two categories,
 - Foundary IPs
 - Macros 
<p align="center">
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

### What is OpenLANE?
OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. It is a tool started for true open source tape-out experience and comes with APACHE version 2.0 . The goal of OpenLANE is to produce clean GDSII without any human intervention. OpenLANE is tuned for Skywater 130nm open-source PDK and can be used to produce hard macros and chips
