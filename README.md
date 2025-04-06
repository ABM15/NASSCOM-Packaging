# NASSCOM-Packaging
Repository for the lab exercises of the "VSD NASSCOM Semiconductor Packaging Workshop" (03/28/2025-04/06/2025 Cohort).

## Module 1 - Packaging Evolution: From Basics to 3D Integration
There are no exercises prescribed for this module.

## Module 2 - From Wafer to Package: Assembly and Manufacturing Essentials
There are no exercises prescribed for this module.

## Module 3 - Labs: Thermal Simulation of Semiconductor Packages with ANSYS

The objective of this lab is to model a FlipChip BGA package and perform a thermal simulation in the Ansys Electronics Desktop (AED) environment. The phases involved are the following:

1) Start the Ansys Electronics Desktop Student software
2) Set up a FlipChip BGA package
3) Thermal definitions and material power sources
4) Meshing and running the thermal analysis
5) Explore results

#### 1 Start the Ansys Electronics Desktop Student software

When starting the Ansys Electronics Desktop software, the main window will display quick access buttons for its different tools (HFSS, Q3D, Circuit, Icepak, Maxwell, Simplorer). The one that will be used in the rest of this lab is Icepak.

![ansystart](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20142039.png)

By clicking the Icepak button, a new Icepak design is created into the project and we navigate into the Icepak environment:

![icepakstart](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20145003.png)

From the Icepak design the necessary menus for different parts of the flow are accessible, for instance: 3D component definition, model, thermal, monitor, mesh, analysis, results.

#### 2 Set up a FlipChip BGA package

The software has pre-defined models of common package formats to avoid having to create them from scratch. To incorporate a FlipChip BGA into the design, we just need to right click on the Icepak design and follow the route: Toolkit-->Geometry-->Packages-->Flipchip_BGA

![ansysflipchiproute](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20150721.png)

A new window "Create Flipchip BGA Package" is displayed, where the datasheet information of the package to be modelled needs to be entered in four tabs: Dimensions, Substrate, Solder and Die. For this lab exercise we will use the defaults provided by Ansys.

**Dimensions**

The package will be oriented in the XY plane, centered in the coordinate origin (xS,yS,zS) = (0.0,0.0,0.0), 15 mm long on the X and Y sides, with a package thickness of 1.6 mm. The model type is "Detailed" with full symmetry.

![flipchipdimensions](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20151530.png)

**Substrate**

We will use 2 layers with 0.36 mm thickness. For the traces, Cu-Pure as material with 0.033 mm thickness, 55% top trace coverage, 0% bottom trace coverage, 0% 1st internal layer coverage, 0% 2nd internal layer coverage. No thermal vias will be used, 0.2 mm diameter and 0.05 mm plate thcikness for the rest.

![flipchipsubstrate](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20152013.png)

**Solder** 

We will use a full array with 14 rows in each coordinate plane, no suppresed and no central rows. The material for the balls will be "Solder-pb50_sn50", with a diameter and height of 0.5 mm each and a ball pitch of 1.0 mm.

![flipchipsolder](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20152136.png)

**Die**

For thermal simulation purposes the die will be considered as a 2D thermal source with a power of 1 W. The area of the die is 8.56 x 856 mm2 and the material "Si-typical" . The underfill will have a bump size of 0.01 mm and "Flipchip underfill" as material. No heatsink will be used.

![flipchipdie](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20151821.png)

**Model creation**

After filling the four tabs and clicking OK the model of the FlipChip BGA package is created. Navigating in the model pane we can observe the model (top hierarchy) or inspect every element, for example: ball group, substrate, die, underfill.

![flipchipmodel](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20161743.png)
![flipchipballgroup](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20161924.png)
![flipchipsubstrate2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20162047.png)
![flipchipdie2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20163140.png)
![flipchipdieunderfill](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20163159.png)

The design list can be checked by double-clicking on the "Model" element under the Icepack project 

![designlist](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20164950.png)

#### 3 Thermal Definitions and Material Power Sources

The next step is defining the boundary conditions for the thermal analysis. We can inspect them under the "Thermal" element of the Icepak project structure.

![thermalviewinspect](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20165734.png)

The "Thermal" element is not empty: two of the boundary conditions were already specified when adding the FlipChip BGA package model: the die power source and the condition given by the trace thickness. We check that they have the correct parameters (1W power for the die source and 0.033 mm thickness for the trace):

