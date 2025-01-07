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
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ number\ of\ cells}
```
```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```

Therefore flop ratio will be
```math
Flop\ Ratio =\frac{1613}{14876}=0.108429685

Percentage =0.108429685*100 = 10.84296854 %
```

# Day 2- Good floorplan vs Bad floorplan and introduction to library cells
## Chip Floor planning

For floorplaninng, we will be taking a chip of height H and width W with a die and a core 
![image](https://github.com/user-attachments/assets/79a68597-86b0-4f80-9334-f7ff1e4dd26a)

**1)**
We will be starting with a netlist that we intend to implement on this chip. We will convert the symbols present in our netlist into physical dimensions.
![image](https://github.com/user-attachments/assets/94ad5e7a-82a3-4304-a477-45931d7e25a1)

The standard cells will be 1unit x 1unit making their area 1 sq. unit.
![image](https://github.com/user-attachments/assets/31ebad1e-9da5-481d-ba03-f800b458ea01)

Using these standard cells, we will find the area of the netlist as well as its utilization factor.

```math
Utilization\ Factor =\frac{Area\ Occupied\ by\ the\ netlist}{Total\ area\ of\ core}
```
```math

Aspect\ Ratio=\frac{Height}{Width}

```

We keep the utilization factor around 50%-60%
![image](https://github.com/user-attachments/assets/fe861440-5809-464b-a01e-048f2422c159)

**2)**
**Pre Placed cells**
We can also have pre placed cells on the chip. We can divide a single block into multiple and implement them independently. There are multiple IP's present like memory, clock generating cell, comparator, mux which come under pre placed cells.
![image](https://github.com/user-attachments/assets/509d2cd2-527d-4af4-9feb-00c63f37118e)
![image](https://github.com/user-attachments/assets/ac609e09-3351-4079-ab43-03e0912554bc)



**3)**
 **Decoupling Capacitors**
 If we have only one power source on the chip, if any combinational logic is far away from the voltage sources, it doesn't get all the power from the voltage source. For example, for a 1V  voltage source, the combinational circuit will get only 0.7V which is not ideal as it can get out of the noise margin range and it will be difficult for the system to understand whether the input given is a 0 or a 1.

 To counter this, we use decoupling capacitors. Everytime the circuit switches, it draws current from the decoupling capacitor and uses the load resistance to replenish its charge.
 ![image](https://github.com/user-attachments/assets/26e0598a-e026-413a-b021-afa0274257a8)
 ![image](https://github.com/user-attachments/assets/d0ec1300-be43-4658-b119-1feec58adffa)
 ![image](https://github.com/user-attachments/assets/e81daf66-f423-4583-945f-0f43a2a6e366)



**4)**
**Power Planning**
In power planning, we decide how to place the Vdd and Ground pins. If there are multiple combinational logic cells across the chip, we use multiple power pins.
![image](https://github.com/user-attachments/assets/13a1497b-70c0-43e3-92d0-991aa0f7c813)
![image](https://github.com/user-attachments/assets/8da2099a-4e80-4041-b01d-f487c663e230)


**5)**
**Pin Placement**
In pin placement, we should know the block placement to optimize the pin placement.
![image](https://github.com/user-attachments/assets/7758f8b2-fa9f-4b11-9b5f-7703eaeae500)


**6)**
**Logical cell placement blockage**
This step makes sure that cells are not placed in pin placement.
![image](https://github.com/user-attachments/assets/9bee8161-b193-4e36-9ccd-348f188fe4e3)



### Steps to run floorplan

The steps till run_synthesis are the same.

```
#Now we run floorplan
run_floorplan
```

**Screenshots of running floorplan**
![Screenshot 2024-12-30 124435](https://github.com/user-attachments/assets/b7b61cdb-ac30-4f72-9988-54cddc8482d9)
![Screenshot 2024-12-30 132212](https://github.com/user-attachments/assets/c2ff41ff-ac2d-4032-8f74-f8929476816e)

According to floorplan def
```math
1000\ Unit\ Distance = 1\ Micron
```
```math
Die\ width\ in\ unit\ distance = 660685 - 0 = 660685
```
```math
Die\ height\ in\ unit\ distance = 671405 - 0 = 671405
```
```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```
```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685\ Microns
```
```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405\ Microns
```
```math
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212425\ Square\ Microns
```

To load the floorplan into magic tool to explore it, 
  we have to give the following commands
  ```
#Change the directory to
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/29-12_09-40/results/floorplan/

#Command to start the floorplan file in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

