![advanced_physical_design](https://user-images.githubusercontent.com/78075225/106164823-6a455880-61b0-11eb-93f9-1f9d29dd7510.png)

# Advanced Physical Design Using Openlane/Sky130

<details>
 <summary><b>Table of Contents</b></summary>

- [Introduction](#introduction)
  * [About OpenLANE](#about-openlane)
  * [SkyWater Open Source PDK](#skywater-open-source-pdk)
- [Day 1 Inception of open-source EDA and OpenLANE and Sky130 PDK](#day-1-inception-of-open-source-eda-and-openlane-and-sky130-pdk)
  * [PDK](#pdk)
  * [OpenLANEflow](#openlaneflow)
  * [Invoking OpenLANE](#invoking-openlane)
  * [Synthesis](#synthesis)
- [Day 2 Floorplan and Placement](#day-2-floorplan-and-placement)
  * [Floorplan](#floorplan)
  * [Viewing Floorplan in Magic](#viewing-floorplan-in-magic)
  * [Placement](#placement)
  * [Viewing Placement in Magic](#viewing-placement-in-magic)
- [Day 3 Design library cell using Magic Layout and ngspice characterization](#day-3-design-library-cell-using-magic-layout-and-ngspice-characterization)
  * [Cloning Reference Gitrepo](#cloning-reference-gitrepo)
  * [Viewing the Inverter Standard Cell in Magic](#viewing-the-inverter-standard-cell-in-magic)
  * [Inverter Layout in Magic](#inverter-layout-in-magic)
  * [Extraction to Spice using Magic](#extraction-to-spice-using-magic)
  * [Viewing the inverter in Ngspice](#viewing-the-inverter-in-ngspice)
- [Day 4 Pre-layout timming analysis and CTS](#day-4-pre-layout-timming-analysis-and-cts)
  * [PnR Guidelines while making Standard Cell set](#pnr-guidelines-while-making-standard-cell-set)
  * [LEF File](#lef-file)
  * [Including Custom Cells in OpenLANE](#including-custom-cells-in-openlane)
  * [Viewing the Custom Inverter cell in Magic](#viewing-the-custom-inverter-cell-in-magic)
  * [Viewing the standard inverter cell](#viewing-the-standard-inverter-cell)
  * [CTS](#cts)
  * [Post-CTS STA Analysis](#post-cts-sta-analysis)
- [Day 5 Final steps for RTL2GDS](#day-5-final-steps-for-rtl2gds)
  * [Checking the part of flow](#checking-the-part-of-flow)
  * [Routing](#routing)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'></a></i></small>

</details>

## Introduction

This project consists of a brief description of a five day workshop of Physical design using openLANE and Sky130 PDK.

### About OpenLANE
OpenLane is an open-source VLSI flow built around open-source tools.It consists of several components such as OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. With openLANE we can have complete RTL to GDSII format without human intervention.

### SkyWater Open Source PDK
The SkyWater Open Source PDK is a collaboration between Google and SkyWater Technology Foundry to provide a fully open source Process Design Kit and related resources. We will be using Sky130 PDK for this project.

## Day 1 Inception of open-source EDA and OpenLANE and Sky130 PDK

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

### OpenLANEflow
 
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

## Day 2 Floorplan and Placement

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

## Day 3 Design library cell using Magic Layout and ngspice characterization
 
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

## Day 4 Pre-layout timming analysis and CTS

### PnR Guidelines while making Standard Cell set
1.Input and output port must lie on vertical and horizontal tracks. 2.Width of standard cell should be odd multiple of track horizontal pitch and likewise height should an odd multiple of track vertical pitch.In order to do so we will adjust the grid definition as per the track definition. The track file is shown in the following picture:

![1 track file](https://user-images.githubusercontent.com/78075225/106118292-f12b0e80-6179-11eb-8738-8275a4d286ab.JPG)

Setting grid definition as per the track definition:

![2 setting grid as per tracks](https://user-images.githubusercontent.com/78075225/106118524-35b6aa00-617a-11eb-9740-cb3ba9ad5316.JPG)

View after converging grid definitions to track definitions:

![3 dia after grid](https://user-images.githubusercontent.com/78075225/106118630-5252e200-617a-11eb-8ea6-1afca5fafd86.JPG)

### LEF File

The LEF file has the information about input ports, output ports , ground and power ports. These are th eonly information needed fo rplace and route. LEF file in a way protect our IP. Our aim is to extract lef file from mag file. In order to create the lef file use write lef in tkcon window:

![4 lef file creation](https://user-images.githubusercontent.com/78075225/106123692-4538f180-6180-11eb-9610-54883fd8f997.JPG)

The lef file gets created inside vststdcelldesign directory:

![5 lef file created](https://user-images.githubusercontent.com/78075225/106123768-5da90c00-6180-11eb-8cfc-afafc8025dbb.JPG)

The lef file:

![6 lef file](https://user-images.githubusercontent.com/78075225/106123845-74e7f980-6180-11eb-8b6c-72009e55b85d.JPG)

Copying the lef file into src file of picorvv32a:

![7 lef file included in src](https://user-images.githubusercontent.com/78075225/106123931-89c48d00-6180-11eb-9bd0-5ad2372159d9.JPG)

Viewing the src file containing the lef file and also the libraries:

![8 src having lef as well libraries](https://user-images.githubusercontent.com/78075225/106123976-96e17c00-6180-11eb-8f23-f0b9902e5632.JPG)

### Including Custom Cells in OpenLANE

Modify the ```picorv32a/src/config.tcl``` file as :

![9 config tclfile](https://user-images.githubusercontent.com/78075225/106124098-baa4c200-6180-11eb-87b6-8e4c737642fe.JPG)

The next step is to prep the design and then the commands ```set lefs [glob $::env(DESIGN_DIR)/src/*.lef]``` and ```add_lefs -src $lefs``` to include sky130_vsdinv.lef in ```~/tmp/meged.lef``` in openlane flow. Then run synthesis. We see slack violations after synthesis:

![10 first synthesis](https://user-images.githubusercontent.com/78075225/106124214-d8722700-6180-11eb-815c-0a7e316c9bf6.JPG)

The following figure shows some modifications to fix slack violations:

![11 chnages to reduce error](https://user-images.githubusercontent.com/78075225/106124347-ffc8f400-6180-11eb-8621-2343881aabe7.JPG)

After doing so, we run synthesis again and see the results:

![12 updated after synthesis](https://user-images.githubusercontent.com/78075225/106124409-11120080-6181-11eb-8ccc-17a201bb4f59.JPG)

### Viewing the Custom Inverter cell in Magic

Run floorplan and placement. Inmvoke magic:

![13 placement](https://user-images.githubusercontent.com/78075225/106124517-2d15a200-6181-11eb-815c-2d2da0cbfc2d.JPG)

### Viewing the standard inverter cell

![14 sky130](https://user-images.githubusercontent.com/78075225/106124595-428acc00-6181-11eb-891a-a0b96ce47d95.JPG)

![15 sky130inv](https://user-images.githubusercontent.com/78075225/106124669-56cec900-6181-11eb-9d53-a3053b64b8cb.JPG)

Copy ```my_base.sdc``` to ```picorc32a/src```:

![16 copying mybase file](https://user-images.githubusercontent.com/78075225/106124799-7cf46900-6181-11eb-8397-3fa8b87cd1c6.JPG)

```my_base.sdc``` file is as shown:

![17 mybase sdc file](https://user-images.githubusercontent.com/78075225/106124889-97c6dd80-6181-11eb-944f-87f750087c4a.JPG)

We can further reduce slack violations by changing the fanout:

![18 change fanout](https://user-images.githubusercontent.com/78075225/106124951-a8775380-6181-11eb-8d26-b70a19e37a77.JPG)

![19 reduced slack with fanout](https://user-images.githubusercontent.com/78075225/106125020-b331e880-6181-11eb-9ab6-c5a44c18b050.JPG)

### CTS

After running floorplan and standard cell placement in OpenLANE we are ready to insert our clock tree for sequential elements in our design. To do so use ```run_cts```.

![20 cts complete](https://user-images.githubusercontent.com/78075225/106125204-deb4d300-6181-11eb-8cbc-3793ea72fabe.JPG)

We can also check the specifications associated with the run_cts using the following commands:

![21 cts specifications](https://user-images.githubusercontent.com/78075225/106125314-04da7300-6182-11eb-848c-4b4dc4ffe431.JPG)

### Post-CTS STA Analysis

OpenLANE has the OpenROAD application integrated into its flow. The OpenROAD application has OpenSTA integrated into its flow. Therefore, we can perform STA analysis from within OpenLANE by invoking OpenROAD.To invoke OpenROAD from OpenLANE:

![22 invoking openroad inside openlane](https://user-images.githubusercontent.com/78075225/106125388-1de32400-6182-11eb-92d3-703eb3e81e54.JPG)

In OpenROAD the timing analysis is done by creating a .db database file. This database file is created from the post-cts LEF and DEF files. To generate the .db files within OpenROAD:

![23 db file](https://user-images.githubusercontent.com/78075225/106125440-2fc4c700-6182-11eb-9081-55306cffaa55.JPG)

After .db generation users can perform tool configuration followed by reporting the propagated clock timing analysis:

![24 cts analysis after min](https://user-images.githubusercontent.com/78075225/106125505-4539f100-6182-11eb-957c-367a25031dfb.JPG)

![25 timing value after cts](https://user-images.githubusercontent.com/78075225/106125566-5420a380-6182-11eb-9179-3fd9d3f1836d.JPG)

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

## Contact

## Acknowledgements



