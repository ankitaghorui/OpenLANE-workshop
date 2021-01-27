# OpenLANE-workshop
Day 1 Inception of open-source EDA, OpenLANE and Sky130 PDK
The openlane working directory consists of two directories-
1.	Openlane_flow  
2.	 Pdk

![](image1.JPG)


PDK 
The PDK folder consists of PDK related information. In our case we will be using Skywater130 PDK. The PDK directory consists of three sub directories which are mentioned as follows:
1.	Skywater-pdk – Consists of foundry provided PDK related files such as timing libraries, LEV files etc.
2.	Open_pdks – Contains scripts that make foundary PDKs to be compatible with open source EDA tools.
3.	Sky130A – The open-source compatible PDK files.  
This SKY130A subdirectory consist of the following files: 
1.	Libs.ref-  contains process specific files
2.	Libs.tech –Contains files specific to tools

Openlane_flow
 
This directory consists of the design folder which consists of some in built designs. In creating a new design of our own, we create inside this design folder. For this project we will be using picorv32a design:



Each design hierarchy comes with two distinct components:
1.	Src folder - Contains verilog files and sdc constraint files
2.	Config.tcl files - Design specific configuration switches used by OpenLANE
The following figure is an example of a configuration file:

Invoking OpenLANE

•	In order to invoke openLANE, go to openlane directory and type ./flow.tcl –interactive  to invoke the openlane tool

•	./flow.tcl is the script which runs the OpenLANE flow
•	OpenLANE can be run interactively or in autonomous mode.
•	Invoking of open lane changes prompt to %
•	The command %package require openlane 9.0 imports all the packages needed to run this flow
•	Next step is to prepare the design. The prep command is used to make file structure for our design.  
•	preparing the design in OpenLANE merges the technology LEF and cell LEF information. Technology LEF information contains layer definitions and a set of restricted design rules needed for PnR flow. The cell LEF contains obstruction information of each standard cell needed to minimize DRC errors during PnR flow:

•	After running this look in the openlane/design/picro32a folder and you will see runs folder being created. Inside the runs folder we will have a folder with the present date and inside it we have these folders:
The config.tcl file shown in this folder contains all the parameters used by OpenLANE for this specific run.
Synthesis
To run synthesis use run_synthesis command. The following picture is a snippet of synthesis completion.
After synthesis,  file is created in synthesis folder. 
