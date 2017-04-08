---
layout:     post
title:      "A Python netCDF Lib"
subtitle:   ""
date:       2016-09-19
author:     "Baoxiang Pan"
header-img: "img/home.jpg"
comments: true
---

There are many technical requirements for a good researcher. Probably the most foundamental one is to  be familiar with a common data format, which includes storing, withdrawing according to demands, dividing or combining data sources, etc.. [netCDF](http://www.unidata.ucar.edu/software/netcdf/)(network Commmon Data Form) is one of the most popular data format for geologists and many other data scientists. For me, the reason to prefer netCDF is for its self-describing and machine-independent properties. A good engineer always make complete and simple abstractions. I think netCDF is a paradigm for this principle.

Many softwares are available for getting access and visualizing netCDF files. For example, we can use ncdump function from [netcdf
 software](http://www.unidata.ucar.edu/downloads/netcdf/index.jsp) to get the data and there descriptions, [NCO](http://nco.sourceforge.net/) provides many useful functions for combining, dividing and reading nc files. [Panoply](http://www.giss.nasa.gov/tools/panoply/) is a most convenient tool for netCDF visualization. But for me, the concern is that I want to have a full dorminant of the data in an integrated developing environment, and get access to data with there specifi units, for example, when I want ot extract the geo-data of certain period from certain region, I don't need a translation between the data's dimensions and their indexes. I can just type in:

```python
NCCut(file,variable,[[start-date,end-date],[start-lat,end-lat],[start-lon,end-lon]])  
```
instead of first looking at start and end indexes and then get data with:

```python
NCCut(file,variable,[[start-date-index,end-date-index],[start-lat-index,end-lat-index],[start-lon-index,end-lon-index]])  
```
This command will give the cutted variables in array form and store it in a new nc file with identical units and variable names.

The lib here also provides a plain netCDF drawing function called NCDraw:

```python
NCDraw(file,variable,time)
```

This can give a local surfplot with continental, coast, country and state division as backgroud.

The lib is available at my [github](https://github.com/lambdamore/California_Drought/tree/master/Code/Python/netcdf). Please feel free to contact me if you have any questions or feedbacks.

