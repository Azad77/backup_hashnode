---
title: "Enhance the accuracy of crop classification in Google Earth Engine using the Random Forest"
datePublished: Sun May 05 2024 13:43:53 GMT+0000 (Coordinated Universal Time)
cuid: clvtl33b7000a09jx7svccdbq
slug: enhance-the-accuracy-of-crop-classification-in-google-earth-engine-using-the-random-forest
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724478075173/16d67b51-121f-4fba-9755-ea86b6f8c9e9.png
tags: sentinel, random-forest, google-earth-engine

---

Hello everyone, in today's tutorial, we're going to dive into Random Forest classification. It's a powerful tool in machine learning that helps categorize data into different classes. Let's break it down step by step.

**1\. Building Decision Trees:** Firstly, the algorithm creates numerous decision trees. Each tree uses a random subset of the training data and features. Think of these trees as a series of questions—like "if this, then that"—that ultimately classify a data point.

**2\. Introducing Randomness:** Now, why random? Well, by picking different data and features randomly for each tree, we prevent the model from becoming too good at the training data but bad at new data. This randomness helps combat overfitting, a common issue in machine learning.

**3\. Making Predictions:** Once we've built all the decision trees, a new data point goes through each tree. Each tree then makes its own prediction about which class the data point belongs to. Finally, the most common prediction among all trees becomes the final classification for the new data point.

**Advantages:** Let's talk about the pros of Random Forest classification:

* **High Accuracy:** It can achieve impressive accuracy on classification tasks.
    
* **Robust to Overfitting:** Random forests are great at handling overfitting.
    
* **Handles Missing Data:** They can effectively deal with missing data points in the training dataset.
    
* **Feature Importance:** The algorithm provides insights into the importance of different features in the classification process.
    

**Disadvantages:** But, like everything, there are drawbacks:

* **Black Box Model:** Random forests can be complex, making it tricky to interpret how they make predictions.
    
* **High Computational Demands:** Building large random forests requires substantial computer power, especially with big datasets.
    

## Enhancing Crop Classification Accuracy with GEE: A Case Study

Now, we're diving into some exciting GEE (Google Earth Engine) code used in our recent paper titled "Improving Crop Classification Accuracy with Integrated Sentinel-1 and Sentinel-2 Data: a Case Study of Barley and Wheat", published by me (Azad Rasul, Dr. Gaylan Ibrahim, and Dr. Haidi Abdullah.

If you used the code for your research, please cite our paper as follows: (Faqe Ibrahim, G.R., Rasul, A. and Abdullah, H., 2023. Improving crop classification accuracy with integrated Sentinel-1 and Sentinel-2 data: A case study of barley and wheat. Journal of Geovisualization and Spatial Analysis, 7(2), p.22.)

**Let's get started with the code.**

### **Sentinel-1 SAR**

First, we'll work with Sentinel-1 SAR (Synthetic Aperture Radar) data. We're specifically loading the C-band SAR Ground Range collection for both VV (vertical-vertical) and VH (vertical-horizontal) polarizations.

We filter these collections based on instrument mode, polarization, orbit direction, resolution, and a region of interest (ROI). Then, we clip the images to our ROI and select the VV or VH bands.

Next, we filter the SAR collections by date, focusing on a specific range. We create mosaics of VV and VH images for this date range.

To visualize these images, we add them as layers to the map. We set center and zoom parameters, then display the SAR VV and VH layers.

Moving on, we apply a filter to reduce speckles in the SAR images. We use a focal mean filter with a specified smoothing radius.

Finally, we add the filtered SAR images as additional layers to the map. This allows us to compare the original and filtered SAR images for both VV and VH polarizations.

