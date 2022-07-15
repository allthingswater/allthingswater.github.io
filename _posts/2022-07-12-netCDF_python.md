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

# Load and have a look at the data
Next, we load the data using the `xr.open_dataset()` function. Here, we are using precipitation data from `APHRODITE`. You can change the directory to your own `.nc` file.

{% highlight python %}
ds = xr.open_dataset(".\data\APHRO_MA_025deg_V1901.2000.nc")
ds
{% endhighlight %}
![ds](https://user-images.githubusercontent.com/109160548/179153669-9fc07fb7-9317-4cfe-85b7-8fe80387bea5.png)

We have loaded the `netcdf` file as an `xarray` dataset. The dataset summary can be viewed by simply runnning `ds`. It shows that our file has 3 dimensions: longitude (lon), latitude (lat) and time. The `Coordinates` section provide values of the dimensions. The `Data variables` shows 2 variables, but we are interested in the `precip` variable which stores the values for precipitation amount. The variables can be returned as an array by simply using `ds.variable_name` or `ds["variable_name"]`.

{% highlight python %}
ds["time"]
{% endhighlight %}

![image](https://user-images.githubusercontent.com/109160548/179155686-597f9f37-8559-491e-8a0b-b01dba73d0c1.png)

{% highlight python %}
ds.precip
{% endhighlight %}

![image](https://user-images.githubusercontent.com/109160548/179157440-a61f6841-75f5-4b6b-bd2f-54bdbbf79395.png)

# Quick plotting
We can quickly plot the data for a single day. 
{% highlight python %}
pr_plot = plt.imshow(ds.precip[180],origin="lower")
plt.colorbar(pr_plot)
{% endhighlight %}

