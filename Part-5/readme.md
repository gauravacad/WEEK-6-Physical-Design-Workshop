# Day-5: Final Steps for RTL2GDS using TritonRoute and OpenSTA  

## [Final steps for RTL2GDS using TritonRoute and OpenSTA](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-5/readme.md#final-steps-for-rtl2gds-using-tritonroute-and-opensta)  

- [Power Distribution Network and Routing](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-5/readme.md#power-distribution-network-and-routing)  
  - [Lab steps to build power distribution network](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-5/readme.md#lab-steps-to-build-power-distribution-network)  
  - [Lab steps from power straps to std cell power](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-5/readme.md#lab-steps-from-power-straps-to-std-cell-power)  
  - [Basics of global and detail routing and configure TritonRoute](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-5/readme.md#basics-of-global-and-detail-routing-and-configure-tritonroute)  

---

## [References](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-5/readme.md#references)  

# Final steps for RTL2GDS using tritonRoute and openSTA


## Power Distribution Network and routing


### Lab steps to build power distribution network


After completion of CTS, now we need to lay down power distribution network(PDN) for the design and it is done by using the command **`gen_pdn`** .

<img width="1468" height="888" alt="image" src="https://github.com/user-attachments/assets/11e8ba05-2b15-49cf-8ba8-51e9ff1f0c96" />


<img width="1466" height="886" alt="image" src="https://github.com/user-attachments/assets/bf8f0a14-1661-432c-a1f4-40f0c3f7a532" />


We can clearly see that "PDN generation was succesful".

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/a6e720aa-34a0-4f1d-b0bd-c1ec4b798c31" />


In the above figure we can see that the pitch of the standard cell rails is 2.720, which we have expected.


### Lab steps from power straps to std cell power

<img width="748" height="497" alt="image" src="https://github.com/user-attachments/assets/f44ceba8-8cf9-4b86-928b-3b94f9a6ff20" />

In the above figure we can observe the path through which power is delivered all the way to standard cells.

- The blocks that we can observe around the design are I/o pads and those with Red and Blue colours are Power Pads. Red pad is for power and the Blue one is for Gnd.
- Those blocks are connected to Power and Gnd Rings, which go around the design and supply power to straps.
- The vertical connections that we can observe for the rings are called Power Straps.
- From Power straps and Rings connections will be made to the Power rails. The standard cell will be placed in between these power rails. The height of the standard cells should be the multiples of the pitch of the rails in order to get power and gnd supplies accurately.

  This is the overview of the PDN structure.


### Basics of global and detail routing and configure TritonRoute
  

The Final stage in the flow is ROUTING. we can start routing by using the command **`run_routing`** .


<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/00f89377-ac16-4bc5-89c6-547f6cce32e9" />


<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/3fc7737f-8d02-491e-93ee-99d76d76dff5" />

From tha above figures we can see that routing is done and it is done with 0 violations, So our routing is succesful but we can see the negative slack. We need to eliminate that negative slack for succesful completion of Physical design flow.

We can see the final layout in gui using magic tool by using the command 

**`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/04-05_21-50/tmp/merged.lef def read /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/04-05_21-50/results/routing/picorv32a.def &`**


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/e71b4d53-3743-4a53-a5df-f7e1bbf27ed6" />




## References

* https://github.com/nickson-jose/vsdstdcelldesign
* https://github.com/google/skywater-pdk
* https://github.com
* Material provided in workshop

