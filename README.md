# Regrid_NC_CDO

Can use command line and CDO to aggregate or resample entire NC files. CDO homepage: https://code.mpimet.mpg.de/projects/cdo  
This page is helpful for describing regridding: https://code.mpimet.mpg.de/projects/cdo/wiki/Tutorial#Interpolation  
Basic CDO and nc commands for taking a look at your data, and some basic usage: https://code.mpimet.mpg.de/projects/cdo/wiki/Tutorial  

## Methods
Horizontal interpolation can be done with the CDO operators:  
remapbil - Bilinear interpolation  
remapbic - Bicubic interpolation  
remapdis - Distance-weighted average remapping  
remapnn - Nearest neighbor remapping  
remapcon - First order conservative remapping  

## Install
install cdo to your linux using:

sudo apt-get install cdo

If you get a package not found error, run:

sudo apt-get update

## Example commands

$ cdo remapbil,targetgrid ifile ofile

$ cdo -f nc remapcon,r360x180 ifile.nc ofile.nc

where targetgrid is a grid file and -f is output file type.

## Grid Description File

Can use a gridfile to explicitly define output. See grid files in this repo. Examples and descriptions are below.

Example:  
gridtype  = lonlat  
gridsize  = 64800  
datatype  = float  
xsize     = 360  
ysize     = 180  
xname     = longitude  
xlongname = "Longitude"  
xunits    = "degrees_east"  
yname     = latitude  
ylongname = "Latitude"  
yunits    = "degrees_north"  
xfirst    = -179.5  
xinc      = 1  
yfirst    = -89.5  
yinc      = 1  


![image](https://user-images.githubusercontent.com/31934468/136450401-caf21d8a-9e02-4591-9b00-c2ef5002dadb.png)
Source: https://code.mpimet.mpg.de/projects/cdo/embedded/index.html

