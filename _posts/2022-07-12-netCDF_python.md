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

![quick_plot](https://user-images.githubusercontent.com/109160548/179161642-fbc61d02-ed8a-48bb-bb87-16de5e3a65b5.png)

Since our file stores spatial data for each time step (every day of year 2000), we first select a single day. In the code above, `ds.precip[180]` selects the 179th day of the year (remember that python indexing starts with a 0). The argument `origin="lower"` is used for matrix plotting that usually starts at lower corner. 

# Combining files with same spatial extent but different time periods
The file we are using have data for a single year only. Most of the time, we may have multiple files for different time periods (say for each year) but havin the same spatial extent. Processing each file repeatedly consumes time and is inefficient. `xarray` provides a function for merging such multiple files together into a continuous spatio-temporal series. 

{% highlight python %}
files=[os.path.join("full_path_to_folder",f) for f in os.listdir(".\data")]

ds = xr.open_mfdataset(files,combine = 'by_coords', concat_dim ="time")
ds
{% endhighlight %}

![ds_merge](https://user-images.githubusercontent.com/109160548/179163212-9a65cc3d-b1d4-4b76-ad13-c91341bbf585.png)


We store the full path of all the .nc files that we want to merge in the `files` variable. Next, merge all the files by co-ordinates (`combine` argument). Notice that the number of longitute and latitude are same as the previous dataset but the time variable has increased covering years 2000-2015. Also note that the data variable `precip` is now a `dask.array` instead of a `data.array`.

# Clip using spatial extent and time
We can clip the file to contain only a specific area or spanning only a subset of time using the `sel` and `slice` functions. Make sure that the you are using the name of the coordinates (instead of lat,lon and time) for your own `.nc` file.
{% highlight python %}
start_date = "2005-01-01"
end_date = "2008-12-31"
clip_ds=ds.sel(lon=slice(79,90),lat=slice(25,31),time=slice(start_date,end_date))
{% endhighlight %}

The clipped file can again be saved as a netCDF file.
{% highlight python %}
clip_ds.to_netcdf('./data/Clipped.nc')
{% endhighlight %}

# Extract values for single point
We can also extract time-series data for a particular point location of interest, maybe at the location of ground-station, and export it as a `csv` file or plot it. 
{% highlight python %}
stn_lat=29.3689
stn_lon=81.2062
stn_val=ds.precip.sel(lon=stn_lon,lat=stn_lat,method='nearest')

df= stn_val.to_dataframe()
df.head()
df.to_csv('.\data\stn_precip.csv')
{% endhighlight %}

![df](https://user-images.githubusercontent.com/109160548/179166959-bf7a2ee6-4378-4ea1-9648-afeb9f50c1d3.png)

{% highlight python %}
stn_val.plot()
{% endhighlight %}

![image](https://user-images.githubusercontent.com/109160548/179167731-a9e15e32-9767-491b-86cf-570e5507b901.png)

I hope this post helps to get you started with the powerful `xarray` package for handling and manipulating `netCDF` files. The `xarray` package provides more advanced and powerful functionalities with user-friendly and extensive documentation, so do check them out at https://docs.xarray.dev/en/stable/index.html.

Until next time!

-Nischal Karki
