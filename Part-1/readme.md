# Day-1: Physical Design Workshop  

## [Inception of open-source EDA, OpenLANE and Sky130 PDK](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#inception-of-open-source-eda-openlane-and-sky130-pdk)  

- [How to talk to computers](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#how-to-talk-to-computers)  
- [Introduction to QFN-48 Package, chip, pads, core, die and IPs](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#introduction-to-qfn-48-package-chip-pads-core-die-and-ips)  
- [Introduction to RISC-V](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#introduction-to-risc-v)  
- [From Software Applications to Hardware](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#from-software-applications-to-hardware)  

---

## [SOC Design and OpenLane](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#soc-design-and-openlane)  

- [Introduction to all components of open-source digital ASIC design](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#introduction-to-all-components-of-open-source-digital-asic-design)  
- [Simplified RTL2GDS Flow](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#simplified-rtl2gds-flow)  
- [Introduction to OpenLANE and Strive chipsets](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#introduction-to-openlane-and-strive-chipsets)  
- [Introduction to OpenLANE detailed ASIC design flow](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#introduction-to-openlane-detailed-asic-design-flow)  

---

## [Get familiar with open-source EDA tools](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#get-familiar-with-open-source-eda-tools)  

- [OpenLane Directory Structure](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#openlane-directory-structure)  
- [Design Preparation Setup](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#design-preparation-setup)  
- [Review files after design prep and run synthesis](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#review-files-after-design-prep-and-run-synthesis)  
- [Steps to characterise Synthesis results](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-1/readme.md#steps-to-characterise-synthesis-results)  


# Inception of open-source EDA, OpenLANE and Sky130 PDK
##  How to talk to computers
###   Introduction to QFN-48 Package, chip, pads, core, die and IPs

**Aurdino Board**: The image below is an Aurdino Microcontroller Board. Here we focus more on the encircled area, which contains the 'Microprocessor',that we will be designing from abstract level till fabrication level by using RTL to GDS flow

<img width="557" height="434" alt="image" src="https://github.com/user-attachments/assets/e34ada42-d1f1-452e-b1c9-68631fd44d68" />


While we cosider the chip, there are 3 main components:

(1) Pads : Through these pads signals can travel into the chip from external sources and viceversa.

(2) Die : It is the whole area of the chip that will be manufactured on the silicon wafer.

(3) Core : It is the area where our entire logic will be implemented.

<img width="1343" height="860" alt="image" src="https://github.com/user-attachments/assets/4273fda0-ae6a-4e21-80ba-a0533656ada3" />


The above mentioned MicroProcessor in an aurdino board is a package that consists of MicroProcessor chip and some other Foundry IP's(Intellectual Property). All of these combined called as a package.

For example, let's consider a package that consists of RISC V SOC and some other IP's such as SRAM , ADC , DAC , PLL etc..

<img width="1257" height="859" alt="image" src="https://github.com/user-attachments/assets/b82041dc-7b4d-452a-9514-645863bae9b8" />



###  Introduction to RISC-V

**ISA**: ISA is known as "Instruction Set Architecture". It is nothing but a way of communicating with the computer.
In general we write codes that need to be executed by the system, using coding languages like C , Java etc. , but machine can't understand those languages. It is where ISA comes into picture. By using ISA the codes that were written wil be converted into assembly language and from there to binary i.e Machine understandable language. This is the purpose of the ISA, and the RISC V ISA is the latest ISA released.

<img width="1737" height="1079" alt="image" src="https://github.com/user-attachments/assets/7f2094cc-6834-4b6b-af7e-b7d451140336" />



### From Software Applications to Hardware

In real life we generally deal with Application Softwares(Apps) in order to communicate with the Hardware.But how it's done exactly?
In between Application software and Hardware, there will be a software called System Software. The Applications enter into the System Software and will be converted into the Hardware understandable language i.e Binary Language.

The System Software consists of different layers:

(1) **O.S** : Other than the general operations like Handling I.O operations, Allocating Memory, Low level System Functions the O.S converts the Application software to respected C,C++,Java etc.. codes.

(2) **Compiler** : The compiler takes output of O.S as input and converts the codes in C,C++,Java etc.. into Instruction set(.exe files). These instructions will be dependent on type of hardware used.

(3) **Assembler** : Assembler converts the .exe files into binary language and provides it to the hardware, and hardware performs the respective operations.


<img width="1741" height="1078" alt="image" src="https://github.com/user-attachments/assets/1313d63a-525e-4d90-b57b-5c5d774d14f5" />




## SOC Design and OpenLane

###  Introduction to all components of open-source digital asic design

In order to design a Open Source Digital ASIC, we primarily need some components. Such as

(1) RTL Designs

(2) EDA Tools

(3) PDK Data

There are some open sources to get these required components. 

For example, In case of RTL Designs we have librecores.org , opencores.org , github.com etc...

In case of EDA Tools we have Qflow , OpenRoad , OpenLane  etc...

In case of PDK Data, Recently in 2020 Google collabarated with SkyWater Technology and made **FOSS 130nm Production PDK** OpenSource.

<img width="681" height="669" alt="image" src="https://github.com/user-attachments/assets/e580793e-33b5-46d9-93d3-dc3ee1604668" />



What are RTL Designs?

RTL(Register-Transfer-Level) design is a crucial step in the VLSI design flow, which involves the creation of electronic circuits using integrated circuits (ICs). It involves the specification of a digital circuit in terms of the flow of digital signals between hardware registers, and the logical operations performed on those signals.

What are EDA Tools?

EDA(Electronic Design Automation) Tools are used to design and verify the functionality of an Integrated Circuit to ensure it deliver's the required performance and density.

What is PDK Data?

PDK(Process Design Kit) is a collection of files used to model a fabrication process for EDA Tools used in the design of an IC.The collection consists of

- Process Design Rules : DRC , LVS , PEX
- Device Models
- Digital Standard Cell Libraries
- I/O Libraries etc....


### Simplified RTL2GDS Flow

The simplified RTL to GDS Flow starts with an RTL file. After going through some set of stages we will get the output as a GDS file, which can be readily sent to foundry for fabrication. The steps involved in the RTL2GDS Flow is of following:

<img width="1188" height="651" alt="image" src="https://github.com/user-attachments/assets/610b3f80-9225-4837-aa6e-9e57a6b38446" />


(1) **synthesis** : 
- In synthesis stage RTL file will be converted into a circuit by using the components from the Standard Cell Library.
- The cells in the Standard Cell Library are called Standard Cells and they have the regular layout of same height but different widths.
- Each cell has different models based on Electrical,HDL,Spice,Layout(Abstract and Detailed) etc....

<img width="827" height="238" alt="image" src="https://github.com/user-attachments/assets/4b9e2721-4a78-4c14-9ba7-f414baa7a052" />


 (2) **Floor Planning** & **Power Planning** :
 - Floor Planning is a stage where the position of the components on the chip will be decided by keeping the area of the chip as minimal as possible by following a set of rules.
 - During the Floor Planning Stage itself the position of I/O pins,ports,pads will be determined.

<img width="808" height="214" alt="image" src="https://github.com/user-attachments/assets/3bd959ef-1c69-4d41-8ac7-60ec5ebebdb3" />


 - In Power Planning stage the Power supply network i.e VDD & GND of the chip will be laid out. During Power PLanning 3 components Power Rings , Power Straps , Power Pads will be laid out.
 - For Power Network Top Metal Layers will be used because the Power Network should have minimum delay as possible and the top layers of metal will have the low resistance, So they are used.

<img width="468" height="239" alt="image" src="https://github.com/user-attachments/assets/360b87fd-b6f2-4f9c-9cb4-842fed778156" />


(3) **Placement** :
- In Placement stage the components are placed within the areas planned during the FloorPlanning Stage.
- Along with them Standard Cells that are required in the design are also placed within the cell boundaries.
- Placement will be performed in 2 stages. They are Global Placement and Detailed Placement.
- During Global Placement the Standard cells may overlap and does not follow the Placement Rules.
- In Detailed Placement every standard cell will be placed in its optimal position by following the Placement rules.

<img width="599" height="226" alt="image" src="https://github.com/user-attachments/assets/4839c229-183f-43e7-8821-c68edf160aa7" />



(4) **CTS**(Clock Tree Synthesis) :
- Before Performing Routing of the signals, we should perform Clock Routing.
- While Routing the clock tha major problem is CLock Skew.
- Clock Skew is the difference in time taken for the clock to reach two different destinations in the design.
- In order to eliminate the clock skew, we should deploy the technique called **Symmetric Tree Structure**.
- There are different types of Symmetric Tree Structures. They are H-tree,I-tree,X-tree etc...

<img width="243" height="184" alt="image" src="https://github.com/user-attachments/assets/dbe2e89f-4c1d-4008-adf3-e01925b9fa16" />


(5) **Routing** :
- Afetr the clock routing is done, now signals must be routed.
- Router uses the remaining metal layers and makes conections in the design.
- Routing will be carried out in 2 stages.They are Global Routing and Detailed Routinng.
- In the stage of Global Routing, the tool generates a Routing guide by following the instructions given in the PDK.
- In the stage of Detailed Routing, actual routing will be done according to the guide generated in the Global Routing Stage.

<img width="754" height="286" alt="image" src="https://github.com/user-attachments/assets/bea49b3b-2e4d-4ed0-8e12-68cc79b3e804" />


(6) **Sign-off** :
- After Routing is done, the chip will be considered as completed and during Sign-off stage different types of checks will be performed.
- Physical Verification Checks : Design Rule Check(DRC) , Layout Vs Schematic(LVS)
- In DRC, the chip will be verified for the violations in the Design Rules provided by the PDK.
- In LVS, the chip will be checked for the functionality whether it matches to the gate level netlist functinality.
- Timing Checks : Static Timing Analysis(STA)
- During STA, the design is checked for Timing violations.


### Introduction to OpenLANE 
OpenLane is started as an Open Source Flow for a true Open Source Tape-out experiment.It was from e-fabless.It is a platform which supports different tools such as Yosys,OpenRoad,Magic,KLlayout and some other Open source tools.It integrates the various steps of Silicon Implementation and abstracts it. At e-fabless they have an SOC family called Strive. Strive is a family of open everything SOCs having Open PDK, Open RTL, Open EDA.The main goal of OpenLane is to "Produce a clean GDS file with no human intervention with no LVS,DRC,Timing violations. It is majorly tuned for Skywater 130nm OpenPDK but also supports XFab180 and GF130G. It is functional out of the box.It can be used Harden Macros and chips. It has two modes of operation , autonomous and interactive. It has a feauture called Design Space Exploration which helps in finding the best set of flow configurations.


### Introduction to OpenLANE detailed ASIC design flow

<img width="834" height="494" alt="image" src="https://github.com/user-attachments/assets/fa5b3027-58e3-4979-934c-795242dbaac4" />

The image shows the OpenLane detailed ASIC Design Flow.The flow starts with Design RTL, It goes through RTL synthesis by Yosys and abc giving an optimised gate level netlist. Now we perform STA on the optimised netlist inorder to check for Timing violations. After STA we perofrm DFT and this step is optional and for this we use FAULT tool.

Fault(for DFT) : 
- Scan Insertion
- Automatic Test Pattern Generation(ATPG)
- Test Pattern Compaction
- Fault coverage
- Fault Simulation

<img width="568" height="220" alt="image" src="https://github.com/user-attachments/assets/67ff1a8d-3f70-4376-83fc-93214b678ae1" />


 After performing DFT next comes Physical Implementation.It is also called as Automated PnR(Place and Route) and for this we use OpenRoad.

 OpenRoad(for Physical Implementation) :
 - Floor/Power Planning
 - End Decoupling Capacitors and Tap Cells Insertion
 - Placement: Global and Detailed
 - Post placement optimization
 - Clock Tree Synthesis
 - Routing: Global and Detailed

 During PnR for every change in the design, we should check for LEC(Logic Equivalance Checking). LEC is used to confirm that the function did not change after modifying the netlist and also during physical implementation we have a important step called "Fake Antenna Diodes Insertion Script".

Dealing with Antenna Rule violations : When a metal wire segment is fabricated, it can act as an antenna.
- Reactive ion etching causes charge to accumilate on the wire.
- Transistor gates can be damaged during fabrication.

There are two solutions for this problem
- Bridging attaches a higher layer intermediary. It requires Router awareness.

<img width="361" height="162" alt="image" src="https://github.com/user-attachments/assets/116526ce-ebea-4ba1-81fc-91423fb54146" />


- Add antenna diode cell to leak away the charges. Antenna diodes are provided by the SCL. For this we took a preventive approach.
  - Add a Fake antenna didoe next to every cell input after placement.
  - Run the Antenna Checker(Magic) on the routed layout.
  - If the checker reports violation on the cell input pin, replace the fake diode cell by a real one 

<img width="238" height="204" alt="image" src="https://github.com/user-attachments/assets/9a51d709-c293-4fc0-bffe-0cef84b93976" />


 And at the end, we perform Physical Verification. Which includes DRC(Design Rule Checking) , LVS(Layout Vs Schematic). Along with the P.V we also performs STA to check for timing violations in the design.
 - MAGIC is used for DRC and SPICE Extraction from Layout.
 - MAGIC and Netgen are used for LVS by comparing Extracted SPICE by MAGIC and Verilog Netlist.


## Get familiar to open-source EDA tools

### OpenLane Directory Structure

 In order to access the OpenLane tool, we will be needing some basic linux commands.They are listed below 
 - pwd : It displays the present working directory and its path.
 - cd : Using this command we can move in both ways in the directory tree.
 - ls : It lists all the sub-directories and files present in the current directory.
 - mkdir : Using this command, we can create a new directory.
 - rmdir : Using his command, we can delete an existing directory.
 - rm : This command is used to delete the files.
 - help : using this command we can know the working of any command.
 - clear : This command clears the terminal.


### Design Preparation Setup

In order to enter into BASH, by being in OpenLane directory we should use a command called **`docker`**. By using docker command we will enter into the Bash. After entering into bash we have to use the script flow.tcl, because this .tcl file contains the steps that need to be executed in the OpenLane and along with the tcl file we need to use -interactive switch in order to perform step by step process. If not used interactive switch the whole flow i.e RTL to GDS will be executed once and the final report will be given. The command that we should use for this is **`./flow.tcl -interactive`**.Now OpenLane is opened and we can observe the change in prompt and now we have to input packages required to run the flow and for this we use the command **`package require openlane 0.9`**.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/46c4894d-4c70-46f9-a076-abca98388013" />


Now we need to select the design on which we are going to perform RTL to GDS flow, we will be having 30 to 40 designs that are pre-built in the design folder in openlane and we will be selecting "picorv32a.v" design for this project.Now in order to perform synthesis(first stage of the project) on this design, first we need to setup the design and for that the command will be **`prep -design picorv32a`**.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/3ed4b30d-e727-42a8-b400-c625c562ae83" />

 
At the end of the terminal we can see that **Preparation is complete**.


### Review files after design prep and run synthesis

After Preparation is done a directory with current date will be created in the runs folder.And in that directory all the directorys that are needed to store the results , reports etc.. will be created.

Initially every directory will be empty because we haven't performed any operations on the design.But we will have a direcrory named tmp and it contains different types of files.One of the files will be "merged.lef" file, it contains metal layer level and cell level information.



Now, it's time to proceed with the first step in the project. we need to perform Synthesis on the design. For this we need to use the command **`run_synthesis`**.Tool will take some time to perform synthesis, when completed it displays the **Synthesis was successful** message.

<img width="1012" height="616" alt="image" src="https://github.com/user-attachments/assets/11a5e51f-a4d9-4b01-bf00-6bfccfe79ebe" />


### Steps to charactirise Synthesis results

Now we need to find out the flipflop percentage in total cells. For this we use reports from Synthesis stage.

<img width="354" height="585" alt="image" src="https://github.com/user-attachments/assets/5dbf15a4-c9c2-4e07-bd7b-a4fca2795c6d" />

In the above image,we can see that the total no.of cells used in the design are 14876 and the count of D-flipflops in the design are 1613. So, the flipflop percentage is calculated as

**Flop Ratio = ((no.of flipflops) / (Total no.of cells))*100 = (1613/14876)*100 = 10.84%**

Before Performing Synthesis the reports directory was empty. After Synthesis the reports that are generated during synthesis will be stored in the reports directory.

<img width="482" height="642" alt="image" src="https://github.com/user-attachments/assets/1b78dfd7-400f-49b4-b1d4-ded4b65a8cb8" />


<img width="862" height="678" alt="image" src="https://github.com/user-attachments/assets/9ebf4472-baf6-417d-9953-ccde891226c2" />


<img width="354" height="585" alt="image" src="https://github.com/user-attachments/assets/5dbf15a4-c9c2-4e07-bd7b-a4fca2795c6d" />

Here the DFF count:  `sky130_fd_sc_hd__dfxtp_2` = `1613`

- And total number of cells = `14876`

    ```
  D flip-flop ratio  = count of DFFs / total number of cells
  		     = 1613 / 14876
  		     = 0.108429685 (OR) 10.8429 %
    ``` 
