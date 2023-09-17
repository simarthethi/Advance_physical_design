# Advance Physical Design using OpenLane and sky130 PDK

This github repository contains the progress made in Advance Physical design using OpneLane and sky130 PDK tools

[Day 1](#day-1)

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
        -We choose an appropriate substrate as per requirement.
        -We go with the most common substrate available - P-type.
   ![Screenshot from 2023-09-17 18-13-04](https://github.com/simarthethi/Advance_physical_design/assets/140998783/4f90f176-fc61-477e-aff7-89a91184c0ad)

2. Creation of Active regions for transistors
        -We have to make isolation for each pocket, this is done by growing Silicon Dioxide of 40nm over the P-type substrate, then deposit an 80nm layer of Silicon nitride.
        -Now deposit 1micron of photoresist. On this we make Mask1 and Mask 2 for the pockets and shower it with UV lights
        -The photoresist under the masks are protected and remaining is etched away with some chemical reaction. Now the mask is removed.
        -Now we etch off the extra silicon nitride, thus only silicon nitride left are the ones protected by the photoresist. Now Remove left photoresist.
        -Now, place the entire thing in oxidation furnace. Silicon nitride protects the SiO2 underneath from growing further.
        -The growth between the nitride layer acts as the isolation as they don't allow the transistor areas to communicate. This growth is also called bird's beak.
        -The remaining nitride layer is etched off.
        -This whole process is called LOCOS - Local oxidation of Silicon

image

        
</details>
        