```javascript
//----------------------------------- SAR -----------------------------------
// Load Sentinel-1 C-band SAR Ground Range collection (log scale, VV, descending)
// roi
var roi = ee.Geometry.Polygon(
  [[[44.253, 36.569],
    [44.293, 36.596],
    [44.367, 36.526],
    [44.328, 36.5]]], null, false);
var collectionVV = ee.ImageCollection('COPERNICUS/S1_GRD')
  .filter(ee.Filter.eq('instrumentMode', 'IW'))
  .filter(ee.Filter.listContains('transmitterReceiverPolarisation', 'VV'))
  .filter(ee.Filter.eq('orbitProperties_pass', 'DESCENDING'))
  .filterMetadata('resolution_meters', 'equals' , 10)
  .filterBounds(roi)
  .map(function(image){return image.clip(roi)})
  .select('VV');
print(collectionVV, 'Collection VV');

// Load Sentinel-1 C-band SAR Ground Range collection (log scale, VH, descending)
var collectionVH = ee.ImageCollection('COPERNICUS/S1_GRD')
  .filter(ee.Filter.eq('instrumentMode', 'IW'))
  .filter(ee.Filter.listContains('transmitterReceiverPolarisation', 'VH'))
  .filter(ee.Filter.eq('orbitProperties_pass', 'DESCENDING'))
  .filterMetadata('resolution_meters', 'equals' , 10)
  .filterBounds(roi)
  .map(function(image){return image.clip(roi)})
  .select('VH');
print(collectionVH, 'Collection VH');

// Filter SAR collections by date
var SARVV = collectionVV.filterDate('2022-04-19', '2022-04-24').mosaic();
var SARVH = collectionVH.filterDate('2022-04-19', '2022-04-24').mosaic();

// Add the SAR images to the map for visualization
Map.centerObject(roi, 12);
Map.addLayer(SARVV, {min:-15,max:0}, 'SAR VV', 0);
Map.addLayer(SARVH, {min:-25,max:0}, 'SAR VH', 0);

// Apply filter to reduce speckle
var SMOOTHING_RADIUS = 50;
var SARVV_filtered = SARVV.focal_mean(SMOOTHING_RADIUS, 'circle', 'meters');
var SARVH_filtered = SARVH.focal_mean(SMOOTHING_RADIUS, 'circle', 'meters');

// Display the filtered SAR images
Map.addLayer(SARVV_filtered, {min:-15,max:0}, 'SAR VV Filtered',0);
Map.addLayer(SARVH_filtered, {min:-25,max:0}, 'SAR VH Filtered',0);
```

And that's it! We've successfully loaded, filtered, and visualized SAR images using Google Earth Engine.

### **Sentinel-2**

Now, let's move on to Sentinel-2A. First, we'll start by masking out clouds and cirrus in Sentinel-2 imagery. This helps us get clearer images for our analysis. We'll use a function called "maskS2clouds" to do this. It selects the quality assessment band, defines cloud and cirrus bits, and creates a mask to indicate clear conditions. Then, we'll load the Sentinel-2 imagery, filter it by date and cloud cover, apply the cloud masking function we just created, and clip it to our region of interest.

Now, let's visualize the Sentinel-2 imagery on the map. We'll set some parameters for better visualization and add the imagery to the map. We can also get some basic information about the imagery by printing it.

Next, we'll take the mean of the Sentinel-2 imagery. This helps us get a clearer picture by reducing noise and variations.

```javascript
//--------------------------- Sentinel 2 -------------------------
// Function to mask clouds and cirrus in Sentinel-2 imagery
function maskS2clouds(image) {
  var qa = image.select('QA60');
  var cloudBitMask = 1 << 10;
  var cirrusBitMask = 1 << 11;
  var mask = qa.bitwiseAnd(cloudBitMask).eq(0)
      .and(qa.bitwiseAnd(cirrusBitMask).eq(0));
  return image.updateMask(mask).divide(10000);
}

// Load Sentinel-2 imagery, filter by date and cloud cover, apply cloud masking, and clip to the ROI
var image = ee.ImageCollection('COPERNICUS/S2_SR')
              .filterDate('2022-05-19', '2022-05-22')
              .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE',5))
              .filterBounds(roi)
              .map(maskS2clouds)
              .map(function(image){return image.clip(roi)});

// Visualization parameters for displaying Sentinel-2 imagery
var vis = { min: 0.0, max: 0.3, bands: ['B4', 'B3', 'B2'] };

// Add Sentinel-2 imagery to the map
Map.addLayer(image, vis, "Sentinel2");

// Get information about the Sentinel-2 imagery
print(image, "Sentinel raw image");

// Take the mean of the Sentinel-2 imagery
var image = image.mean();

// Load additional Sentinel-2 imagery for a different date range
var s2BandNames = ['B2', 'B3', 'B4', 'B7', 'B8'];
var s2BandRename = ['blue', 'green', 'red', 'red_edge', 'nir'];
var collections2 = ee.ImageCollection('COPERNICUS/S2_SR')
              .filterDate('2022-05-19', '2022-05-22')
              .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE',05))
              .select(s2BandNames, s2BandRename)
              .filterBounds(roi)
              .map(function(image){return image.clip(roi)});

print(image, "Sentinel raw image");
var image = collections2.mean();
```

