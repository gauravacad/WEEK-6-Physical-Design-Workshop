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




# Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells

## Chip FloorPlanning Considerations

### Utilization Factor and Aspect Ratio

In order to find out the Utilization Factor and Aspect Ratio, first we need to know how to define height and width of core and die areas.
- Core is an area in a chip which is used to place all the logic cells and components in a chip. It is the place where logic lies in a chip.
- Die is an area that encircles the core area and used for placing I/O related components.

![Screenshot 2024-04-29 162940](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/0579fc7f-009a-4e5b-a3e3-f51fecf1d1b2)


The height and width of core area will be decided by the netlist of the design. It will be based on the no.of components required in order to execute the logic and the height and width of the die area will be dependent on the core area height and width.

![Screenshot 2024-04-29 162542](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/e2885f48-30b3-4aad-b746-f0c3369440db)

For example, lets consider a netlist that is having two logic gates and two flipflops each having area of 1 sq.unit. The netlist contains 4 elements and the minimum total area required for the core area will be 4 sq.units. 

![Screenshot 2024-04-29 162459](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/34d0c495-66bb-4582-b15c-e6adf8619ab6)

![Screenshot 2024-04-29 162658](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/4c09360a-29d5-42f7-aec7-46c16614faaa)


**Utilization Factor** : Utilization Factor is defined as "The ratio of the core area occupied by the netlist to the total core area".For a good FloorPlan, The Utilization Factor should never be '1' because when the Utilization factor becomes '1' , there will be no place for adding additional logic if needed and it will be considered as a bad FloorPlan.

**`Utilization Factor = (Area occupied by netlist / Total core area)`**

**Aspect Ratio** : Aspect Ratio is defined as "The ratio of Height of the core to the width of the core". If the Aspect ratio is '1' , then the core is said to be in a square shape and other than '1' the core will be a rectangle.

**`Aspect Ratio = (Height of the core / Width of the core)`**

Lets consider the above mentioned example and evaluate some cases 

![Screenshot 2024-04-29 162721](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/55cf4d1f-628d-4f2a-a968-744a7be7470e)

In this case, when calculated 
- Utilization factor = (4 squnits)/(4 squnits) = 1
- Aspect Ratio = (2 units)/(2 units) = 1 //The core is in a square shape.


![Screenshot 2024-04-29 162810](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/5b4ef1fb-2d73-4819-95c7-d3c36de576fd)

In this case, when calculated

- Utilization factor = (4 squnits)/(8 squnits) = 0.5
- Aspect Ratio = (2 units)/(4 units) = 0.5 //The core is in a rectangular shape.



