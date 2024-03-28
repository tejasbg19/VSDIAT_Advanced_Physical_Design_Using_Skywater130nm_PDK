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
therefore, the flop percent = 10.84 %<br>


<br>
After synthesis we initiate floor planing using 
`run_floorplan`