After processing the imagery, we move on to calculate the Normalized Difference Vegetation Index (NDVI) from the Sentinel-2 data. NDVI is a key metric for assessing vegetation health and density. We'll use the Near Infrared (NIR) and Red bands to compute NDVI. Then, we'll create a composite image that includes all the Sentinel-2 bands along with the calculated NDVI.

To display these images, we add them as layers on the map. This allows us to visually inspect both the Sentinel-2 composite and the NDVI layer simultaneously, aiding in our analysis.

Now, let's center the map on our region of interest with a zoom level of 13. This gives us a closer look at the area we're studying, making it easier to interpret the results.

```javascript
//---------------------------------- Calculate NDVI ------------------------------
var s2ndvi = image.normalizedDifference(['nir', 'red']); 
var comp = collections2.mean();
var ndvi = comp.normalizedDifference(['nir', 'red']).rename('NDVI');
var composite = ee.Image.cat(comp, ndvi);

Map.centerObject(roi, 13);
```

**Create FeatureCollection representing different land cover types**

Now, let's delve into SAR Classification. We'll start by merging various feature collections representing different land cover types into one cohesive collection. This merged collection, named "newfc," will serve as our reference for training the classifier.

Next, we'll define the SAR (Synthetic Aperture Radar) bands to train the data. By combining the filtered SAR images (SARVV\_filtered and SARVH\_filtered) into one image called "final," we create a comprehensive dataset for classification. The selected bands for training are 'VH' and 'VV'.

To train our Random Forest classifier, we'll sample regions from the merged feature collection and assign random columns. These sampled regions are then split into training and validation datasets.

With the training data prepared, we proceeded to train the Random Forest classifier using the training dataset. This classifier is then applied to the SAR data to perform the classification. We'll visualize the classified SAR image on the map, showing different land cover types with distinct colors.

Additionally, we'll classify the validation data to evaluate the **accuracy of our classification process.**

```javascript
//----------------------------- SAR Classification ------------------------------
var newfc = wheat.merge(barley).merge(Uncultivate_land).merge(Road_airport).merge(bareland).merge(grassland);
var final = ee.Image.cat(SARVV_filtered, SARVH_filtered);
var bands = ['VH', 'VV'];
var training_sar = final.select(bands).sampleRegions({ collection: newfc, properties: ['landcover'], scale: 10 }).randomColumn();
var training_newfc1 = training_sar.filter(ee.Filter.lt('random', 0.7));
var validation_newfc1 = training_sar.filter(ee.Filter.gte('random', 0.7));
var classifier_sar = ee.Classifier.smileRandomForest(60).train({ features: training_newfc1, classProperty: 'landcover', inputProperties: bands });
var classified_sar = final.select(bands).classify(classifier_sar);
print(classified_sar, 'classified SAR');
Map.addLayer(classified_sar, { min: 0, max: 5, palette: ['1667fa', 'c9270d', 'cf7b68', 'ee9a1c', '146d0e', '04bd23', '37fe05'] }, 'SAR Classification');
var validated_sar = validation_newfc1.classify(classifier_sar);
```

### **Sentinel-2A Classification**

Now, let's move on to Sentinel-2A Classification. We'll start by defining the bands to be used for classification. In addition to the spectral bands (blue, green, red, red\_edge, and nir), we'll also include NDVI as a feature. This comprehensive set of features will help us effectively classify land cover types.

Next, we'll sample regions from the composite image based on the defined bands and land cover properties. These sampled regions will then be split into training and validation datasets to facilitate the classifier training process.

We'll train the Random Forest classifier using the training dataset, specifying the input features and the class property. Once trained, the classifier will be applied to the composite image to perform the classification.

