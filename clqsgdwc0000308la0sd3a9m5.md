---
title: "17- Python-Based Kriging for Rainfall Interpolation in Erbil"
datePublished: Sat Dec 30 2023 19:26:01 GMT+0000 (Coordinated Universal Time)
cuid: clqsgdwc0000308la0sd3a9m5
slug: 17-python-based-kriging-for-rainfall-interpolation-in-erbil
tags: python, research, python3, interpretation, kriging, pykrige

---

This code performs spatial interpolation of rain data using kriging, enabling the estimation of rain values at unmeasured locations within the Erbil Governorate, based on the available data.

**1\. Importing Necessary Libraries:**

* **pandas:** Used for loading and manipulating tabular data, like the CSV file.
    
* **numpy:** Provides efficient array operations for numerical computations.
    
* **pykrige.ok:** Offers the OrdinaryKriging class for performing kriging interpolation.
    
* **matplotlib.pyplot:** Used to visualize data and create plots.
    

**2\. Loading Data:**

* `data =` [`pd.read`](http://pd.read)`_csv("Erbil_Rain.csv")`: Reads rain data from a CSV file named "Erbil\_Rain.csv" into a pandas DataFrame.
    

<table><tbody><tr><td colspan="1" rowspan="1"><p>station</p></td><td colspan="1" rowspan="1"><p>rain</p></td><td colspan="1" rowspan="1" colwidth="200"><p>x</p></td><td colspan="1" rowspan="1"><p>y</p></td></tr><tr><td colspan="1" rowspan="1"><p>Qushtapa</p></td><td colspan="1" rowspan="1"><p>350</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.0319</p></td><td colspan="1" rowspan="1"><p>36.0039</p></td></tr><tr><td colspan="1" rowspan="1"><p>Ainkwawa</p></td><td colspan="1" rowspan="1"><p>414</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.0119</p></td><td colspan="1" rowspan="1"><p>36.2206</p></td></tr><tr><td colspan="1" rowspan="1"><p>Khabat</p></td><td colspan="1" rowspan="1"><p>339</p></td><td colspan="1" rowspan="1" colwidth="200"><p>43.67039</p></td><td colspan="1" rowspan="1"><p>36.2758</p></td></tr><tr><td colspan="1" rowspan="1"><p>Bnaslawa</p></td><td colspan="1" rowspan="1"><p>381</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.1124</p></td><td colspan="1" rowspan="1"><p>36.15444</p></td></tr><tr><td colspan="1" rowspan="1"><p>Shorsh</p></td><td colspan="1" rowspan="1"><p>566</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.386</p></td><td colspan="1" rowspan="1"><p>36.1786</p></td></tr><tr><td colspan="1" rowspan="1"><p>Shaqlawa</p></td><td colspan="1" rowspan="1"><p>810</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.3214</p></td><td colspan="1" rowspan="1"><p>36.4056</p></td></tr><tr><td colspan="1" rowspan="1"><p>Harir</p></td><td colspan="1" rowspan="1"><p>591</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.355</p></td><td colspan="1" rowspan="1"><p>36.5475</p></td></tr><tr><td colspan="1" rowspan="1"><p>Khalifan</p></td><td colspan="1" rowspan="1"><p>768</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.4006</p></td><td colspan="1" rowspan="1"><p>36.6039</p></td></tr><tr><td colspan="1" rowspan="1"><p>Soran</p></td><td colspan="1" rowspan="1"><p>701</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.5428</p></td><td colspan="1" rowspan="1"><p>36.6581</p></td></tr><tr><td colspan="1" rowspan="1"><p>Rwandz</p></td><td colspan="1" rowspan="1"><p>736</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.5339</p></td><td colspan="1" rowspan="1"><p>36.6169</p></td></tr><tr><td colspan="1" rowspan="1"><p>Choman</p></td><td colspan="1" rowspan="1"><p>796</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.8808</p></td><td colspan="1" rowspan="1"><p>36.6278</p></td></tr><tr><td colspan="1" rowspan="1"><p>Sidakan</p></td><td colspan="1" rowspan="1"><p>824</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.6711</p></td><td colspan="1" rowspan="1"><p>36.7983</p></td></tr><tr><td colspan="1" rowspan="1"><p>Mergasor</p></td><td colspan="1" rowspan="1"><p>1384</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.3008</p></td><td colspan="1" rowspan="1"><p>36.84</p></td></tr><tr><td colspan="1" rowspan="1"><p>Makhmwr</p></td><td colspan="1" rowspan="1"><p>257</p></td><td colspan="1" rowspan="1" colwidth="200"><p>43.57887</p></td><td colspan="1" rowspan="1"><p>35.77511</p></td></tr><tr><td colspan="1" rowspan="1"><p>Bastora</p></td><td colspan="1" rowspan="1"><p>457</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.16148</p></td><td colspan="1" rowspan="1"><p>36.33709</p></td></tr><tr><td colspan="1" rowspan="1"><p>Dibaga</p></td><td colspan="1" rowspan="1"><p>299</p></td><td colspan="1" rowspan="1" colwidth="200"><p>43.808</p></td><td colspan="1" rowspan="1"><p>35.8747</p></td></tr><tr><td colspan="1" rowspan="1"><p>Gwer</p></td><td colspan="1" rowspan="1"><p>269</p></td><td colspan="1" rowspan="1" colwidth="200"><p>43.499</p></td><td colspan="1" rowspan="1"><p>36.048</p></td></tr><tr><td colspan="1" rowspan="1"><p>Barzewa</p></td><td colspan="1" rowspan="1"><p>700</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.611</p></td><td colspan="1" rowspan="1"><p>36.626</p></td></tr><tr><td colspan="1" rowspan="1"><p>Koya</p></td><td colspan="1" rowspan="1"><p>622</p></td><td colspan="1" rowspan="1" colwidth="200"><p>44.617</p></td><td colspan="1" rowspan="1"><p>36.083</p></td></tr></tbody></table>

**3\. Extracting Data:**

* `x = data['x']`
    
* `y = data['y']`
    
* `rain = data['rain']`: Extracts the x-coordinates, y-coordinates, and rain values from the DataFrame.
    

**4\. Creating a Kriging Object:**

* `ok = OrdinaryKriging(x, y, rain, variogram_model='linear', verbose=False)`: Creates an instance of OrdinaryKriging for spatial interpolation, using a linear variogram model.
    

**5\. Defining a Grid for Interpolation:**

* `grid_x = np.linspace(min(x), max(x), 100)`
    
* `grid_y = np.linspace(min(y), max(y), 100)`: Creates evenly spaced grid points in the x and y directions, covering the spatial extent of the data.
    

**6\. Performing Kriging Interpolation:**

* `z, ss = ok.execute('grid', grid_x, grid_y)`: Performs kriging interpolation on the defined grid, estimating rain values at each grid point and providing associated kriging variance (or squared standard deviation).
    

**7\. Plotting Original Data Points:**

* `plt.scatter(x, y, c=rain, cmap='viridis', label='Original Data')`: Creates a scatter plot of the original data points, with colors representing rain values.
    

**8\. Plotting Interpolated Surface:**

* `plt.contourf(grid_x, grid_y, z, cmap='viridis', levels=50)`: Creates a contour plot of the interpolated rain surface, smoothly visualizing the predicted rain values across the entire grid.
    

**9\. Displaying Plots:**

* [`plt.show`](http://plt.show)`()`: Shows both plots to visualize the original data and the interpolated surface.
    

**The full code is presented below:**

```python
import pandas as pd
import numpy as np
from pykrige.ok import OrdinaryKriging
import matplotlib.pyplot as plt

# Load data from CSV
data = pd.read_csv("Erbil_Rain.csv")

# Assuming the columns are named station, rain, x, and y
x = data['x']
y = data['y']
rain = data['rain']

# Create an instance of OrdinaryKriging
ok = OrdinaryKriging(x, y, rain, variogram_model='linear', verbose=False)

# Define a grid to interpolate
grid_x = np.linspace(min(x), max(x), 100)  # Adjust the number of points as needed
grid_y = np.linspace(min(y), max(y), 100)  # Adjust the number of points as needed

# Perform kriging interpolation on the defined grid
z, ss = ok.execute('grid', grid_x, grid_y)

# Plotting original data points
plt.figure(figsize=(10, 6))

# Plot original data points
plt.scatter(x, y, c=rain, cmap='viridis', label='Original Data')
plt.colorbar(label='Rain (mm)')
plt.title('Original Data Points')
plt.xlabel('X')
plt.ylabel('Y')

# Contour plot of the interpolated surface
plt.figure(figsize=(10, 6))
plt.contourf(grid_x, grid_y, z, cmap='viridis', levels=50)
plt.colorbar(label='Interpolated rain (mm)')
plt.title('Kriging Interpolated Rain')
plt.xlabel('X')
plt.ylabel('Y')

plt.tight_layout()
plt.show()
```