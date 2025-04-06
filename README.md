# NASSCOM-Packaging
Repository for the lab exercises of the "VSD NASSCOM Semiconductor Packaging Workshop" (03/28/2025-04/06/2025 Cohort).

## Module 1 - Packaging Evolution: From Basics to 3D Integration
There are no exercises prescribed for this module.

## Module 2 - From Wafer to Package: Assembly and Manufacturing Essentials
There are no exercises prescribed for this module.

## Module 3 - Labs: Thermal Simulation of Semiconductor Packages with ANSYS

The objective of the lab is to model a FlipChip BGA package and perform a thermal simulation in the Ansys Electronics Desktop (AED) environment. The phases involved are the following:

1) Start the Ansys Electronics Desktop Student software
2) Set up a FlipChip BGA package
3) Thermal definitions and material power sources
5) Define the mesh
6) Perform the thermal simulation
7) Explore results

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













