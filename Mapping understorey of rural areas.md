# Mapping Understorey of Rural Areas in Australian Capital Territory

In this project, grass cover in rural areas of the ACT, Australia was categorised into native/exotic and C3/C4 for efficient management.


## Abstract

Grasslands are an important global terrestrial biome as they provide a range of ecosystem services, including a refugia for thretened plants,, birds, mammals and reptiles. In Australia, grasslands are also a source of feed for livestock. The grasslands are managed to minimise weed invasion, fire attacks, soil erosion and displacement owing to agricultural expansion.


## Introduction

Grasslands are globally ubiquitous, except Antarctica, making it one of the dominant biomes covering approximately 45% of the Earth's terrestrial ecosystems. While glasslands provide habitats for plants, mammals, birds, and reptiles, it contributes approximately 20% of the global soil carbon stocks. Tropical and subtropical grasslands are found mainly in Africa and Australia. In Australia, grasslands provide a range of ecosystem services, including fodder for livestock, refugia for threatened plant and animal species, and protection of soil. 
The overarching aim of the project is to map the understorey vegetation communities of rural areas in the Australian Capital Territory. To this end, the specific objectives include: <br>
- discriminating between exotic, native and native high diversity grassland <br>

- discriminating between C3 and C4 exotic grasses <br>

- discriminating between dominant grass species <br>

- evaluating the performance of machine learning models explored


## Materials and Methods


### Study area




### Field data
The ground reference data was collected from 2018 until the end of 2023, in which visual discrimination of grasses were conducted by experts from the ACT government. The field sampling plots were randomly selected with each plot size equivalent to 400m2 (i.e., 20m by 20m) to match the nominal ground sampling distance of the Sentinel-2 satellite. The geographic coorodinates of a plot were collected using a differential GPS with a sub-meter horizontal accuracy. In each plot, the observer recorded the botanical composition including a fraction of vegetation cover and bare soil. Further, the grasses were separated into perennial/annual, C3/C4 with the level of plant diversity recorded. Post-field processing of the data was done to it clean up, removing bad rows and columns of data. This data was used to build, train and validate machine learning models.





### Sentinel-2 satellite imagery

Sentinel-2 is one of the Earth observation satellite missions operated through the Copernicus Program under the European Space Agency. The Sentinel-2, launched in 2015, on-board satellites that carry sensors collecting optical imagery of differing native resolutions at a planetary scale.


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


In this project, the Sentinel-2 spectral bands, including B2, B3, B4, B5, B6, B7, B8,B8A B11, B12, were used as they provide high resolution imagery and suited for vegetation monitoring. To ensure that the recorded energy were those reflected off the targets of interest, the top of atmosphere Sentinel-2 images retrieved from the Copernicus Open Access Hub via Google Earth Engine were preprocessed to minimise the influence of atmospheric conditions, sun-sensor viewing geometry, and topography. The Sentinel-2 TOA imagery over the study areas acquired from 2018 to 2013 was used as this date aligns with the field observation data. Sensor insentive radiative transfer model leveraging off MODIS product was used for the atmospheric correction [(Yin et al., 2022)](https://doi.org/10.5194/gmd-15-7933-2022). The imagery was also corrected for bidirection reflectance and topographic influence to produce analysis ready data referred to as NBART from here on. A global digital elevation model (DEM) made available through the NASA Shuttle Radar Topography Mission (SRTM) obtained via Google Earth Engine was used to minimise biases due to the relief of the plots. Image pixels affected by cloud and cloud shadow were eliminated using the quality assesssment bands. The project adapted the pre-analysis techniques for obtaining analysis ready NBART products by [Berra et al. (2024)](https://doi.org/10.3390/rs16152695). Since the Sentinel-2 satellites acquire data at varied native spatial resolutions, the imagery obtained at spectral bands with 10m resolution were spatially upscaled to 20m using the nearest neighbourhood geometric resampling method to preserve the original reflecance values and harmonise the data. The DEM was used to compute elevation, slope, and aspect to radiometrically normalize reflectance. 




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

Naturally, spatial relationships exist between the grass types and this should be accounted for. In image analysis, this relationship can be described through a textural analysis of the brightness values recorded by the electromagnetic detector. In this project, the grey level co-occurrence metrics (GLCM) by [Haralick et al., 1973](https://doi.org/10.1109/TSMC.1973.4309314) weree explored as the method is widely used in similar studies (REFERENCES). The GLCM textural method is employed by identifying a pixel in a moving window of pixels and comparing the relationships between the focal pixel and neighbouring pixels through via geographic directions.Through a frequency distribution, statistics such as contrast, homogeneity, dissimilarity, entropy and angular second moment are computed to describe the spatial relationships.  In GEE, several GLCM textural metrics can be computed but the most relevant ones to this study were utilised. These GLCM metrics were CON, HOM, DIS, ENT, and ASM. The GLCM textural analysis requires a single-band grey-scale imagery, thus, a method by [Tassi et al., 2022](https://doi.org/10.3390/rs12223776) leveraging off the NIR, Red, and Blue bands was used. A linear combination of the bands was used as: $\(0.30×NIR)+(0.59×Red)+(0.11×Green)$.


#### Phenological variables



### Topographic variables




### Selecting optimal variables 



### Random forest classification



#### Partitioning reference data



#### Tuning hyperparameters



#### Create and train Random Forest model



#### Classify Sentinel-2 imagery



#### Evaluate the Random Forest model





## Results




## Discussion




## Conclusion




## References
