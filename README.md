# USWaterAccounting
This project hosts code to assemble water budget data for the US from existing data sources. 

Budget data are comprised of elements of annual water **supply** and annual water **consumption** for a specific geographic unit (e.g. state). Values are measured in both physical and monetary terms. 

**Water source data:**

- Annual *environmental* water supply data are derived from downscaled CMIP5 hydrology projections ([link](http://gdo-dcp.ucllnl.org/downscaled_cmip_projections/techmemo/BCSD5HydrologyMemo.pdf)). These data include monthly estimates of runoff, precipitation, evapotranspiration, and soil moisture content at a 1/8th degree spatial resolution across the US for the period of 1950 to 2099. Estimates are provided for 21 different climate projection ensembles applied to the Variable Infiltration Capacity (VIC) Macroscale Hydrologic Model ([link](http://vic.readthedocs.io/en/master/)); see the PDF document for a complete list. For demonstration purposes, this project uses the National Center for Atmospheric Research CCSM4 2.6 projection ensembles as the base data for water supply figures. 

  The scripts execute the following:

  - Downloads monthly runoff (total_runoff), precipitation (pr), evapotranspiration (et), and soil moisture content (smc) data, in NetCDF format, from a central data repository ([link](ftp://gdo-dcp.ucllnl.org/pub/dcp/archive/cmip5/hydro/BCSD_mon_VIC_nc/ccsm4_rcp26_r1i1p1/)) for a given sample year (2000, 2005, and 2010). 

  - Extracts the monthly data from the NetCDF files into 4-dimensional NumPy arrays (time, parameter value, latitude, longitude).

  - Aggregates the time dimension (months) into annual sums, resulting in a 3-dimensional array for each parameter, i.e. a single annual value for each 1/8th degree coordinate pair. 

  - Combines these 3-dimensional arrays, one for each parameter, into a single data frame listing parameter value, latitude, and longitude. 

    - | Longitude | Latitude | Runoff | Precip | ET   | SoilMoisture |
      | --------- | -------- | ------ | ------ | ---- | ------------ |
      |           |          |        |        |      |              |

      ​

  - Using the coordinate pairs, assigns the state and county FIPS code to each record. 

  - Summarize the data by state or county.

**Water use (and reuse) data**

* Water use/reuse data are derived from USGS water use data ([link](https://water.usgs.gov/watuse/)). These data include estimated water usage by category (public supply, domestic, industrial, etc.) at the county level for the entire US for the years 2000, 2005, and 2010. (Data for previous years are available, though the spatial units are different.)

  Scripts are provided here to:

  * Retrieve the data for a particular year. 
  * Summarize by state and by sector.

**Data compilation**

* The supply and use/re-use tables are reformatted to populate cells in a formatted Excel worksheet. 