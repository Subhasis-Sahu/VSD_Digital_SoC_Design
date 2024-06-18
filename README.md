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
      * 1 µm = 1000 unit distance
      * Die width in unit distance = 507215 - 0 = 507215
      * Die height in unit distance = 517935 - 0 = 517935
      * Die width in µm = 507125/1000=507.125 µm 
      * Die height in µm = 517935/1000=517.935 µm 
      * Die Area in µm^2 = (507.125 * 517.935) µm^2 = 262657.786 µm^2

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

## 3.1 Lab 3: Design library cell using Magic Layout and perform ngspice characterization:

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

* extract all # Extraction command to Extract sky130_inv into sky130_inv.ext in present working directory

* ext2spice cthresh 0 rthresh 0 # enable the parasitic extraction before converting ext to spice 

* ext2spice # convert .ext file to .spice file

tkcon window after running above commands:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/fb970d77-130a-40cb-beec-13410616cce8)

Extracted SPICE file:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/54687e28-5ed4-40ca-bf04-403d8dc91d9f)

Extracted SPICE file edited for transient analysis:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/9bbb1646-c168-4958-9610-205cd273cdc5)

Step 4 : ngspice simulation of edited extracted spice netlist file,performing transient analysis,and calculation rise,fall transition and cell delays:

* ngspice sky130_inv.spice # Command to load spice file for simulation to ngspice

* plot y vs time a #plot output and input vs time characteristics

ngspice run screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a02d6111-6fb8-4bfe-bf54-33bdb47c8c64)

screenshot of generated plot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a8e1f9f4-d381-423f-9840-c41ab4d0020c)

* Rise Transition time = Time taken for signal to rise to 80% of final value – Time taken for signal to rise to 20% of final value
* Fall Transition time = Time taken for signal to fall to 20% of final value – Time taken for signal to fall to 80% of final value
* Rise cell Delay = Time taken for output to rise to 50% - Time taken for input to fall to 50%
* Fall cell Delay = Time taken for output to fall to 50% - Time taken for input to rise to 50%

* 20% of 3.3V=0.66V 80% of 3.3V=2.64V 50% of output=1.65V

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

Step 5: Finding problem in the DRC section of the old magic tech file for the skywater process and fixing them.

Link to Sky130 Periphery rules: [](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

cd # Change to home directory

wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz # Command to download the lab files

tar xfz drc_tests.tgz # command to extract lab file

cd drc_tests # Change directory into the lab folder


ls -al # List all files and directories present in the current directory


gvim .magicrc # Command to view .magicrc file


magic -d XR & # Command to open magic tool in better graphics

screenshots of commands run:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/5a448e2e-6ccf-41cb-9b31-7eccd60aa0e2)

Screenshot of magicrc file:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/66ca333d-613b-4efa-8606-a752912924bf)

Screenshot of poly rules:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/1322095c-799a-404e-9cb6-545bed920cf0)

Incorrect poly.9 rule implementation ((poly.9) Poly resistor spacing to poly or spacing (no overlap) to diff/tap 0.480 µm) (spacing present in layout less than 0.48 µm)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/cee89f1b-16d7-442a-be03-ab90b50ee086)

New lines added in sky130A.tech file to update drc:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/623357d8-a4cb-46fb-b1a4-fea1d3077a9f)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/af696cf2-9cf0-43cc-ae89-45fbe365dec9)

Commands to run in tkcon window after tech file edit:

tech load sky130A.tech # Load updated tech file

drc check # Must re-run drc check to see updated drc errors

drc why # show drc errors for selected region

magic window scrrenshot with edits to poly.9 rule,correctly implemented:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/3ac716c1-cbfe-41dc-8c8e-7d6d33151e1c)

nwell rules screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/3595994a-f04b-40eb-83ef-0af0e06b0c38)

Incorrectly implemented nwell.4 rule no drc violation even though no metal-contacted tap present in nwell:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/1284e673-ac3b-4ee1-8dff-0b99be48b90e)

