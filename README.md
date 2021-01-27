# OpenLANE-workshop
## Day 1: Inception of open-source EDA, OpenLANE and Sky130 PDK

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

•	In order to invoke openLANE, go to openlane directory and type ```./flow.tcl –interactive```  to invoke the openlane tool

![image8](https://user-images.githubusercontent.com/78075225/106007748-a14a3a00-60dc-11eb-80cb-81b40fb1635b.JPG)

•	./flow.tcl is the script which runs the OpenLANE flow
•	OpenLANE can be run interactively or in autonomous mode.
•	Invoking of open lane changes prompt to %
•	The command ```%package require openlane 9.0``` imports all the packages needed to run this flow
•	Next step is to prepare the design. The prep command is used to make file structure for our design.  

![image9](https://user-images.githubusercontent.com/78075225/106007907-ca6aca80-60dc-11eb-9dd7-56245cae8d8e.JPG)

•	After running this look in the openLANE_flow/designs/picro32a folder and you will see runs folder being created. Inside the runs folder we will have a folder with the present date and inside it we have these folders:

![image10](https://user-images.githubusercontent.com/78075225/106007995-e40c1200-60dc-11eb-8bce-b42a6f2e72c2.JPG)

The config.tcl file shown in this folder contains all the parameters used by OpenLANE for this specific run.

### Synthesis
To run synthesis use ```%run_synthesis command```. The following picture is a snippet of synthesis completion.

![image11](https://user-images.githubusercontent.com/78075225/106008167-0aca4880-60dd-11eb-86b9-a84ff7bdaf26.JPG)

After synthesis is complete, the synthesis file is created in results subdiresctory under runs directory.

![image12](https://user-images.githubusercontent.com/78075225/106008249-1cabeb80-60dd-11eb-9ba3-868a0b8a2981.JPG)

## Day 2: Floorplan and Placement

### Floorplan
The next step after synthesis is floorplan. In order to run floorplan in OpenLANE use ```%run_floorplan command```. The following figure gives an idea of the on going process after running this command and completion of floorplan:

![1 floorplan ongoing](https://user-images.githubusercontent.com/78075225/106031343-29d4d480-60f5-11eb-9b2b-57c03c0bc78e.JPG)

![2 floorplan competed](https://user-images.githubusercontent.com/78075225/106031437-48d36680-60f5-11eb-95d3-8772ff75f209.JPG)

### Viewing Floorplan in Magic
The Syntax for viewing floorplan in magic is:
 ```magic -T <magic tech file> lef read <lef file> def read <def file>```
In this case the magic technology file is sky130A.tech, and the other two files are merged lef file and def file of floorplan.

![3 floorplann in magic](https://user-images.githubusercontent.com/78075225/106031521-656f9e80-60f5-11eb-8eef-53982cbe44b3.JPG)

### Placement
The floorplan is followed by placement Stage. To run placement in openLANE use the command ```%run_placement```. The following picture shows the completion of placement stage in openLANE.

![4 placement completed](https://user-images.githubusercontent.com/78075225/106032112-12e2b200-60f6-11eb-859b-d6ec6dca3c63.JPG)

### Viewing Placement in Magic
We use the same syntax for viewing placement in magic as used during floorplan. Therefore the syntax will be
```magic -T <magic tech file> lef read <lef file> def read <def file>```

![5 command for placement in magic](https://user-images.githubusercontent.com/78075225/106032340-5e955b80-60f6-11eb-9c83-5474e31c64b2.JPG)

In this case the the lef and def files are the merged lef file and def file of placement.
 
![6 placement in magic](https://user-images.githubusercontent.com/78075225/106032437-7e2c8400-60f6-11eb-94f1-fcf4607987ad.JPG)

## Day 3: Design library cell using Magic Layout and ngspice characterization
 
### Cloning Reference Gitrepo

For the inverter standard cell we take the help of below mentioned repository and clone it to our own design directory
Reference link: https://github.com/nickson-jose/vsdstdcelldesign for cell files.

![1 clone git repo](https://user-images.githubusercontent.com/78075225/106032844-fe52e980-60f6-11eb-8483-91b444863250.JPG)
 
The next step is to copy the tech file skywater.tech file into the vsdstdcelldesign directory. 

![2 copying tech file](https://user-images.githubusercontent.com/78075225/106033069-4a9e2980-60f7-11eb-8860-944d5408bd6d.JPG)

Viewing the vststdcelldesign directory after copying the tech file:

![3 vlsidesignfolder conisting tech file](https://user-images.githubusercontent.com/78075225/106033126-5db0f980-60f7-11eb-8403-98d053392420.JPG)

### Viewing the Inverter Standard Cell in Magic
The following image shows the command to invoke the standard cell in magic:

![4 magic command for inverter](https://user-images.githubusercontent.com/78075225/106033359-ad8fc080-60f7-11eb-810e-efd057ed6a8b.JPG)

### Inverter Layout in Magic

![5 inverter in magic](https://user-images.githubusercontent.com/78075225/106033971-563e2000-60f8-11eb-903b-adac9434d292.JPG)

The tkcon window gives detailed information about the various parts of the cell when prompted to ‘what’.

![5 snap showing details](https://user-images.githubusercontent.com/78075225/106034159-91d8ea00-60f8-11eb-8a9e-5af25f668020.JPG)

### Extraction to Spice using Magic
```extract all``` creates the .ext file and ```ext2spice``` creates the .spice file from the .ext file commands to extract to spice:

![6 extraction](https://user-images.githubusercontent.com/78075225/106034270-ba60e400-60f8-11eb-80ff-faeb74182213.JPG)

Extraction process will lead to creation of the Spice deck file. The following image shows the Spice Deck file which is modified as per the inverted design specifications :

![7 spicefile](https://user-images.githubusercontent.com/78075225/106034715-407d2a80-60f9-11eb-899e-3a34852028b4.JPG)

### Viewing the inverter in Ngspice
The next step is to view the inverter spice file in ngspice:

![8 invoking ngspice](https://user-images.githubusercontent.com/78075225/106034809-6276ad00-60f9-11eb-8426-b08d1e12934e.JPG)

The following image shows the inverter spice file in ngspice:

![9 ngspice view](https://user-images.githubusercontent.com/78075225/106034894-77ebd700-60f9-11eb-802f-1eb848b7fbab.JPG)

The next step is to plot the output, input vs time in ngpice: 

![10 plot command](https://user-images.githubusercontent.com/78075225/106034951-8cc86a80-60f9-11eb-86f8-84661829525d.JPG)

![11 plot 1](https://user-images.githubusercontent.com/78075225/106035161-c8fbcb00-60f9-11eb-8a85-ab3662c3d0c3.JPG)

## Day 5 Final steps for RTL2GDS

### Checking the part of flow
In order to check which part of flow we  are currently in, use  command ```% echo $::env(CURRENT_DEF)```. The CURRENT_DEF holds the def file obtained after clock tree synthesis.

![1 checking last action](https://user-images.githubusercontent.com/78075225/106044984-71179100-6106-11eb-8fa3-57d1fad1cb81.JPG)

The next step is to generate the power distribution network. Use the command ```%gen_pdn``` to do so. The image shows the ongoing process of generating power distribution network:

![2 generating power distribution network](https://user-images.githubusercontent.com/78075225/106045079-8b516f00-6106-11eb-869d-b8f7bf805637.JPG)

### Routing
After generating power distribution network use ```% echo $::env(CURRENT_DEF)```  again to see the updated current def file i.e. pdn.def.
The next step is routing. Before that we will check the routing strategy. In order to do so use ```% echo $::env(ROUTING_STRATEGY)```. After this run routing by using the command ```%run_routing```.

![3 routing strategy and routing](https://user-images.githubusercontent.com/78075225/106045185-a6bc7a00-6106-11eb-97e7-5c2dd21c5228.JPG)



