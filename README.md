# OpenLANE-workshop
## Day 1 Inception of open-source EDA, OpenLANE and Sky130 PDK

The openlane working directory consists of two directories-
1.	OpenLANE_flow  
2.	 Pdk

![image1](https://user-images.githubusercontent.com/78075225/105988686-07779280-60c6-11eb-9d07-126252125cc5.JPG)

### PDK
The PDK folder consists of PDK related information. 

![image2](https://user-images.githubusercontent.com/78075225/105989256-dea3cd00-60c6-11eb-9937-96d4c292cbb8.JPG)

In our case we will be using Skywater130 PDK. The PDK directory consists of three sub directories which are mentioned as follows:
1.	Skywater-pdk – Consists of foundry provided PDK related files such as timing libraries, LEV files etc.
2.	Open_pdks – Contains scripts that make foundary PDKs to be compatible with open source EDA tools.
3.	Sky130A – The open-source compatible PDK files. This SKY130A subdirectory consist of the following files: 

![image3](https://user-images.githubusercontent.com/78075225/105989605-5ffb5f80-60c7-11eb-96bd-f1e2ec6fca13.JPG)

1.	Libs.tech –Contains files specific to tools

![image4](https://user-images.githubusercontent.com/78075225/106006981-d2763a80-60db-11eb-90fd-2188d84d72ee.JPG)

2.	Libs.ref-  contains process specific files

![image5](https://user-images.githubusercontent.com/78075225/106007106-f33e9000-60db-11eb-948b-2f51b232c502.JPG)

### OpenLANE_flow
 
This directory consists of the design folder which consists of some in built designs. In creating a new design of our own, we create inside this design folder. For this project we will be using picorv32a design:

![image6](https://user-images.githubusercontent.com/78075225/106007442-50d2dc80-60dc-11eb-8267-7226179fd052.JPG)

Each design hierarchy comes with two distinct components:
1.	Src folder - Contains verilog files and sdc constraint files
2.	Config.tcl files - Design specific configuration switches used by OpenLANE
The following figure is an example of a configuration file:

![image7](https://user-images.githubusercontent.com/78075225/106007615-811a7b00-60dc-11eb-89f4-aabfaea31a3e.JPG)

### Invoking OpenLANE

•	In order to invoke openLANE, go to openlane directory and type ./flow.tcl –interactive  to invoke the openlane tool

![image8](https://user-images.githubusercontent.com/78075225/106007748-a14a3a00-60dc-11eb-80cb-81b40fb1635b.JPG)

•	./flow.tcl is the script which runs the OpenLANE flow
•	OpenLANE can be run interactively or in autonomous mode.
•	Invoking of open lane changes prompt to %
•	The command %package require openlane 9.0 imports all the packages needed to run this flow
•	Next step is to prepare the design. The prep command is used to make file structure for our design.  

![image9](https://user-images.githubusercontent.com/78075225/106007907-ca6aca80-60dc-11eb-9dd7-56245cae8d8e.JPG)

•	After running this look in the openLANE_flow/designs/picro32a folder and you will see runs folder being created. Inside the runs folder we will have a folder with the present date and inside it we have these folders:

![image10](https://user-images.githubusercontent.com/78075225/106007995-e40c1200-60dc-11eb-8bce-b42a6f2e72c2.JPG)

The config.tcl file shown in this folder contains all the parameters used by OpenLANE for this specific run.

### Synthesis
To run synthesis use '''%run_synthesis command'''. The following picture is a snippet of synthesis completion.

![image11](https://user-images.githubusercontent.com/78075225/106008167-0aca4880-60dd-11eb-86b9-a84ff7bdaf26.JPG)

After synthesis is complete,the synthesis file is created in results subdiresctory under runs directory.

![image12](https://user-images.githubusercontent.com/78075225/106008249-1cabeb80-60dd-11eb-9ba3-868a0b8a2981.JPG)
