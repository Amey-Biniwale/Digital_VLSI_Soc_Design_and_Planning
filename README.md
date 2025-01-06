# Digital_VLSI_Soc_Design_and_Planning
# Day 1- Inception of Open Source EDA, Openlane and Sky130 PDK
## How to talk to computers
### Introduction to QFN-48 package
The OFN-48 is a Quad flat No-leads 48 pin package. It is a 7mmx7mm package with a height of 0.9mm. 
![image](https://github.com/user-attachments/assets/0dd82842-8b4a-43fc-8ed6-fc1868841c14)
The QFN-48 has PADS, Core, and Die. Pads are mechanism used to send signal through the chip. The signal can be sent from inside to outside and vice versa. The core is a place allocated for the placement of logic gates. The Die is the size of the entire chip.

Inside the Core, multiple IP's(Intellectual Property) as well as Macros can be placed.

Intellectual properties are pre designed macros provided by different entities for different purposes.
![image](https://github.com/user-attachments/assets/5a7f39e6-0912-4cfb-a54d-7282dd1c5b41)

### Introduction to RISC-V
![image](https://github.com/user-attachments/assets/0b5961d1-e866-4520-8bea-5af4ae08b91e)
In this course, we will learn how to run an openlane flow from RTL file to GDS file. We will have to write a C programming to code to define the logic of the application you want to implement. Next, you have implement the given C programming file through the openlane flow to complete the layout, placement and routing and many more things.

The C programming file is entered into a compiler which converts it to assembly language file and then to a assembler to convert it to binary bits for the machine to understand.

## SoC Design and Openlane
We will be using RTL IP's, EDA tools, and PDK data to form an ASIC Design. All these components will be taken from open-source sites as it makes it easier to design the flow. 

For the RTL IP's, we will be using librecores.org, opencores.org, github.com and many other open-source websites. For EDA tools, we will be using OpenLANE, and OpenRoad. OpenROAD will be used for static timing analysis.

For the **PDKS**, we will be using Skywater 130nm PDK. SkyWater 130nm PDK is an open source PDK developed by SkyWater and Google in collaboration. PDKs include Process Design Rules like DRC,LVS etc., Device models, Digital Standard Libraries, I/O Libraries and many other things.

For more information on the SkyWater PDK, you can visit [github.com/google/skywater-pdk .](https://github.com/google/skywater-pdk). It was launched on June 30, 2020. 130nm PDKs are used in 6% of all PSK implementation.

The EDA tools can perform the following processes.
![image](https://github.com/user-attachments/assets/ecd0b569-8f21-4f1a-9430-489b60b6c274)
### Simplified RTL2GDS flow

The flow starts with Synthesis moving on to Floorplanning/Powerplanning, Placement, Clock Tree Synthesis, Routing and then ending with Static Timing Analysis.
![image](https://github.com/user-attachments/assets/4c3cfdbf-770e-4ba0-9313-bc6e6b48fd21)

**Synthesis**
The synthesis converts the RTL to a circuit out of components from the standard cell library. There are multiple different standard cells. Standard cells of the same component can have different areas based on the use case.

**Floorplanning/PowerPlanning**
There are 2 types of Floorplanning namely Chip Foorplanning and Macro Floorplanning. Power planning works on the placement of power sources such as Vdd and ground.

**Placement**
Placement is used to place the cells on the floorplan rows, alogned with the sites. It is done in 2 steps.

The first step is Global placement in which the flow places the standard cells in optimal position even when they overlap with each other.

Then, Detailed placement takes place which alters the position of the global placement so they do not overlap.
![image](https://github.com/user-attachments/assets/8f1abc25-dfcd-4db7-9ff6-692d80a0668e)

**Clock Tree Synthesis**
It is done to create a clock distribution network used to deliver the clock to all sequential elements with minimum skew.

**Routing**
It is used to implement interconnect using available metal layers. Metal tracks form a routing grid which is huge as it covers the entire chip.

**Sign Off**
The Sign Off contains the Physical Verifications like Design Rule Check(DRC) and Layout Vs. Schematic(LVS).

It also does the timing verification using Static Timing Analysis.

### OpenLANE
OpenLANE started as an Open-Source Flow for true Open Source Tape-Out Experiment. They use the striVe family of open everythings.

The ASIC flow's main goal is to produce a clean GDSII with no human intervention. The operation has 2 modes namely autonomous and interactive.
![image](https://github.com/user-attachments/assets/23274894-75c3-4a30-ab94-ebe6fbd05c80)

The above image is the OpenLANE ASIC Design Flow.











