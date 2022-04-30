# URBAN_MONITORING_SYSTEM

## Acknowledgements

 - Wu, Q., (2020). geemap: A Python package for interactive mapping with Google Earth Engine. The Journal of Open Source Software, 5(51), 2305. https://doi.org/10.21105/joss.02305
 - Wu, Q., Lane, C. R., Li, X., Zhao, K., Zhou, Y., Clinton, N., DeVries, B., Golden, H. E., & Lang, M. W. (2019). Integrating LiDAR data and multi-temporal aerial imagery to map wetland inundation dynamics using Google Earth Engine. Remote Sensing of Environment, 228, 1-13. https://doi.org/10.1016/j.rse.2019.04.015 (pdf | source code)
 - https://github.com/divamgupta/image-segmentation-keras
 
 
## Problem Statement
In India, the government and other independent private companies depend upon survey teams and remote sensing methods to produce ground reports on several domains. The reports must be assessed by a team who must be physically present on-ground or on-site to perform the required analysis. This induces expense and bias in the production of these ground reports. Our research aims to produce on-demand or monthly or yearly ground reports using Deep Learning analysis on satellite imagery. We propose to automate the entire process by building a model through which new images can be passed and the required inferences can be obtained. The stakeholders involved would highly benefit from the algorithm as it would lead to better response retrieval for the image passed and would rid us of bias. We imply many advanced convolution neural networks (CNNs) which are used for Deep Learning to analyze these geospatial and satellite images.

## Phases Of The Project
Our Project is divided into 3 Phase \
Here are the links \
- Data Aquistion --Prototype Done ,improvements still in process\
- Data Preparation  --Prototype Done ,improvements still in process\
- Deep Learning ---Still in process\
- Report Generator -- Next Phase \

THIS IS STEP-1 MY OUR URBAN MONITORING SYSTEM
# DATA-ACQUISITION
A custom build python based web Scraper which helps in building datasets from Google Earth Engine
## Abstract <br />
Google Earth Engine Explorer (EE Explorer) is a lightweight geospatial image data viewer with access to a large set of global and regional datasets available in the Google Earth Engine Data Catalog. It allows for quick viewing of data with the ability to zoom and pan anywhere on Earth, adjust visualization settings, and layer data to inspect change over time.

Google Earth Engine public data archive includes more than forty years of historical imagery and scientific datasets, updated and expanded daily.It includes the most popular series of Raster series like Sentinel, Landsat, Modis. Google provies its own cloud platform to visualize and do computation on spatial data.Google provides several machine learning algorithms for use. Google Earth Engine platform is not very compatible with deep learning pipelines.

These huge data can be leveraged in building deep learnning models which handles use cases like semantic segmentation and object detection.I developed a tool which can fetch images and corresponding labeled images from Google Earth Engine and arrange it in way it is compatible with deep learning pipelines.



## Library used <br /> 
- **json**
- **geemap**
- **ee**
- **geopandas**
- **os** 
- **glob**
- **gdal** 
- **pandas** 
- **numpy** 
- **math**
- **shapely** 
- **folium**

## Methodology
Terms:
- Date-span--> - User is interested in between this date range
- Region span--> - User is interested in images bounded within this region only
- Cloud Cover percentage--> Given multiple images of same place and time use the image with least cloud cover percentage
- Shape file--> Geometrical file used to filter region of interest

We first use **GEEMAP** to aquire the required image. This image is subject to many filteration like **Date-span**,**Region span**,**Cloud Cover percentage** etc.Then we create a shape file which is rectangular in shape. The coordinates of this shape files covers a small area of interest of the image.We download the image covered by this shape file. Then we up date the coordinates of the shape file to download the next image. We do this continously to build a dateset out Google Earth Engne data catalogue.

The image downloaded from GEEMAP is in .tif format. Keras Segmentation models take input as **png** format. So images undergo required scaling and conversions. Then the images are downloaded in our local machine.\

The following images are acquired from Sentinel dataset and World Settlement Footprint 2015 dataset \

Examples


![SENTINEL](https://user-images.githubusercontent.com/52020282/164910907-3ae48741-3179-46dd-845d-f0e060063a17.png) ![URBAN_MASK-2](https://user-images.githubusercontent.com/52020282/164910913-0352a772-2e95-4f8b-b2ba-9b6b1ba7ebc8.png)

![Unknown-3](https://user-images.githubusercontent.com/52020282/164911229-ac1b05d4-6b0e-4a53-abac-375e24dae720.png)![Unknown-4](https://user-images.githubusercontent.com/52020282/164911237-3a93e974-64e4-4249-bc31-f82d2b03f0db.png)


## Data-Preparation

As mentioned above we will be using keras segmentation models for semantic segmentation.
Keras-segmentation has several prebuilt architecture which can be used for our project.
We need to train these pre-built architecture on our datasets (Acquired during data acquisition)

Before we can utilize these pre-built architectiure the data-set is undergoes required 
preprocessing.


The dataset created has two folders - Sentinel and masks. 

![Review2 (5)](https://user-images.githubusercontent.com/52020282/166094535-0b9eaea6-8164-415d-8673-099f40007d54.png)


**1** First we do conversion of our masked images from pixel values to labelled values.
Our  masked images ranges from 0-255 pixel value, where **0** stands for non_urbanization **255** stand for urbanization.
We convert these pixels values into labels. 

**2** Then we crop our each imaage and corresponding masked images into multiple images
which is compatible with our keras-segmentation models.  

**3** Then we do pixel wise label wise summation .Here we decide whether to consider an image and its corresponding mask or not.
If in the mask we have representation of urbanization label (**1** ) below a threshold (say 30 %) we disregard that image
and corresponding label. 

**4** During filteration we loose images so we augument the remaining images increase the filterd data (*4times) 

**5** Lastly we split the dataset into train test and split 

## Deep-Learning
Still on going we have used several modesl from Keras-segmarntation library
and are working to increase the accuracy of the models


 





