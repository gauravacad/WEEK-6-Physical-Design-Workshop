 
# Day-3: Design Library Cell using Magic Layout and ngspice Characterization  

## [Inception of Layout and CMOS fabrication process](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#inception-of-layout-and-cmos-fabrication-process)  

- [Lab steps to create std cell layout and extract spice netlist](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#lab-steps-to-create-std-cell-layout-and-extract-spice-netlist)  
- [Sky130 Tech File Labs](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#sky130-tech-file-labs)  
- [Lab Steps to create final SPICE deck using Sky130tech](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#lab-steps-to-create-final-spice-deck-using-sky130tech)  
- [Lab Steps to characterize the Inverter using sky130 model files](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#lab-steps-to-characterize-the-inverter-using-sky130-model-files)  

---

## [Lab Introduction to Sky130 PDKs and setup](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#lab-introduction-to-sky130-pdks-and-setup)  

- [Lab Introduction to Magic and steps to load Sky130 tech-rules](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#lab-introduction-to-magic-and-steps-to-load-sky130-tech-rules)  
- [Lab exercise to fix Poly-9 error in Sky130 tech file](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#lab-exercise-to-fix-poly-9-error-in-sky130-tech-file)  
- [Lab challenge exercise to describe DRC error as geometrical construct](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#lab-challenge-exercise-to-describe-drc-error-as-geometrical-construct)  
- [Lab challenge to find missing or incorrect rules and fix them](https://github.com/gauravacad/WEEK-6-Physical-Design-Workshop/tree/main/Part-3#lab-challenge-to-find-missing-or-incorrect-rules-and-fix-them)  



# Design library cell using Magic Layout and ngspice characterization


## Inception of Layout and CMOS fabrication process


### Lab steps to create std cell layout and extract spice netlist


We need to extract the spice netlist from the given Inverter from MAGIC Tool inorder to spice simulation in ngspice tool.

First we need to create an extraction file of the inverter. we can do this by using the command **`extract all`** in the tkcon window. This will create an extracted file in the vsdstdcelldesign directory.

![extracted](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/5044221d-1571-4f26-938f-61d2e3aeceab)

Next we need to create a spice file using this extracted file to use within the ngspice tool.For this the command will be

**`ext2spice cthresh 0 rthresh 0`**, this will not create any new file. 

![tkcon](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/4e4a6585-a209-4a4d-9ab6-ac933d074d77)

After that use command **`ext2spice`** , this will create a spice file in the vsdstdcelldesign directory.

![spice](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/0a8ba608-df8d-412d-9b32-09d2d9d6b24a)

![spice_file](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/37c0bd40-8f32-4f2f-a709-65811dccd312)




## Sky130 Tech File Labs


### Lab Steps to create final SPICE deck using Sky130tech


After extracting the SPICE file, we need to update it according to the design.

![Screenshot from 2024-05-02 11-36-21](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/476c1e09-654f-4853-942f-b30616fb74f8)

After that we need to run the SPICE file in the ngspice tool by using the command  **`ngspice sky130_inv.spice`**

![Screenshot from 2024-05-02 11-38-19](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/9fcf36ae-e6dd-46f3-8204-c4249a38ed22)

Now we need to verify the plot of output vs time, we need to use the command  **`plot y vs time a`**

![Screenshot from 2024-05-02 11-49-54](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/bf215ce3-1c35-406a-b93e-baedbfbd2def)



### Lab Steps to characterize the Inverter using sky130 model files


From the plot that we got from ngspice, we need to characterize four parameters of the Inverter.

- **Rise time** : It is the time taken for the output waveform to go to 80% of its max value from 20% of its max value.

  x0 = 6.16138e-09, y0 = 0.660007

  x0 = 6.20366e-09, y0 = 2.64009

  From the above values, Rise time = 0.0422 ns

- **Fall time** : It is the time taken for the output to fall from 80% of its max value to 20% of its max value.

  x0 = 8.04034e-09, y0 = 2.64003

   x0 = 8.06818e-09, y0 = 0.659993

    From the above values , Fall Time = 0.0278 ns

- **Propogation Delay** : It is the time taken for the 50% of transition from 0 to 1 at the output for the 50% transistion from 1 to 0 at the input side.

  x0 = 2.18449e-09, y0 = 1.64994

  x0 = 2.15e-09, y0 = 1.65011
     From the above values , Prop Delay = 0.034 ns

- **Cell Fall Delay** : It is the time taken for the 50% of transition from 1 to 0 at the output for the 50% transistion from 0 to 1 at the input side.

  x0 = 4.05432e-09, y0 = 1.65

  x0 = 4.05001e-09, y0 = 1.65

   From the above values , cell fall delay = 0.0043 ns

  We have succesfully characterized the Inverter, now we should create a LEF file.



  ### Lab Introduction to Sky130 pdk's and steps to download labs

  
  To download the lab files, being in the home directory use the command

  **`wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz`**

  Now you have downloaded the zip file. To extract the labs from the zip file use the command

  **`tar xfz drc_tests.tgz`**

  In the downloaded files , **`.magicrc`** file serves as the start-up script for MAGIC.

  ![Screenshot from 2024-05-02 14-46-09](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/5ff1b106-2271-4497-b7ec-07fd1bb3bd34)

  ![Screenshot from 2024-05-02 15-07-12](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/27f975da-cdff-4964-b65a-95699b11b791)



  ### Lab Introduction to Magic and steps to load Sky130 tech-rules


  Use the command **`magic -d XR`** to open the Magic tool

  ![Screenshot from 2024-05-02 15-16-02](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/dd47ceb4-4e8f-48db-a3c2-dd5fe5b88165)


  Now, select an area in the gui and guide the pointer on to the metal 3 layer and press P. The selected region will be filled with metal 3. Now in tkcon terminal type the command **`cif see VIA2`** , The metal 3 filled area will be filled VIA2 mask.

  ![Screenshot from 2024-05-02 15-44-45](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/644585de-de5d-412e-ac95-a16ad73e0d94)



 ### Lab exercise to fix Poly-9 error in Sky130 tech file


 Now, lets work on the poly.9 file. Load it into the magic tool by using the command **`load poly.mag`**  in tkcon terminal.

![Screenshot from 2024-05-02 23-54-49](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/be29d16e-1f2a-4271-909c-0ae05afa63a9)


 Check for the spacing between Poly resistor and poly in the layout and compare it with the actual value in the Skywater website. In the image below we can clearly see the error in spacing 
 between them. So now lets resolve it

![Screenshot from 2024-05-03 00-00-55](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/fbd1f1be-aa19-4b33-84fb-212b324fb471)


![Screenshot 2024-05-03 003013](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/7ed03823-bd72-4f6b-a40b-79839afc77c8)


Open the Sky130a.tech file, which is in the drc_tests directory and check for poly.9 keyword and make the changes that are shown in the images below and save it.

![Screenshot from 2024-05-03 00-12-48](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/5cd46200-35d0-4ed9-9737-1d1b9c01c5fb)

![Screenshot from 2024-05-03 00-17-50](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/64791bb7-7edc-4901-83d7-6d1c16745747)

 Now again load the tech file by using the command **`tech load sky130A.tech`** , and again check drc by using command **`drc check`** in the tkcon terminal.

![Screenshot from 2024-05-03 00-20-00](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/1cc3741e-e424-466d-b74a-ae7d24b9be1b)



### Lab challenge exercise to describe DRC error as geometrical construct
 

Now load nwell.mag file into the magic and check for violations.

![Screenshot 2024-05-03 012127](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/950b4a6a-dcaf-4e57-bf12-e6bda2ff602a)

![Screenshot from 2024-05-03 01-45-28](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/7ac6a97a-1ac4-4572-924c-fd4389de7862)

In the above layout we have some violations, Open tech file and make changes as shown

![Screenshot from 2024-05-03 01-32-47](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/1ac46750-2e45-45d1-b9df-0099222e9e19)


![Screenshot from 2024-05-03 01-36-45](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/cb7f2348-0880-4012-a6f4-fe26663efefc)



### Lab challenge to find missing or Incorrect rules and fix them


After updating the tech file load it again and check for errors

![Screenshot from 2024-05-03 01-44-19](https://github.com/katapavanteja/nasscom-vsd-soc-design-program/assets/168015988/f0a0fda2-7cda-4bd9-aee6-542aa47c7a41)

Now after tapping the nwell violations are resolved.



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

