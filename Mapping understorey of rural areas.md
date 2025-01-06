# Mapping Understorey of Rural Areas in Australian Capital Territory

In this project, grass cover in rural areas of the ACT, Australia was categorised into native/exotic and C3/C4 for efficient management.


## Abstract

Grasslands are an important global terrestrial biome as they provide a range of ecosystem services, including a refugia for thretened plants,, birds, mammals and reptiles. In Australia, grasslands are also a source of feed for livestock. The grasslands are managed to minimise weed invasion, fire attacks, soil erosion and displacement owing to agricultural expansion.


## Introduction

Grasslands are globally ubiquitous, except Antarctica, making it one of the dominant biomes covering approximately 45% of the Earth's terrestrial ecosystems. While glasslands provide habitats for plants, mammals, birds, and reptiles, it contributes approximately 20% of the global soil carbon stocks. Tropical and subtropical grasslands are found mainly in Africa and Australia. In Australia, grasslands provide a range of ecosystem services, including fodder for livestock, refugia for threatened plant and animal species, and protection of soil. 
The overarching aim of the project is to map the understorey vegetation communities of rural areas in the Australian Capital Territory. To this end, the specific objectives include: <br>

- differentiating between exotic, native and native high diversity grass <br>

 - differentiating between dominant native grass species, including kangaroo grass, spear grass and Phalaris <br>

- evaluating the performance of machine learning models explored


## Materials and Methods


### Study area



The study area is described by the figure below. 





