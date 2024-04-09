# VSD_Digital_SoC_Design
# Day-1 Introduction to Open Source SoC Design using Openlane:

## 1.1 What is a SoC?
SoC refers to the term System on a Chip. It is a single chip which integrates a whole electronic or a system into it. A SoC may contain digital, analog, mixed-signal devices on the same chip. In a traditional computer system architecture, each system component such as CPU, controller chips, a GPU, and RAM etc., used to be separately installed on the board, but thanks to technological advancements in the semiconductor industry has enabled more and more elements to be integrated in a single silicon chip.
 A current-day system on a chip (SoC) consists of several different components of a system such as the CPU (a microprocessor or microcontroller), memory, input/output (I/O) interface and wireless blocks, on a single silicon substrate. Most SoCs also use various pre-designed hardware block, called as IP Cores, to improve design time to market.

Since it has all the system components on one single chip, SoCs offer the advantages of reduced size, overall system cost, lower power consumption and Increased performance. SoCs are becoming increasingly popular with the growth of mobile computing and IoT (Internet of Things) devices.

## 1.2 SoC Design Flow:
SoC development process can be broken into multiple stages as illustrated in the following figure:
 
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/3e38bb6a-1ae0-4b1c-868b-fe37b18a04cd)

## 1.3 What is Openlane?

OpenLane is a powerful and versatile infrastructure library that enables the construction of digital ASIC physical implementation flows based on open-source and commercial EDA tools. It includes a reference flow (Classic) that is constructed entirely using open-source EDA tools –abstracting their behavior and allowing the user to configure them using a single file. OpenLane also supports extending or modifying flows using Python scripts and utilities. Here are some of the key benefits of using OpenLane:

Flexibility and extensibility: OpenLane is designed to be flexible and extensible, allowing designers to customize the flow to meet their specific needs by developing Python scripts (plugins) and utilities or by modifying the existing configuration file.

Open source: OpenLane is an open-source project that is freely available to use and modify, which makes it a good choice for designers looking for a transparent, cost-effective solution.

Community support: OpenLane capitalizes on OpenLane’s existing community of users and contributors, which means that a wealth of resources is available to help designers get started and troubleshoot any problems they encounter.

![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/c08411b9-fa78-4f21-b14f-6c9b67df6a4e) (Openlane flow)

[Link to Openlane Documentation](https://openlane2.readthedocs.io/en/latest/getting_started/newcomers/index.html#newcomers)

## 1.4 Lab 1: Run  synthesis on "picorv32a" design using Openlane flow,generate outputs and analyse the results,by determining flop ratio.

   Step 1 : Change directory to /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane
    ![changing to openlane directory](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/7b87a8ce-0738-4990-91e2-051831b92c3b)

   Step 2 : set alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u
   
   Step 3 : Invoke Openlane using 'docker' command
   
   Step 4 : Run Openlane flow in interactive mode using following command: ./flow.tcl -interactive
    ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/6e88e7e3-3ea5-497d-a53f-9303ac153d1f)

   Step 5 :Input required package for openlane flow, prep the design and then run synthesis
   
   package require openlane 0.9 #inputs required package for openlane flow
   
   prep -design picorv32a #prepares the picorv32a design for openlane flow
   
   run_synthesis #run synthesis for the prepared design
            
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/b4429451-7253-438d-9f26-49aee4aa8177)
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/4bf08195-3108-487b-825c-fe45aab62ded)
            
   Step 6 : Characterizing synthesis results:
   ![synthesis no  of cells_rpt](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/cad080a3-6921-4b04-bb88-c442fe4272dc)
   ![synthesis no  of DFF_rpt](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/155231b0-bb92-4b95-8f6c-11ff93c398cd)

   Flop Ratio =  (Total no.of DFF’s)/(Total no.of Standard Cells)=1613/14876=0.10843

   # Day-2 Floorplanning and Placement:

   ## 2.1 Lab 2: Run floorplanning & placement for the synthesized design,generate outputs and review the results:
   
   Step 1 : After synthesis of 'picorv32a' design is completed, edit "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/sky130A_sky130_fd_sc_hd_config.tcl" and add your desired 
   floorplan options regarding values of core utilization,aspect ratio,IO metal layer used,core to die offset margin etc.,which would override the default values present in 
   "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/configuration/floorplan.tcl".
   The description of different variables used in the flow at different stages is present "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/configuration/README.md" file

   README.md file describing variables used in flow:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/ca117d0d-cb6e-4f8f-9b62-b657216e4fc3)

   floorplan.tcl file containing default floorplan values:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/8825bc4b-b492-4a85-a0ed-57b059af4cc9)

   floorplan values used for current design:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/6905d727-f7d8-4732-baab-36ac4d008280)

   Step 2 : After floorplan values are set and synthesis is completed, enter
   run_floorplan # runs floorplan for current synthesized design,with floorplan values set in config.tcl file for the current design
   
   floorplan run completed:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/c5c40843-d5d5-4234-87b5-dc89691f4399)

   Step 3 : Calculating Die Area from floorplan.def :

   floorplan.def screenshot:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/94c452db-e4f0-4c11-8334-36fba1a3e004)

   According to values present in floorplan.def :
      1 µm = 1000 unit distance
      Die width in unit distance = 507215 - 0 = 507215
      Die height in unit distance = 517935 - 0 = 517935
      Die width in µm = 507125/1000=507.125 µm 
      Die height in µm = 517935/1000=517.935 µm 
      Die Area in µm^2 = (507.125 * 517.935) µm^2 = 262657.786 µm^2

   Step 4: Loading generated floorplan.def in magic tool and exploring it:

   cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/06-04_14-54/results/floorplan # Change directory to folder containing floorplan.def file

   magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def & # load floorplan.def in magic tool

   floorplan.def screenshot in magic tool:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/c1497daa-2d23-44de-b9a8-7e4961c239dc)

   Equidistant placement of ports:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/c6b3b4eb-93d3-418d-a0c0-9946a59d55cd)

   Port layer as we have set in config.tcl:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a5e83472-d850-4d3d-bce5-f8f2b0ee0d77)
   ![vertical io layer information](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/5978114a-8dfe-4056-bb3a-1a4290822df7)

   Decap cell locations at end of rows (as they are set as endcap in config.tcl):
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/0e127d81-70a7-486c-a69c-e966566285b5)

   Tap cells location (diagonally equidistant):
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/264a03fa-0606-45fc-99e6-6403cb0adfba)

   Unplaced standard cells present at origin:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/61cdd5de-ff8e-4610-9363-7ea10257e266)

   Step 5:Run congestion aware placement,generate outputs and review results:

   run_placement #run congestion-aware placement
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/fc08331c-587a-4062-aa73-51ca7235ffc5)

   Step 6: Loading generated placement.def in magic tool and exploring it:

   cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/06-04_16-22/results/placement  # Change directory to folder containing placement.def file

   magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def & # load floorplan.def in magic tool

   placement.def screenshot in magic tool:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/eaf1ab52-f85a-40bb-8e0a-434c194c4bfd)

   Legally Placed standard cells:
   ![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/b5e9317a-2781-4af4-b8e4-b51894f7a0f3)


