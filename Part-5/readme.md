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

![gen_pdn_command](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/5ce794df-a8a4-4d8c-a687-103a247b6b09)

![pdn_done](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/2e684127-62a7-4e3f-938f-14ce6b0570ad)

We can clearly see that "PDN generation was succesful".

![rails straps_info](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/4a2d278c-849e-4fb1-b906-d297b12c7401)

In the above figure we can see that the pitch of the standard cell rails is 2.720, which we have expected.


### Lab steps from power straps to std cell power

![Screenshot 2024-05-07 104244](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/9cecd9c1-5a25-4a26-851d-11f6ce4fbc49)

In the above figure we can observe the path through which power is delivered all the way to standard cells.

- The blocks that we can observe around the design are I/o pads and those with Red and Blue colours are Power Pads. Red pad is for power and the Blue one is for Gnd.
- Those blocks are connected to Power and Gnd Rings, which go around the design and supply power to straps.
- The vertical connections that we can observe for the rings are called Power Straps.
- From Power straps and Rings connections will be made to the Power rails. The standard cell will be placed in between these power rails. The height of the standard cells should be the multiples of the pitch of the rails in order to get power and gnd supplies accurately.

  This is the overview of the PDN structure.


### Basics of global and detail routing and configure TritonRoute
  

The Final stage in the flow is ROUTING. we can start routing by using the command **`run_routing`** .

![routing_done](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/1e136428-7ac7-4eed-b71d-5b3d754f08b4)

![no_violations](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/fcd6128c-86ba-4871-a904-0713a24f3c3b)

From tha above figures we can see that routing is done and it is done with 0 violations, So our routing is succesful but we can see the negative slack. We need to eliminate that negative slack for succesful completion of Physical design flow.

We can see the final layout in gui using magic tool by using the command 

**`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/04-05_21-50/tmp/merged.lef def read /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/04-05_21-50/results/routing/picorv32a.def &`**


![final_layout](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/6f8f6bcb-8d0f-45bb-a0c4-61ea2db92a15)



## References

* https://github.com/nickson-jose/vsdstdcelldesign
* https://github.com/google/skywater-pdk
* https://github.com
* Material provided in workshop