To visualize the results, we'll add the classified Sentinel-2 image to the map, assigning distinct colors to different land cover types.

Additionally, we'll classify the validation data and print

the confusion matrix and accuracy metrics. This step helps us evaluate the performance of our classifier on unseen data.

```javascript

//-------------------------------- Sentinel-2A Classification -------------------------------
var bandss2 = ['blue', 'green', 'red', 'red_edge', 'nir'];
var trainings2 = composite.select(bandss2).sampleRegions({ collection: newfc, properties: ['landcover'], scale: 10 }).randomColumn();
var training_newfc2 = trainings2.filter(ee.Filter.lt('random', 0.7));
var validation_newfc2 = trainings2.filter(ee.Filter.gte('random', 0.7));
var classifier_S2 = ee.Classifier.smileRandomForest(100).train({ features: training_newfc2, classProperty: 'landcover', inputProperties: bandss2 });
var classified_S2 = composite.select(bandss2).classify(classifier_S2);
Map.addLayer(classified_S2, { min: 0, max: 5, palette: ['1667fa', 'c9270d', 'cf7b68', 'ee9a1c', '146d0e', '04bd23', '37fe05'] }, 'Optical Classification');
var validated_s2 = validation_newfc2.classify(classifier_S2);
print('RF S2 error matrix training: ', classifier_S2.confusionMatrix());
print('RF- S2 accuracy training: ', classifier_S2.confusionMatrix().accuracy());
var testAccuracy = validated_s2.errorMatrix('landcover', 'classification');
print('RF S2 Validation error matrix: ', testAccuracy);
print('RF S2 Validation overall accuracy: ', testAccuracy.accuracy());
```

### **Combine SAR and Sentinel-2 Classification**

Let's now **combine SAR and Sentinel-2 Classification**. To achieve this, we'll define both SAR and optical bands to train the classifier. This includes bands from the optical imagery (blue, green, red, red\_edge, nir, and NDVI) as well as SAR bands (VH and VV).

We'll sample regions from the merged feature collection using the defined bands and split them into training and validation datasets.

Once the training dataset is prepared, we'll train the Random Forest classifier using the training dataset, specifying the input features and the class property.

After training, the classifier will be applied to the combined optical and SAR image to perform the classification.

We'll visualize the combined classification on the map, masking out areas where either SAR or optical data is missing.

Finally, we'll classify the validation data and print the confusion matrix and accuracy metrics for both the training and validation datasets. This comprehensive evaluation will provide insights into the performance of our combined classification approach.

```javascript
//----------------------------- Combine SAR and Sentinel 2 Classification ---------------------
var opt_sar = ee.Image.cat(composite, SARVV_filtered, SARVH_filtered);
var bands_opt_sar = ['VH', 'VV', 'blue', 'green', 'red', 'red_edge', 'nir', 'NDVI'];
var training_opt_sar = opt_sar.select(bands_opt_sar).sampleRegions({ collection: newfc, properties: ['landcover'], scale: 10 }).randomColumn();
var training_newfc3 = training_opt_sar.filter(ee.Filter.lt('random', 0.7));
var validation_newfc3 = training_opt_sar.filter(ee.Filter.gte('random', 0.7));
var classifier_opt_sar = ee.Classifier.smileRandomForest(100).train({ features: training_newfc3, classProperty: 'landcover', inputProperties: bands_opt_sar });
var classifiedboth = opt_sar.select(bands_opt_sar).classify(classifier_opt_sar);
var mask_o = composite.select(0).neq(1000);
var mask_r = SARVV_filtered.neq(1000);
var mask = mask_r.updateMask(mask_o);
Map.addLayer(classifiedboth.updateMask(mask), { min: 0, max: 5, palette: ['1667fa', 'c9270d', 'cf7b68', 'ee9a1c', '146d0e', '04bd23', '37fe05'] }, 'Optical/SAR Classification');
var validated_opt_sar = validation_newfc3.classify(classifier_opt_sar);
var confusionMatrix = classifier_opt_sar.confusionMatrix();
print('RF-Opt/SAR error matrix training: ', classifier_opt_sar.confusionMatrix());
print('RF-Opt/SAR accuracy training: ', classifier_opt_sar.confusionMatrix().accuracy());
print('RF-Opt/SAR Kappa training: ', confusionMatrix.kappa());
print('RF Training Consumer\'s accuracy (rows):', confusionMatrix.consumersAccuracy());
print('RF Training Producer\'s accuracy (columns):', confusionMatrix.producersAccuracy());
print('RF Training array :', confusionMatrix.array());
var testAccuracy = validated_opt_sar.errorMatrix('landcover', 'classification');
print('RF-Opt/SAR Validation error matrix: ', testAccuracy);
print('RF-Opt/SAR Validation overall accuracy: ', testAccuracy.accuracy());
print('RF-Opt/SAR Kappa Validation: ', testAccuracy.kappa());
print('RF Validation Consumer\'s accuracy (rows):', testAccuracy.consumersAccuracy());
print('RF Validation Producer\'s accuracy (columns):', testAccuracy.producersAccuracy());
print('RF Validation array :', testAccuracy.array());
```

