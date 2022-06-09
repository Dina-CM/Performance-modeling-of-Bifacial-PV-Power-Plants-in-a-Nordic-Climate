# Performance modeling of Bifacial PV Power Plants in a Nordic Climate
This repository contains the most important scripts created as a part of the work performed for the master's thesis "Performance modeling of Bifacial PV Power Plants in a Nordic Climate" in Materials Chemistry and Energy Technology. The master's thesis marks the completion of a five-year Master of Science degree in Chemical Engineering and Biotechnology at the Norwegian University of Science and Technology (NTNU) <be>
  
&copy; Dina Christensen Martinsen 

# Repository overview: 
*All scripts included are generalized for brevity. Modified version of these script, tailored to each of the many specific simulation scenarios studied, are used to create the results reported in the master's thesis.* 
##########################################################################

- **Read from database data frames, adjust for timezone and filtering of data**<br>
This file contains the script created to read dataframes containing the extracted data from the database. The location specifics are defined and the initial filtering steps are applied to the collected data. The script also performs the decomposition step by the Disc decomposition model to generate DHI and DNI data. A custom EPW file is also created using this script to be used as input for bifcial_radiance by resampling the measured data to hourly timesteps and sorting the data to the requirements.

- **Uncertainty calculation of irradiance measurements functions**<br>
This file includes the functions created to perform the uncertainty parameterization calculations for the pyranometer measurements and PVRD measurements collected from the site. The uncertainty parameterization was performed using *JCGM 100:2008 GUM  Evaluation of measurement data — Guide to the expression of uncertainty in measurement* in combination with parameter values provided in data sheets and calibration certificates for the measuring equipment as described in the master's thesis.

- **3D-model in bifacial_radiance**<br>
This section contains the 3D-model of the bifacial PV array created in bifacial_radiance. Each and every one of the many simulation scenarios of this work are assigned a Modified version of this script tailored to the specifics of the simulation scenario. For brevity, only the general script is included here.  
The script adds the custom radiance materials file to the folder of each simulation, defines the site specifics, imports the custom EPW file and sets up the 3D-model of the bifacial PV array. All dimensions, positions, angles and labels are added according to the measurements of the bifacial PV array described in the master's thesis. 

- **Ray-tracing procedure**<br>
This file contains the script created to perform the full cell-level ray-tracing procedure in bifacial_radiance. The script generates a sky for the model, defines sensor positions, performs the irradiance analysis and stores the analysis results. 
There are two approaches used for the sky, generation of a cumulative sky to represent the entire year, or a sky created to represent a single timestamp. For the single timestamp sky creation, a loop is used to simulate several hourly timestamps. The example below illustrates the procedure for one single timestamp, including bifacial gain calculations across the array and the creation of irradiance maps. 

- **Mismatch calculations**<br>
This file contains the script created to perform the mismatch calculation in PVMismatch using the cell-level irradiance input from the ray-tracing procedure. The script evaluates the electrical mismatch that occurs between individual cells and includes the influence of bypass diode configuration and circuit design to form modules and then combines the modules into the complete PV system.
Cell parameters for the double diode model are defined and provided by module number corresponding to measurement data from the testing performed at IFE. As the simulation runs, the individual cells are copied and altered according to the input of irradiance to model the power-voltage and current-voltage characteristics at cell to system level. Like for the ray-tracing procedure for single timestamp sky files, the mismatch analysis is performed for timeseries using a loop to analyze each full cell-level irradiance simulation result desired.  

- **custom_materils.rad**
This file contains the radiance materials for the ray-tracing simulations, both the default materials and the custom radiance materials created from the tarp and ground cover characterization performed in this work.  

## Illustration of the 3D-model created in bifacial_radiance as a part of this master's thesis
![Picture2](https://user-images.githubusercontent.com/102217024/172667340-25460ed7-92b5-4bf0-89f2-989c80b0ee5d.png)

  
## Prerequisites:  
The use of the scripts included in this repository requireds the previous installation of [RADIANCE](https://github.com/NREL/Radiance) and [bifacial_Radiance](https://bifacial-radiance.readthedocs.io/en/latest/index.html#), as well as python with numpy, jupyter and pvlib.  
  
