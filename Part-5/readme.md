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


# Routing and Design rule check (DRC)


- `Maze Routing - Lee's Algorithm`
<p align="center">
  <img width="1903" height="1075" alt="168" src="https://github.com/user-attachments/assets/fd6dc733-025d-490a-8457-4517f9394ccb" />

</p>

<p align="center">
  <img width="1880" height="1072" alt="169" src="https://github.com/user-attachments/assets/264ce1ca-1714-4b05-858d-a2e3888cb64d" />

</p>

- DRC Check
  
<p align="center">
  <img width="1920" height="1080" alt="170" src="https://github.com/user-attachments/assets/d2aa7dee-a686-4b09-bd33-8f9111ee7b96" />

</p>
<p align="center">
  <img width="1833" height="1032" alt="171" src="https://github.com/user-attachments/assets/128553ec-c234-4a48-be20-724df2921f80" />

</p>

- Parasitics Extraction
<p align="center">
  <img width="1920" height="1080" alt="172" src="https://github.com/user-attachments/assets/1e7ef683-0b21-4674-9a40-4c81f05f7c9e" />
  
</p>


# Power Distribution Network and routing

- to get generate power distribution network. complete until the cts will the follwoing commands 

```shell
prep -design picorv32a -tag 20-03_18-30 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

set ::env(SYNTH_STRATEGY) "DELAY 0"
set ::env(SYNTH_SIZING) 1

run_synthesis

init_floorplan
place_io
global_placement_or
detailed_placement
tap_decap_or
detailed_placement

run_cts
```
- use the command `gen_pdn` to generate the power distribution network
  
<p align="center">
  <img width="1854" height="906" alt="196" src="https://github.com/user-attachments/assets/6d0ad34f-7805-42ac-983f-a4da3721223a" />

</p>
<p align="center">
  <img width="1851" height="912" alt="197" src="https://github.com/user-attachments/assets/220c3ba3-3163-4f04-93c3-1801a073a345" />

</p>

- to view the pdn output naviagte to the directory `openlane_working_dir/openlane/designs/picorv32a/runs/20-03_18-30/tmp/floorplan/` in here we have `12-pdn.def` file
- `def` files can viewed in magic. command is 👇

```shell
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 12-pdn.def &
```

<p align="center">
  <img width="1845" height="920" alt="193" src="https://github.com/user-attachments/assets/259eca64-4fdd-4f15-8968-8764f6293875" />

</p>
<p align="center">
<img width="1732" height="928" alt="194" src="https://github.com/user-attachments/assets/71c7e04b-9110-45d9-88ba-805f4748d568" />

</p>
<p align="center">
 <img width="1747" height="909" alt="195" src="https://github.com/user-attachments/assets/1b142588-c8ec-4847-84f0-888aa5550775" />

</p>


### the next step, which is left is routing..

- use the command `run_routing` to perform routing.

<p align="center">
  <img width="1842" height="906" alt="198" src="https://github.com/user-attachments/assets/1796e304-9db5-49a9-a9a4-57227492b8d6" />

</p>
<p align="center">
  <img width="1853" height="888" alt="199" src="https://github.com/user-attachments/assets/6c298129-8215-4852-b390-99318d399068" />

</p>
<p align="center">
  <img width="1855" height="898" alt="200" src="https://github.com/user-attachments/assets/bfaefad1-c66f-4ac2-a086-8fbfcef7af22" />

</p>

- It took 1 hour for complete routing
- Routing started with `26890` violations in the `1st optimization` iteration and finally reduced to `0` violations in the `57th optimization` iteration

- To open routing file naviagte to directory `cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/20-03_18-30/results/routing/` there we have def which is read magic
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
```
<p align="center">
  <img width="1000" height="" src="../images/201.png">
</p>
<p align="center">
  <img width="1000" height="" src="../images/202.png">
</p>
<p align="center">
  <img width="1000" height="" src="../images/203.png">
</p>

- The `picorv32a.def.png` from the routing is 👇 
![](../images/picorv32a.def.png)





## References

* https://github.com/nickson-jose/vsdstdcelldesign
* https://github.com/google/skywater-pdk
* https://github.com
* Material provided in workshop

