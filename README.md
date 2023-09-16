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

<details/>

# Day 2        
<details>
        
<summary>Chip FLoorplanning consideration</summary>
        
</details>


        