![thermaldiebc](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20165414.png)
![themaltrace](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20170201.png)

We still need to add a thermal boundary condition in the substrate. For this, we right-click on the Flipchip_BGA1_substrate element and follow the route "Assign thermal--> source"

![thermalsubstrateroute1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20170510.png)

In the next window we configure "Fixed Temperature" as the type of Thermal Condition and we fix it to AmbientTemp

![thermalsubstrateroute2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20170903.png)

A new boundary condition is added in the "Thermal" group as "Source1":

![newsource1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20171110.png)

Since there is an overlap warning with the boundary condition "Flipchip_BGA1_trace1" we remove this one and remain with only two of them: "Flipchip_BGA1_die_source" and "Source1"

![thermalremoved](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20171531.png)

The next step is adding the necessary monitors. We will add three point temperature monitors: one in the die, one in the substrate and one in the underfill. The process to add a monitor is right clicking on the corresponding element and then following the route "Assign Monitor --> Point...". In the next window we select "Temperature". The process is shown below for our three point monitors:

![substratemonitor1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20171823.png)
![substratemonitor2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20171841.png)
![diemonitor1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20171909.png)
![diemonitor2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20171932.png)
![underfillmonitor1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20172039.png)
![underfillmonitor2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20172050.png)

After adding the three point temperature monitors, they are displayed in the "Monitor" element tree of the Icepak design.

![allmonitors](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20172136.png)

#### 4 Meshing and Running the Thermal Analysis

The next step is generating the mesh. This can be done by clicking the "Generate Mesh" button of the "Simulation" tab as shown below:

![generatemesh](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20180240.png)

After finishing the generation the mesh can be visualized and a window opens, allowing us to observe the Mesh Display and Quality tabs:

![aftermesh1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20180323.png)

The Quality tab allows to observe the "Face aligment" and "Skewness" metrics of the meshing:

![aftermesh2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20180353.png)
![aftermesh3](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20180413.png)

The next step is to set up the analysis. For this, we right-click on the "Analysis" Tree Element of the Icepak design and click on "Add Solution Setup..."

![addsolsetup](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20181741.png)

In the dialog that opens we leave the default values for the "General", "Convergence" and "Solver Setting" tabs.

![general](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20181936.png)
![convergence](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20181948.png)
![solversettings](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20181958.png)

The "Setup1" analysis can be seen now in the "Analysis" tree element of the Icepak design. 

We can validate the meshing and the analysis by clicking the "Validate" button in the "Simulation" tab:

![validate](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20182456.png)

There is a warning that the object "Flipchip_BGA1_die_underfill" does not have a mesh. We right-click on the element and click on "Assign Mesh Region". 
![assignmeshregion](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20183018.png)

We leave the default values on the "SubRegion" window:

![asmr2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20183043.png)

In the "General" tab of the "Mesh Region" the box "Enable Mesh Function" needs to be ticked:

![asmmr3](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20183111.png)

The resulting mesh is shown below. The new mesh region "MeshRegion1" is displayed in the Mesh tree element.

![asmr4](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20183315.png)

When generating the mesh again, the software is not capable of meshing "MeshRegion1" so we delete and stay with the previous mesh.

To proceed with the simulation we click on "Analyze All":

![analyzeall](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20185801.png)

#### 5  Exploring the results

To observe the results we select the whole package in the viewer, right-click on it and in the route "Plot Fields --> Temperature --> Temperature"

![plotfieldtemp1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20190026.png)

In the "Create Field Plot" Box we tick the boxes "Specify Name", "Specify Folder" and "Plot on surface only"

![plotfieldtemp2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20190221.png)

Clicking on the "Surface Smoothing" button, we activate Gaussian smoothing:

![gaussiansmoothing](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20190239.png)

We can now see the temperature plot. As expected the hottest surface is the die and the heat flow towards the outside of the package and the substrate can be seen through the temperature coloring:

![templot1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20190347.png
![templot2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20190425.png)
![tempplot3](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20190438.png)

## Module 4 - Ensuring Package Reliability: Testing and Performance Validation

There are no exercises prescribed for this module.

## Module 5 - Package Design and Modelling: Building a Semiconductor Package from Scratch

The objective of this lab is to build a semiconductor package from scratch. The necessary phases are the following:

1) Create the die and the substrate in AEDT
2) Add the die attach material and bond pads
3) Create the wire bond and assign the material
4) Apply the mold compound and finalize the package

