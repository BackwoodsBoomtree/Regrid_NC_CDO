# Resample or Aggregate NC Files

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
remapcon2- Second order conservative remapping 
see this paper for the differences of con and con2: https://journals.ametsoc.org/view/journals/mwre/127/9/1520-0493_1999_127_2204_fasocr_2.0.co_2.xml

## Install
### install cdo to your linux, use:

sudo apt-get install cdo

If you get a package not found error, run:

sudo apt-get update

### On mac-os, to install cdo, run:

brew install cdo

## Example commands
by default, can run:

$ cdo remapcon,r360x180 ifile ofile

% this function makes 360 columns and 180 rows based on the lon and lat of your input file.
eg. if resample 1deg map from 4by5 map, by default the center is -89.75 and edge is -89.5;
If you desire to define the edges exactly as you need (eg. -90 on left edge, center point be -89.5),
then you need to write a txt file to define your own values, name the file gridfile.txt and run:

$ cdo -remapcon,gridfile.txt ifile ofile


## Other example commands
$ cdo remapbil,targetgrid ifile ofile

$ cdo -f nc remapcon,r360x180 ifile.nc ofile.nc

where targetgrid is a grid file and -f is output file type.

## Grid Description File

You can use a gridfile to explicitly define output. See grid files in this repo. Examples and descriptions are below.

An example for regridding to 1by1 degree:  
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

## Renaming for NC files created in R

* NC files created by R (terra) need to have the proj and grid_mapping paramaters renamed
```
beg_cmd_rename_crs = ''.join(['ncrename -a crs@proj4,proj_params '])
for i in range(len(in_files)):
    cmd_rename_crs = ' '.join([beg_cmd_rename_crs, in_files[i]])
    os.system(cmd_rename_crs)
    
beg_cmd_rename_grid = ''.join(['ncrename -a ', var_name, '@grid_mapping,grid_mapping_name '])
for i in range(len(in_files)):
    cmd_rename_grid = ' '.join([beg_cmd_rename_grid, in_files[i]])
    os.system(cmd_rename_grid)
```

![image](https://user-images.githubusercontent.com/31934468/136450401-caf21d8a-9e02-4591-9b00-c2ef5002dadb.png)
Source: https://code.mpimet.mpg.de/projects/cdo/embedded/index.html

