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

OpenLANE flow is based in OpenROAD Magic VLSI Layout Tool Fault Yosys QFlow and ABC. OpenLANE uses Regression Testing in which it runs OpenLANE on 70-75 designs and compares the results to the best known ones.

It has Design for Test(DFT) which performs the tasks of Scan Insertion, Automatic Test Pattern Generation, Test Patterns Compaction, Fault Coverage, and Fault Simulation.

In Physical Implementation, it does the Placement and Routing of the cells along with floor/powerplanning, Clock Tree Synthesis and much more

Logic Equivalence Check(LEC) is used to formally confirm that the function did not change after modifying the netlist.

In the flow, we also have to deal with antenna rules violation which can be solved using Bridging or adding an antenna diode cell to leak away the charges.

In the last step, we do Timing verification and Physical verification of the chip.

## Get familiar to open-source EDA tools

Getting to know the various commands:

1. pwd: It shows the current directory the user is present.
2. cd: This command helps the user move from one directory to another.
3. ls-ltr: It lists all the sub- directories and files that the directory contains.
4. help: This command helps the user with the information for any command the user wants to gain knowledge about.
5. clear: This command clears the terminal.
6. mkdir: This command creates a new directory.

There are few key file like libs.ref which contains information about standard cells, IO cells, etc. and libs.tech which contains all the information regarding the EDA tools.

To get into OpenLANE flow we have to set our directory to
```
cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane
```
To invoke the OpenLANE flow, we have to give the following commands
```
docker # this command enters us into the OpenLANE flow

./flow.tcl -interactive

#We need to open the necessary packages
package require openlane 0.9

#To run any design, we have to prepare it
prep -design picorv32a

#Now, to run the synthesis, give the command
run_synthesis
```

Once you run the synthesis an new file will be created under the runs directory in the picorv32a directory.

Screenshots of running the code:
![Screenshot 2024-12-29 151121](https://github.com/user-attachments/assets/cfaa0c20-dde0-4743-b53b-745a9cd060d0)
![Screenshot 2024-12-29 151132](https://github.com/user-attachments/assets/e91ab422-9784-47ab-b053-2a0827ae0f29)

After running the synthesis, we get the following data
![Screenshot 2024-12-29 152547](https://github.com/user-attachments/assets/b4d6629b-b562-4f9d-bef0-2f374a2cbbe7)
![Screenshot 2024-12-29 152601](https://github.com/user-attachments/assets/5face9d6-c395-4332-9520-4316e9d8ebd5)
 Using this we have to find the flop ratio.
 ```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```
```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```

Therefore flop ratio will be
```math
Flop\ Ratio =\frac{1613}{14876}=0.108429685

Percentage =0.108429685*100 = 10.84296854 %
```
















