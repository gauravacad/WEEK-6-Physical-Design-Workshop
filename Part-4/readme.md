
# Day-4: Pre-layout Timing Analysis and Importance of Good Clock Tree  

## [Pre-layout timing analysis and importance of good clock tree](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#pre-layout-timing-analysis-and-importance-of-good-clock-tree)  

- [Timing modelling using delay tables](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#timing-modelling-using-delay-tables)  
  - [Lab steps to convert grid info to track info](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#lab-steps-to-convert-grid-info-to-track-info)  
  - [Lab steps to convert magic layout to standard cell LEF](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#lab-steps-to-convert-magic-layout-to-standard-cell-lef)  
  - [Introduction to timing libs and steps to include new cell in synthesis](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#introduction-to-timing-libs-and-steps-to-include-new-cell-in-synthesis)  
  - [Lab steps to configure synthesis settings to fix slack and include vsdinv](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#lab-steps-to-configure-synthesis-settings-to-fix-slack-and-include-vsdinv)  

- [Timing analysis with ideal clocks using openSTA](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#timing-analysis-with-ideal-clocks-using-opensta)  
  - [Lab steps to configure OpenSTA for post-synth timing analysis](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#lab-steps-to-configure-opensta-for-post-synth-timing-analysis)  

- [Clock tree synthesis TritonCTS and signal integrity](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#clock-tree-synthesis-tritoncts-and-signal-integrity)  
  - [Lab steps to run CTS using TritonCTS](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#lab-steps-to-run-cts-using-tritoncts)  

- [Timing analysis with real clocks using openSTA](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#timing-analysis-with-real-clocks-using-opensta)  
  - [Lab steps to analyze timing with real clocks using OpenSTA](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#lab-steps-to-analyze-timing-with-real-clocks-using-opensta)  
  - [Lab steps to execute OpenSTA with right timing libraries and CTS assignment](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#lab-steps-to-execute-opensta-with-right-timing-libraries-and-cts-assignment)  
  - [Lab steps to observe impact of bigger CTS buffers on setup and hold timing](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/blob/main/Part-4/readme.md#lab-steps-to-observe-impact-of-bigger-cts-buffers-on-setup-and-hold-timing)
  - 

  # Pre-layout timing analysis and importance of good clock tree

## Timing modelling using delay tables

### Lab steps to convert grid info to track info


 Now to proceed further we will be needing LEF file of the Inverter cell. we need to extract if from the current Inverter cell.

 From PNR point of view, while designing standard cell set two things must be considered
 - The Input and output ports must lie on the intersection of the Vertical and Horizontal tracks.
 - The width of the standard cell should be an odd multiple of the track pitch and height should be an odd multiple of track vertical pitch.

 Open the tracks.info file to know more about tracks

 
 <img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/ad395296-ca7e-4626-b289-0e0f45a08c55" />

 In the cell design input and output ports are on the li1 layer.We need to convert the grid into tracks.

 Open the tkcon window and give the command for grid according to the track file.


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/e72a4756-75af-493c-bd1c-d67b06bc5212" />
 Now we can see that both input and output ports are placed at the intersection of the tracks. Here our second condition also satisfies as 3 boxes are covered between the boundaries.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/f0abb107-42fe-4742-8071-11775d5dc1de" />



### Lab steps to convert magic layout to standard cell LEF


Now we need to extract the LEF file.First save .mag file by using the command **`save sky130_vsdinv.mag`** in the tkcon terminal.
<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/d034bcd3-ea14-44e1-8480-48bc433ef306" />


Now open the saved .mag file using the command **`magic -T sky130A.tch sky130_vsdinv.mag &`**


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/abd41a2e-1a93-4ae1-bb91-507d51bc2a0b" />


Now in the tkcon terminal use the command **`lef write`** in order to create a LEF file.


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/561b4cf2-a205-4cbb-88ae-409bad204f19" />

 Now we can open the LEF file and go through it.


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/712bf695-787b-4583-a996-5e81e940c9d8" />

 
### Introduction to timing libs and steps to include new cell in synthesis


To proceed futher lets keep all the required files at single place thet is in src directory. First copy the extracted LEF file into src directory.

After LEF file we need to copy the required libraries, here we will have different types of libraries such as fast , slow, typical etc.. , we need to copy all those .lib files to src directory by using **`cp`** command.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/b84211f1-4566-42b7-8620-72d6934b950f" />


Now we need to make some changes in the .config file as shown in the image
<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/c74a1945-ac49-4dfc-88f1-ccbc4615b78a" />



After that we need to open bash using command **`docker`** being in openlane directory. And enter into the open lane and prepare the design as shown in figure. Once preparation is complete we need to use following commands 

**`set lefs [glob $::env(DESIGN_DIR)/src/*.lef]`**

**`add_lefs -src $lefs`**

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/a20bd83c-53bb-4529-8de5-1def9e1db4cb" />

And now again use the command **`run_synthesis`** and check whether it maps our custom vsdinverter or not.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/e13893b1-8134-451f-9fb0-9333382bd993" />


From the above figure we can see that synthesis was succesful and also we have 1554 instances of our vsdinverter. So this stage is successful.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/5a18bcd2-44f0-4bb7-8f59-2d4e9a2f04f6" />


 Now as we done with Floorplan stage, we can proceed to placement stage by using the command **`run_placement`**

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/65889100-7355-49fb-b8cf-569c195aec13" />

 Now after the placement is done,lets check whether the cell that we have created is placed in the design. For this being in the placement directory we should use the command

 **`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`**

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/73595a73-adaa-4eda-8103-118f0535a58c" />


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/ec8195a0-b6a6-4bb6-a799-c7247c77920e" />



 Clearly we can see that the cell that we have created " sky130_vsdinv" is placed in the design and now lets check whether it is alligned correctly with other cells or not by using the command **`expand`** in the tkcon terminal.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/9fe7adf8-d470-4931-9ccf-9516508012e8" />


 Yes,Its perfectly alligned!



 ## Timing analysis with ideal clocks using openSTA


 ### Lab steps to configure OpenSTA for post-synth timing analysis


Next step is to perform STA on the design. For this first we need to complete the synthesis stage. After synthesis is done some steps need to be followed.

First, we need to create a new file **`pre_sta.conf`** in the openlane directory.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/1a5a4172-1291-4fd4-8235-bdbf1485b127" />


After that we need to create another file called **`my_base.sdc`** in the src directory which is picorv32a directory.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/525fd559-ebe4-456a-902b-e52237a5d423" />


Now we need to use the command **`sta pre_sta.conf`** being in the openlane directory.

We can say that STA is succesful when the slack that we will get equals to that of synthesis stage.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/b7742aa1-9029-41fe-9f23-9bedf34e503d" />


As we can see that Slack is equal to of that we got in synthesis stage. So STA is succesful.



## Clock tree synthesis TritonCTS and signal integrity


### Lab steps to run CTS using TritonCTS


After improving the timing of the design, the previous design should be replaced with improved design by using the command

**`write_verilog //path of the previous design//`**

Now the design will get updated with the improved version.

Now we can start working on it, starting with Floorplan by using the same commands that were used before. After succesful completion of Floorplan we should do placement by using the command **`run_placement`**.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/d403b13b-8d66-4b88-abe2-1ae54ad0396d" />

After placement is done, we can proceed with cts stage. To perform CTS we should use the command **`run_cts`**.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/1f84ea04-c0c0-41c7-aa97-c76f5d798ea9" />


After completion of the cts we can observe that in the synthesis results directory a new **.cts** file is added. The newly added CTS file contains both the previous netlist and also the clock buffers that were added during the cts stage.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/8611036b-5bc4-4ce9-9c95-ddda2c2a5128" />



## Timing analysis with real clocks using openSTA


### Lab steps to analyze timing with real clocks using OpenSTA


 To create a database in the openroad, first we need to enter into the openroad by using the command **`openroad`**.

 After that we need to follow the following list of commands in the openroad

 **`read_lef /openLANE_flow/designs/picorv32a/runs/04-05_21-50/tmp/merged.lef`**

 **`read_def /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/cts/picorv32a.cts.def`**

 **`write_db pico_cts.db`**

 **`read_db pico_cts.db`**

 **`read_verilog /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/synthesis/picorv32a.synthesis_cts.v`**

 **`read_liberty $::env(LIB_SYNTH_COMPLETE)`**

 **`read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc`**

 **`set_propagated_clock [all_clocks]`**

**`report_checks -path_delay min_max -format full_clock_expanded -digits 4`**

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/6b15b30f-8817-4559-bdea-65041186807c" />

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/29e4347b-6e07-4503-bb0d-0d5d1583eba1" />



After all these steps the db will get created and by using the last command we will get a timing report too.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/59e69c26-eb7c-4901-b3b4-c277c606eede" />



### Lab steps to execute OpenSTA with right timing libraries and CTS assignment


To remove sky130_fd_sc_hd__clkbuf_1 from the list

**`set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]`**

To check the current value of CTS_CLK_BUFFER_LIST

**`echo $::env(CTS_CLK_BUFFER_LIST)`**

To check the current value of CURRENT_DEF

**`echo $::env(CURRENT_DEF)`**

To set def as placement def

**`set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/placement/picorv32a.placement.def`**

To run cts

**`run_cts`**

To check the current value of CTS_CLK_BUFFER_LIST

**`echo $::env(CTS_CLK_BUFFER_LIST)`**



### Lab steps to observe impact of bigger CTS buffers on setup and hold timing


We need to follow the similar steps that we have followed earlier in the openroad.

**`read_lef /openLANE_flow/designs/picorv32a/runs/04-05_21-50/tmp/merged.lef`**

**`read_def /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/cts/picorv32a.cts.def`**

**`write_db pico_cts1.db`**

**`read_db pico_cts1.db`**

**`read_verilog /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/synthesis/picorv32a.synthesis_cts.v`**

**`read_liberty $::env(LIB_SYNTH_COMPLETE)`**

**`link_design picorv32a`**

**`read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc`**

**`set_propagated_clock [all_clocks]`**

**`report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4`**

**`report_clock_skew -hold`**

**`report_clock_skew -setup`**


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/0e5bedc1-5397-4132-8eb1-d032ee8b15de" />


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/229d89ee-b299-4b07-a65c-0d1949209406" />
