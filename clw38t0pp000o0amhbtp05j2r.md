---
title: "Calculating Common Remote Sensing Indices in Python"
datePublished: Sun May 12 2024 07:57:50 GMT+0000 (Coordinated Universal Time)
cuid: clw38t0pp000o0amhbtp05j2r
slug: calculating-common-remote-sensing-indices-in-python
tags: python, index, remotesensing

---

Hey there! Today, we're diving into some Python code to analyze satellite imagery. We'll be using data from Landsat, specifically focusing on a location near Erbil, the capital city of the Kurdistan Region in Iraq.

### Import necessary libraries

```python
import rasterio  # Library for reading and writing raster data
import matplotlib.pyplot as plt  # Plotting library
```

First off, we'll access the satellite data stored on Google Cloud. Landsat imagery is organized by paths and rows, and for our analysis, we're interested in Landsat Path 168 and Row 35.

We'll grab the necessary bands from Landsat: the Red, Near Infrared (NIR), and Shortwave Infrared (SWIR) bands. These bands are essential for calculating various indices like NDVI (Normalized Difference Vegetation Index), NDBI (Normalized Difference Built-up Index), and NDWI (Normalized Difference Water Index).

```python
url = "https://storage.googleapis.com/gcp-public-data-landsat/LC08/"+\
       "01/168/035/LC08_L1TP_168035_20170923_20171013_01_T1/"
# The url variable holds the base URL for Landsat data on Google Cloud Storage.

redband = 'LC08_L1TP_168035_20170923_20171013_01_T1_B{}.TIF'.format(4)
nirband = 'LC08_L1TP_168035_20170923_20171013_01_T1_B{}.TIF'.format(5)
swirband = 'LC08_L1TP_168035_20170923_20171013_01_T1_B{}.TIF'.format(6)
```

```python
with rasterio.open(url+redband) as src:
    redImage = src.read(1).astype('f4')
# rasterio.open(url+redband) as src: This line opens the raster file specified by the URL concatenated
# with the redband variable. The redband variable typically contains the filename of 
# the red band image. The with statement ensures that the raster file is properly closed after use.
# The raster data is read from band 1 (read(1)) and converted to a floating-point array (astype('f4')).
# The resulting array is stored in the redImage variable.

with rasterio.open(url+nirband) as src:
    nirImage = src.read(1).astype('f4')

with rasterio.open(url+swirband) as src:
    swirImage = src.read(1).astype('f4')
```

Once we have our bands, we'll calculate NDVI, NDBI, and NDWI. These indices help us understand vegetation, built-up areas, and water bodies in the satellite imagery.

### **Normalized Difference Vegetation Index (NDVI)**

```python
def calc_ndvi(nir, red):
    '''Calculate NDVI from integer arrays'''
    ndvi = (nir - red) / (nir + red) # This line calculates the NDVI using the formula: (NIR - Red) / (NIR + Red).
    return ndvi

# Apply a function
ndvi = calc_ndvi(nirImage, redImage)

# Display NDVI
plt.imshow(ndvi, cmap='RdYlGn')
plt.colorbar()
plt.title("NDVI", fontsize=20)
plt.xlabel('Column #')
plt.ylabel('Row #')
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715500052112/61cd9c12-5ff1-460e-96fe-5eeeb5afdf3c.png align="center")

### **Normalized Difference Built-up Index (NDBI)**  

```python
def calc_ndbi(swir,nir):
    '''Calculate NDBI from integer arrays'''
    ndbi = (swir - nir) / (swir + nir)
    return ndbi
# Apply a function
ndbi = calc_ndbi(swirImage,nirImage)

# Display NDBI
plt.imshow(ndbi, cmap='RdYlGn')
plt.colorbar()
plt.title("NDBI", fontsize=20)
plt.xlabel('Column #')
plt.ylabel('Row #')
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715500130566/c01fe795-a691-449d-ba30-ac364f51754c.png align="center")

### **Normalized Difference Water Index (NDWI)**  

```python
# define a function
def calc_ndwi(nir,swir):
    '''Calculate NDWI from integer arrays'''
    ndwi = (nir - swir) / (nir + swir)
    return ndwi
# Apply a function
ndwi = calc_ndwi(nirImage,swirImage)

# Diasplay NDWI
plt.imshow(ndwi, cmap='RdYlGn')
plt.colorbar()
plt.title("NDWI", fontsize=20)
plt.xlabel('Column #')
plt.ylabel('Row #')
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715500182473/3eedaf62-50ed-4a1e-a7e7-e587664cb0f1.png align="center")

Now, let's talk about NBR (Normalized Burn Ratio). It's another important index, especially for assessing fire damage. We'll calculate NBR using the NIR and SWIR bands.

After calculating NBR, we'll export it as a GeoTIFF file for further analysis or sharing with others. This file will contain valuable information about burn severity in the area.

Finally, we'll visualize the NBR map to get a clearer picture of the burn severity distribution. This visualization will help us interpret the results and understand the extent of the fire damage.

### **Normalized Burn Ratio (NBR) Index**

```python
# Define a function
def calc_nbr(nir, swir):
    '''Calculate NBR using NIR and SWIR bands.'''
    nbr = (nir - swir) / (nir + swir)
    return nbr

# Landsat data URL
url = "https://storage.googleapis.com/gcp-public-data-landsat/LC08/"+\
       "01/168/035/LC08_L1TP_168035_20170923_20171013_01_T1/"
nirband = 'LC08_L1TP_168035_20170923_20171013_01_T1_B5.TIF'
swirband = 'LC08_L1TP_168035_20170923_20171013_01_T1_B6.TIF'

# Open NIR and SWIR bands
with rasterio.open(url + nirband) as src_nir, rasterio.open(url + swirband) as src_swir:
    nir = src_nir.read(1).astype('f4')
    swir = src_swir.read(1).astype('f4')

    # Calculate NBR
    nbr = calc_nbr(nir, swir)

    # Export the output to a local GeoTIFF file
    output_file = "nbr_output.tif"
    with rasterio.open(
        output_file,
        'w',
        driver='GTiff',
        width=nir.shape[1],
        height=nir.shape[0],
        count=1,
        dtype=nbr.dtype,
        crs=src_nir.crs,
        transform=src_nir.transform
    ) as dst:
        dst.write(nbr, 1)

    # Display nbr
    plt.imshow(nbr, cmap='RdYlGn')
    plt.colorbar()
    plt.title("NBR", fontsize=20)
    plt.xlabel('Column #')
    plt.ylabel('Row #')
    plt.show()
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715500248068/f95d19d3-0ff4-4686-835a-afbcfdc8c776.png align="center")

And that's it! By leveraging Python and satellite imagery, we can gain valuable insights into environmental changes and make informed decisions.