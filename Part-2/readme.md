# Day-2: Floorplanning and Placement  

## [Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells) 

- [Chip FloorPlanning Considerations](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#chip-floorplanning-considerations)  
- [Utilization Factor and Aspect Ratio](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#utilization-factor-and-aspect-ratio)  
- [Concept of pre-placed cells](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#concept-of-pre-placed-cells)  
- [De-coupling Capacitors](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#de-coupling-capacitors)  
- [Power Planning](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#power-planning)  
- [Pin placement and logical cell placement blockage](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#pin-placement-and-logical-cell-placement-blockage)  
---
## [Steps to run floorplan using OpenLANE](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#steps-to-run-floorplan-using-openlane)  

- [Review Floorplan files and steps to view floorplan](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#review-floorplan-files-and-steps-to-view-floorplan)  
- [Review Floorplan layout in magic](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#review-floorplan-layout-in-magic)  

---

## [Library Binding and Placement](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#library-binding-and-placement)  

- [Netlist binding and initial place design](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#netlist-binding-and-initial-place-design)  
- [Optimize placement using estimated wire-length and capacitance](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/edit/main/Part-2/readme.md#optimize-placement)

---


# Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells

## Chip FloorPlanning Considerations

### Utilization Factor and Aspect Ratio

In order to find out the Utilization Factor and Aspect Ratio, first we need to know how to define height and width of core and die areas.
- Core is an area in a chip which is used to place all the logic cells and components in a chip. It is the place where logic lies in a chip.
- Die is an area that encircles the core area and used for placing I/O related components.

<img width="913" height="660" alt="image" src="https://github.com/user-attachments/assets/3bcd3eda-582b-4109-9c93-63eeefe106b0" />



The height and width of core area will be decided by the netlist of the design. It will be based on the no.of components required in order to execute the logic and the height and width of the die area will be dependent on the core area height and width.

<img width="871" height="277" alt="image" src="https://github.com/user-attachments/assets/39987274-22d6-4062-8764-b06c4cf2e256" />


For example, lets consider a netlist that is having two logic gates and two flipflops each having area of 1 sq.unit. The netlist contains 4 elements and the minimum total area required for the core area will be 4 sq.units. 

<img width="848" height="671" alt="image" src="https://github.com/user-attachments/assets/95ca0f3b-4b13-4dcc-9170-7a2af1e405ed" />


<img width="384" height="330" alt="image" src="https://github.com/user-attachments/assets/0e261c0e-4e78-4275-8906-ff4d2f28dba6" />



**Utilization Factor** : Utilization Factor is defined as "The ratio of the core area occupied by the netlist to the total core area".For a good FloorPlan, The Utilization Factor should never be '1' because when the Utilization factor becomes '1' , there will be no place for adding additional logic if needed and it will be considered as a bad FloorPlan.

**`Utilization Factor = (Area occupied by netlist / Total core area)`**

**Aspect Ratio** : Aspect Ratio is defined as "The ratio of Height of the core to the width of the core". If the Aspect ratio is '1' , then the core is said to be in a square shape and other than '1' the core will be a rectangle.

**`Aspect Ratio = (Height of the core / Width of the core)`**

Lets consider the above mentioned example and evaluate some cases 

<img width="348" height="327" alt="image" src="https://github.com/user-attachments/assets/65a6ffe2-205e-451a-9c21-17c39ea0f54c" />


In this case, when calculated 
- Utilization factor = (4 squnits)/(4 squnits) = 1
- Aspect Ratio = (2 units)/(2 units) = 1 //The core is in a square shape.


<img width="562" height="367" alt="image" src="https://github.com/user-attachments/assets/2740c703-0b77-4f2d-9c45-bb8570749b40" />


In this case, when calculated

- Utilization factor = (4 squnits)/(8 squnits) = 0.5
- Aspect Ratio = (2 units)/(4 units) = 0.5 //The core is in a rectangular shape.


<img width="692" height="604" alt="image" src="https://github.com/user-attachments/assets/ce0031ce-470a-402e-aec7-7278956e5697" />


In this case , when calculated

- Utilization factor = (4 squnits)/(16 squnits) = 0.25
- Aspect Ratio = (4 units)/(4 units) = 1 //The core is in a square shape.


### Concept of pre-placed cells

The concept of pre-placing cells is nothing but reusing already designed blocks by not designing them again and again. The most commonly used pre-placed blocks are Memory , comparators , Mux etc.. , These blocks can be called as Macros (or) I.P's .We need to place these macros very carefully in such a way that if these blocks are more connected to input pins, then we should place these close to those input pins. These should be placed in a way such that the wiring length should be decreased.

The term Pre-placed refers to "Placing those blocks prior to placement stage that is in Floorplan stage. After placing those blocks in Floorplan stage we need to define some placement blockages in order to avoid Placing of other standard cell near to those blocks by the tool during placement stage. By using this pre-placed cells the Time-to-Market can be reduced.

<img width="1022" height="667" alt="image" src="https://github.com/user-attachments/assets/69e4906f-1333-4da0-867e-7b9c48c582c4" />



### De-coupling Capacitors

Generally these pre-placed blocks will be high-power draining blocks. In some cases, the power they recieve from the power source will not be sufficient for them to perform switching i.e the signal will not be in the range of its noise margin because there will be a voltage drop in the inter-connecting wires. In this case, the De-coupling Capacitors comes into the picture. 

<img width="923" height="674" alt="image" src="https://github.com/user-attachments/assets/ea69b498-367d-4dd6-8a86-362cc443cf56" />


These De-cap cells will be placed near to the blocks that will drain high power. When there is no switching is being performed the De-cap cell will be connected to power source and gets charged to its high level and when the switching is being performed the De-cap cells will be connected to the blocks and the power required for the block will be supplied by the De-cap cell, and when ever the switching stops again the De-cap cell will start to getting charged. This is the working of De-cap cells and these cells plays a crucial role in the circuit design.

<img width="1285" height="610" alt="image" src="https://github.com/user-attachments/assets/4419dba4-32ee-42c8-ac1b-c11bab132b94" />



### Power Planning

In the previous section we used De-cap cells to manage power for different blocks.But Decap cells have some limitations such as Leakage power and increase in the area of chip. To overcome these we use a technique called Powerplanning. In some areas of the chip when there is more  switching happening, two tyoes of phenomena can occur
- Voltage drop
- Ground bounce

<img width="955" height="647" alt="image" src="https://github.com/user-attachments/assets/5d4d9be6-26f7-4231-8c19-45443fc792af" />


**Voltage drop** : When a group of cells are simultaneously switching from 0 to 1, then every cell needs the power and In case the power is supplying from one source, there may occur the shotage of power and drop in the input voltage happens at that place. This is called as "Voltage Drop". The problem occurs only when the voltage level goes below the noise margin.

<img width="962" height="235" alt="image" src="https://github.com/user-attachments/assets/c55e0900-3459-429b-87ba-39f27f35a364" />


**Ground Bounce** : When a group of cells are simultaneoisly switching from 1 to 0, then every cell dumps the power to th ground simultaneously to the same ground pin. In this case the ground instead of being at 0 experiences a short rise in the voltage and this is called as "Ground Bounce".The problem occurs only when the voltage level goes above the noise margin.

<img width="955" height="246" alt="image" src="https://github.com/user-attachments/assets/340c632b-6900-4a5a-8c80-423465484b3e" />

In order to avoid these abnormalities, a technique called Power Planning is used. In this technique two different Power mashes are used, one for Vdd and another one for Ground.These meshes are prepared by using top two metal layers because they should have less voltage drop. These meshes will be spread across the design and are connected to multiple sources of Vdd and Ground.

<img width="920" height="708" alt="image" src="https://github.com/user-attachments/assets/4c51bd24-1470-47c6-9600-affd85403492" />


With this technique whenever a cell needs power to switch from 0 to 1, it takes from nearest Vdd layer and if a cell needs to drain the power it will drain it to the nearest Ground Layer.

<img width="894" height="676" alt="image" src="https://github.com/user-attachments/assets/fbad2702-8d33-4d00-9472-0895ce0aed34" />



### Pin placement and logical cell placement blockage

Pin Placement is one of the crucial step in the design process. Bad pin placement results increase in the length of wire used for connectivity, which inturn results in some adverse affects.
Pins should be placed in such a way that the required for connecting them to the blocks should be as less as possible. For example if an input pin is driving two blocks then that pin should be placed near to those two blocks.

Let's consider the below design

<img width="754" height="682" alt="image" src="https://github.com/user-attachments/assets/b1d7810c-b189-45b4-9d79-8d6f2dc2ae35" />


For the above design the effective pin placement will look like as follows

<img width="915" height="639" alt="image" src="https://github.com/user-attachments/assets/15242894-a281-417b-b4ef-87ba7905a829" />


In the above pin placement, we can observe two things 
- The order of input pins and output pins is random. As already mentioned the pins should be placed based on the connectivity not based on the order.
- The pins used for clock signals are larger in size when compared to pins used for signals, this is because clock is one of the important signal in the design and delays and voltage drops in the clock signal leads to failure of the chip. That is the reason why we use higher metal layers for routing the clock in the design.

After finishing the pin placement, we should use placement blockages outside of the core area and inside of the die area inorder to avoid placement and routing tool using that space for placement and routing, because it is the area dedicated only for Pin Placement purpose.

![Screenshot 2024-04-29 225000](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/428dda61-6e63-4c8a-b11f-51c5f7da5cb9)


### Steps to run floorplan using OpenLANE


For Floorplan to run smoothly, as a designer we should take care of some switches, that makes changes to the floorplan when changed. For example Utilization factor and aspect ratio are also part of switches. Designer should cross check these switches before initializing floorplan whether they are alligned with the project or not. Below image shows different types of switches in floorplan stage.

![floorplan_switches](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/e31bdee9-2776-4d28-9e7e-c036b3378b03)


![floorplan tcl](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/a666b97c-cb76-4b4e-9c8a-3995db52f61a)

In the OpenLane lowest priority is given to system default(Floorplanning.tcl) and the second highest priority will be given to config.tcl and the highest priority will be given to PDK_varient.tcl for considering the values for switches.


### Review Floorplan files and steps to view floorplan

After confirming that all the switches are as per requirement, now we should executr a command **`run_floorplan`** , in order to start the floorplan stage.

If any errors occur during the floorplan stage it will display those errors.If it does not display any errors then our floorplan stage has succesfully completed.

![floorplan_done](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/d8ffd0cf-245b-47e1-b9c9-47b5352811c9)

After completion of the floorplan we can check the report generated by the tool and check some of the aspects like die area etc.. , but in order to view the design in GUI we should use MAGIC tool.

![Floorplan_report](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/7b320946-dfe0-4f09-a673-20727517a8a7)

In order to enter into the MAGIC tool we need to use the command

**` magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &`**

And in GUI floorplan looks like this![floorplan_layout(magic)](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/4abb51b3-dbbf-4abe-bdd5-fe9d1c7557ce)


### Review Floorplan layout in magic

While in the GUI, to allign the design to the middle of the screen. First we need to select the whole design by pressing S in the keyboard and then V in the keyboard.

In order to zoom to any particular area first left click the mouse and select the area to zoom and then right click again, and then press Z in the keyboard to zoom in the selected area.

In order to know the details of any cell in the design, just move the cursor to that cell and press S to select the cell and then in the window of tkcon enter the command "what" then it will displey the details of the selected ine.

![vertical_io_pin](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/a28b636e-8614-4f03-85bc-3d715aaab4ec)


![horizontal_io_pin](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/b5d1258f-6447-4f2c-9af0-515cc752618e)


![Decap_cell](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/87d6e43b-79b7-4d1b-9368-73ce6702bf8c)



## Library Bindidng and Placement

### Netlist binding and initial place design

In the netlist every element has its own shape, for example And gate has a different shape and or gate has a different shape. But in a library every element has only a square or rectangle shape. A Library consists of every elements that can be readily used and also the elements comes with their respective properties such as area, delay etc.. . We will have different versions of the same element with different properties.

![Screenshot 2024-04-30 152912](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/f3aa46fa-675b-425a-b871-6073429312bd)


![Screenshot 2024-04-30 152937](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/ed3e79b7-5bc0-4a50-a555-7622a1d3e5f0)

In the above picture we have 3 different sets of same elements. The elements which are larger in size are faster but occupies larger area and the smaller set will occupy less area but are slower when compared to larger ones.


### Optimize placement using estimated wire-length and capacitance

During Placement we should definitely consider the estimated wire length and place the cells according to it. Wire length is estimated by calculating the distance from input source of those cells and the distance to the output sinks that are being driven by them. 

For above example tool will place the blocks by using the estimated wire length as shown in the below figure

![Screenshot 2024-04-30 154924](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/f60da452-6c6d-4304-8108-726e41852c30)


### Congestion aware placement using replace


After successful Floorplanning, the next step in the design process is Placement. Placement stage will consist of two stages 
- Global Placement - In Global Placement stage tool decides the places for all standard cells in the design.
- Detailed Placement - In Detailed Placement stage the tool places all the standard cells in their designated places and legalization of the Placement will be done. Legalization is nothing but making sure that standard cells are not overlapped on each other in the design and are placed with in the site rows of the design.

In order to start the placement we need to use the command **`run_placement`**.

After Placement is done to check whether the cells are placed correctly or not, we need to check GUI and that will be done using MAGIC tool with the following command

**`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`**

![Screenshot from 2024-04-30 22-13-00](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/a5a4b928-7bff-4c9f-bef4-408367312c06)


![Screenshot from 2024-04-30 22-14-10](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/9a284840-6402-40f6-aa1c-9c6c50cb1909)


![Screenshot from 2024-04-30 22-15-57](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/378e46cd-3f9c-4176-8695-2a739af85bba)

**Screentshot:** Run_floorplan

<img width="1063" height="621" alt="image" src="https://github.com/user-attachments/assets/7f17dda0-dcbf-4b33-abc6-f7a3c53343a6" />

**Screentshot:** finding Magic file and Display
<img width="1062" height="633" alt="image" src="https://github.com/user-attachments/assets/4de5554e-4c34-44c0-9250-133d8825d624" />

**Screentshot:** finding Magic file and Display

<img width="1063" height="627" alt="image" src="https://github.com/user-attachments/assets/0cc4e398-3ba1-43d9-8eb9-ae3e799c2886" />

---
<img width="1232" height="644" alt="image" src="https://github.com/user-attachments/assets/ed650090-7b49-4674-af58-344f7c43cddc" />







