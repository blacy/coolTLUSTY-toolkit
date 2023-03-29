# coolTLUSTY-toolkit
python tools I made for post-processing 1d radiative-convective structure and spectral models in the coolTLUSTY output format, as
well as in the process of creating updated molecular absorption cross sections for use with coolTLUSTY.  

coolTLUSTY_model_class.py: defines a python "model" object with the following functions, initiated from a matching structure  
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
                          to a given wavelength, this approach could miss some nuances (requires separate molecule-by-molecule  
                          absorption cross sections and the chemical abundance table)

coolTLUSTY_input_tables.py: python module containing tools for reading and interpolating within coolTLUSTY-format
                            abundance tables, gas-phase opacity tables, rayleigh scattering tables, and mie tables

coolTLUSTY_tables: directory containing pre-tabulated values needed for coolTLUSTY runs. These include: chemical abundances, 
                   gas-phase absorption opacities, rayleigh scattering, water-ice mie table
                   
opacity_analyzer.ipynb: inspired by Caroline Morley's opacity-wizard, this notebook shows some examples of comparing the relative
                        contributions of different opacity sources for a given temperature, pressure, and chemical composition

construct_coolTLUSTY_opacity_table.py: given either a coolTLUSTY-format abundance table, or a Sonora-Bobcat format abundance
                                       table, construct an opacity table for use with coolTLUSTY. 

The absorption cross sections for individual absorbers can be obtained from this zenodo data-set: 
They are 25 GB when decompressed and include: H2O, CH4, NH3, PH3, H2S, CO, CO2, HCN, TiO, VO, SiO, MgH, FeH, CaH, CrH, TiH, and H2, 
as well as Allard 2016 and Allard 2019 Na and K resonant doublets. If you make use of them, please cite Lacy & Burrows 2023 which describes
their calculation with exocross in the appendix, as well as the original work done to generate line lists which are included as part of the 
hdf5 headers for each molecule's file.
