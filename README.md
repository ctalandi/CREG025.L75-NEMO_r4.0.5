# CREG025.L75-NEMO_r4.0.5 <br>
This reprository hold #1 the NEMO code source (how to download it) as associated input files as well (hereafter namelists) and #2 the list of other input files to describe the grid, the bathymetry and the surface forcing used to perform the numerical experiment called CREG025.L75-ERA01NEM405LAS. <br>

## OVERVIEW
The CREG025.L75-ERA01NEM405LAS experiment relies on the ocean/sea ice models from the NEMO numerical plateform [NEMO](https://www.nemo-ocean.eu); it uses both NEMO-OPA and NEMO-SI3 models for the ocean and the sea ice components respectively. It aims at simulating the ocean/sea-ice dynamics over the north Atlantic ocean (starting from ~25°N), the Greenland-Iceland-Norway seas and the whole Arctic basin with a limit along the Bering strait.<br>
* The horizontal grid is a 1/4 degree i.e. from ~25km up to ~12km in most of the Arctic basin.
* A 75 vertical levels from 1m close to the surface up to 200m below 4000m.
* The model time step is ∆t=720s.
* The period simulated covers the range 1979-2009 (31-year long).

### SOURCE CODE : 
   * The ocean/sea ice model: <br>
	** The code source relies on the official NEMO release 4.0.5. Information can be found there https://forge.ipsl.jussieu.fr/nemo/wiki/Users#. 
	*** This official release can be downloaded with the following commnand line:
```
svn co https://forge.ipsl.jussieu.fr/nemo/svn/NEMO/releases/r4.0/r4.0.5 
```
	*** The specific code source changes associated to this experiment in the [MY_SRC](./NEMOGCM/cfgs/CREG025.L75-ERA01NEM405LAS/MY_SRC) directory. The [arch](./NEMOGCM/arch) list all computing architectures on which NEMO has been compiled as templates.
   * The XIOS libray to perform outputs:<br>
	** Outputs have been realised in using the XIOS 2.5 library; the revision 1763 has been downloaded and compiled. More information can be found there [XIOS](https://forge.ipsl.jussieu.fr/nemo/chrome/site/doc/NEMO/guide/html/install.html#extract-and-install-xios).
r1763

### INPUT FILES :
1 - Time invariant input files:
   * Domain configuration: <br>
	** Description: This domain file gathers the horizontal grid, the bathymetry as the grid points geographical location as well of the configuration. This file has been extracted from an existing global ORCA025.L75 configuration file.<br>
	** File name: ```CREG025.L75_domain_cfg.nc```<br>
   * Ocean initialisation: <br>
	** Description: World Ocean Atlas 2009 at 1°x1° climatology <br>
	** File name:```woa09_temperature01_monthly_1deg_t_an_CMA_drowned_Ex_L75.nc, woa09_salinity01_monthly_1deg_s_an_CMA_drowned_Ex_L75.nc``` <br>
   * Ice initialisation:<br>
	** Description: January climatology computed over the period 1998-2007 from a global ocean numerical experiement called ORCA12.L46-MAL95. <br>
	** File name:```CREG025_SOSIE-CREG12_drowned_ORCA12.L46-MAL95_y1998-2007m01_icemod.nc```<br>
   * Tidal mixing parametrization: <br>
	** Description: A new comprehensive parameterization of mixing by breaking internal tides and lee waves (de Lavergne et al., 2019) <br>
	** File name:```mixing_power_bot.nc, mixing_power_pyc.nc, mixing_power_cri.nc, decay_scale_bot.nc, decay_scale_cri.nc``<br>
   * Distance to the coast:<br>
	** Description: gives the distance to the coast of each ocean grid points. It is used to switch off the SSS restoring in a 400km wide range from the coast.<br>
	** File name: ```dist_coast_CREG025_vh20161121.nc```<br>

2 - Time varying input files:
   * Surface forcing:<br>
	** Description: The atmospheric forcing data set [ERA5](https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/era5), with ```CORE bulk formulae``` (from NCAR) and relative winds (ocean surface velocity components taken into account for the wind stress<br>
	** File name: ```<var>_ERA5-1440x721-CREG025.nc``` <var> stands for either u10,v10,msdwswrf,msdwlwrf,mtpr,msr,t2,q2.<br>
	** Frequency: hourly for all fields <br>
   * Rivers and Greenland melting fluxes:<br>
	** Description: A blend of data from Dai & Trenberth for rivers volume fluxes and Bamber for fresh water resulting from Greenland melting<br>
	** File name: ```CREG025_runoff_monthly_combined_Dai_Trenberth_Bamber.nc``<br>
	** Frequency: monthl<br>
   * Open boundaries:<br>
	** Description: 2 open boundaries conditions limit the regional domain, data are used there to force the model and are extracted from a previous global numercial simulation called ORCA025.L75-GJM189 [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4626012.svg)](https://doi.org/10.5281/zenodo.4626012)<br>
	** File name: ```ORCA025.L75-GJM189-CREG025.L75-BDY_south__<var>.nc``` and ```ORCA025.L75-GJM189-CREG025.L75-BDY_north_<var>.nc```. <var> stands vor SSH, U, V, T, S and ice for the Bering open boundar<br>
	** Frequency: monthly <br>
   * Chlorophyll climatology:<br>
	** Description: Seawiffs satellite data climatology over the period 1999-2005<br>
	** File name: ```chlaseawifs_c1m-99-05_smooth_CREG_R025_vh20161117``<br>
	** Frequency: monthly<br>
   * World Ocean Atlas 2009 surface salinity:<br>
	** Description: Sea surface salinity restoring with a piston velocity of 167 mm/day ( 60 days/10 meters<br>
	** File name: ```woa09_sst01-12_monthly_1deg_t_an_CMA_drowned_Ex_L75.nc```<br>
	** Frequency: monthly<br>
   * World Ocean Atlas 2009 surface temperature:<br>
	** Description: to avoid SSS restoring where the SST climatology temperature is at the freezing point, i.e. in presence of sea-ice<br>
	** File name: ```woa09_sss01-12_monthly_1deg_s_an_CMA_drowned_Ex_L75.nc```<br>
	** Frequency: monthly<br>
