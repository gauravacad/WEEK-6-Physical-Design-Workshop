
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

