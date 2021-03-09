# RasterMCDA-QGIS_Plugin
## PROTOTYPE

QGIS Plugin, featuring raster-based Multi Criteria Decision Analysis (MCDA) decision rules calculations.

RasterMCDA initially was implemented during my Bachelor studies in Geoinformation at the Carinthia University of Applied Science (CUAS). 

This was the first time for me implementing a QGIS Plugin.

Main source MCDA Theory/Mathematical formulas:
Malczewski, J. (1999) GIS and Multicriteria Decision Analysis. John Wiley and Sons, Inc., New York.

### PLUGIN AND ONLINE DOCUMENTATION STATUS: WORK IN PROGRESS


# How to use it:
After installing, the Plugin can be found in “Plugins” Tab

![grafik](https://user-images.githubusercontent.com/79254477/110510666-b8c90980-8103-11eb-88ea-8afee105b628.png)

There are two tools available:
- MCDA – Raster: for raster-based decision rules calculations
- MCDA – Weighting (Pairwise): for calculating Weights using Pairwise comparison


## Input raster files
All tools use valid raster files as input. These raster files are representing different criteria for a decision problem.
The raster files must have following properties:
- The same pixel size/spatial resolution/cell size (all input files)
- The same coordinate reference system (geographic or projected) (all input files)
- Same extend/origin (all input files)
- Must be numeric (all input files)
- Must not be standardized (Values between 0-1) 
- The plugin will “auto standardize” the raster layers if they are not

For testing these test raster files can be used: https://github.com/awallner-WallE/RasterMCDA-QGIS_Plugin/tree/main/test_data
The test files include three 4x4 standardized criteria raster files (factors) and one constraint map (Boolean raster file).

![grafik](https://user-images.githubusercontent.com/79254477/110510865-e6ae4e00-8103-11eb-9348-da2509245205.png)

### NOTE that the performance of the Plugins calculations with bigger raster files is very slow (tool MCDA – Raster). Also, the rest of QGIS is blocked during the calculations.

## Calculate weights with MCDA – Weighting (Pairwise)

Weights are used to include the “preferences” or “importance” of the different criteria into the calculations. The weights can be directly assigned in the “MCDA – Raster” tool or calculated with the “MCDA – Weighting (Pairwise)” tool. The following chapter describes the calculation workflow:

### Tool GUI:

![grafik](https://user-images.githubusercontent.com/79254477/110511022-15c4bf80-8104-11eb-8c42-101643da05ff.png)


Criteria can be added to the calculation with the “Add Factor” button.
In the example we add all three test criteria layers and fill the Pairwise comparison matrix according to the Scale of Saaty.
### Do only fill values in the lower-left diagonal side of the matrix

Example:

![grafik](https://user-images.githubusercontent.com/79254477/110511063-21b08180-8104-11eb-8b7f-e0191dceb4ee.png)
 
This would mean:
- factor2 is ”very strong more important” than factor1
- factor 3 is “moderate more important” than factor 1
- factor 3 is “moderate less important” than factor 2

After filling in the values, the output location can be set with the “Browse” button. The calculation can be started with the “OK” button.
The result will be saved in a “*.wpc” file. This file contains key-value pairs of the criteria names with the according calculated weight and the consistency ratio. For a consistent weighting the consistency ratio must be less than 0.1.

After the calculation is finished, the user is getting informed about the result by a “Message Box”. This “Message Box” contains the weights and the consistency ratio. If the consistency ratio is to high (above 0.1) The “Message Box” contains information that the consistency ratio is too high and there is inconsistency within his input (Figure 11). The user can check/change the input after the message was shown.

## Decision rules Calculation with MCDA – Raster

The tool MCDA – Raster can be used to execute raster-based decision rules calculations with a variable number of criterion layers.

### Tool GUI:

![grafik](https://user-images.githubusercontent.com/79254477/110511115-32f98e00-8104-11eb-8da7-2f0535e88156.png)
 

The user can choose between different decision rules through the “different decision rules tabs”. For the explanation the WLC is used.

![grafik](https://user-images.githubusercontent.com/79254477/110511146-3a209c00-8104-11eb-8c5e-ccf2efa08619.png)

 
The user can add a layer as a criterion with the “Add as Criterion” layer or ad a layer as a constraint with the “Add as constraint” button. In the example all three criterion layers are added as criterion and the constraint layer is added as constraint.

![grafik](https://user-images.githubusercontent.com/79254477/110511171-4147aa00-8104-11eb-9f7e-b667b3303d80.png)

Within the table the user can input if the criterion is a cost or benefit criterion (cost (0): the higher the values the worse, benefit (1): the higher the value the better). In the example the default value 1 (benefit) is ok.
The user can now directly assign the weights within the table. For example:

![grafik](https://user-images.githubusercontent.com/79254477/110511211-4ad11200-8104-11eb-9f57-0f585d443472.png)
 
This means (oversimplified):
- factor1 is the most important criterion for the problem
- factor 3 is the least important criterion for the problem
### NOTE THAT THE SUM OF WEIGHTS SHOULD BE 1

Also calculated weights (*.wpc file from “MCDA – Weighting (Pairwise)” tool) can be loaded with the “Load weights …” button. 
### Note: after loading weights, the table cannot be edited anymore.

![grafik](https://user-images.githubusercontent.com/79254477/110511273-57ee0100-8104-11eb-9f3e-a627e3f83fec.png)
 
After filling in the values, the output location can be set with the “Browse” button. The calculation can be started with the “OK” button. After the calculation the result will be added to QGIS.

![grafik](https://user-images.githubusercontent.com/79254477/110513101-24ac7180-8106-11eb-9a8e-70b85b156bea.png)


# Explanation of different Decision Rules will come in Future


