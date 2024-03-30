# VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK
This repo is about my journey through VSDIAT Advanced Physical Design course using SkyWater 130nm PDK &amp; open source EDA tools. 
# Day-1

## Introduction

**ASIC** stands for **Application-Specific Integrated Circuit**. An ASIC is a type of integrated circuit (IC) that is designed for a specific application or purpose. Unlike general-purpose ICs such as microprocessors or memory chips, which are designed to perform a wide range of functions, ASICs are tailored to perform a single function or a set of closely related functions efficiently.
## Types of ASICs

1. **Full-Custom ASICs**:
   - Designed from scratch, offering maximum performance and customization.
   - Require significant time, expertise, and cost for development.

2. **Semi-Custom ASICs**:
   - Utilize pre-designed and pre-verified blocks (IP cores or libraries) along with custom-designed portions.
   - Strike a balance between performance and design effort.

3. **Programmable ASICs (FPGAs)**:
   - While not strictly ASICs, Field-Programmable Gate Arrays (FPGAs) offer reconfigurable logic.
   - Can be programmed to perform specific functions, providing flexibility similar to ASICs but with less performance optimization.

## ASIC Design Flow

The ASIC design flow outlines the process of designing and fabricating an Application-Specific Integrated Circuit. The flow can be boardly be clasified into **Front End** & **Back End**:<br>

-**Front End** involes the following steps:

1. **Specification and Architecture Definition**:
   - Define the requirements and functionality of the ASIC.
   - Create the architectural design, including block diagrams and high-level logic.

2. **RTL Design and Simulation**:
   - Write Register Transfer Level (RTL) code using hardware description languages like Verilog or VHDL.
   - Simulate the RTL design to verify functionality and performance using tools like ModelSim or VCS.

3. **Synthesis & Gate Level Netlist**:
   - Convert the RTL code into a gate-level netlist using synthesis tools such as Synopsys Design Compiler or Cadence Genus.
   - Optimize the netlist for area, power, and timing constraints.<br>


-**Back End** involves the following steps:

4. **Static Timing Analysis (STA)**:
   - Perform STA to ensure that timing requirements are met and that there are no violations.
   - Address any timing issues through design modifications or constraints.

5. **Floorplanning and Place-and-Route**:
   - Define the physical layout of the ASIC including placement of functional blocks and routing channels.
   - Use tools like Cadence Innovus or Synopsys ICC for automated place-and-route.

6. **Physical Verification**:
   - Perform Design Rule Checking (DRC) and Layout vs. Schematic (LVS) checks to ensure layout correctness and adherence to manufacturing rules.
   - Address any violations found during physical verification.
   - GDS II file will be forwarded to foundry.
7. **Post-Silicon Validation**:
   - Fabricate the ASIC using semiconductor manufacturing processes.
   - Test and validate the fabricated ASIC to ensure functionality and performance meet specifications.

8. **Production and Deployment**:
   - Once validated, the ASIC is ready for mass production.
   - Deploy the ASIC in the target application or market.