Changes made in sky130A.tech file to properly implement nwell.4 rule:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/1b9ced5e-b123-4bda-93e0-1871b0bb9968)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/0ef092db-2d56-4861-a4bb-8b03cc0e2ce0)

Commands to run in tkcon window:

tech load sky130A.tech # Load updated tech file
drc check # Must re-run drc check to see updated drc errors
drc why # Selecting region displaying the new errors and getting the error messages 

magic tool screenshot with nwell.4 rule implemented:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/85276ceb-735a-42c3-bf66-1e0dee7d5db1)

# Day-4 Pre-layout timing analysis and importance of good clock tree:

Step 1: Verify if custom inverter cell is ready to be inserted into openlane flow:

Conditions to be verified before moving forward with custom designed cell layout:

Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.

tracks.info of sky130_fd_sc_hd screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/81f37ea1-11d2-4920-81ba-4ed818e718cd)


cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign # Change directory to vsdstdcelldesign

magic -T sky130A.tech sky130_inv.mag & # Command to open custom inverter layout in magic tool

help grid # Get syntax for grid command

grid 0.46um 0.34um 0.23um 0.17um # Set grid values according to values present in tracks.info file for sky130_fd_sc_hd

layout with new grid values:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/67f059a7-992d-4fff-8079-ed3ef298abb3)

Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.(verified)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/391fc377-0b4b-4b50-9561-f3db6f4ab1dc)

Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.(verified)
Horizontal Track Pitch=0.480 um and Width of standard cell =0.480*3=1.380 um
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a3da4690-866d-48be-a243-3a456f20fbf2)

Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.(verified)
Vertical Track Pitch=0.340 um and Width of standard cell =0.340*8=2.72 um
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/ad6ff531-8668-4880-9d1e-916948fedb45)


Step 2: save custom inverter layout with a name and generate its corresponding lef

save sky130_vsdinv.mag # Command to save layout with a given name

magic -T sky130A.tech sky130_vsdinv.mag & # Command to open custom inverter layout in magic tool

lef write # generate lef of current layout in magic tool
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/45b461d1-5629-45c4-899a-4f2d83efbfe3)

Screenshot of newly generated lef:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/aabb890e-5008-4feb-b865-a6d3cf698b9e)

Step 2:Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory

cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/ # Copy lef file

cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/ # Copy lib files
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/4d55aee8-296c-4ed0-91d2-df25a3422978)

Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow:

set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"

set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"

set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

config.tcl screenshot with above added lines:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/2c8f3ad6-8531-4cc9-82bc-0a2627686e43)

Step 3: Perform openlane flow synthesis with newly inserted custom inverter cell:
cd ~/Desktop/work/tools/openlane_working_dir/openlane # Change directory to openlane flow directory

docker #run openlane docker subsystem
./flow.tcl -interactive # open openlane in interactive mode

package require openlane 0.9 #inputs required package for openlane flow

prep -design picorv32a #prepares the picorv32a design for openlane flow

run_synthesis #run synthesis for the prepared design
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/571b10ba-84da-425f-97d9-6c37df27b694)

Step 4 : Reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters:

Note current generated design values before modifying parameters to improve timing:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/4975e66a-9211-4c30-b653-7c9402e04c29)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/8e8a5cfc-9d60-4f95-a1cf-28aeb2cecd3c)

Commands to change value of design parameters and improve timing:
prep -design picorv32a -tag 09-04_13-19 -overwrite # Now once again we have to prep design so as to update variables

