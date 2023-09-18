# Advance Physical Design using OpenLane and sky130 PDK

This github repository contains the progress made in Advance Physical design using OpneLane and sky130 PDK tools

[Day 1](#day-1)

[Day 2](#day-2)

[Day 3](#day-3)

[Day 4](#day-4)

[Day 5](#day-5)



# Day 1

<details>
<summary>Introductiion to RISC-V ISA and Inception of open source EDA, OpenLane and sky130 PDK</summary>

**Inrtoduction to QFN-48 package**

QFN-48 Package:
        QFN stands for "Quad Flat No-leads," and it is a type of surface-mount integrated circuit (IC) package. The "48" indicates the 
number of pins or leads in the package. QFN packages are popular due to their compact size, excellent thermal performance, and ease of 
manufacturing. They are commonly used in a wide range of electronic devices, including microcontrollers, RF (Radio Frequency) chips, and 
power management ICs.

![day_1_package pin diagram](https://github.com/simarthethi/Advance_physical_design/assets/140998783/84a118d6-3ad2-4d96-9ad0-e7182550d9e7)
        

*Chip*:
        The term "chip" typically refers to an integrated circuit (IC) or microchip. It is a small, thin piece of semiconductor material 
(usually silicon) on which electronic components such as transistors, capacitors, and resistors are fabricated. Chips are the fundamental 
building blocks of electronic devices, and they perform various functions, from processing data in microprocessors to amplifying signals in 
amplifiers.

![Screenshot from 2023-09-10 10-34-08](https://github.com/simarthethi/Advance_physical_design/assets/140998783/d8f51074-f02b-4f43-bdab-d87fe3d3c16d)

- We use something call wire bonds to connerct the pins to the boundary of the chip.

*Pads*:
        Pads are metalized areas on the surface of an integrated circuit package or printed circuit board (PCB) that serve as connection 
points for soldering or making electrical connections. In the context of a QFN-48 package, there are 48 pads that correspond to the 48 pins 
of the package. These pads facilitate the electrical connection between the chip inside the package and the external circuitry.

 ![Screenshot from 2023-09-10 10-34-35](https://github.com/simarthethi/Advance_physical_design/assets/140998783/64c7e9ba-421c-40f3-8039-bba31c00246f)
       

 *Core*:
        In the context of integrated circuits, the term "core" typically refers to the central processing unit (CPU) or the primary 
computational and control unit of a microprocessor. It is where most of the processing and data manipulation occur. In other contexts, 
"core" may refer to the central or essential part of a system or device.

*Die*:
        The "die" is the actual silicon chip within an integrated circuit package. It contains the transistors, logic gates, and other 
electronic components that perform the chip's intended function. The die is usually very small and encapsulated within the package to 
protect it from environmental factors and to facilitate electrical connections.

*IPs (Intellectual Property)*:
        In the realm of semiconductor design, "IP" often refers to Intellectual Property, specifically semiconductor IP cores. These are pre-
designed and pre-verified blocks of intellectual property that can be integrated into custom chip designs. They include things like CPU 
cores, memory controllers, and various functional blocks. Integrating IP cores into a chip design can significantly accelerate development 
and reduce the need to design complex components from scratch.

Here we are taking an example of the sample SoC - RISC-V on the chip
![day_1_package pin diagram](https://github.com/simarthethi/Advance_physical_design/assets/140998783/a0797ab8-4703-4790-bf60-c332af0117df)

-A typical chip contains SOC, SRAM, ADC, DAC, PLL etc
![Screenshot from 2023-09-10 10-34-53](https://github.com/simarthethi/Advance_physical_design/assets/140998783/972f7e1b-bbf0-43e3-88d6-5ba1c4394661)



**Inroductuction to RISC-V ISA**

RISC-V is an open-source instruction set architecture (ISA) for computer processors. An instruction set architecture defines the set of 
instructions that a processor can execute and the organization and behaviour of those instructions. RISC-V is unique in that any single 
company or organization does not own it. and it is freely available for anyone to use, modify, and implement without the need for licensing 
fees or proprietary restrictions.

![Screenshot from 2023-09-10 11-12-30](https://github.com/simarthethi/Advance_physical_design/assets/140998783/fba2d664-b965-4ee5-8ca0-3cec22d5d81d)

Application software (apps) and hardware are linked by 'system software'.There are various layers of system software. This includes major 
components like Compiler and Assembler.

The compiler compiles high-level codes like C and C++ to Instructions(eg: the codes inside .exe files) that can be read by the Assembler. 
The Assembler converts it into binary codes which the machine can understand. The instructions act as an interface between the high-level 
language and the machine language.

The converted binary is then given to an RTL snippet that understands the instruction. This is done by a Hardware Description Language 
(HDL). This is basically called RTL implementation and a netlist is being generated. with this, a physical design implementation of the 
design is generated.

The RISC-V project began at the University of California, Berkeley in 2010, and it has since gained significant traction in both academia 
and industry. Its open nature has led to a growing ecosystem of hardware and software developers collaborating to create a wide range of 
products, from simple embedded devices to high-performance supercomputers.

**SoC design and OpenLane**

Desiging Digital Application Specific Integrated Chip(ASIC) require several elements. They are as follows:

- RTL IP's
- EDA tools
- PDK tools

![Screenshot from 2023-09-10 11-14-09](https://github.com/simarthethi/Advance_physical_design/assets/140998783/0e144a06-07b7-405f-8fe1-f1ccf99428ee)

*RTL IP (Register-Transfer Level Intellectual Property)*:
RTL IP refers to pre-designed and pre-verified blocks of digital logic or functional modules that are expressed at the register-transfer 
level (RTL). RTL is a hardware description level that captures the behavior of a digital circuit in terms of data transfers between 
registers and logic operations. RTL IP cores are reusable building blocks that can be integrated into larger ASIC or FPGA designs. These 
cores can include various functions such as processors, memory controllers, communication interfaces, and more. Designers often use RTL IP 
to save time and effort when creating complex digital systems.

*EDA Tools (Electronic Design Automation Tools)*:
EDA tools are software applications that facilitate the design and verification of electronic circuits, including ASICs, FPGAs, and other 
digital systems. These tools cover various stages of the design flow, from conceptualization to physical implementation.

*PDK Tools (Process Design Kit Tools)*:
A Process Design Kit (PDK) is a collection of tools, libraries, and documentation provided by semiconductor foundries to enable designers 
to create ASICs and other integrated circuits using their specific manufacturing processes. PDK tools are part of the PDK package and serve 
several purposes

Now-a-days there are a lot of open source tools that can be used to design a *Digital ASIC*

![day1_Into-pic](https://github.com/simarthethi/Advance_physical_design/assets/140998783/b64efa50-aab5-4ac1-940e-2047b609e4af)

**Introduction to OpenLane**

OpenLane is an open-source ASIC (Application-Specific Integrated Circuit) design flow framework that automates the process of designing 
custom integrated circuits. The design flow in OpenLane consists of several stages, each with specific tasks and objectives.

-Here is a simplified RTL to GDSII flow diagram

![Screenshot from 2023-09-10 11-26-43](https://github.com/simarthethi/Advance_physical_design/assets/140998783/c4195262-9909-4a93-8fb9-62107fb81798)

-RTL-synthesis:
        RTL (Register-Transfer Level) synthesis is a crucial stage in the OpenLane ASIC design flow, where the high-level RTL description of your custom logic is translated into a gate-level netlist. This netlist consists of standard cells (logic gates) and their interconnections, making it suitable for subsequent stages such as placement and routing.

-Floorplanning:
        Floorplanning involves defining the physical layout of the chip, specifying the locations of major functional blocks, and allocating space for routing and other components. This step sets the foundation for efficient placement and routing.

-Powerplanning
        Power network is constructed.

 -Placement:
        During placement, OpenLane determines the precise locations of individual standard cells (logic gates) within the chip area defined in the floorplan. It aims to optimize area, power, and timing by positioning cells strategically.       

-Clock Tree Synthesis (CTS):
        CTS is the process of designing and building a clock distribution network that ensures clock signals reach all sequential elements (flip-flops) in a synchronized manner. Proper CTS is crucial for maintaining timing constraints.

-Routing:
        The routing stage involves determining the physical interconnections between standard cells, including metal layers and wires. OpenLane uses tools like TritonRoute to create a routed design that adheres to design rule constraints.
        
-Signoff (Detail and Final Verification):
        After placement and routing, OpenLane performs detailed design rule checking (DRC) and final verification to ensure the layout complies with fabrication constraints and meets specified requirements for timing, area, and power.

-GDSII Generation:
        Once the design passes verification, OpenLane generates a GDSII (Graphics Data System II) file, which is the final output file that contains the complete layout data for fabrication. The GDSII file is used by semiconductor foundries to manufacture the chip.

OpenLane integrated several key open source tools over the execution stages:

- RTL Synthesis, Technology Mapping, and Formal Verification : yosys + abc
- Static Timing Analysis: OpenSTA
- Floor Planning: init_fp, ioPlacer, pdn and tapcell
- Placement: RePLace (Global), Resizer and OpenPhySyn (formerly), and OpenDP (Detailed)
- Clock Tree Synthesis: TritonCTS
- Fill Insertion: OpenDP/filler_placement
- Routing: FastRoute or CU-GR (formerly) and TritonRoute (Detailed) or DR-CU
- SPEF Extraction: OpenRCX or SPEF-Extractor (formerly)
- GDSII Streaming out: Magic and KLayout
- DRC Checks: Magic and KLayout
- LVS check: Netgen
- Antenna Checks: Magic
- Circuit Validity Checker: CVC

**OpenLane Installation**

Prior to the installation of the OpenLane install the dependencies and packages using the command shown below :
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
```
Docker Installation :
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world

sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot 


# Check for installation
sudo docker run hello-world
```
Steps to install OpenLane, PDKs and Tools
```bash
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane --recurse-submodules 
cd OpenLane
make
make test
cd /OpenLane/designs/ci
cp -r * ../
```

*Steps for synthesis in OpenLane*
```bash
cd ~/OpenLane
make mount
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```
Viewing the netlist generated during synthesis
```bash
cd /OpenLane/designs/picorv32a/runs/RUN_2023.09.08_13.53.29/results/synthesis
vim picorv32a.v
```
![Screenshot from 2023-09-09 19-12-11](https://github.com/simarthethi/Advance_physical_design/assets/140998783/71e22d01-bdd1-469e-a631-b986abe2a911)

To check the status report

![Screenshot from 2023-09-09 19-26-50](https://github.com/simarthethi/Advance_physical_design/assets/140998783/e1b37238-d852-48ec-b1e9-3fa778e7036c)
![Screenshot from 2023-09-09 19-26-55](https://github.com/simarthethi/Advance_physical_design/assets/140998783/a44c9beb-f571-48c2-ab76-d6ceb0c163f4)

</details>

# Day 2        
<details>
        
<summary>Chip FLoorplanning consideration</summary>

**Width and Height of core and die**

Lets begin an example of a netlist as follows:
![Screenshot from 2023-09-16 15-06-17](https://github.com/simarthethi/Advance_physical_design/assets/140998783/0b06c5be-f834-46cc-963a-6b2921cc7013)

In here we see that the gates and flipflops have a certain shape which is for our understanding so that we differentiate between them. But in an electonic design the gates and other components are taken in the shapes of squares and rectangles so that we can define the size of the components

![Screenshot from 2023-09-16 15-21-01](https://github.com/simarthethi/Advance_physical_design/assets/140998783/8189e1d6-facf-4184-b3e4-a42082abcc62)

*Utilisation Factor*

```bash
Utilisation factor: Area covered by the netlist/total area of the core
```

- The ratio of area occupied by the cells in the netlist to the total area of the core
- Best practice is to set the utilisation factor less than 50% so that there will be space for optimisations, routing, inserting buffers etc.,

*Aspect Ratio*
```bash
Aspect ratio : width/height
```

- Aspect ratio is the ratio of height to the width of the die.
- Aspect Ratio of 1 indicates that the die is a square die

These two Parameters are important to derive the width and height of the core and die, and now we can move ahead to define the location of preplaces cells.

**Pre-placed Cells**

- Whenever there is a complex logic which is repeated multiple times or a design given by a third-party it can be perceived as abstract black box with input and output ports, clocks etc. We can also create black boxes ourselves for the design in case as per the requirements. They can be IPs or Macros
- These Macros and IPs are placed in the core at first before placing the standard cells and power planning. These are optimally such that the cells which are more connected to each other are placed nearby and oriented for input and ouputs.
- Once they have been placed, the location are not altered later on for routing. Thus they have been fixed on the chip.
- These pre-placed cells have to be surrounded with de-coupling capacitors.

**De-coupling Capacitors**

- The resistances and capacitances associated with long wire lengths can cause the power supply voltage to drop significantly before reaching the logic circuits. This can lead to the signal value entering into the undefined region, outside the noise margin range.
- De-coupling capacitors are huge capacitors charged to power supply voltage and placed close the logic circuit. Their role is to decouple the circuit from power supply by supplying the necessary amount of current to the circuit. They pervent crosstalk and enable local communication.

**Power Planning**

- Each block on the chip, however, cannot have its own decap unlike the pre-placed cells.
Thus, when multiple units are discharging, we observe a ground bumb and in case of multiple
charing units, we see a voltage droop.
- When thses are under noise range designed, we won't face any issue, but if they get beyond
the defined noise range, we experience undesired behaviour from the design.
- To fix this issue, we will go for a better power plan for the chip, such that each unit can
use the Vdd and Gnd near to it.
- A common way to accomplish this is to have VDD and VSS pads connected to the horizontal and
vertical power and GND lines which form a power mesh.

**Pin Placement**

- The input, output and Clock pins are placed optimally such that there is less complication
in routing or optimised delay.
- Note - CLK needs least resistive path, as they provide signals to all the flops
continuously, thus have bigger IO ports.
- There are different styles of pin placement in openlane like random pin placement, uniformly
spaced etc.,

Run Floorplan on OpenLane

- Importance files in increasing priority order:
        floorplan.tcl - System default envrionment variables
        conifg.tcl
        sky130A_sky130_fd_sc_hd_config.tcl

- Floorplan envrionment variables or switches:
        FP_CORE_UTIL - floorplan core utilisation
        FP_ASPECT_RATIO - floorplan aspect ratio
        FP_CORE_MARGIN - Core to die margin area
        FP_IO_MODE - defines pin configurations (1 = equidistant/0 = not equidistant)
        FP_CORE_VMETAL - vertical metal layer
        FP_CORE_HMETAL - horizontal metal layer

Now, we will look into how to generate the floorplan using OpenLane.
```bash
run_floorplan
```
![week 3 day_2 rn_floorplan](https://github.com/simarthethi/Advance_physical_design/assets/140998783/a1fd458f-88bc-44fd-8229-276d462c7d08)

-    We may review floorplan files by checking the floorplan.tcl. The system defaults will
have been overriden by switches set in conifg.tcl and further overriden by switches set in
sky130A_sky130_fd_sc_hd_config.tcl.

-    Post the floorplan run, a .def file will have been created within the results/floorplan
directory. It has the various informations such as the die area and unit lenghts used.

```bash
cd /OpenLane/designs/picorv32a/runs/RUN_2023.09.08_13.53.29/results/floorplan
less picorv32.def
```
![def_file floorplan](https://github.com/simarthethi/Advance_physical_design/assets/140998783/df2dfd33-a3cc-4f9f-90a3-c52ee015aa02)

- we can't read how the components and the netlists are placed in the floorplan by reading the .def file
Hence we'll view the floorplan in Magic

**View floorplan on magic**

To view the floorplan, Magic is invoked after moving to the results/floorplan directory:
```bash
 magic -T ~/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &
```
![day_2 magic](https://github.com/simarthethi/Advance_physical_design/assets/140998783/118f2cd3-0e61-4e86-b051-d40eeb4d1350)

One can zoom into Magic layout by selecting an area with left and right mouse click followed by pressing "z" key.

Various components can be identified by using the what command in tkcon window after making a selection on the component.

Zooming in also provides a view of decaps present in picorv32a chip.

The standard cell can be found at the bottom left corner.

You can clearly see I/O pins, Decap cells and Tap cells. Tap cells are placed in a zig zag manner or you can say diagonally

![Screenshot from 2023-09-16 15-35-42](https://github.com/simarthethi/Advance_physical_design/assets/140998783/c2e60927-3637-4913-9ac7-f4ab2a0eb30c)
        
</details>

<details>
<summary>Library binding and Placement</summary>

First and foremost, we need to bind the netlist with physical cells. We have shapes for OR, 
AND and every cell for pratice purpose. But in reality we dont have such shapes, we have give 
an physical dimensions like rectangles or squares weight and width. This information is given 
in libs and lefs. Now we place these cells in our design by initilaising it.

Now we look into Placement and its optimisation.

**Optimise Placement**

The next step is placement. Once we initial the design, the logic cells in netlist in its physical dimisoins is placed on the floorplan. Placement is perfomed in 2 stages:

- Global Placement: Cells will be placed randomly in optimal positions which may not be legal and cells may overlap. Optimization is done through reduction of half parameter wire length.
- Detailed Placement: It alters the position of cells post global placement so as to legalise them. Legalisation of cells is important from timing point of view.

Optimization is stage where we estimate the lenght and capictance, based on that we add buffers. Ideally, Optimization is done for better timing.

- Run Placement on OpneLane
```bash
run_placement
```
![Screenshot from 2023-09-16 19-46-38](https://github.com/simarthethi/Advance_physical_design/assets/140998783/d720e1d3-c957-49ab-9fdf-6dad80f7cf22)

- The objective of placement is the convergence of overflow value. If overflow value
progressively reduces during the placement run it implies that the design will converge and
placement will be successful. Post placement, the design can be viewed on magic within
results/placement directory:

```bash
magic -T ~/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &
```

![Screenshot from 2023-09-16 19-50-39](https://github.com/simarthethi/Advance_physical_design/assets/140998783/c6af81a1-8521-4666-ac3d-fa8f9576c6fe)

- Zoomed in image

![Screenshot from 2023-09-16 19-56-44](https://github.com/simarthethi/Advance_physical_design/assets/140998783/b5facee6-dc04-46ed-ad29-af48d945d0ac)

</details>

<details>
<summary>Cell design and characterisation flow</summary>

Under this section, we will go through a thorough insight into the Characterizatiob flow and various steps involved, what are my inputs given, my intermediate outputs and final results we get.

Standard cell design flow involves the following

- Inputs:
        PDKs
        DRC & LVS rules
        SPICE models
        Libraries
        User-defined specifications.

- Design steps:
        Circuit design
        Layout design (Art of layout Euler's path and stick diagram)
        Extraction of parasitics
        Characterization (timing, noise, power).

- Outputs:
        CDL (circuit description language)
        LEF
        GDSII
        extracted SPICE netlist (.cir)
        timing, noise and power .lib files

**Standard Cell Characterization Flow**

A typical standard cell characterization flow includes the following steps:

1.Read in the models and tech files
2.Read extracted spice netlist
3.Recognise behaviour of the cell and buffers
4.Read the subcircuits
5.Attach the necessary power sources
6. Apply stimulus to characterization setup
7.Provide necessary output capacitive loads
8.Provide necessary simulation command



Now all 8 steps are provided together as a configuration file to a characterization software called **GUNA**.

![Screenshot from 2023-09-16 20-01-31](https://github.com/simarthethi/Advance_physical_design/assets/140998783/487de96c-a55b-40f5-85bb-33066b1a43d8)

This software generates timing, noise, power models. These .libs are classified as Timing characterization, power characterization and noise characterization.

</details>

<details>
<summary> General Timing and Characterization parametes </summary>

Under this section, we will look into the timing characterization and get an understanding of 
various semantics and syntax of the three .lib files for noise, power and noise.

First we go through the various Timing Parameter Definitions


**Propagation Delay**

The time difference between when the transitional input reaches 50% of its final value and when the output reaches 50% of its final value. Poor choice of threshold values lead to negative delay values. Even thought you have taken good threshold values, sometimes depending upon how good or bad the slew, the dealy might be still +ve or -ve.

```bash
Propagation delay = time(out_thr) - time(in_thr)
```

**Transition Time**

The time it takes the signal to move between states is the transition time , where the time is measured between 10% and 90% or 20% to 80% of the signal levels.  
```bash
Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)

Low transition time = time(slew_high_fall_thr) - time (slew_low_fall_thr)
```
</details>

# Day 3

<details>
<summary>Cmos Invertor ngspice lab </summary>
        
**IO Placer revision**

- PnR is a iterative flow and hence, we can make changes to the environment variables in the fly to observe the changes
in our design.
- Let us say If I want to change my pin configuration along the core from equvi distance randomly placed to someother
placement, we just set that IO mode variable on command prompt as shown below
```bash
set ::env(FP_IO_MODE) 2
```
Floorplan after chaning the format of IO placement. We can see the pins are now not equi-distant. 
![day_3 floorplan not equidistant](https://github.com/simarthethi/Advance_physical_design/assets/140998783/ddbe368c-a566-4a95-948e-b45742b84393)

**Spice Deck Creation**
Spice Deck Creation

- Spice deack is the connectivity information of netlist. Thus it is a netlist that contains component connectivity, inputs to be provided and tap points for taking output and connectivity of the substrate.
- The source of PMOS is connected to Vdd and Source of NMOS is connected to GND, Vss in this case. Vin is given to the gates and Vout is taken out. We take the Cload as ```10fF``` for now.
- Now we define the PMOS and NMOS width and length as ```0.375um``` and ```0.25um``` respectively. We give ```2.5V``` as Vdd and Vin. Common Vss is given.
- Identify the nodes, name them. Nodes are points between which a component is connected.
- We can now write the spice deck. We also specify the simulation type.
- We also import the model file for NMOS and PMOS for information of parameters related to transistors

![Screenshot from 2023-09-17 18-03-48](https://github.com/simarthethi/Advance_physical_design/assets/140998783/46060e6b-679b-44f8-894b-cbec87607c0e)

**Spice Simulation**

- We will run the simulation for the deck created with different widths and lengths for the PMOS and NMOS.

![Screenshot from 2023-09-17 18-05-10](https://github.com/simarthethi/Advance_physical_design/assets/140998783/f67ae84c-07af-45d8-856f-593128a9ac2b)

- From the waveform, irrespective of switching the shape of it are almost same. We can see the characteristics are maintained across all sizes of CMOS. So CMOS as a circuit is a robust device hence use in designing of logic gates. Parameters that define the robustness of the CMOS are

**Switching Threshold (Vm)**
        It is the point where out ```Vin = Vout```. To determine, we extend a 45 degree line from the origin.
        At this point, both the transistors are in saturation region, means both are turned on and have high chances of current flowing driectly from VDD to Ground called Leakage current.
        At this point, ```Vgs = Vds``` and ```Idsn = -Idsp```.

![Screenshot from 2023-09-17 18-07-00](https://github.com/simarthethi/Advance_physical_design/assets/140998783/38688c93-eae3-41d3-b191-a3ced4711603)

**Rise and Fall Delay**
- We will run a transient simulation and plot Vin and VOut with respect to time.
- To determine the Rise time, we take the rising input and corresponding falling output and note the time for ```Vdd/2``` i.e. 50% of the Vdd.
- For fall time, same is repeated but for the falling input and corresponding rising input.

**Steps to GIT CLONE vsdstdcelldesign**

- We will git clone a custom made repo for this course in the OpenLane directory of our local system.
```bash
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
- To invoke magic to view the sky130_inv.mag file, the sky130A.tech file must be included in the command along with its path. To ease up the complexity of this command, the tech file can be copied from the magic folder to the vsdstdcelldesign folder.

- Invertor Layout using Magic
![Screenshot from 2023-09-17 15-47-50](https://github.com/simarthethi/Advance_physical_design/assets/140998783/fd2de0bf-5fe8-47a8-bb92-edb10302aa89)


</details>

<details>
<summary>Inception of Layout and CMOS Fabrication Process</summary>

Under this section we will look into the Fabrication process. We will look into the various steps for 16-mask fab procedure

**16-MASK CMOS Process***

1. Selecting a substrate
- We choose an appropriate substrate as per requirement.
- We go with the most common substrate available - P-type.
   ![Screenshot from 2023-09-17 18-13-04](https://github.com/simarthethi/Advance_physical_design/assets/140998783/4f90f176-fc61-477e-aff7-89a91184c0ad)

2. Creation of Active regions for transistors
- We have to make isolation for each pocket, this is done by growing Silicon Dioxide of 40nm over the P-type substrate, then deposit an 80nm layer of Silicon nitride.
- Now deposit 1micron of photoresist. On this we make Mask1 and Mask 2 for the pockets and shower it with UV lights
- The photoresist under the masks are protected and remaining is etched away with some chemical reaction. Now the mask is removed.
- Now we etch off the extra silicon nitride, thus only silicon nitride left are the ones protected by the photoresist. Now Remove left photoresist.
- Now, place the entire thing in oxidation furnace. Silicon nitride protects the SiO2 underneath from growing further.
- The growth between the nitride layer acts as the isolation as they don't allow the transistor areas to communicate. This growth is also called bird's beak.
- The remaining nitride layer is etched off.
- This whole process is called LOCOS - Local oxidation of Silicon image
![Screenshot from 2023-09-17 18-21-59](https://github.com/simarthethi/Advance_physical_design/assets/140998783/d2a84c8d-1eba-402f-b8e5-7f45f18f767c)

3. Formation of N-Well and P-Well
- The N-well and P-well regions are created separately.
- P-well formation involves photolithography and ion implantation of p-type Boron material into the p-substrate. Energy required is 200keV.
- N-well is formed similarly with n-type Phosphorus material. Energy requirement is 400keV.
- This ion implantation damages the SiO2 layer.
- High-temperature furnace processes drive-in diffusion to establish well depths, known as the twin-tub process.
![Screenshot from 2023-09-17 18-23-46](https://github.com/simarthethi/Advance_physical_design/assets/140998783/a06852e6-c614-41f1-8663-e52e75636a20)

4.Formation of Gate Terminal
- Gate is the most important terminal as here we control the input voltage.
- Important parameters for gate formation include oxide capacitance and doping concentration.
- A polysilicon layer is deposited and photolithography techniques are applied to create NMOS and PMOS gates.
- The SiO2 layers over Nwell and Pwell are etched off using polysulpuric acid and fresh layer is made with goof thickness.
![Screenshot from 2023-09-17 18-24-29](https://github.com/simarthethi/Advance_physical_design/assets/140998783/6c609940-98bb-4962-b702-a8c4036e9fbb)

5.Lightly-Doped Drain(LDD) Formation
- This is done to achieve a doping profile --> P+, P-, N for NMOS and N+, N- and P for PMOS.
- LDD is created to control hot electron and short channel effects.
![Screenshot from 2023-09-17 18-24-52](https://github.com/simarthethi/Advance_physical_design/assets/140998783/8a5f1c79-85ca-40b0-b92b-42703b647e5b)

6.Source and Drain Formation
- Thin oxide layers are added to avoid channel effects during ion implantation.
- N+ and P+ implants are performed using Arsenic implantation and high-temperature annealing.
![Screenshot from 2023-09-17 18-25-23](https://github.com/simarthethi/Advance_physical_design/assets/140998783/f193716b-845d-42fb-a1d1-f4982308970a)

7.Local Interconnect Formation
- Thin screen oxide is removed through etching in HF solution.
- Titanium deposition through sputtering is initiated.
- Heat treatment results in chemical reactions, producing low-resistant titanium silicon dioxide for interconnect contacts and titanium nitride for top-level connections, enabling local communication.
![Screenshot from 2023-09-17 18-25-32](https://github.com/simarthethi/Advance_physical_design/assets/140998783/30ca77c0-4074-4437-ae5d-110e647a984c)

8.Higher Level Metal Formation
- To achieve suitable metal interconnects, non-planar surface topography is addressed.
- Chemical Mechanical Polishing (CMP) is utilized by doping silicon oxide with Boron or Phosphorus to achieve surface planarization.
- TiN and blanket Tungsten layers are deposited and subjected to CMP.
- An aluminum (Al) layer is added and subjected to photolithography and CMP.
- This constitutes the first level of interconnects, and additional interconnect layers are added to reach higher-level metal layers.
![Screenshot from 2023-09-17 18-25-48](https://github.com/simarthethi/Advance_physical_design/assets/140998783/25975269-616c-4366-a14a-862bec7b64fb)

9.Dielectric Layer Addition
- Finally, a dielectric layer, typically Si3N4, is applied to safeguard the chip.

This complex process results in the creation of advanced integrated circuits with multiple layers of interconnects, essential for modern electronic devices.

**Introduction to SKY130 Basic Layout and LEF**

From Layout, we see the layers which are required for CMOS inverter. Inverter is, PMOS and NMOS connected together.

- Gates of both PMOS and NMOS are connected together and fed to input(here ,A), NMOS source connected to ground(here, VGND), PMOS source is connected to VDD(here, VPWR), Drains of PMOS and NMOS are connected together and fed to output(here, Y).
- The First layer in skywater130 is localinterconnect layer(locali) , above that metal 1 is purple color and metal 2 is pink color.
- If we want to see connections between two different parts, place the cursor over that area and press S one times. The tkson window gives the component name.
![Screenshot from 2023-09-17 21-57-02](https://github.com/simarthethi/Advance_physical_design/assets/140998783/fb4fa745-5840-4383-9e34-64b0bad4ea2e)

**LEF - Library Exchange File**

-    The layout of a design is defined in a specific file called LEF.
-    It includes design rules (tech LEF) and abstract information about the cells.
        - Tech LEF - Technology LEF file contains information about the Metal layer, Via Definition and DRCs.
        - Macro LEF - Contains physical information of the cell such as its Size, Pin, their direction.

**Designing standard cell**

- First we need to provide bounding box width and height in tkson window. lets say that width of BBOX is 1.38u and height is 2.72u. The command to give these values to MAGIC is ```property Fixed BBOX (0 0 1.32 2.72)```
- After this, Vdd, GND segments which are in metal 1 layer, their respective contacts and atlast logic gates layout is defined Inorder to know the logical functioning of the inverter, we extract the spice and then we do simulation on the spice.

**SPICE extraction in MAGIC**

To extract it on spice we open TKCON window, the steps are :

-    Know the present directory - pwd
- create an extration file - the command is ```extract all``` and ```sky130_inv.ext``` files has been created
- create spice file using .ext file to be used with our ngspice tool - the commands are
        - ```ext2spice cthresh 0 rthresh 0``` - extracts parasatic capcitances also since these are actual layers - nothing is created in the folder
        - ```ext2spice``` - a file sky130_inv.spice has been created.
![Screenshot from 2023-09-17 16-53-03](https://github.com/simarthethi/Advance_physical_design/assets/140998783/72efc390-38a4-4685-8fb7-75651fdba9e4)

</details>

<details>
<summary>Lab on sky130A tech file</summary>

Under this section, we will go over how to infer the spice deck file and how to run the transient analysis using NGspice. Once the simulation is done, we will characterise the simulation plot.

**Spice Deck**

- The design is scaled to 0.01u
- The NMOS and PMOS are defined as
        - ```cell_name drain_node gate_node source_node model_file_name```
```bash
M1000 Y A VGND VGND nshort_model.0 w=35 l=23
M1001 Y A VPWR VPWR pshort_model.0 w=37 l=23
```

- We will include the model files for NMOS and PMOS from the ```libs``` directory.

```bash
 .include ./libs/nshort.lib
 .include ./libs/pshort.lib
```


- Now, we set up the connections to the nodes with ground, Vdd and input pulses.
        - VGND to VSS 0V
        - Supply voltage VPWR to GND.
        - Sweeping a pulse input.
- Now we set the transient analysis.
```bash
VDD VPWR 0 3.3V
VSS VGND 0 0V
Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns)
.tran 1n 20n
.control
run
.endc
.end
```
-final Spice deck for simulation
![Screenshot from 2023-09-17 17-06-21](https://github.com/simarthethi/Advance_physical_design/assets/140998783/e760261c-6f5f-45e6-8e8b-e27edaa763f6)

**NGpsice Simulation and Characterization**
-  Code to run the simulation
```bash
ngspice sky130_inv.spice
```
![Screenshot from 2023-09-17 17-37-29](https://github.com/simarthethi/Advance_physical_design/assets/140998783/8b5c617b-082b-416c-883e-5756b7b3a433)

-  To get the plot for output against time with the sweeping input
```bash
plot y vs time a
```
![Screenshot from 2023-09-17 19-09-21](https://github.com/simarthethi/Advance_physical_design/assets/140998783/845f53d8-daef-42b3-8939-04e4b74de212)


- Now we have to characterise the plot.
- There are four timing parameters used to characterize the inverter standard cell:
        - Rise transition - Time taken for the output to rise from 20% to 80% of max value => ```2.240 - 2.143 = 0.067ns```
        - Fall Transition - Time taken for the output to fall from 80% to 20% of max value => ```4.0921 - 4.049 = 0.0431ns```
        - Cell Rise delay - Difference in time(50% output rise) to time(50% input fall) => ```2.17333 - 2.13 = 0.0433ns```
        - Cell Fall delay - Difference in time(50% output fall) to time(50% input rise) => ```4.076 - 4.0501 = 0.0259ns```

**DRC Challenges**

Under this section, we will go over

- In-depth overview of Magic's DRC engine
- Introduction to Google/Skywater DRC rules
- Lab : Warm-up exercise : Fixing a simple rule error
- Lab : Main exercie : Fixing or create a complex error

**Introdution to Magic and Skywater PDK**

*Lab Setup*

- Setup to view the layouts
- For extracting and generating views, Google/skywater repo files were built with Magic
- Technology file dependency is more for any layout. hence, this file is created first.
- Since, Pdk is still under development, there are some unfinished tech files and these are packaged for magic along with lab exercise layout and bunch of stuff into the tar ball

```bash
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
```
- Once we have downloaded the archive in the home directory, we extract it to get the lab .mag files

![Screenshot from 2023-09-17 19-14-48](https://github.com/simarthethi/Advance_physical_design/assets/140998783/bf25a7c9-4aa4-43e3-84bc-0a967d46339c)

- There is a hidden file ```.magicrc``` which directs to the various resources for the lab work ahead.
```bash
magic -d XR
```
![Screenshot from 2023-09-17 22-32-35](https://github.com/simarthethi/Advance_physical_design/assets/140998783/627594f5-1abe-4d2f-b584-e6671a10e096)

- Other way to load it is by defining the name while running magic.
```bash
magic -d XR <file_name>.mag
```
- We will open up met3.mag
- We see multiple independent example metal layouts with some DRC errors. We can refer these errors in the the Skywater PDK design rules which are flageed in the DRC engine.
- We can make a frame around a metal region and in command window write ```drc why``` --> this gives us the DRC violated.

![Screenshot from 2023-09-17 22-36-15](https://github.com/simarthethi/Advance_physical_design/assets/140998783/aef1df1e-68f1-4f46-aa79-86444093c77f)

- Magic uses a lot of derived layers. To see these layers we can make a large box area and use following commands to see metal cut
```bash
cif see VIA2
```

***LAB***

*Exercise 1*


- Load the poly.mag
- Check the drc violation for poly.9
- Refer the error using skywater pdk design rules
        - We find that distance between regular polysilicon & poly resistor should be 22um but it is showing 17um and still no errors . We should go to sky130A.tech file and modify as follows to detect this error.
- In line this

```bash
*******************************************************
spacing npres *nsd 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"
*******************************************************
```
edit 
```bash
*******************************************************
spacing npres allpolynonres 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"
*******************************************************
```
Next edit. In line shown
```bash
*******************************************************
spacing xhrpoly,uhrpoly,xpc alldiff 480 touching_illegal \
	"xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"
*******************************************************
```
edit
```bash
*******************************************************
spacing xhrpoly,uhrpoly,xpc allpolynonres 480 touching_illegal \
	"xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"
*******************************************************
```
- After this, we ```tech load sky130.tech``` file and execute ```drc check```

![Screenshot from 2023-09-17 22-41-49](https://github.com/simarthethi/Advance_physical_design/assets/140998783/3ccd5dc8-a877-42e7-8ab7-ed0531349b6b)

- We can select ```poly.9``` and run ```drc why``` to check for errors. Now its fine.

![Screenshot from 2023-09-17 22-43-04](https://github.com/simarthethi/Advance_physical_design/assets/140998783/620118e0-82e0-4c55-a115-85f0aa73d52f)

</details>
        
# Day 4

<details>
<summary>Timing Analysis and Clock Tree Synthesis (CTS)</summary>

**Standard Cell LEF generation**

During Placement, entire mag information is not necessary. Only the PR boundary, I/O ports, Power and ground rails of the cell is required. This information is defined in LEF file. The main objective is to extract lef from the mag file and plug into our design flow.

**Grid into Track info**

*Track* :A path or a line on which metal layers are drawn for routing. Track is used to define the height of the standard cell.

To implement our own stdcell, few guidelines must be followed

- I/O ports must lie on the intersection on Horizontal and vertical tracks
- Width and Height of standard cell are odd mutliples of Horizontal track pitch and Vertical track pitch

This information is defined in tracks.info.
```bash
/.volare/sky130A/libs.tech/openlane/sky130_fd_sc_hd/tracks.info
```
```bash
li1 X 0.23 0.46
li1 Y 0.17 0.34
met1 X 0.17 0.34
met1 Y 0.17 0.34
met2 X 0.23 0.46
met2 Y 0.23 0.46
met3 X 0.34 0.68
met3 Y 0.34 0.68
met4 X 0.46 0.92
met4 Y 0.46 0.92
met5 X 1.70 3.40
met5 Y 1.70 3.40
```
- It tells us about all the metal layers as such.
- We learnt that the input port and output for should be on the intersection of horizontal and vertical tracks, to verify this we set the grids as 
```bash
grid 0.46um 0.34um 0.23um 0.17um
```
![Screenshot from 2023-09-18 00-54-21](https://github.com/simarthethi/Advance_physical_design/assets/140998783/c5ad194a-6231-453e-90e1-a930e306d82d)

- The second condition is also verified. The X-pitch is 0.46 and we can see that the standard cell is 3 times that, thus an odd multiple.
- The same can be verified for the height of the standard cell.

**Creation of Ports**

- Once the layout is ready, the next step is extracting LEF file for the cell.

- Certain properties and definitions need to be set to the pins of the cell. For LEF files, a cell that contains ports is written as a macro cell, and the ports are the declared as PINs of the macro.

- Our objective is to extract LEF from a given layout (here of a simple CMOS inverter) in standard format. Defining port and setting correct class and use attributes to each port is the first step.

- Method for definng ports
	- In Magic Layout window, first source the .mag file for the design (here inverter). Then Edit >> Text which opens up a dialogue box.
	- For each layer (to be turned into port), make a box on that particular layer and input a label name along with a sticky label of the layer name with which the port needs to be associated. Ensure the Port enable checkbox is checked and default checkbox is unchecked.
![Screenshot from 2023-09-18 00-59-56](https://github.com/simarthethi/Advance_physical_design/assets/140998783/695d66ac-cc9b-487c-b6e7-0af54a353fc9)


- Port A (input port) and port Y (output port) are taken from locali (local interconnect) layer. Also, the number in the textarea near enable checkbox defines the order in which the ports will be written in LEF file (0 being the first).
- For power and ground layers, the definition could be same or different than the signal layer. Here, ground and power connectivity are taken from metal1 (Notice the sticky label).

**Port Class and Port Use Attributes**

- After defining ports, the next step is setting port class and port use attributes.
- Select port A in magic:
```bash
port class input
port use signal
```
- Select Y area
```bash
port class output
port use signal
```
- Select VPWR area
```bash
port class inout
port use power
```
- Select VGND area
```bash
port class inout
port use ground
```
![Screenshot from 2023-09-17 23-45-29](https://github.com/simarthethi/Advance_physical_design/assets/140998783/99dd7c34-6770-480b-b396-28612a7554d0)

![Screenshot from 2023-09-17 23-46-11](https://github.com/simarthethi/Advance_physical_design/assets/140998783/55bfb6ed-81ff-48c6-972d-14848394aa1d)

**Extraction of LEF file**

- Name the custom cell through tkcon window as sky130_shant.mag.
- We generate lef file by command:
```bash
lef write
```
- Upon checking the directory, we can see the lef file being generated.
![Screenshot from 2023-09-18 00-00-04](https://github.com/simarthethi/Advance_physical_design/assets/140998783/b0dfd7e0-39de-4025-8e45-f315dfcb1d94)
- lef file generated.
![Screenshot from 2023-09-18 00-01-10](https://github.com/simarthethi/Advance_physical_design/assets/140998783/6e02681e-34f7-47bd-a405-7cb16365f00a)

![Screenshot from 2023-09-18 00-01-15](https://github.com/simarthethi/Advance_physical_design/assets/140998783/e06a94a1-0ff4-439e-9427-7242d24fab31)

**Including Custom Cell ASIC Design**

- First, we transfer the lef file generated ```sky130_simar.lef``` into the ```/home/simar-thethi/OpenLane/designs/picorv32a/src``` directory.

- Then we will transfer the ```sky130_fd_sc_hd__fast.lib```, ```sky130_fd_sc_hd__slow.lib``` and ```sky130_fd_sc_hd__typical.lib``` into the same directory.

- For this, we edit the config.json file as below
```bash
{
  "DESIGN_NAME": "picorv32",
  "VERILOG_FILES": "dir::src/picorv32a.v",
  "CLOCK_PORT": "clk",
  "CLOCK_NET": "clk",
  "FP_SIZING": "relative",
  "GLB_RESIZER_TIMING_OPTIMIZATIONS": true,
  "LIB_SYNTH" : "dir::src/sky130_fd_sc_hd__typical.lib",
  "LIB_FASTEST" : "dir::src/sky130_fd_sc_hd__fast.lib",
  "LIB_SLOWEST" : "dir::src/sky130_fd_sc_hd__slow.lib",
  "LIB_TYPICAL":"dir::src/sky130_fd_sc_hd__typical.lib",
  "TEST_EXTERNAL_GLOB":"dir::/src/*",
  "SYNTH_DRIVING_CELL":"sky130_vsdinv",
  "pdk::sky130*": {
    "FP_CORE_UTIL": 35,
    "CLOCK_PERIOD": 24,
    "scl::sky130_fd_sc_hd": {
      "FP_CORE_UTIL": 30
    }
  }
}
```
Now, we integrate standard cell on OpenLane flow after make mount, and follow up
```bash
prep -design picorv32a -tag RUN_2023.09.16_08.19.33 -overwrite 
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```

![Screenshot from 2023-09-18 01-17-54](https://github.com/simarthethi/Advance_physical_design/assets/140998783/8c49ae86-3188-4eec-a9db-0c9890723a88)

- Synthesis log file
![Screenshot from 2023-09-18 01-19-36](https://github.com/simarthethi/Advance_physical_design/assets/140998783/e7c0860d-dcee-4dff-86dc-7340b521e144)

- Static timing analysis (STA) log file
![Screenshot from 2023-09-18 01-20-41](https://github.com/simarthethi/Advance_physical_design/assets/140998783/ce0a1980-d154-4e07-80ff-1bf68a3610ef)

**Delay Table**

Delay is a parameter that has huge impact on our cells in the design. Delay decides each and every other factor in timing. For a cell with different size, threshold voltages, delay model table is created where we can it as timing table.

-  Delay of a cell depends on input transition and out load.

Lets say two scenarios, we have long wire and the cell(X1) is sitting at the end of the wire : the delay of this cell will be different because of the bad transition that caused due to the resistance and capcitances on the long wire. we have the same cell sitting at the end of the short wire: the delay of this will be different since the tarn is not that bad comapred to the earlier scenario. Eventhough both are same cells, depending upon the input tran, the delay got chaned. Same goes with o/p load also.

VLSI engineers have identified specific constraints when inserting buffers to preserve signal integrity. They've noticed that each buffer level must maintain consistent sizing, but their delays can vary depending on the load they drive. To address this, they introduced the concept of "delay tables", which essentially consist of 2D arrays containing values for input slew and load capacitance, each associated with different buffer sizes. These tables serve as timing models for the design.

When the algorithm works with these delay tables, it utilizes the provided input slew and load capacitance values to compute the corresponding delay values for the buffers. In cases where the precise delay data is not readily available, the algorithm employs a technique of interpolation to determine the closest available data points and extrapolates from them to estimate the required delay values.

![Screenshot from 2023-09-18 01-22-09](https://github.com/simarthethi/Advance_physical_design/assets/140998783/cf70499d-debe-41ac-a762-b7dff2a01919)

**Custom Cell inclusion in OpenLane Flow**

- We have seen till the synthesis for the custom standard cell in OpenLane flow, and verified the synthesis and STA log files. We will pick it from there now.

- First check the slack for the synthesis.

- The slack was positive, therefore we can proceed, else would have to work on the slack.

- Now we run the floorplan and placement processes.
```bash
run_floorplan
run_placement
```
![Screenshot from 2023-09-18 01-25-07](https://github.com/simarthethi/Advance_physical_design/assets/140998783/38e7fe85-59e9-42dc-98f8-b7329699b403)

- Now, we check for legality &To check the layout invoke magic from the ```results/placement``` directory

![Screenshot from 2023-09-18 01-27-14](https://github.com/simarthethi/Advance_physical_design/assets/140998783/eeac82c8-5fe2-42d7-97e3-7210ee8f9dbc)

</details>

<details>
<summary>Timing Analysis with Ideal Clocks using OpenSTA </summary>

Set-up Timing Analysis

- Right now, we will consider the ideal clocks, thus the clock tree are not yet made.
- We take a single clock and anlysis launch and capture flops. 

![image](https://github.com/simarthethi/Advance_physical_design/assets/140998783/89706c18-fbd5-4368-883d-ccf5af64536c)

- In this, we assume that launch flop is triggered at the first posedge of clk and the capture flop recieves the value at the next posedge.
- Suppose there was some combinational logic between the two, the delay of the logic should be less than the time period of the clock.
- Thus the clock frequency and time period, and the combinational logic are designed with correspondence to each other.
- Therefore my setup time for the combinational logic should be less than the time period of the clock.
- Now, we will look into more real and practical conditions.
- We look into the capture flop. It is made of multiple gates and muxes, which will have there mosfets, resistances and capacitances.
- Thus will have delay associated to them.

![image](https://github.com/simarthethi/Advance_physical_design/assets/140998783/a661ebab-a435-449c-87f9-278168bfb4cd)


- Suppose the flop was developed with 2 muxes as shown. We have to condsider the delays.
- This affect the combinational logic delay requirement. Now, the clock period T is not avaiable. The capture flop needs some setup time.
- Thus the time avaiable for the combinational logic now is T - setupTime of capture flop.
- Clock Jitter - clock is generated from PLL which has inbuilt circuit which cells and some logic. There might variations in the clock generation depending upon the ckt. These variations are collectivity known as clock uncertainity. In that jitter is one of the parameter. It is uncertain that clock might come at that exact time withought any deviation.
- That is why it is called clock_uncertainity Skew, Jitter and Margin comes into clock_uncertainity

![image](https://github.com/simarthethi/Advance_physical_design/assets/140998783/2c7ac8c9-e697-4c12-b4eb-e8801b3e18af)

**Post-Synthesis Analysis using OpenSTA**

Timing analysis is carried out outside the OpenLANE flow using OpenSTA tool. For this, pre_sta.conf is required to carry out the STA analysis. Invoke OpenSTA outside the openLANE flow as follows:
```bash
sta pre_sta.conf
```
Since clock tree synthesis has not been performed yet, the analysis is with respect to ideal clocks and only setup time slack is taken into consideration. The slack value is the difference between data required time and data arrival time. The worst slack value must be greater than or equal to zero. If a negative slack is obtained, following steps may be followed:

- Change synthesis strategy, synthesis buffering and synthesis sizing values
- Review maximum fanout of cells and replace cells with high fanout
- sdc file for OpenSTA is modified.

```base.sdc``` is located in ```vsdstdcelldesigns/extras``` directory. So, we copy it into our design folder using ```cp my_base.sdc /home/simar-thethi/OpenLane/designs/picorv32a/src/```

![Screenshot from 2023-09-18 10-14-38](https://github.com/simarthethi/Advance_physical_design/assets/140998783/7390b453-65e8-4382-93cc-59e0872f60a0)


From the timing report, we can improve slack by upsizing the cells i.e., by replacing the cells with high drive strength and we can see significant changes in the slack. Since there were no timing violations, we can skip this step.

Since clock is propagated only once we do CTS, In placement stage, clock is considered to be ideal. So only setup slack is taken into consideration before CTS.

 </details>

<details>
<summary> Clock Tree Synthesis TritonCTS and Signal Integrity </summary>

- This plays a vital role in the creation of integrated circuits (ICs), particularly in the realm of digital electronics, where precise timing is of utmost importance. CTS involves the establishment of an organized network or structure of pathways for distributing the clock signal within the IC. This meticulous process guarantees that the clock signal effectively reaches all the sequential components, such as flip-flops and registers, in a synchronized and punctual fashion.

-    It can be implemeted in various ways and the choice of the specific technique depends on the design requirements, constraints, and goals.

-    Some of the different types of approches to clock tree synthesis are:

Balanced Tree CTS:
The clock signal is spread out evenly, like branches of a tree. This helps ensure that all parts of the chip get the clock at about the same time, reducing timing problems. It's a straightforward method, but it might not save as much power as other methods.

H-tree CTS:
It is like a tree shape with the letter "H." It's great for spreading out clock signals across big chips. This tree structure helps make sure the timing is good and saves power, especially in large areas of the chip.

Star CTS:
In a star CTS, the clock signal is distributed from a single central point (like a star) to all the flip-flops. This approach simplifies clock distribution and minimizes clock skew but may require a higher number of buffers near the source.

Mesh CTS:
In a mesh CTS, clock wires are arranged in a mesh-like grid pattern, and each flip-flop is connected to the nearest available clock wire. It is often used in highly regular and structured designs, such as memory arrays. Mesh CTS can offer a balance between simplicity and skew minimization.

Adaptive CTS:
Adaptive CTS techniques adjust the clock tree structure dynamically based on the timing and congestion constraints of the design. This approach allows for greater flexibility and adaptability in meeting design goals but may be more complex to implement.

**Crosstalk in VLSI**

- Crosstalk in VLSI refers to unwanted interference or coupling between adjacent conductive traces or wires on an integrated circuit (IC) or chip.
- It occurs when the electrical signals on one wire influence or disrupt the signals on neighboring wires.Uncontrolled crosstalk can lead to data corruption, timing violations, and increased power consumption.
- Mitigation: VLSI designers employ various techniques to mitigate crosstalk, such as optimizing layout and routing, using appropriate shielding, implementing proper clock distribution strategies, and utilizing clock gating to reduce dynamic power consumption when logic is idle

**Clock net sheilding in VLSI**

- Clock net shielding in VLSI refers to a technique used to protect the clock signal from interference or crosstalk. The clock signal is critical for synchronizing the operations of various components on a chip, and any interference can lead to timing issues and performance problems.
- VLSI designers may use shielding techniques to isolate the clock network from other signals, reducing the risk of interference. This can include dedicated clock routing layers, clock tree synthesis algorithms, and buffer insertion to manage clock distribution more effectively.
- VLSI designs often have multiple clock domains. Shielding and proper clock gating help ensure that clock signals do not propagate between domains, avoiding metastability issues and maintaining synchronization.

Note - In this stage clock is propagated and make sure that clock reaches each and every clock pin from clock source with mininimum skew and insertion delay. Inorder to do this, we implement H-tree using mid point strategy. For balancing the skews, we use clock invteres or bufferes in the clock path. Before attempting to run CTS in TritonCTS tool, if the slack was attempted to be reduced in previous run, the netlist may have gotten modified by cell replacement techniques. Therefore, the verilog file needs to be modified using the ```write_verilog``` command. Then, the synthesis, floorplan and placement is run again.

LAB Continued

- We will continue after the synthesis, floorplan and placement. We run the CTS as
```bash
run_cts
```
![Screenshot from 2023-09-18 02-11-19](https://github.com/simarthethi/Advance_physical_design/assets/140998783/7cd4aa4f-df56-468a-b7c8-03a98a3fac0a)




 
</details>

<details>
<summary>Timing Analysis with Real Clocks using OpenSTA</summary>

- Analyzing setup time is a crucial element of designing digital circuits, especially in synchronous digital systems.
- It pertains to the duration during which a signal must remain steady and valid prior to the arrival of the clock edge.
- Guaranteeing the fulfillment of setup time prerequisites is vital for averting data errors and securing the correct functioning of the digital circuit.

![image](https://github.com/simarthethi/Advance_physical_design/assets/140998783/64d56528-8a4b-4491-80c3-d64aca2a0bac)



- To ensure the setup time requirements are met we need to make sure of some things:

    Selecting proper Filp flops or latches.
    Optimize combinational logic
    Clock Skew Analysis
    Timing constraints
- Meeting setup time requrirements is cruical for a good digital circuit operation. If not done can result in data errors and multifunctioning of the circuit.

**Holding Timing Analysis using Real Clock**

- Analysis of hold time is an equally vital component of digital circuit design, especially in synchronous systems.
- It concerns the minimum duration during which a data input (D) needs to maintain its stability and validity after the clock edge before any changes can occur.
- Ensuring that hold time requirements are met is essential to prevent data corruption and ensure the proper operation of digital circuits.
![image](https://github.com/simarthethi/Advance_physical_design/assets/140998783/644e119b-1178-48d6-987f-ac2fde0f9800)

**LAB continued**
```bash
openroad
read_lef /home/shant/OpenLane/designs/picorv32a/runs/RUN_2023.09.11_06.05.06/tmp/merged.nom.lef 
read_def /home/shant/OpenLane/designs/picorv32a/runs/RUN_2023.09.11_06.05.06/results/cts/picorv32.def 
read_verilog /home/shant/OpenLane/designs/picorv32a/runs/RUN_2023.09.11_06.05.06/results/synthesis/picorv32.v
write_db pico_cts.db
read_db pico_cts.db
read_verilog /home/shant/OpenLane/designs/picorv32a/runs/RUN_2023.09.11_06.05.06/results/synthesis/picorv32.v
link_design picorv32
read_liberty $::env(LIB_SYNTH_COMPLETE)
read_sdc /home/shant/OpenLane/designs/picorv32a/src/my_base.sdc
set_propagated_clock (all_clocks)
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```

- Since, clock is propagated, from this stage, we do timing analysis with real clocks. From now post cts analysis is performed by operoad within the openlane flow
- Hold Slack
![Screenshot from 2023-09-18 11-03-56](https://github.com/simarthethi/Advance_physical_design/assets/140998783/bc447aa4-ff81-4fb9-9fff-aaa7cd053d85)

- Setup Slack
![Screenshot from 2023-09-18 11-04-04](https://github.com/simarthethi/Advance_physical_design/assets/140998783/819839ec-826d-41f1-9b7a-c3eb4c70db01)

</details>

# Day 5

<details>
<summary>Routing and Design Rule Check</summary>

**Maze Routing and Lee's Algorithm**

- Routing is the process of establishing a physical connection between two pins. Algorithms designed for routing take source and target pins and aim to find the most efficient path between them, ensuring a valid connection exists.
- The Maze Routing algorithm, such as the Lee algorithm, is one approach for solving routing problems.Here a grid similar to the one created during cell customization is utilized for routing purposes.
- The Lee algorithm starts with two designated points, the source and target, and leverages the routing grid to identify the shortest or optimal route between them.
- Lee's Algorithm has its limitations. It can be time consuming when dealing with millions of pins.It essentially constructs a maze and then numbers its cells from the source to the target. here are alternative algorithms that address similar routing challenges.
- Here in this case he shortest path is one that follows a steady increment of one.There might be multiple paths, but the best path that the tool will choose is one with less bends.The route should not be diagonal and must not overlap an obstruction such as macros. The Lee algorithm prioritizes selecting the best path, typically favoring L-shaped routes over zigzags. If no L-shaped paths are available, it may resort to zigzag routes. This approach is particularly valuable for global routing tasks.
- This algorithm however has high run time and consume a lot of memory thus more optimized routing algorithm is preferred .
![image](https://github.com/simarthethi/Advance_physical_design/assets/140998783/48e7db0b-7a24-40cf-af11-133f711ec6d5)

**Design Rule Check**

- Design rule checks are physical checks of metal width, pitch and spacing requirement for the different layers which depend on different technology nodes.It verifies whether a design meets the predefined process technology rules given by the foundry for its manufacturing.

- The layout of a design must be in accordance with a set of predefined technology rules given by the foundry for manufacturability. After completion of the layout and its physical connection, an automatic program will check each and every polygon in the design against these design rules and report any violations.

![image](https://github.com/simarthethi/Advance_physical_design/assets/140998783/6e65848a-70c7-4102-b059-6c816bb4632b)
 
</details>

<details>
<summary>Power Distribution Network and Routing</summary>

- Unlike the general ASIC flow, Power Distribution Network generation is not a part of floorplan run in OpenLANE. PDN must be generated after CTS and post-CTS STA analyses:
- We can check whether PDN has been created or no by check the current def environment variable: ```echo $::env(CURRENT_DEF)```
```bash
gen_pdn
```
![Screenshot from 2023-09-18 23-56-23](https://github.com/simarthethi/Advance_physical_design/assets/140998783/24df2f2b-2c5e-4cb8-a765-ad870597aaff)

- gen_pdn Generates the power distribution network.
- The power distribution network has to take the design_cts.def as the input def file.
- Power rings,strapes and rails are created by PDN.
- From VDD and VSS pads, power is drawn to power rings.
- Next, the horizontal and vertical strapes connected to rings draw the power from strapes.
- Stapes are connected to rings and these rings are connected to std cells. So, standard cells get power from rails.
- Here are definitions for the straps and the rails. In this design, straps are at metal layer 4 and 5 and the standard cell rails are at the metal layer 1. Vias connect accross the layers as required.

![image](https://github.com/simarthethi/Advance_physical_design/assets/140998783/0f438984-93f4-4429-a754-48cf0e514696)

 
</details>
<details>
<summary>Routing</summary>

In the realm of routing within Electronic Design Automation (EDA) tools, such as both OpenLANE and commercial EDA tools, the routing process is exceptionally intricate due to the vast design space. To simplify this complexity, the routing procedure is typically divided into two distinct stages: Global Routing and Detailed Routing.

- The two routing engines responsible for handling these two stages are as follows:

	-    Global Routing:

    In this stage, the routing region is subdivided into rectangular grid cells and represented as a coarse 3D routing graph. This task is accomplished by the "FASTE ROUTE" engine.

	-    Detailed Routing:

    Here, finer grid granularity and routing guides are employed to implement the physical wiring. The "tritonRoute" engine comes into play at this stage. "Fast Route" generates initial routing guides, while "Triton Route" utilizes the Global Route information and further refines the routing, employing various strategies and optimizations to determine the most optimal path for connecting the pins.

Key Features of TritonRoute

- Initial Detail Routing: TritonRoute initiates the detailed routing process, providing the foundation for the subsequent routing steps.

-    Adherence to Pre-Processed Route Guides: TritonRoute places significant emphasis on following pre-processed route guides. This involves several actions:

-    Initial Route Guide Analysis: TritonRoute analyzes the directions specified in the preferred route guides. If any non-directional routing guides are identified, it breaks them down into unit widths.

-    Guide Splitting: In cases where non-directional routing guides are encountered, TritonRoute divides them into unit widths to facilitate routing.

-    Guide Merging: TritonRoute merges guides that are orthogonal (touching guides) to the preferred guides, streamlining the routing process.

-    Guide Bridging: When it encounters guides that run parallel to the preferred routing guides, TritonRoute employs an additional layer to bridge them, ensuring efficient routing within the preprocessed guides.

Assumes route guide for each net satisfy inter guide connectivity Same metal layer with touching guides or neighbouring metal layers with nonzero vertically overlapped area( via are placed ).each unconnected termial i.e., pin of a standard cell instance should have its pin shape overlapped by a routing guide( a black dot(pin) with purple box(metal1 layer))

**TritonRoute problem statement**
```bash
Inputs : LEF, DEF, Preprocessed route guides
Output : Detailed routing solution with optimized wire length and via count
Constraints : Route guide honoring, connectivity constraints and design rules.
```
The space where the detailed route takes place has been defined. Now TritonRoute handles the connectivity in two ways.

- Access Point(AP) : An on-grid point on the metal of the route guide, and is used to connect to lower-layer segments, pins or IO ports,upper-layer segments. Access Point Cluster(APC) : A union of all the Aps derived from same lower-layer segment, a pin or an IO port, upper-layer guide.

**TritonRoute run for routing**

Make sure the CURRENT_DEF is set to pdn.def
- Start routing by using
```bash
run_routing
```
![Screenshot from 2023-09-18 23-57-59](https://github.com/simarthethi/Advance_physical_design/assets/140998783/1602934c-fef9-4ef9-a247-a0a6ae6cbd3f)


![Screenshot from 2023-09-18 02-40-57](https://github.com/simarthethi/Advance_physical_design/assets/140998783/962a76a5-f183-4880-a1df-c7e43bd74497)

**Layout in magic tool post routing**

- The design can be viewed on magic within results/routing directory. Run the follwing command in that directory:
```bash
magic -T ~/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def &
```
![Screenshot from 2023-09-18 16-50-39](https://github.com/simarthethi/Advance_physical_design/assets/140998783/7a5e2c7e-b37e-4a29-ba1d-727288779aa7)

![Screenshot from 2023-09-18 16-59-46](https://github.com/simarthethi/Advance_physical_design/assets/140998783/94c56d6c-c293-44bd-a330-bd44dabf8adc)




 
</details>
