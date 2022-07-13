---
title:  "Handling and Manipulating netCDF file in python"
mathjax: true
layout: post
categories: media
---
![image](https://user-images.githubusercontent.com/109160548/178548932-1665e40a-1561-4f3a-a49a-413f7fcb6d77.png)

`NetCDF` is a widely used data storage format, capable of storing high-dimensional, array-oriented data. Climatic variables such as precipitation, temperature , soil moisture, atmospheric concentrations and many more that are produced from sources like satellite observations, reanalysis, climate models etc. requires spatio-temporal analysis and hence are often stored in netcdf `.nc` file format. 


![structure](https://user-images.githubusercontent.com/109160548/178547196-de404e22-36d9-4397-b2e3-7493b7e93378.png) \
*Fig 1: Structure of a netcdf file* 

This blog helps to get started with [xarray](https://docs.xarray.dev/en/stable/) - a powerful tool for reading, writing and manipulating N-dimensional data files and is particularly emphasized on handling `netcdf` files. `xarray` is very much similar to `pandas`, so if you already have a basic grip over `pandas`, it will be a lot more intuitive. 


## LETS CODE! 
First of all, import all the required packages
{% highlight python %}
import numpy as np                        # numerical computations
from matplotlib import pyplot as plt      # visualisation
import xarray as xr                       # for netcdf
import pandas as pd                       
import os
{% endhighlight %}

Next, we load the data using the `xr.open_dataset()` function. Here, we are using precipitation data from `APHRODITE`. You can change the directory to your own `.nc` file.

{% highlight python %}
# Load and have a look at the data
ds = xr.open_dataset(r"E:\precip_1981.nc")
ds
{% endhighlight %}
![ds_output](https://user-images.githubusercontent.com/109160548/178642934-d8dc260c-3a30-4e9b-a4fe-b922ab0f0afa.png)

We have loaded the `netcdf` file as an `xarray` dataset. The summary shows 


