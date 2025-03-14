# Design and Implementation of 64-point Fast Fourier Transform (FFT/IFFT) Chip for OFDM-based 802.11a WLAN
ET4067 VLSI for Digital Communication System (VHDL RTL Implementation)  
EE382M VLSI-I (Verilog RTL Implementation + Physical Implementation + Timing Signoff)  
EE382M Verification of Digital System (Formal Verification + Logical Equivalence Checking + Universal Verification Methodology)  

(C) 2014 Bagus Hanindhito  
(C) 2019 Bagus Hanindhito, Reshma Rajarama Nayak, Shvetha Senthil Kumar  
(C) 2020 Bagus Hanindhito, Ashen Ekanayake, Tosin Jemilehin  

## Introduction
### Brief Overview
This is the RTL implementation, physical implementation, and verification of 64-point FFT/IFFT processor based on the design proposed in the papers listed below. The circuit uses Fixed-Point Q4.12 data format consists of 16-bit real data and 16-bit imaginary data.   
[1] K. Maharatna, E. Grass and U. Jagdhold, "A 64-point Fourier transform chip for high-speed wireless LAN application using OFDM," in IEEE Journal of Solid-State Circuits, vol. 39, no. 3, pp. 484-493, March 2004, doi: 10.1109/JSSC.2003.822776.  
The projects also use the following resources.  
[2] (https://github.com/jeremytregunna/ksa)  
[3] (https://www.eda.ncsu.edu/wiki/FreePDK45:Contents)  

### Related Courses
This repository contains the project files that were used for project related to the courses listed below.  
#### ET4067 VLSI for Digital Communication System (Fall 2014), Institut Teknologi Bandung, Indonesia (Lecturer: Achmad Fuad Mas'ud)
The initial RTL implementation of the circuit was done in VHDL as a part of the course project of ET4067 taught by Achmad Fuad Mas'ud. As an addition, simulation-based verification was done using Altera Quartus II 9.1sp2 and ModelSim-Altera 6.5b. The verification was done manually against the Matlab code provided in this repository. The carry-look-ahead adder is used throughout the design. There are two known bugs in this design that were fixed on the later project. It is recommended to use the Verilog RTL implementation instead.
* the synthesizer couldn't synthesize the correct carry-look-ahead adder, instead it synthesizes ripple-carry-adder).
* the master control signals to trigger the output counter.   

The deliverables of this project are listed below.
* RTL implementation in VHDL
* Matlab script as the testbench (Matlab R2014a)
* Simulation-based verification (Altera Quartus II 9.1sp2 and ModelSim-Altera 6.5b)
* Project Report in Indonesian

#### EE382M VLSI-I (Fall 2019), The University of Texas at Austin, United States (Lecturer: Jacob Abraham)
The RTL implementation was done in Verilog. The adder was changed into kogge-stone adder [2] to improve the performance of the custom chips. The previous bugs were also fixed and new feature to overlap FFT/IFFT computation was also introduced in the form of next_data signal. Functional verification was done using Synopsys VCS/DVE with the help of the testbench created in Matlab script. The design was synthesized to produce gate-level verilog netlist using Synopsys Design Compiler on FreePDK45 library [3]. The design achieved clock speed of 200MHz on Pre-Implementation Static Timing Analysis using Synopsys PrimeTime.   

The physical implementation is done using Cadence Innovus 18.1 Implementation System for automatic place and route tool. We use multi-mode multi-corner (MMMC) analysis with only one corner (typical). The netlist and constraints were imported from the verilog gate-level netlist and SDC generated by Synopsys Design Compiler. The implementation steps were performed: floorplanning, powerplanning, placement, pre-CTS optimization, clock-tree synthesis, post-CTS optimization, routing, and post-routing optimization. Physical verification was done inside the Innovus and using the Mentor Calibre. Finally, static timing analysis was done using PrimeTime.  

The deliverables of this project are listed below.
* RTL implementation in Verilog
* Simulation-based verification (Synopsys VCS/DVE)
* Synthesized gate-level netlist (Synopsys Design Compiler)
* Physical implementation and verification (Cadence Innovus, Mentor Calibre)
* Static timing analysis report (Synopsys PrimeTime)  

#### EE382M Verification of Digital System (Spring 2020), The University of Texas at Austin, United States (Lecturer: Jacob Abraham)
The project target was to verify the FFT/IFFT processor created on earlier project. There are three verification methods that were done in this project. The Formal Verification (FV) method using Cadence JasperGold was done to verify the Master Control block. The Universal Verification Methodology (UVM) using ModelSim was done to verify the whole circuit functionality by instantiating one FFT and one IFFT instances. Finally, Logical Equivalence Checking (LEC) was done to verify the design at RTL level against the synthesized design at gate-level and to verify the design at RTL-level against the physically-implemented design at gate-level.  

The deliverables of this project are listed below.
* Formal Verification SystemVerilog script and TCL script for Master Control block (Cadence JasperGold)
* Universal Verification Methodology SystemVerilog script for whole circuit functional verification (Mentor ModelSim)
* Logical Equivalence Checking script (Cadence Conformal LEC)

## Architecture
You can get the code, compile them, and run them very easily by following these steps.
### Mathematical Review
### Top-Level Diagram
### The Input Circuit
### The 8-point FFT
### The Interdimensional Multiplier
### The CB Buffer
### The Output Buffer
### The Master Control

## Contributing and Citing
If you are interested to use or modify the code for your next project, please cite accordingly. I will be very grateful for any contribution on this code.
```
@misc{bagus_hanindhito_2020_3834733,
    author       = {Bagus Hanindhito},
    title        = {{Two Level Branch Predictor Simulator}},
    month        = May,
    year         = 2020,
    doi          = {10.5281/zenodo.3834733},
    version      = {1.0.0},
    publisher    = {Zenodo},
    url          = {https://doi.org/10.5281/zenodo.3834733}
    }
```

## Authors
Bagus Hanindhito  
Undergraduate Student at Department of Electrical Engineering  
Institut Teknologi Bandung  
Graduate Student at Department of Electrical and Computer Engineering    
The University of Texas at Austin    

## License
The code is licensed under GNU Affero General Public License v3.0. Please see LICENSE file included in the source code.

## Acknowledgments
ET4067 VLSI for Digital Communication System, Fall 2014  
* Achmad Fuad Mas'ud (Lecturer)

EE382M VLSI-I, Fall 2019 (https://www.cerc.utexas.edu/~jaa/vlsi/)  
* Jacob Abraham (Lecturer)
* Ling Lin (TA)
* Hyunsu Chae (TA)
* Sunny Bhagia (TA)
* Reshma Rajarama Nayak (Team Member)
* Shvetha Senthil Kumar (Team Member)

EE382M Verification of Digital System, Spring 2020 (https://www.cerc.utexas.edu/~jaa/verification/)
* Jacob Abraham (Lecturer)
* Ling Lin (TA)
* Hyunsu Chae (TA)
* Ashen Ekanayake (Team Member)
* Tosin Jemilehin (Team Member)