![Design Flow](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/a3ba69f3-3d2a-4653-af35-ee4543156f2f)
Source:[https://pdfreshers.blogspot.com/2018/12/asic-design-flow.html](https://pdfreshers.blogspot.com/2018/12/asic-design-flow.html)
<br><br><br>

## OpenLane:

**OpenLane** uses SkyWater's 130nm Process Design Kit (PDK) and incorporates many open-source Electronic Design Automation (EDA) tools for each of the anove mentioned flow steps. Some of the EDA tools used in OpenLane include:

- RTL Synthesis, Technology Mapping, and Formal Verification: Yosys + ABC
- Static Timing Analysis: OpenSTA
- Floor Planning: init_fp, ioPlacer, pdn, and tapcell
- Placement: RePLace (Global), Resizer, OpenPhySyn (formerly), OpenDP (Detailed)
- Clock Tree Synthesis: TritonCTS
- Fill Insertion: OpenDP/filler_placement
- Routing: FastRoute or CU-GR (formerly), TritonRoute (Detailed) or DR-CU
- SPEF Extraction: OpenRCX or SPEF-Extractor (formerly)
- GDSII Streaming out: Magic and KLayout
- DRC Checks: Magic and KLayout
- LVS check: Netgen
- Antenna Checks: Magic
- Circuit Validity Checker: CVC

The main goal of OpenLane was to create an open-source RTL to GDSII platform that generates a GDSII file without requiring human intervention. We can run OpenLane flow in **interactive mode** too using **"-interactive"** option. OpenLane design flow is described by the below image.

![OpenLane Design Flow](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/2fc18871-5344-46de-afba-50dbf99a148a)<br>
Source: [https://openlane.readthedocs.io/en/latest/flow_overview.html](https://openlane.readthedocs.io/en/latest/flow_overview.html)

<br>
<br>
<br>


## Getting Started

To list the tools and PDKs we will be using, follow these steps in your terminal:

1. Navigate to the work folder on your desktop using the `cd` command:
   ```bash
   cd Desktop/
   cd work/
   cd vsdflow/
   cd work/
   cd tools/
   ls -ltr
![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 10_31_20 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/572ba914-887d-4984-b2c5-a4393cd72091)




2. To list all the PDKs:
   ```bash
   cd Desktop/
   cd work/
   cd tools/
   cd openlane_working_dir/
   cd pdks/
   ls -ltr
![Screenshot 3_28_2024 10_47_16 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/f12a72e3-d2bb-4f92-a0a1-7d92d8d50185)




3. Whatever work we will be doing, it will be in the openlane directory, to open it follow the below steps in terminal,
   ```bash
   cd Desktop/
   cd work/
   cd tools/
   cd openlane_working_dir/
   cd openlane/
![Captures 3_28_2024 10_58_25 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/bec472e7-0a47-4fe3-bd8f-4e38b2a66915)

   


4. To run OpenLane in interactive mode follow the following steps after opening the openlane directory as shown in above image:
   ```bash
   docker
   pwd
   ./flow.tcl -interactive
![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 11_40_27 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/7bd8b59c-0a52-4cb7-9ca9-722eaf173601)
<br><br><br>
## The design flow of Picorv32a:


When we open the picorv32a directory in the terminal under the designs directory of the OpenLane directory, we will only see 3 files:

- `SRC` (which contains a Verilog-A file "picorv32a.v" & an SDC file that contains design constraints and timing assignments "picorv32a.sdc")
- `sky130A_sky130_fd_sc_hd_config.tcl`
- `config.tcl`

The order of timing and design parameters is as follows: `sky130A_sky130_fd_sc_hd_config.tcl` > `config.tcl` > `OpenLane default values`.

After opening OpenLane in interactive mode as shown above, we will begin the flow by creating various files needed using the command:

    `package require openlane 0.9<br>
    prep -design picorv32a`

If we list out the contents of picorv32a directory now we will see the new directory named runs created,
![Captures 3_28_2024 12_30_39 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/0f34c256-4248-498e-9ba8-08e0e5a431e9)



If we open the runs directory, we will find various new directories like `results`,`reports`logs`,`temp` created to store the various outputs of the design flow.
![Captures 3_28_2024 12_34_25 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/bdc64ed1-d47e-4acf-bc06-3239e8743b0a)


After preperation is completed we run synthesis using the command <br>
`run_synthesis`
<br>
openlane will run synthesis as well as Static Timing Analysis (STA) under the above command itself. After completion of the synthesis we will get a report as shown below.

![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 12_49_19 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/9e57ba65-928a-43e6-bfcd-955d481f05e1)


### Task-1:
**Flop Ratio:** It is the ratio of total number of D flip-flops to the total number of cells in a design.<br>
flop ratio = number of D flip-flop ÷ total number of cells<br>
<br>
![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 1_17_45 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/d2ab6c29-c54d-4449-aed8-ce9c6c1a1896)
Total number of D flip-flop in the design = 1613 <br>
<br>
![New Issue · tejasbg19_VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK - Google Chrome 3_28_2024 1_18_51 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/e3ec3a0d-812d-4463-af47-c9b7781b8d4a)
Total number of cells in the design = 14876<br>
therefore, flop ratio = 1613/14876 = 0.108429<br>
Therefore, the flop percentage = 10.84%

After synthesis, we initiate floor planning using:<br>

   `run_floorplan`

![Captures 3_28_2024 4_28_11 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/2a842f62-a80f-4b13-b678-e730a8b44299)

![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 4_27_37 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/cfef4541-19d3-4b4d-ae74-a3fdafb08144)

### Task-2:
**Die Area:**
![VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK_README md at main · tejasbg19_VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK - Google Chrome 3_28_2024 4_40_06 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/9ebe5c96-36fb-4f31-ba1a-f610de7fb3f4)

Area of die in micrometer = (660685*671405)*10^(12) = 443587.21um

#### Visualizing the floor plan using Magic:<br>
User
Area of die in micrometer = (660685*671405)*10^(12) = 443587.21um

#### Visualizing the floor plan using Magic:<br>
Open floor plan result & then pass the result to magic using below commands:
3. Whatever work we will be doing, it will be in the openlane directory, to open it follow the below steps in terminal,
  
         cd Desktop/
         cd work/
         cd tools/
         cd openlane_working_dir/
         cd openlane/
         cd designs/
         cd picorv32a/
         cd runs/
         cd 28-03_06-26/
         cd results/
         cd floorplan
         magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &


picorv32a floor plan in magic:
![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 5_01_06 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/c961dde3-e7cb-476a-a7b3-221a4519a97e)
<br>
zommed view of the die (select the section you want to zoom by placing cursor on it & pressing `s` key from keyboard and press `z` for zoom in and press `shift+z` to zoom out)

![VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK_README md at main · tejasbg19_VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK - Google Chrome 3_28_2024 5_30_04 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/6c28cdb6-2fef-4c8f-bf90-ab68f0d6e225)
After floor planning, we initiate placement using the following command in OpenLane:

      
      run_placement
 
![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 6_34_10 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/5f9bf537-ad15-4b11-be5c-3cbf4732be53)

We can visualize the placement in Magic using the following in terminal in `placement` directory of `result` directory:
     
      
      
      magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &




![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 6_34_41 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/863ed786-215e-4195-9c17-93c702dc2a5d)

![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 6_35_00 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/d55fc273-2c5d-435a-90e5-33d179b2ee45)


Zoomed view of the placement with `power(Vdd & Vss) mesh` clrealy visible as well as `standard cells` placed in `standard cell row`.
![vsdworkshop  Running  - Oracle VM VirtualBox 3_28_2024 6_59_26 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/5576a078-442c-405a-81bd-326c2320ba98)


# Day-3

## Importing vsdstdcell design from GitHub & analyzing using Magic Layout:

We need to clone the custom standard inverter repo [vsdstdcelldesign](https://github.com/nickson-jose/vsdstdcelldesign).
Follow the following steps in terminal to clone the above mentioned repo into openlane directory.
       
         cd Desktop/work/tools/openlane_working_dir/openlane
         git clone https://github.com/nickson-jose/vsdstdcelldesign


We can verify weather the cloning was sucessful or not using `ls -ltr` to list the contents of openlane directory.
Now we need to copy the magic tech files from pdks directory to our vsdstcelldesign directory to avoid giving the complete address of tech file every time we use `magic -T` command to view the layout, navigateto the magic tech files and follow the steps shown below,



         cd /Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic
         cp sky130A.tech Home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
![vsdworkshop  Running  - Oracle VM VirtualBox 3_29_2024 1_43_30 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/1fcdb152-1de9-490b-befb-dd4ab91e858e)
         
<br> <br>         

now we can open the downloaded vsdstdcell inverter using magic tool,

      cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
      magic -T sky130A.tech sky130_inv.mag &
![vsdworkshop  Running  - Oracle VM VirtualBox 3_29_2024 3_07_38 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/6a7dd1f6-8836-467b-a9a0-1660831de442)

### Verifying the different layers & connection of the inverter:

To know about a layer, place your cursor on it and press `s` from your keyboard, which will select the layer/cell, now type `what` in `tkcon` window of magic, it will give the name of the layer. 

![vsdworkshop  Running  - Oracle VM VirtualBox 3_29_2024 8_01_57 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/e617479b-38a2-4f1e-aa2f-d0cfd52cc2ea)
![vsdworkshop  Running  - Oracle VM VirtualBox 3_29_2024 8_19_19 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/24eb9790-be42-444d-ad42-4d4c8809a4f7)
To verify or know about the connectivity of a layer, place your cursor on the layer and press `s` twice or thrice, magic will highlight all the connections of the desired layer.


Verifying the connectivity of output with the drain of PMOS & NMOS
![vsdworkshop  Running  - Oracle VM VirtualBox 3_29_2024 8_21_43 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/cc969c7c-b5b6-4a55-8096-4cd87e5228f8)


Verifying the connectivity of source of PMOS to Vdd
![vsdworkshop  Running  - Oracle VM VirtualBox 3_29_2024 8_22_00 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/fe69c136-3cef-422c-8dc6-11a1f4b90988)

### DRC error in Magic

Whenever a DRC error occurs, find the error by navigating to `DRC` in magic and clicking on `DRC Find next error`, the tkcon window will display what error we have & according to that design needs to be corrected.

![vsdworkshop  Running  - Oracle VM VirtualBox 3_29_2024 9_42_54 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/14a473eb-bc9e-4f8a-8945-8e2b482b69d9)


DRC error being highlighted
![vsdworkshop  Running  - Oracle VM VirtualBox 3_29_2024 9_43_04 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/be0a4ec7-bf2c-4318-9a06-65f84de62235)


`tkcon` window showing the error.
![vsdworkshop  Running  - Oracle VM VirtualBox 3_29_2024 9_43_10 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/0a319b14-0fd8-4534-8ef5-c7733f261cda)



### SPICE extraction of inverter

To know in which which directory our tkcon window is opened used `pwd` command. Then use the command `extract all` command in tkcon window, this will create a new `.ext` in the same directory.

![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 10_27_43 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/8e54c161-3ba3-453e-9a78-6b859fe3c6f9)


Verifying weather `.ext` file has been created or not.
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 10_27_51 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/c7e44a72-1454-4ffc-bf13-8d16ada01bc0)



To get SPICE of `.spice` format, we use the following commands 


      ext2spice cthresh 0 rthresh 0
      ext2spice

To open the SPICE file, use the command `less (file name)`
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 10_34_41 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/c6e3931c-fb2b-4818-928a-171819e4922d)


To measure the size of unit grid box in magic, select one grid box & use the command `box` in `tkcon` window, whose output will look like the below image
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 10_54_46 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/22e8c79f-d856-45f9-a766-19e26a5cbdf8)


### Editing the SPICE file

`.spice` is edited as shown below in txt editor
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 11_40_28 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/c82377c4-4358-4517-9c74-b2cf8deb3b94)


after editing, install the ngspice simulator & run the `.spice` file as shown below
    
      

      sudo apt install ngspice 
      // password= vsdiat
      ngspice sky130_inv.spice

The above code should give you below output
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 11_42_21 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/7c12b973-5d9d-4e65-90b2-5c69c882c08d)


To plot the output, 


      plot y vs time a 

![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 11_48_13 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/d2b0bb1f-250b-421c-8345-05a31317aed9)
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 11_49_35 AM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/025bfaeb-fa58-4c3f-a70c-f0de7cb567de)


### Task-3
#### Characterization of the plot:
**Rise Transition:** The time taken by the output waveform to transit from a value of 20% of the maximum value to the 80 % of the maximum value.

Using right click, a new zoomed plot window cab be opened
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 12_07_22 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/b86c759b-166c-4617-811a-603cc5b49962)

![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 12_08_25 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/f5f38019-1d2d-4509-9f9b-398eaba23784)


ngspice will give the x & y coordinates of a point by just clicking on the points in plot.
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 12_22_30 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/b553a03c-deb5-4485-9830-cd9d89d3c804)

Therefore, Rise transition time = (2.24684 - 2.18233)ns = 0.06451ns 



**Fall Transition:** The time taken by the output waveform to transit from a value of 80% of the maximum value to the 20 % of the maximum value.
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 12_44_16 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/42db019b-45d7-456d-a4ad-c25fa84b033e)
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 12_43_55 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/3bc6033f-19f2-4335-85e6-6608deb44569)
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 12_43_21 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/02d4c66f-a20b-4c88-b300-06dd36055676)

Therefore the fall transition time = (4.09557 - 4.05304)ns = 0.04253ns 




**Rise Cell Delay /Rise Propagation Delay:** It is the diffrence time taken by Output to rise to 50% & Time taken by Input to fall to 50%
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 12_55_23 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/98f90509-f61c-4bd9-87ed-7120aee8abeb)
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 12_55_43 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/99fef724-adb7-4cb8-8ff4-eab3a4e961f9)
Therefor, Rise cell delay = (4.07805 - 4.05005)ns = 0.028ns


**Fall Cell Delay/ Fall Propagation Delay:** It is the difference time taken by Output to fall to 50% & Time taken by Input to rise to 50%
<br> similar to above we calculate the fall dealy


### Task-4
#### Identifying DRC errors in downloaded magic design & rectifying them:

Here we will download some deigns which have DRC errors and correct them as [the rules](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)
<br><br>
We will download designs from [open circuits archive](http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz) following the below steps,


   
      // we will download it in home directory
      cd 
      wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
      // to extract the compressed file
      tar xfz drc_tests.tgz
      cd drc_tests
      // to list all the compnents of the folder
      ls -al
      // to open magic in better quality
      magic -d XR &

![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 3_36_22 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/dd8e73dd-6fc7-40ed-a261-b48a6046a0a3)
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 3_36_33 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/997df863-f060-4c5e-bb3a-b5f0fb86b581)


#### DRC failure to identify poly to polyresistor distance violation

![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 5_55_13 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/d74968d2-e373-4e22-82f3-5a24f8d4ffcd)
As we can see in the above image even tough the height of the box or distance between poly & polyresisitor is 21um, we are not getting a DRC error(incorrect poly.9), we need to rectify it.

Firt open the `sky130A.tech` file in `viGMV` editor then add the rules that specify the distance between poly & polyresistor as below
   

    
     // inside drc_tests directory
     vi sky130A.tech

Then add the new rules as shown below
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 8_11_28 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/fa4a1151-e118-45b6-95c0-bc93bf9d4670)
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 8_13_40 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/04d321d0-d7c1-41b1-87c2-adae5634016e)


Then to load the newly edited tech file into magic use the below code in `tkcon` window of magic,
      
      
     
      tech load sky130A.tech
      drc check
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 8_18_48 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/d905d0dd-6200-48d2-ac5a-5cdb475b3b6e)
![vsdworkshop  Running  - Oracle VM VirtualBox 3_30_2024 8_21_03 PM](https://github.com/tejasbg19/VSDIAT_Advanced_Physical_Design_Using_Skywater130nm_PDK/assets/163899793/7b0533ee-9324-4428-9f3b-1f2f173c22c3)