![image](https://github.com/user-attachments/assets/49059f02-64c1-4fbf-b80c-a706067dc977)








### Field data


The figure below is an overview of the methodology.





![image](https://github.com/user-attachments/assets/7bdb329b-5694-4768-87bd-c44d8e40fe3b)





The ground reference data was collected from 2018 until the end of 2023, in which visual discrimination of grasses were conducted by experts from the ACT government. The field sampling plots were randomly selected with each plot size equivalent to 400m^2 (i.e., 20m by 20m) to match the nominal ground sampling distance of the Sentinel-2 satellite. The geographic coorodinates of a plot were collected using a handheld GPS with a horizontal accuracy of approximately 5m. In each plot, the observer recorded the botanical composition including a fraction of vegetation cover and bare soil. Further, the grasses were separated into perennial/annual, C3/C4 with the level of plant diversity recorded. Post-field processing of the data was done to clean it up, removing bad rows and columns of data. This data was used to build, train and validate machine learning models.





### Sentinel-2 satellite imagery

Sentinel-2 is one of the Earth observation satellite missions operated through the Copernicus Program under the European Space Agency (ESA). The Sentinel-2, launched in 2015, on-board satellites that carry sensors collecting optical imagery of differing native resolutions at a planetary scale. The table below describes the spectral bands of Sentinel-2, including the key use and spatial resolution.


|Band (description)|Key use|Resolution (m)|
|:----|:----|:---|
|B1 (coastal aerosol) |aerosols correction|60|
|B2 (Blue) |land monitoring|10|
|B3 (Green) |land monitoring|10|
|B4 (Red) |land monitoring|10|
|B5 (Red-edge 1) |land monitoring|20|
|B6 (Red-edge 2) |land monitoring|20|
|B7 (Red-edge 3) |land monitoring|20|
|B8 (Near infrared) |land monitoring|10|
|B8A (Red-edge 4) |land monitoring|20|
|B9 (Water vapour |water vapour correction|60|
|B10 (Cirrus) |cirrus detection|60|
|B11 (Shortwave infrared 1) |land monitoring|20|
|B12 (Shortwave infrared 2) |land monitoring|20|


In this project, the Sentinel-2 spectral bands, including B2, B3, B4, B5, B6, B7, B8, B8A, B11, B12, were used as they provide high resolution imagery and suited for vegetation monitoring. To ensure that the electromagnetic energy recorded by the sensor were those reflected off the targets of interest, the top of atmosphere Sentinel-2 images retrieved from the Copernicus Open Access Hub via Google Earth Engine were preprocessed to minimise the influence of atmospheric conditions, and sun-sensor viewing geometry. The Sentinel-2 TOA imagery over the study areas acquired from 2018 to 2013 was used as this date aligns with the field observation data. Sensor insentive radiative transfer model leveraging MODIS product was used for the atmospheric correction [(Yin et al., 2022)](https://doi.org/10.5194/gmd-15-7933-2022). The imagery was also corrected for bidirection reflectance to produce analysis ready data referred to as NBAR from here on. A global digital elevation model (DEM) made available through the NASA Shuttle Radar Topography Mission (SRTM) obtained via Google Earth Engine was used to minimise biases due to the relief of the plots. Image pixels affected by cloud and cloud shadow were eliminated using the quality assesssment bands. The project adapted the pre-analysis techniques for obtaining analysis ready NBART products by [Berra et al. (2024)](https://doi.org/10.3390/rs16152695). Since the Sentinel-2 satellites acquire data at varied native spatial resolutions, the imagery obtained at spectral bands with 10m resolution were spatially upscaled to 20m using the nearest neighbourhood geometric resampling method to preserve the original reflecance values and harmonise the data. The DEM was used to compute elevation, slope, and aspect to radiometrically normalise reflectance. 




#### Spectral indices

The NBART was analysed to derive spectral indices that measure the biophysical and chemical conditions of the grasses. Spectral indices are obtained from the bands applying different arithmetric operations; despite there are many spectral indices only those that require the nominal resolution (20m) bands and relevant to the project were utilised. The spectrall indices, include the normalised vegetation index (NDVI), soil-adjusted vegetation index (SAVI), enhanced vegetation index (EVI). The others were green chlorophyll vegetation index (GCVI), plant senescence reflectance index (PSRI), and bare soil index (BSI). The table below details the spectral indices used. 


|Index|Formula|Reference| 
|:----|:----|:---|
|NDVI|(NIR-Red)÷(NIR+Red)|[Rouse et al., 1973](https://ntrs.nasa.gov/citations/19740022614)|
|SAVI|((NIR-Red)÷(NIR+Red+0.5))× 1.5|[Huete, 1998](https://doi.org/10.1016/0034-4257(88)90106-X)|
|EVI |((NIR-Red)÷(NIR+6×Red-7.5×Blue+1))× 2.5|[Huete et al., 2002](https://doi.org/10.1016/S0034-4257(02)00096-2)|
|GCVI|(NIR-Green)-1|[Gitelson et al., 2003](https://doi.org/10.1078/0176-1617-00887)|
|PSRI  |((Red-Blue)÷Red)×Red-edge 2)|[Merzlyak et al.,1999](http://dx.doi.org/10.1034/j.1399-3054.1999.106119.x)|
|BSI |[(SWIR2+Red)-(NIR+Blue)]÷[(SWIR2+Red)+(NIR+Blue)]|[Bera et al., 2020](https://doi.org/10.1007/s42489-020-00060-1)|
|B7 (red-edge) |land monitoring|20|
|B7 (red-edge) |land monitoring|20|




#### Textural and segmentataion 

Naturally, spatial relationships exist between the grass types and this should be accounted for. In image analysis, this relationship can be described through a textural analysis of the brightness values recorded by the electromagnetic detector. In this project, the grey level co-occurrence metrics (GLCM) by [Haralick et al., 1973](https://doi.org/10.1109/TSMC.1973.4309314) were explored as the method is widely used in similar studies (REFERENCES). The GLCM, a second order statistical analysis of an image, is employed by identifying a pixel in a pre-determined moving window of pixels and comparing the relationships between the focal pixel and neighbouring pixels in a specific direction and distance. Through descriptive statistical methods, many textural metrics can be computed. In the GEE, eighteen GLCM metrics sourced from the works of [Haralick et al., 1973](https://doi.org/10.1109/TSMC.1973.4309314) and [Conners et al., 1984](https://sdoi.org/10.1016/0734-189X(84)90197-X) can be computed. However, the relevance of the metrics is study-specific and for this reason only five of the metrics were explored in this study. These were sum average (AVG), variance (VAR), contrast (CON), inverse difference moment (IDM) and entropy (ENT). The formulae for the metrics are from [Hall-Beyer, 2017)](https://doi.org/10.1080/01431161.2016.1278314).




|Metric|Formula|Description|
|:----|:----|:---|
|CON|$$\sum_{i,j=0}^{N-1}  P_{i,j} \left( {i-j} \right)^2 $$|Measure local contrast|
|IDM|$$\sum_{i,j=0}^{N-1}  {P_{i,j}\over 1+ \left( {i-j} \right)^2} $$|Measure homogeneity|
|ENT |$$\sum_{i,j=0}^{N-1} P_{i,j} \left( {-lnP_{i,j}} \right)$$|Measure randomness in grey-levels|
|AVG|$$\sum_{i,j=0}^{N-1}  i\left(P_{i,j}\right)$$|Measure mean grey-levels|
|VAR  |$$\sum_{i,j=0}^{N-1}  P_{i,j} \left( {i-μ_i} \right)^2 $$|Measure the spread of grey-levels|



To compute the GLCM metrics in GEE, a 8-bit grey-scale imagery is required. Although many approaches for selecting a single-band imagery for the GLCM textural analysis exist, including using an NDVI layer, a recent method by [Tassi et al., 2022](https://doi.org/10.3390/rs12223776) leveraging the NIR, Red, and Blue bands was used. A linear combination of the bands was used as: <br>




**$\(0.30×NIR)+(0.59×Red)+(0.11×Green)$** 




Image segmentation is another method to explore the capability of the Sentinel-2 to differentiate between the grasses as pixels with similar spatial and spectral attributes, such as colour, luminance and texture, are clustered together to form homogeneous superpixels referred to as spectral objects or clusters. Image segmentation methods perform object-based analysis of the pixels and can remove redundant data. The Simple Non-Iterative Clustering (SNIC) algorithm by [Achanta and Susstrunk, 2017](https://doi.org/10.1109/CVPR.2017.520) was used to segment the Sentinel-2 pixels into spectral clusters. The SNIC algorithm requires input variables such as compactness factor for spatial distance weighting and connectivity and neighbourhood size for efficient grouping of the pixels. The SNIC input parameters used by [Tassi and Vizzari, 2020] (https://doi.org/10.3390/rs12223776) for a land cover classification study in Europe were replicated in this study. The SNIC clusters were used a predictor variable.



### Sentinel-1

Sentinel-1 is another Earth observation satellite mission operated by the ESA with the aim of monitoring the environment from space regardless of atmospheric and weather conditions. The Sentinel-1 carries a sensor that transmits and records microwave energy that bounced off environmental targets, including grasslands. Because the Sentinel-1 uses artificial microwave energy it is capable of  penetrating through cloud cover and taking photos of the Earth at any time. Thus, the Sentinel-1 complements the Sentinel-2 for continuous mapping of the environment, while providing spectral information that characterises the variations in structural and moisture conditions of the vegetation. The Sentinel-1 sensor can be operated in four different modes, but the imagery obtained from the interferometric wide swath mode (IW) are recommended and available for land monitoring. This study used imagery from the IW mode that were already pre-processed to a ground range detected product (near analysis ready) by the ESA and were retrievable from the GEE data catalog. The Sentinel-1 is a synthetic aperture radar system, measuring the amplitude and phase of the microwave energy in multiple polarisations. The Sentinel-1 typically transmits the microwave energy in vertical orientation and records the retun signal in either vertical or horizontal orientation making the Sentinel-1 a dual-polarisation system in that the data comprises VV and VH polarisation bands. Given the physical structure of vegetation canopy is more sensitive to the VH polarisation only this band was used in this study; the inherent speckle noise was not filtered out as this lowers the spectral and spatial variability required to differentiate pixels. Temporal changes in the vegetation due to degradation and regrowth is not same for the different species, and since the Sentinel-1 data has no missing data points this was used to track the phenological growth behaviour of the species. A Fourier harmonics function was applied to the Sentinel-1 time series data to compute amplitude and phase bands. The bands were adjusted to spatially align with the regions of interest and the Sentinel-2 data and pixels that were not grassland were masked using the method discussed earlier.


#### Phenological variables

The biophysical conditions of plant species, including annual and perennial grasses, change through the growth calendar. While perennial grasses maybe green throughout the year, annual grasses may disappeear during the dry or low or rainfall seasons. The growth phenology of the plants can be an importantt information to differentiate between the grass types. Thus, a collection of time series NDVI imagery was used to extract phenological variabales, including start of season and end of season, to differentiate between the plants. Missing data points in the series due to cloud cover and cloud shadow were replaced with a synthetic data using an interpolation algorithm. The original distribution of the data was smoothed to ascertain dates characterising start of growth and end of growth for the plants. The Harmonic ANalysis of Time Series (HANTS) algorithm with the GEE was used to retrieve the pphenological variables. 




### Topographic variables

The NASA SRTM was used to compute elevation, slope, and aspect, and were used to discriminate the plant types. 


### Selecting optimal variables 

Separability index involving all the predictor variables was computed to remove redundant variables.


### Random forest classification

Random Forest (RF) is a decision tree ensemble machine learning algorithm widely used for land cover monitoring as it is not limited by data structure and minimises overfitting the data. Additionally, the RF is computationally less expensive to implement as only few hyperparameters require tuning.  The RF operates by randomly selecting a proportion of the instances to train a decision tree, wile replacing the samples to be re-used in the next iteration. This sampling a subset of instances with replacement to create decision trees is referred to as boostrap aggregating (i.e., bagging). The RF creates multiple decision trees to avoid overfitting; the final descision tree is obtained through majority voting. The RF classification algorithm in GEE was used, requiring the tuning for hyperparameters such as the number of trees to grow, number of the predictor variables to use and the proportion of instances to train a decision tree at every iteration. In GEE, these hyperparameters are the *numberOfTrees*, *variablesPerSplit*, and *bagFraction*, respectively.  The *numberOfTrees* values tested ranged between 10 and 150 at an interval of 10, *variablesPerSplit* values ranged between 1-10, while *bagFraction* was by increment of 10 with the maximum limit being 90%. The *numberOfTrees*, *variablesPerSplit*, and *bagFraction* with the highest accuracy were used as the optimal values for model training. 






![image](https://github.com/user-attachments/assets/0ed0f4bc-d2a9-4bda-a6b8-60d0ad633234)





#### Partitioning reference data



#### Tuning hyperparameters



#### Create and train Random Forest model



#### Classify Sentinel-2 imagery



#### Evaluate the Random Forest model





## Results




## Discussion




## Conclusion




## References
