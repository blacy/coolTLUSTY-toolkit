# coolTLUSTY-toolkit
Python tools I made for post-processing 1d radiative-convective structure and spectral models in the coolTLUSTY output format, as
well as tools used to create updated molecular absorption cross sections with exocross.  

# Contents:

**coolTLUSTY_model_class.py**: defines a python "model" object with the following functions, initiated from a matching structure 
and spectral file in the format output by coolTLUSTY ("fort.20" and "fort.21" from a run of coolTLUSTY) 
                           
(1) quickly pull up some standard figures showing atmospheric structure and associated spectrum

(2) back out chemical abundance profiles for either equilibrium chemistry or quenching chemistry 
for CO-CH4 and N2-NH3 (requires the chemical abundance table utilized in the coolTLUSTY run)

(3) infer the location and opacity of clouds, assuming you implemented them in the same way as 
Lacy & Burrows 2023

(4) calculate a contribution function for each wavelength or an average contribution function for a 
photometric bandpass (requires the opacity table utilized in the coolTLUSTY run for equilibrium chemistry,
requires opacity tables and abundance table for quenched chemistry)

(5) approximately identify spectral features based on the dominant opacity source at the pressure 
layer where tau = 2/3 for each wavelength. NOTE that this is only an approximation! When multiple 
pressure layers dominated by different opacity sources are contributing nearly equal amounts of flux 
to a given wavelength, this approach could miss some nuances (requires separate molecule-by-molecule absorption cross sections and the chemical abundance table)

**coolTLUSTY_input_tables.py**: python module containing tools for reading and interpolating within coolTLUSTY-format abundance tables, gas-phase opacity tables, rayleigh scattering tables, and mie tables

**coolTLUSTY_tables**: directory containing pre-tabulated values needed for coolTLUSTY runs. These include: chemical abundances, gas-phase absorption opacities, rayleigh scattering, water-ice mie table
                   
**opacity_analyzer.ipynb**: inspired by Caroline Morley's opacity-wizard, this notebook shows some examples of comparing the relative contributions of different opacity sources for a given temperature, pressure, and chemical composition. Intended as a quick start guide for the user to modify and examine their own cases of interest.

**construct_coolTLUSTY_opacity_table.py**: script to construct an opacity table for use with coolTLUSTY given either a coolTLUSTY-format 
 abundance table, or a Sonora-Bobcat format abundance table. 
 
 **exocross_scripts**: directory containing some examples of scripts to download data from ExoMol, create exocross input files, and submit calculations for a grid of temperatures and pressures to run on one of the Princeton computing clusters (uses slurm for job scheduling). These are mostly for my future reference & to make my methods transparent, but could perhaps be useful to others wanting to calculate their own cross sections.

---------------------------------------------------------------------------------------------------------

The **absorption cross sections for individual molecules** can be obtained from this zenodo data-set: << fill in once it's ready >>

They are 25 GB when decompressed and include: H2O, CH4, NH3, PH3, H2S, CO, CO2, HCN, TiO, VO, SiO, MgH, FeH, CaH, CrH, TiH, and H2, as well as Allard 2016 and Allard 2019 Na and K resonant doublets. SO2 and the Hargreaves CH4 are in progress. If you make use of these, please cite both Lacy & Burrows 2023 which describes their calculation with exocross, as well as the original work done to generate line lists which are included as part of the hdf5 header for each molecule's file.
