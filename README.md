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

**Front End** involes the following steps:

1. **Specification and Architecture Definition**:
   - Define the requirements and functionality of the ASIC.
   - Create the architectural design, including block diagrams and high-level logic.

2. **RTL Design and Simulation**:
   - Write Register Transfer Level (RTL) code using hardware description languages like Verilog or VHDL.
   - Simulate the RTL design to verify functionality and performance using tools like ModelSim or VCS.

3. **Synthesis & Gate Level Netlist**:
   - Convert the RTL code into a gate-level netlist using synthesis tools such as Synopsys Design Compiler or Cadence Genus.
   - Optimize the netlist for area, power, and timing constraints.<br>
**Back End** involves the following steps:

4. **Static Timing Analysis (STA)**:
   - Perform STA to ensure that timing requirements are met and that there are no violations.
   - Address any timing issues through design modifications or constraints.

5. **Floorplanning and Place-and-Route**:
   - Define the physical layout of the ASIC including placement of functional blocks and routing channels.
   - Use tools like Cadence Innovus or Synopsys ICC for automated place-and-route.

6. **Physical Verification**:
   - Perform Design Rule Checking (DRC) and Layout vs. Schematic (LVS) checks to ensure layout correctness and adherence to manufacturing rules.
   - Address any violations found during physical verification.

7. **Post-Silicon Validation**:
   - Fabricate the ASIC using semiconductor manufacturing processes.
   - Test and validate the fabricated ASIC to ensure functionality and performance meet specifications.

8. **Production and Deployment**:
   - Once validated, the ASIC is ready for mass production.
   - Deploy the ASIC in the target application or market.

