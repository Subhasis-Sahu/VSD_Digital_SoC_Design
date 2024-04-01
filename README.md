# VSD_Digital_SoC_Design
#Day-1 Introduction to Open Source SoC Design using Openlane:

##1.1 What is a SoC?
SoC refers to the term System on a Chip. It is a single chip which integrates a whole electronic or a system into it. A SoC may contain digital, analog, mixed-signal devices on the same chip. In a traditional computer system architecture, each system component such as CPU, controller chips, a GPU, and RAM etc., used to be separately installed on the board, but thanks to technological advancements in the semiconductor industry has enabled more and more elements to be integrated in a single silicon chip.
 A current-day system on a chip (SoC) consists of several different components of a system such as the CPU (a microprocessor or microcontroller), memory, input/output (I/O) interface and wireless blocks, on a single silicon substrate. Most SoCs also use various pre-designed hardware block, called as IP Cores, to improve design time to market.

Since it has all the system components on one single chip, SoCs offer the advantages of reduced size, overall system cost, lower power consumption and Increased performance. SoCs are becoming increasingly popular with the growth of mobile computing and IoT (Internet of Things) devices.

##1.2 SoC Design Flow:
SoC development process can be broken into multiple stages as illustrated in the following figure:
 
![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/3e38bb6a-1ae0-4b1c-868b-fe37b18a04cd)

##1.3 What is Openlane?

OpenLane is a powerful and versatile infrastructure library that enables the construction of digital ASIC physical implementation flows based on open-source and commercial EDA tools. It includes a reference flow (Classic) that is constructed entirely using open-source EDA tools –abstracting their behavior and allowing the user to configure them using a single file. OpenLane also supports extending or modifying flows using Python scripts and utilities. Here are some of the key benefits of using OpenLane:

Flexibility and extensibility: OpenLane is designed to be flexible and extensible, allowing designers to customize the flow to meet their specific needs by developing Python scripts (plugins) and utilities or by modifying the existing configuration file.

Open source: OpenLane is an open-source project that is freely available to use and modify, which makes it a good choice for designers looking for a transparent, cost-effective solution.

Community support: OpenLane capitalizes on OpenLane’s existing community of users and contributors, which means that a wealth of resources is available to help designers get started and troubleshoot any problems they encounter.

![image](https://github.com/Subhasis-Sahu/VSD_Digital_SoC_Design/assets/165357439/c08411b9-fa78-4f21-b14f-6c9b67df6a4e) (Openlane flow)

[Link to Openlane Documentation](https://openlane2.readthedocs.io/en/latest/getting_started/newcomers/index.html#what-is-openlane)

##1.4 Lab 1: Run  synthesis on "picorv32a" design using Openlane flow,generate outputs and analyse the results,by determining flop ratio.