set lefs [glob $::env(DESIGN_DIR)/src/*.lef] 

add_lefs -src $lefs # Addiitional commands to include newly added lef to openlane flow merged.lef

echo $::env(SYNTH_STRATEGY) # Command to display current value of variable SYNTH_STRATEGY

set ::env(SYNTH_STRATEGY) "DELAY 3" # Command to set new value for SYNTH_STRATEGY

echo $::env(SYNTH_BUFFERING) # Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled

echo $::env(SYNTH_SIZING) # Command to display current value of variable SYNTH_SIZING

set ::env(SYNTH_SIZING) 1 # Command to set new value for SYNTH_SIZING

echo $::env(SYNTH_DRIVING_CELL) # Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not

run_synthesis # Now that the design is prepped and ready, we can run synthesis again

Screenshot of running above commands:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/9de7b543-ad7e-43b1-8959-5421c083529a)

Screenshot of merged.lef in tmp directory with our custom inverter set as macro:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/2a1a1d64-eebd-461a-adf8-7bf07db2d433)

Area increase and worst negative slack=0:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/4631caf5-fec2-4928-882c-1f9728fb2bff)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/8527a62d-c5da-43ec-995b-707370268e21)

Step 5 : Run Floorplan,Placement and verify whether custom cell is accepted in PnR flow or not:
run_floorplan facing error:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/e0d54bdb-36de-44c4-8ea8-7175244fc477)

So,after synthesis,run following commands:

init_floorplan # Following three commands sourced from "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl" & it is also available in Floorplan Commands section in                         "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md"
place_io
tap_decap_or

Screenshot of running above three floorplan commands:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a00260c8-bee0-4d04-8ae5-bd0684f6065c)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/c885d604-0efa-4bb1-8cb4-cb1cdbd5a79d)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/d2349af7-a8e2-4954-aafd-53dbe166df37)

run_placement #run placement after floorplan is done :
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/37a9e553-c28c-4532-9fa8-ddd1f144f77e)

Load placement def in magic tool:
cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/09-04_13-19/results/placement/ # change directory to newly generated placement.def file

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def & #invoke magic tool and open placement.def

placement.def screenshot in magic tool:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/2f858a6b-92ce-4f41-8a33-a93515378573)

Screenshot of custom inverter in placement def with insertion with proper abutment:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/7d07951b-e9d6-4ca1-8fc9-dd9290623c43)

expand # tkcon Command to view internal connectivity layers

Abutment of power pins of custom inverter with other library cells clearly visible in following screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/2a86aae9-c9d8-4d38-abc7-b60c69af7f79)

Step 6 : Perform Post synthesis Static Timing Analysis with OpenSTA tool:
Rerun synthesis without adding any parameters to improve timing

cd ~/Desktop/work/tools/openlane_working_dir/openlane # Change directory to openlane flow directory

docker #run openlane docker subsystem
./flow.tcl -interactive # open openlane in interactive mode

package require openlane 0.9 #inputs required package for openlane flow

prep -design picorv32a #prepares the picorv32a design for openlane flow

set lefs [glob $::env(DESIGN_DIR)/src/*.lef] 

add_lefs -src $lefs # Addiitional commands to include newly added lef to openlane flow merged.lef

set ::env(SYNTH_SIZING) 1 # Command to set new value for SYNTH_SIZING

run_synthesis #run synthesis for the prepared design

synthesis successful with above commands:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/843a8319-3766-46db-bcd8-61c85aa2b702)

create pre_sta.conf in "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/pre_sta.conf" :
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/887c1a26-3596-436e-9b48-313e66b2b17e)

create my_base.sdc in "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/my_base.sdc" based on "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/scripts/base.sdc" file :
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a3e6224b-301f-4eea-a773-f57a53ad2d72)

Commands to run STA in another terminal:

cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane # Change directory to openlane

sta pre_sta.conf # Command to invoke OpenSTA tool with script
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/00bfbbf4-375a-44e1-8a39-a1b6dd7baa94)

As more fanout is creating more delay,we can rerun synthesis with parameter to reduce fanout to improve delay:

prep -design picorv32a -tag 09-04_15-19 -overwrite # Now once again we have to prep design so as to update variables

set lefs [glob $::env(DESIGN_DIR)/src/*.lef] 

add_lefs -src $lefs # Addiitional commands to include newly added  custom inv lef to openlane flow merged.lef


set ::env(SYNTH_SIZING) 1 # Command to set new value for SYNTH_SIZING

set ::env(SYNTH_MAX_FANOUT) 4 # Command to set new value for SYNTH_MAX_FANOUT

echo $::env(SYNTH_DRIVING_CELL) # Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not

run_synthesis # Now that the design is prepped and ready, we can re-run synthesis using this command:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/f8cb9de2-643d-402d-9b13-51d5c5be035e)

Rerun STA in new terminal window:
cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane # Change directory to openlane

sta pre_sta.conf # Command to invoke OpenSTA tool with script
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/0f950d12-b1a2-452e-8e47-bb1f0156b304)

Step 7 : Perform Timng ECO fixes to reduce timing violations:

OR gate of drive strength 2 is driving 4 fanouts:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/c3a019d3-d9a9-47b8-989d-4d963867ac85)

commands to perform analysis and basic timing eco:
report_net -connections _11672_ # Reports all the connections to a net

help replace_cell # Checking command syntax

replace_cell _14510_ sky130_fd_sc_hd__or3_4 # Replacing cell

report_checks -fields {net cap slew input_pins} -digits 4 # Generating custom timing report

slack is seen as reducing:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/ad32bb8e-f1db-42a5-b3a8-58d90b16d213)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/b7169cba-4324-405c-a71c-5f02abccb179)

OR gate of drive strength 2 is driving 4 fanouts:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/621404fc-4a86-4afb-a5fa-3c3e24297880)

report_net -connections _11675_
replace_cell _14514_ sky130_fd_sc_hd__or3_4
report_checks -fields {net cap slew input_pins} -digits 4

slack is seen as reducing:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/53a4df6c-6892-4e93-9633-0799819b10df)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/f683e555-8d61-4c68-8083-d28ce7e470c3)

OR gate of drive strength 2 driving OA gate leads to more delay:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/3b9154d1-75df-414c-bfee-082a36f9a897)

report_net -connections _11643_

replace_cell _14481_ sky130_fd_sc_hd__or4_4

report_checks -fields {net cap slew input_pins} -digits 4

slack is seen as reducing:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/7e74d0d7-3a6f-4dda-9a1a-2d459bbc07b2)

OR gate of drive strength 2 driving OA gate leads to more delay:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/84c54ba1-6fcf-40fa-b288-30eaf43454c8)

report_net -connections _11668_

replace_cell _14506_ sky130_fd_sc_hd__or4_4

report_checks -fields {net cap slew input_pins} -digits 4

slack is seen as reducing:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/68b29d76-fd7a-46e3-9f20-f4c5b07fcd6a)


report_checks -from _29043_ -to _30440_ -through _14506_ # Commands to verify instance _14506_ is replaced with sky130_fd_sc_hd__or4_4

Replaced instance as seen in the screenshot:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/c55f7500-c786-4ce2-9256-8ff98d364de4)

ECO fixes were started at wns -23.9000ns and after fixes, wns = -22.6173, which is a reduction of 1.2827 ns of violation.

Step 8 : Replacing the old netlist with the new netlist generated after timing ECO fix , and implementing the floorplan, placement and cts:

Commands to make copy of old netlist:
cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/09-04_15-19/results/synthesis/ # Change from home directory to synthesis results directory

ls # List contents of the directory

cp picorv32a.synthesis.v picorv32a.synthesis_old.v # Copy and rename the netlist

ls # List contents of the directory
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/8e66548c-3782-409b-a764-b7f04006282e)

In OpenSTA window:
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/09-04_15-19/results/synthesis/picorv32a.synthesis.v #overwrite current synthesis netlist
exit # exit from OpenSTA

instance _14506_ is replaced with sky130_fd_sc_hd__or4_4 (verified in netlist):
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/60fef426-ec0b-4c71-9d05-59df90bff884)

Rerun synthesis,floorplan,and placement and CTS in the netlist with no timing violations:

prep -design picorv32a -tag 09-04_13-19 -overwrite # Now once again we have to prep design so as to update variables

set lefs [glob $::env(DESIGN_DIR)/src/*.lef] 

add_lefs -src $lefs # Addiitional commands to include newly added lef to openlane flow merged.lef

set ::env(SYNTH_STRATEGY) "DELAY 3" # Command to set new value for SYNTH_STRATEGY

set ::env(SYNTH_SIZING) 1 # Command to set new value for SYNTH_SIZING

run_synthesis # Now that the design is prepped and ready, we can run synthesis again
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/1f733537-f2b5-40bc-8f07-fd1fedbc291e)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/d929250a-4491-415d-83ee-0dedfaa1600d)


So,after synthesis,run following commands:

init_floorplan # Following three commands sourced from "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl" & it is also available in Floorplan Commands section in                         "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md"

place_io

tap_decap_or
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/91d69f74-12a5-48dc-9ea7-89aaf154735d)

run_placement #perform placement after floorplan
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/0dd5cbcc-863d-4e90-b407-5837953bc85f)

run_cts #perform cts after placement
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/0fb61b8c-061b-4b51-b68c-a61e75972673)

Step 9 : Post-CTS OpenROAD Static Timing Analysis:

Commands to open OpenROAD Tool and create OpenROAD database from within openlane flow:
openroad # Command to run OpenROAD tool

read_lef /openLANE_flow/designs/picorv32a/runs/09-04_13-19/tmp/merged.lef # Reading lef file

read_def /openLANE_flow/designs/picorv32a/runs/09-04_13-19/results/cts/picorv32a.cts.def # Reading def file

write_db pico_cts.db # Create an OpenROAD database to work with

read_db pico_cts.db # Loading the created database in OpenROAD
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/ea99d9f0-baa4-4543-8c2b-19e2a44e8752)

read_verilog /openLANE_flow/designs/picorv32a/runs/09-04_13-19/results/synthesis/picorv32a.synthesis_cts.v # Read netlist post CTS

read_liberty $::env(LIB_SYNTH_COMPLETE) # Read library for design

link_design picorv32a # Link design and library

read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc # Read in the custom sdc we created

set_propagated_clock [all_clocks] # Setting all clocks as propagated clocks as this is post-cts analysis
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/0f9d1d26-65fe-4170-ac41-06de5e566aed)


help report_checks # Check syntax of 'report_checks' command

report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4 # Generating custom timing report

exit # Exit to OpenLANE flow
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a5ca2b6a-a822-4f3c-93ca-17c8d4ae6506)

Step 10 : Exploring post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST':

echo $::env(CTS_CLK_BUFFER_LIST) # Checking current value of 'CTS_CLK_BUFFER_LIST'

set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0] # Removing 'sky130_fd_sc_hd__clkbuf_1' from the list

echo $::env(CTS_CLK_BUFFER_LIST) # Checking current value of 'CTS_CLK_BUFFER_LIST'


echo $::env(CURRENT_DEF) # Checking current value of 'CURRENT_DEF'

set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/09-04_13-19/results/placement/picorv32a.placement.def # Setting current def as placement def
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/96ec8adc-fe99-408e-b617-23a129b8446f)

run_cts # rerun CTS
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/919c51ff-838d-4486-a99b-a8ad898d596e)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/61793da1-d543-4779-bc24-c3debbd153d9)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/4a660019-00b7-446f-8013-488e8c58e552)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/426f6e75-4744-4766-9fef-3e824b0b0bea)

echo $::env(CTS_CLK_BUFFER_LIST) # Checking current value of 'CTS_CLK_BUFFER_LIST'


Commands to open OpenROAD Tool and create OpenROAD database from within openlane flow:

openroad # Command to run OpenROAD tool

read_lef /openLANE_flow/designs/picorv32a/runs/09-04_13-19/tmp/merged.lef # Reading lef file

read_def /openLANE_flow/designs/picorv32a/runs/09-04_13-19/results/cts/picorv32a.cts.def # Reading def file

write_db pico_cts.db # Create an OpenROAD database to work with

read_db pico_cts.db # Loading the created database in OpenROAD

read_verilog /openLANE_flow/designs/picorv32a/runs/09-04_13-19/results/synthesis/picorv32a.synthesis_cts.v # Read netlist post CTS
read_liberty $::env(LIB_SYNTH_COMPLETE) # Read library for design

link_design picorv32a # Link design and library

read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc # Read in the custom sdc we created

set_propagated_clock [all_clocks] # Setting all clocks as propagated clocks as this is post-cts analysis

![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/01d73c39-e473-469d-868a-39570caddb16)


report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4 # Generating custom timing report
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a201bafa-557f-42b2-b0ee-5a7c06f615a1)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/2b6677d1-f080-420c-a9ba-6158ac26fd9d)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/57c7d365-3160-45dd-a615-9a2f1724ea4c)


report_clock_skew -hold # Report hold skew

report_clock_skew -setup # Report setup skew
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/38bb725d-0617-4206-9aab-ac2fd8de4c6f)



exit # Exit to OpenLANE flow


echo $::env(CTS_CLK_BUFFER_LIST) # Checking current value of 'CTS_CLK_BUFFER_LIST'

set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1] # Inserting 'sky130_fd_sc_hd__clkbuf_1' to first index of list

echo $::env(CTS_CLK_BUFFER_LIST) # Checking current value of 'CTS_CLK_BUFFER_LIST'
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/e14e3400-a69e-43db-b6fd-64807aed6cfc)

# Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

Step 1: Now as CTS is performed,we can proceed to PDN(Power Distribution Network) generation in openlane:

gen_pdn #Command to generate power distribution network
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/ffb80aa0-64c2-4f65-963d-02bbb983f740)

cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/09-04_13-19/tmp/floorplan/ #change directory containing PDN def

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def & #Command to open PDN def in magic tool

PDN def Screenshots:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/bc01796f-0b26-4d9a-a132-7a698045b318)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/04d57d79-a39f-4105-b953-fcaf00447b01)

Step 2 : Performing detailed routing using TritonRoute and exploring the routed layout:

echo $::env(CURRENT_DEF) # Check value of 'CURRENT_DEF'

echo $::env(GLOBAL_ROUTER) #Specifies which global router to use. Values: `fastroute` or `cugr`,(Default: `fastroute`) 

echo $::env(DETAILED_ROUTER) # Specifies which detailed router to use. Values: `tritonroute`, `tritonroute_or`, or `drcu`. <br> (Default: `tritonroute`)

echo $::env(ROUTING_OPT_ITERS) # Specifies the maximum number of optimization iterations during Detailed Routing in TritonRoute (Default: `64`)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a3450ac6-652b-4c0c-b377-ea65caf3e21a)

more details about routing env variables present in "/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/configuration/README.md"


run_routing # Command for detailed route using TritonRoute

Routing Completed:

![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/a0c26f43-b804-498e-9a97-7960d91af7ea)

![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/93130ed6-510f-403a-85ec-652ab9968a55)


cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/09-04_13-19/results/routing/ # Change directory to path containing routed def

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def & # Command to load the routed def in magic tool

Routed def screenshots:
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/d327826a-9f7d-4d23-93fc-8ae574a16aef)
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/ec4e20d1-66b9-42d8-aa1b-6737a6cc0036)




Step 3 : Post-route STA analysis:

path of SPEF file post route: /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/09-04_13-19/results/routing/picorv32a.spef

Similarly,post_route STA analysis can be performed using OpenROAD flow within openlane.
We have to create a new db as def has changed from cts to routing.
We have to use pre_route netlist.
SPEF file (contains information about parasitic capacitance of nets) has to be read using "read_spef /openLANE_flow/designs/picorv32a/runs/09-04_13-19/results/routing/picorv32a.spef" command before generating custom timing report.






































































































   












    




    