### **Export the results to Google Drive**

To complete our analysis, let's **export the results to Google Drive**. We'll start by exporting the classified Sentinel-2 image as a GeoTIFF file.

This export operation includes several parameters such as the image to export, a description for the exported file, the spatial resolution (scale) in meters, the region of interest (roi), the folder in Google Drive to save the exported file, and the maximum number of pixels to export.

Once the export is initiated, Google Earth Engine will process the image and save it to the specified folder in your Google Drive account.

```javascript
//----------------------------------- Export Results ----------------------------------------
// Export the classified Sentinel-2 image to Google Drive
Export.image.toDrive({
    image: classified_S2, // Classified Sentinel-2 image
    description: 'S2_RF_10m', // Description
    scale: 10, // Spatial resolution
    region: roi, // Region of interest
    folder: "M.Gaylan_Classification", // Google Drive folder
    maxPixels: 1e13 // Maximum number of pixels
});
```

### The complete code is as follows:

```javascript
//The code is prepared by Dr. Azad Rasul: azad.rasul@soran.edu.iq
//---------------------------------------------------------------------------
// roi
var roi = ee.Geometry.Polygon(
  [[[44.253, 36.569],
    [44.293, 36.596],
    [44.367, 36.526],
    [44.328, 36.5]]], null, false);
//----------------------------------- SAR -----------------------------------
// Load Sentinel-1 C-band SAR Ground Range collection (log scale, VV, descending)
var collectionVV = ee.ImageCollection('COPERNICUS/S1_GRD')
  .filter(ee.Filter.eq('instrumentMode', 'IW'))
  .filter(ee.Filter.listContains('transmitterReceiverPolarisation', 'VV'))
  .filter(ee.Filter.eq('orbitProperties_pass', 'DESCENDING'))
  .filterMetadata('resolution_meters', 'equals' , 10)
  .filterBounds(roi)
  .map(function(image){return image.clip(roi)})
  .select('VV');
print(collectionVV, 'Collection VV');

// Load Sentinel-1 C-band SAR Ground Range collection (log scale, VH, descending)
var collectionVH = ee.ImageCollection('COPERNICUS/S1_GRD')
  .filter(ee.Filter.eq('instrumentMode', 'IW'))
  .filter(ee.Filter.listContains('transmitterReceiverPolarisation', 'VH'))
  .filter(ee.Filter.eq('orbitProperties_pass', 'DESCENDING'))
  .filterMetadata('resolution_meters', 'equals' , 10)
  .filterBounds(roi)
  .map(function(image){return image.clip(roi)})
  .select('VH');
print(collectionVH, 'Collection VH');

// Filter SAR collections by date
var SARVV = collectionVV.filterDate('2022-04-19', '2022-04-24').mosaic();
var SARVH = collectionVH.filterDate('2022-04-19', '2022-04-24').mosaic();

// Add the SAR images to the map for visualization
Map.centerObject(roi, 12);
Map.addLayer(SARVV, {min:-15,max:0}, 'SAR VV', 0);
Map.addLayer(SARVH, {min:-25,max:0}, 'SAR VH', 0);

// Apply filter to reduce speckle
var SMOOTHING_RADIUS = 50;
var SARVV_filtered = SARVV.focal_mean(SMOOTHING_RADIUS, 'circle', 'meters');
var SARVH_filtered = SARVH.focal_mean(SMOOTHING_RADIUS, 'circle', 'meters');

// Display the filtered SAR images
Map.addLayer(SARVV_filtered, {min:-15,max:0}, 'SAR VV Filtered',0);
Map.addLayer(SARVH_filtered, {min:-25,max:0}, 'SAR VH Filtered',0);

//--------------------------- Sentinel 2 -------------------------
// Function to mask clouds and cirrus in Sentinel-2 imagery
function maskS2clouds(image) {
  var qa = image.select('QA60');
  var cloudBitMask = 1 << 10;
  var cirrusBitMask = 1 << 11;
  var mask = qa.bitwiseAnd(cloudBitMask).eq(0)
      .and(qa.bitwiseAnd(cirrusBitMask).eq(0));
  return image.updateMask(mask).divide(10000);
}

// Load Sentinel-2 imagery, filter by date and cloud cover, apply cloud masking, and clip to the ROI
var image = ee.ImageCollection('COPERNICUS/S2_SR')
              .filterDate('2022-05-19', '2022-05-22')
              .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE',5))
              .filterBounds(roi)
              .map(maskS2clouds)
              .map(function(image){return image.clip(roi)});

// Visualization parameters for displaying Sentinel-2 imagery
var vis = { min: 0.0, max: 0.3, bands: ['B4', 'B3', 'B2'] };

// Add Sentinel-2 imagery to the map
Map.addLayer(image, vis, "Sentinel2");

// Get information about the Sentinel-2 imagery
print(image, "Sentinel raw image");

// Take the mean of the Sentinel-2 imagery
var image = image.mean();

// Load additional Sentinel-2 imagery for a different date range
var s2BandNames = ['B2', 'B3', 'B4', 'B7', 'B8'];
var s2BandRename = ['blue', 'green', 'red', 'red_edge', 'nir'];
var collections2 = ee.ImageCollection('COPERNICUS/S2_SR')
              .filterDate('2022-05-19', '2022-05-22')
              .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE',05))
              .select(s2BandNames, s2BandRename)
              .filterBounds(roi)
              .map(function(image){return image.clip(roi)});

print(image, "Sentinel raw image");
var image = collections2.mean();

//---------------------------------- Calculate NDVI ------------------------------
var s2ndvi = image.normalizedDifference(['nir', 'red']); 
var comp = collections2.mean();
var ndvi = comp.normalizedDifference(['nir', 'red']).rename('NDVI');
var composite = ee.Image.cat(comp, ndvi);

Map.centerObject(roi, 13);

//----------------------------- SAR Classification ------------------------------
var newfc = wheat.merge(barley).merge(Uncultivate_land).merge(Road_airport).merge(bareland).merge(grassland);
var final = ee.Image.cat(SARVV_filtered, SARVH_filtered);
var bands = ['VH', 'VV'];
var training_sar = final.select(bands).sampleRegions({ collection: newfc, properties: ['landcover'], scale: 10 }).randomColumn();
var training_newfc1 = training_sar.filter(ee.Filter.lt('random', 0.7));
var validation_newfc1 = training_sar.filter(ee.Filter.gte('random', 0.7));
var classifier_sar = ee.Classifier.smileRandomForest(60).train({ features: training_newfc1, classProperty: 'landcover', inputProperties: bands });
var classified_sar = final.select(bands).classify(classifier_sar);
print(classified_sar, 'classified SAR');
Map.addLayer(classified_sar, { min: 0, max: 5, palette: ['1667fa', 'c9270d', 'cf7b68', 'ee9a1c', '146d0e', '04bd23', '37fe05'] }, 'SAR Classification');
var validated_sar = validation_newfc1.classify(classifier_sar);

//-------------------------------- Sentinel-2A Classification -------------------------------
var bandss2 = ['blue', 'green', 'red', 'red_edge', 'nir'];
var trainings2 = composite.select(bandss2).sampleRegions({ collection: newfc, properties: ['landcover'], scale: 10 }).randomColumn();
var training_newfc2 = trainings2.filter(ee.Filter.lt('random', 0.7));
var validation_newfc2 = trainings2.filter(ee.Filter.gte('random', 0.7));
var classifier_S2 = ee.Classifier.smileRandomForest(100).train({ features: training_newfc2, classProperty: 'landcover', inputProperties: bandss2 });
var classified_S2 = composite.select(bandss2).classify(classifier_S2);
Map.addLayer(classified_S2, { min: 0, max: 5, palette: ['1667fa', 'c9270d', 'cf7b68', 'ee9a1c', '146d0e', '04bd23', '37fe05'] }, 'Optical Classification');
var validated_s2 = validation_newfc2.classify(classifier_S2);
print('RF S2 error matrix training: ', classifier_S2.confusionMatrix());
print('RF- S2 accuracy training: ', classifier_S2.confusionMatrix().accuracy());
var testAccuracy = validated_s2.errorMatrix('landcover', 'classification');
print('RF S2 Validation error matrix: ', testAccuracy);
print('RF S2 Validation overall accuracy: ', testAccuracy.accuracy());

//----------------------------- Combine SAR and Sentinel 2 Classification ---------------------
var opt_sar = ee.Image.cat(composite, SARVV_filtered, SARVH_filtered);
var bands_opt_sar = ['VH', 'VV', 'blue', 'green', 'red', 'red_edge', 'nir', 'NDVI'];
var training_opt_sar = opt_sar.select(bands_opt_sar).sampleRegions({ collection: newfc, properties: ['landcover'], scale: 10 }).randomColumn();
var training_newfc3 = training_opt_sar.filter(ee.Filter.lt('random', 0.7));
var validation_newfc3 = training_opt_sar.filter(ee.Filter.gte('random', 0.7));
var classifier_opt_sar = ee.Classifier.smileRandomForest(100).train({ features: training_newfc3, classProperty: 'landcover', inputProperties: bands_opt_sar });
var classifiedboth = opt_sar.select(bands_opt_sar).classify(classifier_opt_sar);
var mask_o = composite.select(0).neq(1000);
var mask_r = SARVV_filtered.neq(1000);
var mask = mask_r.updateMask(mask_o);
Map.addLayer(classifiedboth.updateMask(mask), { min: 0, max: 5, palette: ['1667fa', 'c9270d', 'cf7b68', 'ee9a1c', '146d0e', '04bd23', '37fe05'] }, 'Optical/SAR Classification');
var validated_opt_sar = validation_newfc3.classify(classifier_opt_sar);
var confusionMatrix = classifier_opt_sar.confusionMatrix();
print('RF-Opt/SAR error matrix training: ', classifier_opt_sar.confusionMatrix());
print('RF-Opt/SAR accuracy training: ', classifier_opt_sar.confusionMatrix().accuracy());
print('RF-Opt/SAR Kappa training: ', confusionMatrix.kappa());
print('RF Training Consumer\'s accuracy (rows):', confusionMatrix.consumersAccuracy());
print('RF Training Producer\'s accuracy (columns):', confusionMatrix.producersAccuracy());
print('RF Training array :', confusionMatrix.array());
var testAccuracy = validated_opt_sar.errorMatrix('landcover', 'classification');
print('RF-Opt/SAR Validation error matrix: ', testAccuracy);
print('RF-Opt/SAR Validation overall accuracy: ', testAccuracy.accuracy());
print('RF-Opt/SAR Kappa Validation: ', testAccuracy.kappa());
print('RF Validation Consumer\'s accuracy (rows):', testAccuracy.consumersAccuracy());
print('RF Validation Producer\'s accuracy (columns):', testAccuracy.producersAccuracy());
print('RF Validation array :', testAccuracy.array());

//----------------------------------- Export Results ----------------------------------------
// Export the classified Sentinel-2 image to Google Drive
Export.image.toDrive({
    image: classified_S2, // Classified Sentinel-2 image
    description: 'S2_RF_10m', // Description
    scale: 10, // Spatial resolution
    region: roi, // Region of interest
    folder: "M.Gaylan_Classification", // Google Drive folder
    maxPixels: 1e13 // Maximum number of pixels
});
```

I hope you found this tutorial helpful! If you did, don't forget to like and subscribe for more content. Until next time, happy coding!

Please consider subscribing to my [**YouTube channel**](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enrol in my [**Udemy course**](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).