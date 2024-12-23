# Mapping Understorey of Rural Areas in Australian Capital Territory

In this project, grass cover in rural areas of the ACT, Australia was categorised into native/exotic and C3/C4 for efficient management.


## Abstract



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
|B2 (blue) |land monitoring|10|
|B3 (green) |land monitoring|10|
|B4 (red) |land monitoring|10|
|B5 (red-edge) |land monitoring|20|
|B6 (red-edge) |land monitoring|20|
|B7 (red-edge) |land monitoring|20|
|B8 (near infrared) |land monitoring|10|
|B8a (near infrared) |land monitoring|20|
|B9 (water) |water vapour correction|60|
|B10 (cirrus) |cirrus detection|60|
|B11 (shortwave infrared) |land monitoring|20|
|B12 (shortwave infrared) |land monitoring|20|


In this project, the land monitoring bands were used as they provide high resolution imagery and suited for vegetation monitoring. To ensure that the recorded energy were those reflected off the targets of interest, the top of atmosphere Sentinel-2 images retrieved from the Copernicus Open Access Hub via Google Earth Engine were preprocessed to minimise the influence of atmospheric conditions, sun-sensor viewing geometry, and topography. The Sentinel-2 TOA imagery over the study areas acquired from 2018 to 2013 was used as this date aligns with the field observation data. Sensor insentive radiative transfer model leveraging off MODIS product was used for the atmospheric correction [(Yin et al., 2022)](https://doi.org/10.5194/gmd-15-7933-2022). The imagery was also corrected for bidirection reflectance and topographic influence to produce analysis ready data referred to as NBART from here on. A global digital elevation model (DEM) made available through the NASA Shuttle Radar Topography Mission (SRTM) obtained via Google Earth Engine was used to minimise biases due to the relief of the plots. Image pixels affected by cloud and cloud shadow were eliminated using the quality assesssment bands. The project adapted the pre-analysis techniques for obtaining analysis ready NBART products by [Berra et al. (2024)](https://doi.org/10.3390/rs16152695). The DEM was used to compute elevation, slope, and aspect to radiometrically normalize reflectance. 




#### Spectral indices

The NBART was analysed to derive spectral indices that measure the biophysical and chemical conditions of the grasses. Spectral indices are obtained from the bands applying different arithmetric operations; despite there are many spectral indices only those that require the highest resolution (10m) bands and were relevant to the project were utilised. The table below details the spectral indices used. 


|Index|Equation|Reference|
|:----|:----|:---|
|NDVI|(NIR-Red)÷(NIR+Red)|[Rouse et al. 1973](https://ntrs.nasa.gov/citations/19740022614)|
|B4 (red) |land monitoring|10|
|B5 (red-edge) |land monitoring|20|
|B6 (red-edge) |land monitoring|20|
|B7 (red-edge) |land monitoring|20|
|B8 (near infrared) |land monitoring|10|
|B8a (near infrared) |land monitoring|20|
|B9 (water) |water vapour correction|60|
|B10 (cirrus) |cirrus detection|60|
|B11 (shortwave infrared) |land monitoring|20|
|B12 (shortwave infrared) |land monitoring|20|



#### Textural and segmentataion 




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