After maximizing the screen, if you want to align the design to the middle
1. Select the design using ``` s ```
2. Press ``` V ``` to align it in the middle

To zoom,
1. Left click and then right click the desired area
2. Press ```Z``` to zoom on the selected region

To get details about the present cell
1. Drag the mouse over the cell
2. Press ```S```
3. In the tkcon window, type ```what```


![Screenshot 2024-12-30 133107](https://github.com/user-attachments/assets/6ae5e2cf-b294-4635-8066-23313f69048a)
![Screenshot 2024-12-30 133254](https://github.com/user-attachments/assets/3ecaf3a7-e3fc-414a-80fe-aae77bf929c9)
![Screenshot 2024-12-30 133935](https://github.com/user-attachments/assets/c7836b00-3178-4e30-9392-c93cd43a0299)

## Placement
To start the placement, complete till the floorplan step and then,

```
#Command to run placement
run_placement
```

The software will run Global Placement initially followed by Detailed placement

**Screemshots of placement**

![Screenshot 2024-12-30 155849](https://github.com/user-attachments/assets/e507c680-bd1f-4e74-ab85-47ae9acf77aa)

To open the placement file, 

 ```
#Change the directory to
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/29-12_09-40/results/placement/

#Command to start the floorplan file in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

![Screenshot 2024-12-30 160046](https://github.com/user-attachments/assets/c88c3574-0b3d-4342-af89-31c075af49af)


### Placement and Routing

**1) Bind netlist with physical cells**

The physical cells are rectangular in shape and not in their original shape

All blocks are present in the library where it also has additional information about the cells

The cells can come in various areas based on the resistance and speed the user wants.

**2) Placement **

We have a floorplane with shapes and sizzes of cells in netlist

We have to place the cells on the floorplan in the optimized manner.

To reduce the dropping of voltage, we also use multiple buffers to regenerate the signal.

![image](https://github.com/user-attachments/assets/e115c13f-ac43-4a6f-9617-0bf8548cd34e)

### Cell Design Flow

**Inputs**
For design flow to work, it should be inputted with PDKs, DRC and LVS Rules, SPICE Models, Library and user defined specifications

**Design Steps**

1) Circuit Design : Implementation of the design
2) Layout Design : Form the layout of the design
3) Characterization

**Outputs**
CDL(Circuit Description Language), GDSII, LEF, extracted spice netlist

### Characterizations

1) Read model file
2) Read extracted spice list
3) Recognize behaviour of cell
4) Read subcircuit of cell
5) Attach necessary power sources
6) Apply stimulus(input)
7) Provide output capacitance
8) Provide necessary simulation commands


### Timing Characterization

** Timing Threshold Definations**
1) Slew low rise threshold: 20% of supply voltage in rising output
2) Slew high rise threshold: 80% of supply voltage in rising output
3) Slew low fall threshold: 20% of supply voltage in falling output
4) Slew high fall threshold: 80% of supply voltage in falling output
5) input rise threshold: 50% of input while rising
6) input falling threshold: 50% of input while falling
7) output rising threshold: 50% of output while rising
8) output falling threshold: 50% of output while falling


**Screenshots of timing characterizations**
![rising_20% graph](https://github.com/user-attachments/assets/ec093ec1-191e-408a-8140-0077ce16f1e2)
![falling_20%_graph](https://github.com/user-attachments/assets/39140c4f-97f5-4ae7-b478-a82027913ead)
![falling_20%](https://github.com/user-attachments/assets/5cca9e2a-e189-4397-a501-5e6c3e28ebec)

# Day 3- Design library cell using Magic Layout and ngspice

### VTC-Spice Simulations

**SPICE Deck**
 It deals with compnent connectivity, component values, identifying nodes

![Screenshot 2024-12-30 202536](https://github.com/user-attachments/assets/87046edc-4afc-45ec-b05a-91bb7eac57ef)


**Git cloning vsdstdcelldesign**

To clone the vsdstdcelldesign into your directory, 
```
# Go to openelane directory
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository
git clone https://github.com/nickson-jose/vsdstdcelldesign
```

This repository contains all the necessary information to build and run the OpenLane flow, which performs a full ASIC implementation from RTL to GDSII.

It includes the procedure to create a custom LEF file and also contains the steps to integrate the custom LEF file into the OpenLANE flow

Next, we have to open the inverter layout thriugh the Magic Tool
```
#Go to the vsdstdcelldesign directory
cd vsdstdcelldesign

#copy the magic tech file
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

#Open the inverter layout
magic -T sky130A.tech sky130_inv.mag &
```

**Screenshots**
![Screenshot 2025-01-02 125909](https://github.com/user-attachments/assets/35505ccf-6ee2-4fec-8fb7-9ad2f607740c)
![Screenshot 2025-01-02 130008](https://github.com/user-attachments/assets/75629f30-b995-4360-9ea4-b134255ba334)


Use the same steps as previously used to identify the nmos and pmos

![Screenshot 2025-01-02 191116](https://github.com/user-attachments/assets/4b28e051-d2aa-44fe-97c6-f84b4cd19257)
![Screenshot 2025-01-02 191157](https://github.com/user-attachments/assets/9d2aff8b-cfd0-453b-8138-651e07038d98)


**Spice Extraction of Inverter in magic**

Use the following commands to extract the spice file of the custom inverter layout

```
extract all

ext2spice cthresh 0 rthresh 0

ext2spice
```

**Screemshots**

![Screenshot 2025-01-02 194610](https://github.com/user-attachments/assets/d9e41902-6c84-4d3b-9bd8-b056b3859867)

The modified spice file:

![image](https://github.com/user-attachments/assets/0ce219d2-c06d-420d-ac63-5f1b8c17b9bf)



**Post Layout ngspice simulation**

To run the ngspice simulator, enter the following commands
```
# Command to open the ngspice simulator
ngspice sky130_inv.spice

# Plot the output over time
plot y vs time a
```

**Screenshots**
![Screenshot 2025-01-03 125633](https://github.com/user-attachments/assets/06c4d136-30c8-48ee-aff0-6265529282be)


**Screenshots of the waveform coording to the terminologies**

1)Rising 20%
![rising_20% graph](https://github.com/user-attachments/assets/8c94cd2b-40c2-41c2-a942-80f82799d690)

![rising_20%](https://github.com/user-attachments/assets/1f87b979-fa68-49cc-827d-179e5d80a4cf)

2)falling 20%
![falling_20%_graph](https://github.com/user-attachments/assets/2c16dd00-1456-4385-9da1-d65c63a62246)

![falling_20%](https://github.com/user-attachments/assets/862c86be-acde-42ac-a15e-f72585f89716)

3)rising 80%
![rising_80%_graph](https://github.com/user-attachments/assets/db6553b2-7865-47ae-9ce6-2a136b88c73e)

![rising_80%](https://github.com/user-attachments/assets/fbc6dc64-afd9-466f-b6ff-f375e30f5369)

4)falling 80%
![falling_80%_graph](https://github.com/user-attachments/assets/53ef2deb-5722-4fca-8bb6-7fc24383d2e3)

![falling_80%](https://github.com/user-attachments/assets/8c2ea507-e474-40d0-9885-50b245ee2d84)

5)rising 50%
![rising_50%_graph](https://github.com/user-attachments/assets/9c8389d8-50c9-4967-b58f-40586b092598)

![rising_50%](https://github.com/user-attachments/assets/2cf8f942-9ca1-4967-a322-53e2b9c77acb)

6)falling 50%
![falling_50%_graph](https://github.com/user-attachments/assets/c649bbb8-942d-40e8-9d72-272d0a6c5847)

![falling_50%](https://github.com/user-attachments/assets/1f284846-103b-4371-a92a-053b4a6406b9)


```math
Rise\ transition\ time = Time\ taken\ for\ output\ to\ rise\ to\ 80\% - Time\ taken\ for\ output\ to\ rise\ to\ 20\%

```
```math
Rise\ transition\ time = 2.20009 - 2.17992 = 0.02017\ ns = 20.17\ ps

```

```math
Fall\ transition\ time = Time\ taken\ for\ output\ to\ fall\ to\ 20\% - Time\ taken\ for\ output\ to\ fall\ to\ 80\%

```

```math
Fall\ transition\ time = 4.0799 - 4.06652 = 0.01338\ ns = 13.38\ ps

```

```math
Rise\ Cell\ Delay = Time\ taken\ for\ output\ to\ rise\ to\ 50\% - Time\ taken\ for\ input\ to\ fall\ to\ 50\%

```

```math
Rise\ Cell\ Delay = 2.18049 - 2.1499 = 0.03059\ ns = 30.59\ ps

```

```math
Fall\ Cell\ Delay = Time\ taken\ for\ output\ to\ fall\ to\ 50\% - Time\ taken\ for\ input\ to\ rise\ to\ 50\%

```

```math
Fall\ Cell\ Delay = 4.05341- 4.05 = 0.00341\ ns = 3.41\ ps

```



























