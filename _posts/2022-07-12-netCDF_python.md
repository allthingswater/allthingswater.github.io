---
title:  "Handling and Manipulating netCDF file in python"
mathjax: true
layout: post
categories: media
---
![image](https://user-images.githubusercontent.com/109160548/178548932-1665e40a-1561-4f3a-a49a-413f7fcb6d77.png)

`NetCDF` is a widely used data storage format, capable of storing high-dimensional, array-oriented data. Due to its simpler and robust structure, it is a common storage format for the spatio-temporal nature of climatic data. Anything, that is changing in both space and time  

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




