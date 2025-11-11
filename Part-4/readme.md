
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

 ![Screenshot from 2024-05-03 14-25-47](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/c2dfc964-c417-409b-a3c4-6f799d31741e)

 In the cell design input and output ports are on the li1 layer.We need to convert the grid into tracks.

 Open the tkcon window and give the command for grid according to the track file.

![Screenshot from 2024-05-03 14-41-05](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/3e6c78c1-4883-4858-8332-3cb6d451dfbb)

 Now we can see that both input and output ports are placed at the intersection of the tracks. Here our second condition also satisfies as 3 boxes are covered between the boundaries.

![Screenshot from 2024-05-03 14-43-07](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/11ac8a4d-9e0f-40fa-9b70-d07415a46ca2)



### Lab steps to convert magic layout to standard cell LEF


Now we need to extract the LEF file.First save .mag file by using the command **`save sky130_vsdinv.mag`** in the tkcon terminal.

![Screenshot from 2024-05-03 15-06-12](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/773a41d2-5c04-4481-bd6c-0342d686e21f)

Now open the saved .mag file using the command **`magic -T sky130A.tch sky130_vsdinv.mag &`**

![Screenshot from 2024-05-03 15-10-20](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/1b3829cf-0f5b-4bfc-bc41-089e1014f306)

Now in the tkcon terminal use the command **`lef write`** in order to create a LEF file.

![Screenshot from 2024-05-03 15-12-34](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/eebf9888-d9fa-4d53-a91c-d3998b1faaef)

 Now we can open the LEF file and go through it.

![Screenshot from 2024-05-03 15-15-52](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/85905d3c-ccdc-4f3a-ad3c-ccda8672cb70)

 
### Introduction to timing libs and steps to include new cell in synthesis


To proceed futher lets keep all the required files at single place thet is in src directory. First copy the extracted LEF file into src directory.

After LEF file we need to copy the required libraries, here we will have different types of libraries such as fast , slow, typical etc.. , we need to copy all those .lib files to src directory by using **`cp`** command.

  ![Screenshot from 2024-05-03 15-40-24](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/d5eda7fb-d80f-4ae2-b393-b5d3807c44d2)

Now we need to make some changes in the .config file as shown in the image

![Screenshot from 2024-05-03 16-01-12](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/635dbe20-014c-4eb8-a798-5c360be1f282)

After that we need to open bash using command **`docker`** being in openlane directory. And enter into the open lane and prepare the design as shown in figure. Once preparation is complete we need to use following commands 

**`set lefs [glob $::env(DESIGN_DIR)/src/*.lef]`**

**`add_lefs -src $lefs`**

![Screenshot from 2024-05-03 16-22-21](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/ae8f5081-bccd-4e13-a4c4-ebb9704e8d83)

And now again use the command **`run_synthesis`** and check whether it maps our custom vsdinverter or not.

![Screenshot from 2024-05-03 16-28-45](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/34d10bf0-9d1c-4795-af34-c74ebfc6a03f)

From the above figure we can see that synthesis was succesful and also we have 1554 instances of our vsdinverter. So this stage is successful.




![Screenshot from 2024-05-03 22-50-28](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/a035ddeb-bb1d-4ff5-8760-4bac7fcd62c6)

 Now as we done with Floorplan stage, we can proceed to placement stage by using the command **`run_placement`**

![Screenshot from 2024-05-03 22-51-48](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/2c16610e-7eac-4855-a2f5-8ee1d2fdc4b1)

 Now after the placement is done,lets check whether the cell that we have created is placed in the design. For this being in the placement directory we should use the command

 **`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`**

![Screenshot from 2024-05-03 23-01-51](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/90cd7edf-09d6-4c67-94ac-baeb8ebe49b2)

![Screenshot from 2024-05-03 23-04-53](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/943b3346-a76b-4dbe-8079-b55e0c5da016)


 Clearly we can see that the cell that we have created " sky130_vsdinv" is placed in the design and now lets check whether it is alligned correctly with other cells or not by using the command **`expand`** in the tkcon terminal.

![Screenshot from 2024-05-03 23-06-49](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/0117d6f3-7935-4e30-84c6-5f97865d5b89)

 Yes,Its perfectly alligned!



 ## Timing analysis with ideal clocks using openSTA


 ### Lab steps to configure OpenSTA for post-synth timing analysis


Next step is to perform STA on the design. For this first we need to complete the synthesis stage. After synthesis is done some steps need to be followed.

First, we need to create a new file **`pre_sta.conf`** in the openlane directory.

![pre_sta conf](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/7847af0f-d514-4277-b0db-fcc622cc3646)

After that we need to create another file called **`my_base.sdc`** in the src directory which is picorv32a directory.

![my_base sdc](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/0df33cc7-db83-4611-88df-e9cb2e0d196c)

Now we need to use the command **`sta pre_sta.conf`** being in the openlane directory.

We can say that STA is succesful when the slack that we will get equals to that of synthesis stage.

![sta_done](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/e8f90b9c-848f-49e5-bd7b-a7a78a0f48fe)

As we can see that Slack is equal to of that we got in synthesis stage. So STA is succesful.



## Clock tree synthesis TritonCTS and signal integrity


### Lab steps to run CTS using TritonCTS


After improving the timing of the design, the previous design should be replaced with improved design by using the command

**`write_verilog //path of the previous design//`**

Now the design will get updated with the improved version.

Now we can start working on it, starting with Floorplan by using the same commands that were used before. After succesful completion of Floorplan we should do placement by using the command **`run_placement`**.

![placement_done](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/b2bc9249-6c30-4ea1-a953-e102ec8c77f1)

After placement is done, we can proceed with cts stage. To perform CTS we should use the command **`run_cts`**.

![cts_done](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/a022b59d-6f48-4806-8b35-97626c8bf5bf)

After completion of the cts we can observe that in the synthesis results directory a new **.cts** file is added. The newly added CTS file contains both the previous netlist and also the clock buffers that were added during the cts stage.

![cts v _file](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/b21c6b13-f78f-45c9-a2dd-57c6f06cf0e8)


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

![steps_to_db](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/b2490265-5cce-4c54-a1a5-e04d928df9f0)

![db_created](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/d4b47d98-eef0-4e16-8845-4196fb1eb75b)


After all these steps the db will get created and by using the last command we will get a timing report too.

![db_done](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/03755c81-1025-4938-8176-a493c63881f5)


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

![Screenshot from 2024-05-05 06-23-26](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/10e89ad9-f9fd-4646-bf3a-b04e98980485)


![Screenshot from 2024-05-05 06-17-10](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/beee43d7-b727-41ad-b57e-c34c3879c155)
