---
title:  "Handling and Manipulating netCDF file in python"
mathjax: true
layout: post
categories: media
---
![image](https://user-images.githubusercontent.com/109160548/178548932-1665e40a-1561-4f3a-a49a-413f7fcb6d77.png)

`NetCDF` is a widely used data storage format, capable of storing high-dimensional, array-oriented data. Due to its simpler and robust structure, it is a common storage format for the spatio-temporal nature of climatic data. Some of the example data includes satellite/gridded precipitation datasets, outputs from climatic models - basically everything that is changing in both space (gridded) and time (time-series). 

![structure](https://user-images.githubusercontent.com/109160548/178547196-de404e22-36d9-4397-b2e3-7493b7e93378.png)
**Fig: Structure of a netcdf file**

## Code

Embed code by putting `{{ "{% highlight language " }}%}` `{{ "{% endhighlight " }}%}` blocks around it. Adding the parameter `linenos` will show source lines besides the code.


{% highlight python %}
# Load Libraries

import numpy as np
from matplotlib import pyplot as plt
import xarray as xr
import pandas as pd
import os
{% endhighlight %}



## Images

Upload an image to the *assets* folder and embed it with `![title](/assets/name.jpg))`. Keep in mind that the path needs to be adjusted if Jekyll is run inside a subfolder.

A wrapper `div` with the class `large` can be used to increase the width of an image or iframe.

![Flower](https://user-images.githubusercontent.com/4943215/55412447-bcdb6c80-5567-11e9-8d12-b1e35fd5e50c.jpg)

[Flower](https://unsplash.com/photos/iGrsa9rL11o) by Tj Holowaychuk

## Embedded content

You can also embed a lot of stuff, for example from YouTube, using the `embed.html` include.

{% include embed.html url="https://www.youtube.com/embed/_C0A5zX-iqM" %}
