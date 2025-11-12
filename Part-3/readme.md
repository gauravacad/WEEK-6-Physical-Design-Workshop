 
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

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/bdeb6058-a17f-42ff-947f-a3254b037bf2" />


Next we need to create a spice file using this extracted file to use within the ngspice tool.For this the command will be

**`ext2spice cthresh 0 rthresh 0`**, this will not create any new file. 

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/2ae3ed29-43f4-42a4-bac1-003cbf67c8d0" />


After that use command **`ext2spice`** , this will create a spice file in the vsdstdcelldesign directory.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/42903385-d88a-4d2b-a458-7eec33c12f51" />


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/72fcb1ad-77a2-4acd-873f-4762cd410888" />





## Sky130 Tech File Labs


### Lab Steps to create final SPICE deck using Sky130tech


After extracting the SPICE file, we need to update it according to the design.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/8822fcaf-eb30-42dc-b5e7-205da269dab6" />


After that we need to run the SPICE file in the ngspice tool by using the command  **`ngspice sky130_inv.spice`**

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/bce30f08-5519-4132-8cd7-1cc46fbaf025" />


Now we need to verify the plot of output vs time, we need to use the command  **`plot y vs time a`**

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/de1cb66c-e447-432a-8b6e-3572922d8a3d" />




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

  <img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/aa9c8b3a-b8a5-4af6-a016-72e3a2b62eaa" />


 <img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/c98c0e45-5e8c-4aee-8790-653a0f70bf0e" />




  ### Lab Introduction to Magic and steps to load Sky130 tech-rules


  Use the command **`magic -d XR`** to open the Magic tool

  <img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/869ab2b8-a752-43b0-8d1b-31ce861d2e27" />



  Now, select an area in the gui and guide the pointer on to the metal 3 layer and press P. The selected region will be filled with metal 3. Now in tkcon terminal type the command **`cif see VIA2`** , The metal 3 filled area will be filled VIA2 mask.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/434eb4e0-e6a6-4598-89ca-12cd50e0cca2" />




 ### Lab exercise to fix Poly-9 error in Sky130 tech file


 Now, lets work on the poly.9 file. Load it into the magic tool by using the command **`load poly.mag`**  in tkcon terminal.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/f4fbcb89-e2ed-49c6-8aa5-6b47d8955f3f" />



 Check for the spacing between Poly resistor and poly in the layout and compare it with the actual value in the Skywater website. In the image below we can clearly see the error in spacing 
 between them. So now lets resolve it

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/ad3bfc88-b8b9-43f9-9c97-c35f0419794d" />



<img width="1157" height="444" alt="image" src="https://github.com/user-attachments/assets/a1e25c02-f2ea-4233-80b1-b87c1de142dc" />



Open the Sky130a.tech file, which is in the drc_tests directory and check for poly.9 keyword and make the changes that are shown in the images below and save it.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/34962f56-79c5-4626-a3b5-792a2ee69766" />


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/7aa498fe-b6a7-43e1-b55c-6a2262f5e128" />


 Now again load the tech file by using the command **`tech load sky130A.tech`** , and again check drc by using command **`drc check`** in the tkcon terminal.

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/04d07231-2a5d-49a9-bc30-21d0ee0c585d" />




### Lab challenge exercise to describe DRC error as geometrical construct
 

Now load nwell.mag file into the magic and check for violations.

<img width="906" height="397" alt="image" src="https://github.com/user-attachments/assets/7226c11e-c163-479a-a445-d7fa343e0f0a" />


<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/19513a98-fb3e-4e66-ba1b-06edeb947b10" />


In the above layout we have some violations, Open tech file and make changes as shown

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/c26576da-ef37-4f6c-bf7b-95f4b134ffc1" />



<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/2540069b-706a-42a9-afc4-26275cc97075" />




### Lab challenge to find missing or Incorrect rules and fix them


After updating the tech file load it again and check for errors

<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/5c640e02-5941-4b2c-80f8-cf26279c9b14" />


Now after tapping the nwell violations are resolved.