# Day-3 Design library cell using Magic Layout and ngspice characterization:

## 2.1 Lab 2: Design library cell using Magic Layout and perform ngspice characterization:

Step 1 : Clone custom inverter standard cell design from github repository :

cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane # Change directory to openlane directory.

git clone https://github.com/nickson-jose/vsdstdcelldesign # Clone the repository with custom inverter design.

cd vsdstdcelldesign # Change into repository directory.

cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech . # Copy magic tech file to the repo directory for easy access.

magic -T sky130A.tech sky130_inv.mag & # Command to open custom inverter layout in magic.
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/5aec9a95-a5b2-4ea0-96b2-6079f27d3e58)

Step 2 : View custom inverter layout in magic tool:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/b4af8a3d-56af-4022-b254-2e2b47f8ff06)

custom inverter nmos:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/0c5406ac-12fb-45b8-8da7-cc15f17ecfc0)

custom inverter pmos:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/ce8cbf08-e529-4d43-b726-af674c36350c)

DRC after polysilicon layer deletion:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/c3dcee1d-6c27-4d7f-af7e-55e18e8ef4c7)

Step 3 : SPICE extraction of inverter in magic:

extract all # Extraction command to Extract sky130_inv into sky130_inv.ext in present working directory

ext2spice cthresh 0 rthresh 0 # enable the parasitic extraction before converting ext to spice 

ext2spice # convert .ext file to .spice file

tkcon window after running above commands:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/fb970d77-130a-40cb-beec-13410616cce8)

Extracted SPICE file:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/54687e28-5ed4-40ca-bf04-403d8dc91d9f)

Extracted SPICE file edited for transient analysis:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/9bbb1646-c168-4958-9610-205cd273cdc5)

Step 4 : ngspice simulation of edited extracted spice netlist file,performing transient analysis,and calculation rise,fall transition and cell delays:

ngspice sky130_inv.spice # Command to load spice file for simulation to ngspice

plot y vs time a #plot output and input vs time characteristics

ngspice run screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a02d6111-6fb8-4bfe-bf54-33bdb47c8c64)

screenshot of generated plot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a8e1f9f4-d381-423f-9840-c41ab4d0020c)

Rise Transition time = Time taken for signal to rise to 80% of final value – Time taken for signal to rise to 20% of final value
Fall Transition time = Time taken for signal to fall to 20% of final value – Time taken for signal to fall to 80% of final value
Rise cell Delay = Time taken for output to rise to 50% - Time taken for input to fall to 50%
Fall cell Delay = Time taken for output to fall to 50% - Time taken for input to rise to 50%

20% of 3.3V=0.66V 80% of 3.3V=2.64V 50% of output=1.65V

20% output rise screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/aabd4161-266c-4c2b-b455-e67e971501b2)

80% output rise screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/1b12136d-623f-4094-99b7-92f8646eefdc)

ngspice output rise transition values corresponding terminal window screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/fcaec6f2-6e76-45ff-8901-516399a1a3d1)

Output Rise Transition time = (2.24039 - 2.18024) ns = 0.6015ns

20% output fall screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/b4d63039-3521-48b7-866f-5f9bf5d01861)

80% output fall screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/0eba35ee-55b8-4d0a-8673-b935847e3de8)

ngspice output fall transition values corresponding terminal window screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/b6c4692e-b2a5-48ec-a39e-e8ec7989f99d)

Output Fall Transition time = (4.09349 - 4.05097) ns = 0.04252ns

plot for rise delay:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/326b0b25-70b8-4444-a7d0-a444a7c14ad4)

ngspice output for rise delay:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a3ae06d2-aeeb-415f-a13a-70cf6de22c59)

Rise cell delay = (2.20782 - 2.14966) ns = 0.05816ns

plot for fall delay:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/8afc0f06-a132-4161-914d-e1c1b502dfdf)

ngspice output for fall delay:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/02967178-3a09-4f8a-9279-ddeb85eef3fc)

Fall cell delay = (4.07585 - 4.04943) ns = 0.02602ns




























   












    




    







