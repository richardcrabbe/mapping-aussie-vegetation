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



The location of the study area is the grasland areas of the ACT, Australia and this is represented by the figure below. 





![image](https://github.com/user-attachments/assets/fe06ba49-ea94-490c-91c4-daeb8150b0fd)











The methodology was adapted from recent similar studies, including [Poortinga et al., 2019](https://doi.org/10.3390/rs11070831), [Tassi et al., 2022](https://doi.org/10.3390/rs12223776), and [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) . The figure below is an overview of the methodology.





![image](https://github.com/user-attachments/assets/7bdb329b-5694-4768-87bd-c44d8e40fe3b)





### Reference data

The ground reference data was collected from 2018 until the end of 2023, in which visual discrimination of grasses were conducted by experts from the ACT government. The field sampling plots were randomly selected with each plot size equivalent to 400m^2 (i.e., 20m by 20m) to match the nominal ground sampling distance of the Sentinel-2 satellite. The geographic coorodinates of a plot were collected using a handheld GPS with a horizontal accuracy of approximately 5m. In each plot, the observer recorded the botanical composition including a fraction of vegetation cover and bare soil. Further, the grasses were separated into perennial/annual, C3/C4 with the level of plant diversity recorded. Post-field processing of the data was done to clean it up, removing bad rows and columns of data. This data was used to build, train and validate the machine learning classifier.





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


In this project, the Sentinel-2 spectral bands, excluding B1, B5, B6, B7, B8A, B9 and B10, were used as they provide high resolution imagery and suited for vegetation monitoring. The Sentinel-2 imagery over the study areas acquired from 2018 to 2013 was used as this date aligns with the field observation data. To ensure that the electromagnetic energy recorded by the sensor were those reflected off the targets of interest, the Bottom of Atmosphere Sentinel-2 imagery retrieved from the Copernicus Open Access Hub via Google Earth Engine were used. However, there was not Bottom of Atmosphere (BoA) product for 2018, so the Top of Atmposphere (ToA) product was collected and corrected for atmospheric influence using the sensor insentive radiative transfer model in GEE [(Yin et al., 2022)](https://doi.org/10.5194/gmd-15-7933-2022). Once the BoA imagery was obtained for all years, a bidirection reflectance distribution function was applied to minimise errors due to temporal variations in the sun-sensor viewing geometry. Image pixels affected by cloud and cloud shadow were masked using the quality assesssment bands. The project adapted the pre-analysis techniques, including cloud/shadow, atmospheric correction and BRDF methods by [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) to convert the ToA or BoA imagery to analysis ready data (ARD).  Since the Sentinel-2 satellites acquire data at varied native spatial resolutions, the imagery obtained at spectral bands with 10m resolution were spatially upscaled to 20m using the nearest neighbourhood geometric resampling method to preserve the original reflecance values and harmonise the data. 


#### Spectral indices

The ARD was analysed to extract spectral indices that measure the biophysical conditions of the grasses. Spectral indices are obtained from the bands applying different arithmetric operations; despite there are many spectral indices only those that require the nominal resolution (20m) bands and relevant to the project were utilised. The spectral indices, include the normalised vegetation index (NDVI), normalised water index (NDWI), soil-adjusted vegetation index (SAVI), enhanced vegetation index (EVI). Other spectral indices include the normalised burnt ratio (NBR), normalized difference phenology index (NDPI), green chlorophyll vegetation index (GCVI), normalised difference tillage index (NDTI), and bare soil index (BSI). The table below details the spectral indices used. 


|Index|Formula|Reference| 
|:----|:----|:---|
|NDVI|$${NIR-Red}\over{NIR+Red}$$|[Rouse et al., 1973](https://ntrs.nasa.gov/citations/19740022614)|
|NDWI|$${NIR-SWIR2}\over{NIR+SWIR2}$$|[Gao, 1996](https://doi.org/10.1016/S0034-4257(96)00067-3)|
|SAVI|$$\left({NIR-Red}\over{NIR+Red+0.5}\right)×{1.5}$$|[Huete, 1998](https://doi.org/10.1016/0034-4257(88)90106-X)|
|EVI |$$\left({NIR-Red}\over{NIR+6×Red-7.5×Blue+1}\right)× {2.5}$$|[Huete et al., 2002](https://doi.org/10.1016/S0034-4257(02)00096-2)|
|GCVI|$$\left({NIR}\over{Green}\right)-{1}$$|[Gitelson et al., 2003](https://doi.org/10.1078/0176-1617-00887)|
|BSI |$$\left({(SWIR2+Red)}-{(NIR+Blue)}\right)\over\left({(SWIR2+Red)}+{(NIR+Blue)}\right)$$|[Bera et al., 2020](https://doi.org/10.1007/s42489-020-00060-1)|



The NDVI, BSI, a textural measure (i.e, GLCM contrast) derived from Sentinel-1 (see the section on Sentinel-1 for details) were combined using user-defined thresholds to mask out pixels that were not grassland.



#### Textural and segmentataion 

Naturally, spatial relationships exist between the grass types and this should be accounted for. In image analysis, this relationship can be described through a textural analysis of the brightness values recorded by the electromagnetic detector. In this project, the grey level co-occurrence metrics (GLCM) by [Haralick et al., 1973](https://doi.org/10.1109/TSMC.1973.4309314) were explored as the method is widely used in similar studies (REFERENCES). The GLCM, a second order statistical analysis of an image, is employed by identifying a pixel in a pre-determined moving window of pixels and comparing the relationships between the focal pixel and neighbouring pixels in a specific direction and distance. Through descriptive statistical methods, many textural metrics can be computed. In the GEE, eighteen GLCM metrics sourced from the works of [Haralick et al., 1973](https://doi.org/10.1109/TSMC.1973.4309314) and [Conners et al., 1984](https://sdoi.org/10.1016/0734-189X(84)90197-X) can be computed. However, the relevance of the metrics is study-specific and for this reason only five of the metrics were explored in this study. These were sum average (AVG), variance (VAR), contrast (CON), inverse difference moment (IDM) and entropy (ENT). The formulae for the metrics are from [Hall-Beyer, 2017)](https://doi.org/10.1080/01431161.2016.1278314).




|Metric|Formula|Description|
|:----|:----|:---|
|CON|$$\sum_{i,j=0}^{N-1}  P_{i,j} \left( {i-j} \right)^2 $$|Measure local contrast|
|IDM|$$\sum_{i,j=0}^{N-1}  {P_{i,j}\over 1+ \left( {i-j} \right)^2} $$|Measure homogeneity|
|ENT |$$\sum_{i,j=0}^{N-1} P_{i,j} \left( {-lnP_{i,j}} \right)$$|Measure randomness in grey-levels|
|AVG|$$\sum_{i,j=0}^{N-1}  i\left(P_{i,j}\right)$$|Measure mean grey-levels|
|VAR  |$$\sum_{i,j=0}^{N-1}  P_{i,j} \left( {i-μ_i} \right)^2 $$|Measure the spread of grey-levels|



ASM = Angular Second Moment and IDM = Inverse Difference Moment. Pi,j refers to the probability of values i (labels of the columns) and j (labels of the rows) occurring in adjacent pixels in the original image within the pre-determined neighbourhood window. Regarding the GLCM Correlation, µ is mean and σ the standard deviation.


To compute the GLCM metrics in GEE, a 8-bit grey-scale imagery is required. Although many approaches for selecting a single-band imagery for the GLCM textural analysis exist, including using an NDVI layer, a recent method by [Tassi et al., 2022](https://doi.org/10.3390/rs12223776) leveraging the NIR, Red, and Blue bands was used. A linear combination of the bands was used as: <br>




**$\(0.30×NIR)+(0.59×Red)+(0.11×Green)$** 




Image segmentation is another method to explore the capability of the Sentinel-2 to differentiate between the grasses as pixels with similar spatial and spectral attributes, such as colour, luminance and texture, are clustered together to form homogeneous superpixels referred to as spectral objects or clusters. Image segmentation methods perform object-based analysis of the pixels and can remove redundant data. The Simple Non-Iterative Clustering (SNIC) algorithm by [Achanta and Susstrunk, 2017](https://doi.org/10.1109/CVPR.2017.520) was used to segment the Sentinel-2 pixels into spectral clusters. The SNIC algorithm requires input variables such as compactness factor for spatial distance weighting and connectivity and neighbourhood size for efficient grouping of the pixels. The SNIC input parameters used by [Tassi et al., 2022](https://doi.org/10.3390/rs12223776) for a land cover classification study in Europe were replicated in this study. The SNIC clusters were used a predictor variable.


Annual image collection for the spectral indices, GLCM textural metrics and SNIC clusters were created and from which composites such as maximum, medoid, 20th and 80th percentile spectral information were computed. Annual is defined as the period from June to May the following year to  mark the phenological growth calendar of the plants. 

### Sentinel-1

Sentinel-1 is another Earth observation satellite mission operated by the ESA with the aim of monitoring the environment from space regardless of atmospheric and weather conditions. The Sentinel-1 carries a sensor that transmits and records microwave energy that bounced off environmental targets, including grasslands. Sentinel-1 is a synthetic aperture radar system, measuring the amplitude and phase of the microwave energy in multiple polarisations. Because the Sentinel-1 uses artificial microwave energy it is capable of  penetrating through cloud cover and taking photos of the Earth at any time. Thus, the Sentinel-1 complements the Sentinel-2 for continuous mapping of the environment, while providing spectral information that characterises the variations in structural and moisture conditions of the vegetation. The Sentinel-1 typically transmits the microwave energy in vertical orientation and records the return signal in vertical and horizontal orientations making the Sentinel-1 a dual-polarisation system in that the data comprises VV and VH polarisation bands.The Sentinel-1 sensor can be operated in four different modes, but the imagery obtained from the interferometric wide swath mode (IW) are recommended and available for land monitoring. This study used imagery from the IW mode that were already pre-processed to a ground range detected product (i.e., analysis ready data) by the ESA and were retrievable from the GEE data catalog. The pixel size of the ground range detected Sentinel-1 imagery is 10m and this is created from single look complex imagery by applying a multi-look algorithm. Further preprocessing steps such as thermal noise removal, radiometric calibration and terrain correction were performed before making the data available in GEE. Given the physical structure of vegetation canopy is more sensitive to the VH polarisation, only this band was used in this study. The inherent speckle noise associated with the Sentinel-1 imagery was not filtered out as this lowers the spectral and spatial variability required to differentiate pixels. 

#### Phenological variables extracted from the Sentinel-1

The biophysical conditions of plant species, including annual and perennial grasses, change through the growth calendar. While perennial grasses maybe green throughout the year, annual grasses may disappeear during the dry or low rainfall seasons. The growth phenology of the plants can be an importantt information to differentiate between the grass types. Sentinel-1, in contrast to the optical Sentinel-2 imagery, is not affected by cloud cover or shadow; thus, a multitemporal Sentinel-1 data was anlysed to extract phenological information about the species. A Fourier harmonics function was applied to the Sentinel-1 time series data to compute amplitude and phase bands. The bands were adjusted to spatially align with the regions of interest and the Sentinel-2 data and pixels that were not grassland were masked using the method discussed earlier. Annual composites of the Sentinel-1 imagery were created to extract the phenological information of the plants. Through the annual composites, additional composites including maximum, medoid, 20th and 80th percentile of the phase and amplitude information were created.  A similar approach was used by [Poortinga et al., 2019](https://doi.org/10.3390/rs11070831) in a land cover classification project conducted in Myanmar.


### Topographic variables

The NASA  Shuttle Radar Topography Mission (SRTM), a global topographic data, was obtained from the GEE data archive to compute elevation, slope, and aspect.  The NASA SRTM elevation data has a pixel size of approximately 30m, this was adjusted to match the Sentinel-2 pixels before computing the topographic variables. The elevation, slope and aspect images were added to the composite images from Sentinel-2 and Sentinel-1 to make a single image of several bands.


### Random forest classification

Random Forest (RF) is a decision tree ensemble machine learning algorithm widely used for land cover monitoring as it is not limited by data structure and minimises overfitting the data [Breiman, 2000](https://doi.org/10.1023/A:1010933404324). Additionally, the RF is computationally less expensive to implement as only few hyperparameters require tuning.  The RF operates by randomly selecting a proportion of the instances to train a decision tree, wile replacing the samples to be re-used in the next iteration. Sampling a subset of instances with replacement to create decision trees is referred to as boostrap aggregating (i.e., bagging). The RF creates multiple decision trees to avoid overfitting; the final descision tree is obtained through majority voting. The figure below explains how the Random Forest classification algorithm functions. The RF classification algorithm in GEE was used, requiring the tuning for hyperparameters such as the number of trees to grow, number of the predictor variables to use and the proportion of instances to train a decision tree at every iteration. In GEE, these hyperparameters are the *numberOfTrees*, *variablesPerSplit*, and *bagFraction*, respectively.  The *numberOfTrees* values tested ranged between 10 and 150 at an interval of 10, *variablesPerSplit* values ranged between 1-10, while *bagFraction* was by increment of 10 with the maximum limit being 90%. The *numberOfTrees*, *variablesPerSplit*, and *bagFraction* with the highest accuracy were used as the optimal values for model training. 






![image](https://github.com/user-attachments/assets/0ed0f4bc-d2a9-4bda-a6b8-60d0ad633234)





#### Data partitioning, selecting optimal predictors and classification

The reference data was used to randomly sample pixels for each cover class, which was then split into two sets with 80% of the samples representing the training set while the remaining was used for evaluating the accuracy of the Random Forest classifier. A Random Forest classification model was trained using the predictor variables and optimal hyperparameter values in probability mode to predict cover classes. The predictor variables were assessed to remove redundant variables. Methods such as correlation analysis, principal component analysis and separability indices have been used to select the optimal predictor variables for RF models. However, in this work, we used the mean decrease impurity method which is built-into the RF algorithm in the GEE. Once the best predictor variables were identified (the top 15 variables) a parsimonius RF model was created using these variables. The RF classifier was applied to the class cover to produce probability maps for each class cover. The class probability maps

"A decision tree and Monte-Carlo simulation were used to create the final land cover assemblage. The decision tree was used to set the order and thresholds used to combine each of the primitives together into one final land cover map. The decision tree was run 100 times with a Monte-Carlo simulation process [85]. The Monte-Carlo process entailed adding a grid with random numbers to each of the primitives. It produces a final land cover map, which is the mode of the 100 simulations and a probability map which is the count of the mode divided by the total number of model runs."




#### Evaluate the Random Forest model

The test set was used to evaluate the accuracy of the RF classifier in that user's accuracy, prouducer's accuracy, F-1 score were computed from a confusion matrix table. Additionally, the distribution of class probabilities were produced.



## Results




## Discussion




## Conclusion




## References


Achanta, R., & Susstrunk, S. (2017). Superpixels and Polygons Using Simple Non-iterative Clustering. 2017 IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 4895–4904. https://doi.org/10.1109/CVPR.2017.520 <br>
Amarasingam, N., E Kelly, J., Sandino, J., Hamilton, M., Gonzalez, F., L Dehaan, R., Zheng, L., & Cherry, H. (2024). Bitou bush detection and mapping using UAV-based multispectral and hyperspectral imagery and artificial intelligence. Remote Sensing Applications: Society and Environment, 34, 101151. https://doi.org/10.1016/j.rsase.2024.101151 <br>
Amarasingam, N., Hamilton, M., Kelly, J. E., Zheng, L., Sandino, J., Gonzalez, F., Dehaan, R. L., & Cherry, H. (2023). Autonomous Detection of Mouse-Ear Hawkweed Using Drones, Multispectral Imagery and Supervised Machine Learning. Remote Sensing, 15(6), 1633. https://doi.org/10.3390/rs15061633 <br>
Bannari, A., Morin, D., Bonn, F., & Huete, A. R. (1995). A review of vegetation indices. Remote Sensing Reviews, 13(1–2), 95–120. https://doi.org/10.1080/02757259509532298