#### 1 Create the die and the substrate in AEDT

We start the AEDT software and click on the Q3D button to start a Q3D Extractor Design:

![aedtstart](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20192100.png)
![q3destart](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20192111.png)

The first step is defining the rectangle of the die with the specified dimensions ( 3mm x 3mm, 0.2 thickness). The easiest way is to graphically draw a rectangle and adjust the position values in the Parameters option of the contextual menu.

![ds1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193040.png)
![ds2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193113.png)
![ds3](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193137.png)
![ds4](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193201.png)

To add the thickness information to the model, the rectangle needs to be selected and we follow the route Modeler-->Surface--> Thicken Sheet...". In the opening window we enter 0.2 mm.

![ds5](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193234.png)
![ds6](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193257.png)
![ds7](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193314.png)
![ds8](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193328.png)

The material needs to be changed to "silicon" and the name of the rectangle to "Die":

![ds9](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193506.png)
![ds10](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193549.png)
![ds11](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193601.png)
![ds12](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193636.png)
![ds13](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193659.png)

The following step is defining the substrate in the specified dimensions (5 mm x 5 mm, 0.5mm thickness). The easiest way is to draw a new rectangle that encompasses the die footprint and adjust the position values in the Parameters option of the contextual menu. 

![ds14](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193750.png)
![ds15](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193910.png)
![ds16](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20193929.png)

The thickness is added into the model using again the "Modeler-->Surface--> Thicken Sheet.." route after selecting the new rectangle

![ds17](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20194042.png)
![ds18](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20194107.png)

In the resulting geometry the substrate totally encloses the die. Since this does not make sense, since the substrate needs to be at a lower height than the die and not otherwise. A way to correct this is specifying a negative thickness of the same value:

![ds19](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20194157.png)
![ds20](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20194211.png)

The resulting geometry now makes sense. The name of the second rectangle needs to be changed to "Substrate" and the material to "FR4_epoxy":

![ds21](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20194755.png)
![ds22](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20194807.png)

#### 2 Add the die attach material and bond pads

The next step is to create the die attach material. However, in the geometry, the substrate and the die are adjacent so far, which is not totally correct. The substrate position in the vertical axis needs to be lowered by the thickness of the die attach, typically 0.1 mm. We do this in the Properties option of the conextual menu.

![da1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20194928.png)

Now there is a space between the substrate and the die where to add the die attach material layer:

![da2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20194947.png)

We create a new rectangle of the same dimensions of the die ( 3mm x 3mm), centered at the origin of coordinates (0,0,0), as the die, but with a negative thickness of 0.1mm:

![da3](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20195154.png)
![da4](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20195353.png)

The material of the new rectangle is changed to "modified_epoxy" and the name to "DieAttach"

![da5](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20195517.png)
![da6](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20195526.png)

The next step is to create the die bond pad. We define a rectangle of dimensions 0.2 mm x 0.2 mm and about 0.5mm into the Y axis. Since it needs to be placed on top of the die, its height is Z=0.2mm.

![da7](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20195716.png)
![da9](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20195858.png)
![da10](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20195957.png)
![da11](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20200052.png)

The next step is to create the substrate bond pad. We define a new rectangle of the same dimensions (0.2 mm x 0.2 mm) but placed on the substrate, that is, Z=-0.1mm.

![da12](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20200148.png)

Both bond pad rectangles are renamed:

![da13](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20200355.png)
![da14](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20200425.png)

#### 3 Create the wire bond and assign the material

The next step is to create the wire bond between the previously created die and substrate bond pads. For that we click on the "Draw Bondwire" button at the "Draw" tab.

![wb1](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20200725.png)

We trace a line connecting both bond pads:

![wb2](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20200753.png)

A Bondwire dialog window appears. We accept the defaults for the JEDEC4 norm.

![wb3](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20200806.png)

The bond wire is created:

![wb4](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20200856.png)
![wb5](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20200954.png)

To illustrate better the real layout we define a second die bond pad of the same dimensions (0.2mm x 0.2mm), 0.5mm into the X axis:

![wb6](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20201205.png)
![wb7](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20201258.png)

Finally we change the material of the bond wire from "copper" to "gold":

![wb8](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20201412.png)
![wb9](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20201429.png)
![wb10](https://github.com/ABM15/NASSCOM-Packaging/blob/main/Screenshot%202025-04-06%20201451.png)

#### 4 Apply mold compound and finalize the package model


   













