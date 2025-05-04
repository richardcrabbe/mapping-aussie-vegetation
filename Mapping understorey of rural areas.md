# Mapping Understorey of Rural Areas in Australian Capital Territory

In this project, the grassland communities in rural ACT, Australia, were categorised into high quality native, low quality native and exotic species types for efficient management.


## Abstract

Grasslands are an important global terrestrial biome as they provide various ecosystem services, including refugia for thretened plants, birds, mammals and reptiles. The lowland areas of the Australian Capital Territory are dominated by grassland communities that are important to Australian biodiversity. However, the expanse of the ACT grassland communities has decreased chiefly due to weed invasion, fire and feral animal attacks, inappropriate grazing regimes, urbanisation, and agricultural expansion or improvements. The ACT Natural Temperate Grasslands is listed as a critically endangered ecological community under the Commonwealth legislation (EPBC Act 1999) and the ACT Nature Conservation Act 2014. Continuous monitoring of the grasslands is an efficient management practice to minimise or prevent many of the threats and stresses of the grassland vegetation communities. This project utilised multitemporal satellite imagery from Sentinel-1 and Sentinel-2, elevation data, and a Random Forest classification algorithm in Google Earth Engine (a cloud-based geospatial analysis platform) to (1) differentiate between exotic, native and native high diversity grass; (2) differentiate between dominant native grass species, including kangaroo grass, spear grass and Phalaris; and (3) quantify the performance and uncertainty of a Random Forest classification model. A range of predictors relevant for both pixel-based and object-based analysis, including spectral indices, textural and segmentation variables derived from the Sentinel-2 data, phenological variables derived from the Sentinel-1, and topographical variables from the elevation data, were used to teach a Random Forest algorithm to discriminate between grassland types. Monte Carlo simulation and conformal prediction methods were used to quantify the uncertainty associated with the Random Forest model. The accuracy of the Random Forest model was assessed using a data set separate from the one used to teach the model, and statistical metrics such as overall accuracy, user's accuracy, producer's accuracy, and F1-score were used to describe the performance of the model.


## Introduction

Grasslands are globally ubiquitous, excluding Antarctica and extreme desert areas and highest mountains, making it one of the dominant biomes covering approximately 40% of the Earth's terrestrial ecosystems ([Petermann and Buzhdygan, 2021](https://doi.org/10.1016/j.cub.2021.06.060)). Specifically, grasslands are found in temperate, tropical and subtropical environments, and variations in temperature and precipitation drive the global distribution. In Australia, grasslands are spatially varied, mimicking regional climatic patterns and fire regimes. The Australian grasslands, including temperate, alpine and Monaro grasslands spanning the southeastern part of the country, are a habitat for many flora and fauna species ([McIvor, 1994](https://www.fao.org/4/y8344e/y8344e0g.htm)). In the Australian Capital Territory (ACT), grassland communities predominate the lowland areas. The communities comprise the Natural Temperate Grasslands (NTG), native grassland and degraded native grassland under the ACT Native Grassland Conservation Strategy [ACT Government, 2017]. The ACT lowland grasslands are predominantly perennial tussock grasses, such as *Poa*, *Themeda*, *Austrodanthonia*, *Rytidosperma*, and *Austrosipa* ([Brawata et al., 2017](https://www.act.gov.au/__data/assets/pdf_file/0009/2539629/lowland-native-grassland-ecosystem-condition-monitoring-plan-2017.pdf)) and can be found mainly in nature reserves. The spatial extent of the ACT grasslands has considerably decreased due to urbanisation, invasion of exotic species and weeds, agricultural improvements, and inappropriate grazing and fire regimes. Consequently, the NTG is categorised as a critically endangered ecological community under the Environment Protection and Biodiversity Conservation Act (EPBC Act, 1999) and the ACT Nature Conservation Act 2014. Monitoring grassland conditions is required to address the threats and stressors in time. Although field-based monitoring methods can be used for grassland management, direct physical assessment methods can be expensive to sustain, especially monitoring at a landscape scale.

Satellite remote sensing provides a more cost-efficient approach for continuous monitoring of grasslands at a large scale. Earth observation satellites take multispectral photographs for a detailed spectral analysis of terrestrial vegetation. Through spectral indices such as the normalised difference vegetation index (NDVI), soil-adjusted vegetation index (SAVI), enhaced vegetation index (EVI), and normalised difference water index (NDWI), spectral data from the satellite sensors can be used to track the health and vigour of vegetation. Earth observation satellites, such as Landsat and Moderate Resolution Imaging Spectroradiometer (MODIS), have been extensively used for grassland monitoring. [Meng et al., (2022)](https://doi.org/10.3390/rs14092094)  leveraged MODIS NDVI products, including maximum, mean and sum of NDVI for large-scale temperate grassland mapping in Inner Mongolia. In a different study, time series of MODIS NDVI was analysed to extract phenological metrics to differentiate between alpine meadows, steppes, and desert grasses in the Tibetan Plateau ([Wang et al., 2015](https://doi.org/10.1080/17538947.2013.860198)), while a similar study leveraged the MODIS EVI to classify grasslands into meadow steppe, typical steppe, desert steppe, high-cold meadow steppe, high-cold typical steppe and shrub herbosa ([Wen et al., 2010](https://doi.org/10.1109/JSTARS.2010.2049001)). Landsat 8 was used to map high-diversity grassland and degraded grassland with an accuracy higher than 80% ([Fassnach et al., 2015](https://doi.org/10.1016/j.jag.2015.06.005)). The advent of the Sentinel satellites operated under the Copernicus Program by the European Space Agency complements the existing sensors to offer improved opportunities for grassland monitoring from space as the Sentinel satellites provide higher spatial, spectral and temporal information about the environment. Integrating satellite sensors, including optical and synthetic aperture radar (SAR), and machine learning and deep learning techniques have been used to improve grassland mapping. [Badreldin et al., (2021)](https://doi.org/10.3390/rs13244972) combined MODIS, Sentinel-2 and Sentinel-1 data and Random Forest to classify grasslands into native, tame and mixed species in Canada. The study achieved prediction accuracies higher than 85% for the native grasslands. In Tasmania (Australia), [Meville et al.,(2015)](https://doi.org/10.1016/j.jag.2017.11.006) combined Landsat ETM+ and WorldView-2 and Random Forest to differentiate lowland native grasslands of *Poa labillardierei* , *Themeda triandra* and lowland native grassland complex predominantly species from the *Danthonia* genus. The average prediction accuracies varied between 54% and 87%. [Crabbe et al., (2019)](https://doi.org/10.3390/rs11030253) explored multitemporal Sentinel-1 data to discriminate pastural grasses into C3, C4, and mixed, while in a different study, a range of machine learning methods and a combination of Sentinel-1 and Sentinel-2 data were used to map species diversity for a grazing property in Australia ([Crabbe et al., 2020](https://doi.org/10.1016/j.jag.2019.101978)). 

This study aims to differentiate grassland types in lowland ACT to support the ACT Native Grassland Conservation Strategy and Action Plans for efficient management of the Natural Temperate Grasslands, providing baseline for tracking changes and evaluating climate, anthropogenic and management practices on the grassland communities. To achieve this aim, the following specific objectives were addressed: <br> 

- extract grassland pixels from a heterogeneous landscape

- differentiate between exotic, high quality native and low quality native grass <br>

- appraise the performance and uncertainty of a Random Forest classfication model


## Materials and Methods




### Study area



The location of the study area is the grassland areas of the ACT, Australia, represented by Fig. 1. 





![image](https://github.com/user-attachments/assets/aafaff09-ecf7-4569-a99e-c90376f47570)|
|:--:|
| *Fig. 1. The study location with red pixels showing grassland areas investigated.*|









### Workflow


Fig. 2 is an overview of the cardinal workflow. 





![image](https://github.com/user-attachments/assets/30fd2cb9-38be-4f28-acc1-62c254bfdcff)|
|:--:|
| *Fig. 2. An overview of the workflow, including the datasets and principal methods employed.*|





The methodology was adapted from similar studies, including [Poortinga et al., 2019](https://doi.org/10.3390/rs11070831); [Tassi and Vizzari, 2020](https://doi.org/10.3390/rs12223776); and [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) and was implemented using Google Earth Engine JavaScript API and R. The previous studies that implemented similar land cover classification workflow reported a prediction accuracy ranging from 82% to 91%. The Google Earth Engine (GEE) is a cloud-based platform offering a combination of satellite imagery (including Landsat, MODIS, and Sentinel) and other geospatial datasets, integrated development environment and algorithms to make planet-scale remote sensing analysis and sharing of results easy ([Gorelick et al., 2017](https://doi.org/10.1016/j.rse.2017.06.031)). The GEE entails large-scale computing resources accessible via JavaScript API and Python API, and is automatically synced with GitHub for easy project collaboration through code sharing and version control. 



### Software

Google Earth Engine (GEE) Java Script API, R and QGIS were employed in this study. The GEE was used for image preprocessing, postprocessing, analysis and classification; the R was used for model development and evaluation; and QGIS was used for the preparation of the final map for visualisation purposes only. 

### ACT data

Field survey data was collected from 2019 to 2023 (inclusive), in which experts from the ACT government conducted visual discrimination of grasses. The field sampling plots were randomly selected with each plot size equivalent to $400m^2$ (i.e., 20m by 20m) to suit the nominal ground sampling distance of the Sentinel-2 satellite. The geographic coordinates of a plot were collected using a handheld GPS with a horizontal accuracy of approximately 5m. The observer recorded the botanical composition in each plot, including a fraction of vegetation cover, bare soil, and level of diversity categorised as low  quality native, moderate quality native and high quality native. The vegetation cover comprised proportions of native C3 and C4 plants and exotic annual and perennial plants. Post-field processing of the data was done to remove bad data points. The vegetation cover of the plots was varied, so plots with a minimum of 70% cover and contained level of diversity information were retained for the analysis. The high quality native and moderate quality native plots were merged to increase the sample size. 

A ratio of the proportion of native plants to exotic perennials was computed and used to label plots, low quality native, high quality native or exotic, using a threshold of 0.5. If the ratio is larger than 0.5, the plot is labelled native; otherwise, the plot is presumed to be dominated by an exotic grass. The label data was used to build, train and validate the machine learning classifier.

The ACT Vegetation Map and Plant Community Type (PCT) map layers were used to identify the regions of interest. The ACT Vegetation Map is a spatial layer for which native and derived vegetation in the ACT are classified into 64 plant communities utilising high-resolution aerial optical and LiDAR imagery (1-5m grid resolution), stereo pair interpretation, and extensive field data and existing reports ([ACT Government, 2024](https://actmapi-actgov.opendata.arcgis.com/datasets/ACTGOV::actgov-vegetation-map-2023/about)). The scale of the ACT Vegetation Map is 1:10000 and the attributes table provides a detailed description of the features, such as the dominant tree species, dominant shrub species, dominant ground cover species, canopy cover, understory and shrub cover, and vegetation community structure (i.e., woodland, forest, grassland). The PCT is another ACT map product that delineates the extent (via ongorund GPS  mapping) and ecological zones (via the assessment of attributes related to vegetation structure, floristic composition, and level of disturbance) of the plant communities ([ACT Government, 2024](https://cdn.arcgis.com/home/item.html?id=88e1076a4db243a797f7ce0f22b9db8d)). The ACT Vegetation Map and PCT contain grassland polygon features, which were retrieved using the spatial analysis tool in QGIS 3.10. The grassland layer for lowland ACT was used to identify the regions of interest for the study.

A digital elevation model, with a ground sampling distance of 1m, acquired through a LiDAR survey over the ACT in 2020, was used to characterise the topography of the study regions. elevation, slope, Aspect, Eastness and northness


Through the LiDAR data, the ACT government has created a canopy cover layer in both raster and vector file formats. In this study, the canopy cover layer was used to exclude pixels that were not grasslands.





### Sentinel-2 satellite imagery and processing

Sentinel-2 is one of the Earth observation satellite missions operated through the Copernicus Program under the European Space Agency (ESA). The Sentinel-2, launched in 2015, carries a multispectral instrument that collects optical imagery of differing native resolutions at a planetary scale. Table 1 describes the spectral bands of Sentinel-2, including the key use and spatial resolution.



*Table 1. Characteristics of Sentinel-2 spectral bands, including key use and spatial resolution.*
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


In this project, the Sentinel-2 spectral bands were used as they provide high resolution imagery and are suited for vegetation monitoring. The Sentinel-2 imagery over the study areas acquired from 2019 to 2013 was used as this date aligns with the field observation data. To ensure that the electromagnetic energy recorded by the sensor was reflected off the targets of interest, the Bottom of the Atmosphere (BoA) Sentinel-2 imagery retrieved from the Copernicus Open Access Hub via Google Earth Engine was used. A Sentinel-2 image tile is approximately 110km x 110km, the study area was completely covered by four different image tiles. The number of Sentinel-2 images varied between the annual vegetation growth calendars (Jun-May) in that 216, 216, 214, 212, and 222 images for 2019, 2020, 2021, 2022 and 2023, respectively, were used. Despite the Sentinel-2 BOA products are potentially free from atmospheric effects, additional imgage preprocessing was conducted to deal with cloud cover, cloud shadow and distortions due to sun-satellite viewing angle.   


#### Cloud and cloud shadow masking

Cloud cover, cloud shadow and other atmospheric effects in the imagery were corrected by identifying and masking the affected pixels using the Sentinel-2-specific quality assessment, Cloud Score+ product develoed by Google [Pasquarella et al. (2023)](https://ieeexplore.ieee.org/document/10208818). The cumulative distribution function of possible cloud score values not lower than 70% were used as the threshold for retaining cloud-free pixels. The Harmonized Landsat and Sentinel-2 (HLS) GEE module by [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) was used for further image processing. 

#### BRDF correction

The nadir view angles of the Sentinel-2 satellites is not temporally invariant, causing dircetional reflecction on surface materials which can be accounted for via a bidirectional reflectance distribution function (BRDF) [Roy et al. (2017)](https://doi.org/10.1016/j.rse.2017.06.019). The BRDF within the HLS module [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) was applied to minimise errors in the imagery due to temporal variations in the sun-sensor viewing geometry. 

#### Sentinel-2 image composites 

Since the Sentinel-2 satellites acquire data at varied native spatial resolutions, the imagery obtained at spectral bands with 20m resolution was spatially downscaled to 10m using the nearest neighbourhood geometric resampling method to preserve the original reflectance values and harmonise the data. The Sentinel-2 has 13 spectral bands, but only the blue, green, red, nir, swir1 and swir2 were used. In this study, one year of images is regarded as a composite, thus, five different image composites were analysed in this study since the study period spans 2019-2023.

#### Sentinel-2 derivatives and annual statistics 

The standard deviation and mediod [Flood (2013)](https://doi.org/10.3390/rs5126481) were computed for the blue, green, red, nir, swir1, and swir2 bands. Give the growth pattern may vary between years, the medoid of the 20th and 80th percentile were included in the yearly compsite. The medoid was computed using the GEE composite module developed by [Principe (2019)](https://github.com/fitoprincipe/geetools-code-editor). Additionally, we computed the standard deviation of the normalised difference for the nir and swir2, green and swir, and nir and red. The bands in the Sentiel-2 composites were used to calculate additional covariates.


The bands in the composites were used to calculate a series of
covariates. Table Table A.1 provides an overview of covariates used in
the study including the spatial resolution. The letters ND indicate that
the normalized difference between the first and second bands were
calculated, p20 and p80 refer to the 20th and 80th percentile respectively.
For some combinations there are more common names such as
Normalized Difference Water Index (NDWI, McFeeters, 1996), Normalized
Burn Ratio (NBR, Key and Benson, 1999), Normalized Difference
Snow Index (NDSI, Salomonson and Appel, 2004) and Normalized
Difference Vegetation Index (NDVI, Rouse et al., 1974). The source or
calculation for the other covariates are described in the next paragraphs






A module was used to compute medoid, standard deviation, and 20th and 80th percentile.
The ARD was analysed to extract spectral indices that measure the biophysical conditions of the grasses. Spectral indices were obtained from the bands applying different arithmetic operations; despite the many spectral indices available in literature, only those that require the nominal resolution (10m) bands and are relevant to the project were utilised. The spectral indices, include the normalised difference vegetation index (NDVI), normalised difference water index (NDWI), soil-adjusted vegetation index (SAVI), enhanced vegetation index (EVI), green chlorophyll vegetation index (GCVI), and bare soil index (BSI). Table 2 details the spectral indices, formulae and principal references.  


*Table 2. Spectral indices derived from the Sentinel-2 imagery. NIR = near infrared and SWIR = shortwave infrared.*
|Index|Formula|Reference| 
|:----|:----|:---|
|NDVI|$${NIR-Red}\over{NIR+Red}$$|[Rouse et al., 1973](https://ntrs.nasa.gov/citations/19740022614)|
|NDWI|$${NIR-SWIR2}\over{NIR+SWIR2}$$|[Gao, 1996](https://doi.org/10.1016/S0034-4257(96)00067-3)|
|SAVI|$$\left({NIR-Red}\over{NIR+Red+0.5}\right)×{1.5}$$|[Huete, 1998](https://doi.org/10.1016/0034-4257(88)90106-X)|
|EVI |$$\left({NIR-Red}\over{NIR+6×Red-7.5×Blue+1}\right)× {2.5}$$|[Huete et al., 2002](https://doi.org/10.1016/S0034-4257(02)00096-2)|
|GCVI|$$\left({NIR}\over{Green}\right)-{1}$$|[Gitelson et al., 2003](https://doi.org/10.1078/0176-1617-00887)|
|BSI |$${(SWIR2+Red)}-{(NIR+Blue)}\over\{(SWIR2+Red)}+{(NIR+Blue)}$$|[Bera et al., 2020](https://doi.org/10.1007/s42489-020-00060-1)|





*Table 3. Covariates for 2019 only. The cohorts of the covariates derived from the Sentinel-2 imagery are spectral features (SP), spectral indices (SI), and statistic (STA). The phenology covariates (PHE) were derived from Sentinel-1, topographical covariates (TOP) were from the ACT LiDAR data and the spatial coordinates of the reference data representing the longitude and latitude (LL) covariates were used to account for spatial autocorrelation.*



|Covariate|Cohort|Formula|Reference|
|:----|:----|:---|:---|
|blue|SP|| |
|green |SP|| |
|red|SP|| |
|nir|SP|| |
|swir1|SP|| |
|siwr2 |SP|| |
|blue_p20|SP|| |
|blue_p80 |SP|| |
|green_p20|SP|||
|green_p80|SP|||
|red_p20|SP|||
|red_p80|SP|||
|nir_p20 |SP|||
|nir_820 |SP|||
| swir1_p20|SP|||
| swir1_p80|SP|||
|swir2_p20 |SP|||
| swir2_p80|SP|||
|ND_blue_green_p20 |SI|||
| ND_blue_green_p80|SI|||
|ND_blue_red_p20 |SI|||
| ND_blue_red_p80|SI|||
|ND_blue_nir_p20 |SI|||
|ND_blue_nir_p80 |SI|||
| ND_blue_swir1_p20|SI|||
|ND_blue_swir1_p80 |SI|||
| ND_blue_swir2_p20|SI|||
|ND_blue_swir2_p80 |SI|||
|ND_green_red_p20 |SI|||
|ND_green_red_p80 |SI|||
| ND_green_nir_p20|SI|||
| ND_green_nir_p80|SI|||
| ND_green_swir1_p20|SI|||
|ND_green_swir1_p80 |SI|||
|ND_green_swir2_p20 |SI|||
|ND_green_swir2_p80 |SI|||
|ND_red_swir1_p20 |SI|||
| ND_red_swir1_p80|SI|||
| ND_red_swir2_p20|SI|||
| ND_red_swir2_p80|SI|||
| ND_nir_red_p20|SI|||
|ND_nir_red_p80 |SI|||
| ND_nir_swir1_p20|SI|||
|ND_nir_swir1_p80 |SI|||
|ND_nir_swir2_p20 |SI|||
|ND_nir_swir2_p80 |SI|||
|ND_swir1_swir2_p20 |SI|||
| ND_swir1_swir2_p80|SI|||
|EVI_p20 |SI|||
|EVI_p80 |SI|||
| SAVI_p20|SI|||
| SAVI_p80|SI|||
| IBI_p20|SI|||
|IBI_p80 |SI|||
|blue_stdDev |STA|||
| green_stdDev|STA|||
|red_stdDev|STA|||
| nir_stdDev|STA|||
| swir1_stdDev|STA|||
|swir2_stdDev |STA|||
| ND_green_swir1_stdDev|STA|||
|ND_nir_red_stdDev |STA|||
| ND_nir_swir2_stdDev|STA|||
| phase2019|PHE|||
| amp2019|PHE|||
| elevation|TOP|||
|slope |TOP|||
|aspect |TOP|||
| eastness|TOP|||
| northness|TOP|||
|longitude |LL|||
| latitude|LL|||






#### Textural and segmentataion 

Naturally, spatial relationships exist between the grass types, and this can be leveraged to improve discrimination between species. In image analysis, the spatial relationship between pixels can be described through a textural analysis of the brightness values recorded by the electromagnetic detector. In this project, the grey level co-occurrence metrics (GLCM) by [Haralick et al., 1973](https://doi.org/10.1109/TSMC.1973.4309314) were explored as the method is widely used in similar studies, including [Mohammadpour et al., 2022](https://doi.org/10.3390/rs14184585), [Zhang et al., 2024](https://doi.org/10.1080/15481603.2024.2385170), and [Bazzo et al., 2024](https://doi.org/10.1016/j.ecoinf.2024.102813). The GLCM, a second order statistical analysis of an image, is employed by identifying a pixel in a pre-determined moving window of pixels and comparing the relationships between the focal pixel and neighbouring pixels in a specific direction and distance. Through descriptive statistical methods, many textural metrics can be computed. In the GEE, eighteen GLCM metrics, sourced from the works of [Haralick et al., 1973](https://doi.org/10.1109/TSMC.1973.4309314) and [Conners et al., 1984](https://sdoi.org/10.1016/0734-189X(84)90197-X), can be calculated. However, the relevance of the metrics is study-specific, and for this reason, only five of the metrics were explored in this study (Table 3). These were the sum average (AVG), variance (VAR), contrast (CON), inverse difference moment (IDM) and entropy (ENT). The formulae for the metrics are from [Hall-Beyer, 2017)](https://doi.org/10.1080/01431161.2016.1278314).



*Table 3. Grey level co-occurrence metrics derived from the Sentinel-2, including contrast (CON), inverse difference moment (IDM), entropy (ENT), average (AVG) and variance (VAR) of grey levels. N is the sample size, while Pi,j represents the probability of values i (labels of the columns) and j (labels of the rows) occurring in adjacent pixels in the original image within the pre-determined neighbourhood window.*
|Metric|Formula|Description|
|:----|:----|:---|
|CON|$$\sum_{i,j=0}^{N-1}  P_{i,j} \left( {i-j} \right)^2 $$|local contrast|
|IDM|$$\sum_{i,j=0}^{N-1}  {P_{i,j}\over 1+ \left( {i-j} \right)^2} $$|homogeneity|
|ENT |$$\sum_{i,j=0}^{N-1} P_{i,j} \left( {-lnP_{i,j}} \right)$$|randomness in grey-levels|
|AVG|$$\sum_{i,j=0}^{N-1}  i\left(P_{i,j}\right)$$|mean grey-levels|
|VAR  |$$\sum_{i,j=0}^{N-1}  P_{i,j} \left( {i-μ_i} \right)^2 $$|spread in grey-levels|



To compute the GLCM metrics in GEE, an 8-bit grey-scale imagery is required. Although many approaches for selecting single-band imagery for the GLCM textural analysis exist, including using an NDVI layer, a recent method by [Tassi  and Vizzari., 2020](https://doi.org/10.3390/rs12223776) leveraging the NIR, Red, and Blue bands was used. A linear combination of the bands was used as: <br>




**$\(0.30×NIR)+(0.59×Red)+(0.11×Green)$** 



The GLCM contrast, NDVI, and BSI were combined using user-defined thresholds to mask out pixels that were not grassland.


Image segmentation is another method to explore the capability of the Sentinel-2 to differentiate between the grasses as pixels with similar spatial and spectral attributes, such as colour, luminance and texture, are clustered together to form homogeneous superpixels referred to as spectral objects or clusters. Image segmentation methods perform object-based analysis of the pixels and can remove redundant data. The Simple Non-Iterative Clustering (SNIC) algorithm by [Achanta and Susstrunk, 2017](https://doi.org/10.1109/CVPR.2017.520) was used to segment the Sentinel-2 pixels into spectral clusters. The SNIC algorithm requires input variables such as compactness factor for spatial distance weighting and connectivity and neighbourhood size for efficient grouping of the pixels. The SNIC input parameters used by [Tassi and Vizzari, 2020](https://doi.org/10.3390/rs12223776) for a land cover classification study in Europe were replicated in this study. The SNIC clusters were used as a predictor variable.


Annual image collection for the spectral indices, GLCM textural metrics and SNIC clusters were created, from which composites such as maximum, medoid, 20th and 80th percentile spectral information were computed. The medoid is analogous to the univariate median, however, it is more insensitive to outliers and applicable to multi-dimensional data such as multispectral imagery. Further details on medoid is given in ([Flood, 2013](https://doi.org/10.3390/rs5126481)). Annual is defined as the period from June to May the following year to mark the phenological growth calendar of the plants. To streamline computation time, only the medoid composites were used to extract the GLCM textural metrics and SNIC clusters.

### Sentinel-1

Sentinel-1 is another Earth observation satellite mission operated by the ESA, launched into orbit in 2013, to monitor the environment from space regardless of atmospheric and weather conditions. The Sentinel-1 carries a sensor that transmits and records microwave energy that bounces off environmental targets, including grasslands. Sentinel-1 is a synthetic aperture radar system that measures the amplitude and phase of microwave energy in multiple polarisations. Because the Sentinel-1 uses artificial microwave energy, it can penetrate cloud cover and take photos of the Earth anytime. Thus, the Sentinel-1 complements the Sentinel-2 for continuous mapping of the environment while providing spectral information that characterises the variations in structural and moisture conditions of the vegetation ([Saatchi et al., 1995](https://doi.org/10.1029/95JD00852)). The Sentinel-1 typically transmits the microwave energy in vertical orientation and records the return signal in vertical and horizontal orientations, making the Sentinel-1 a dual-polarisation system in that the data comprises VV and VH polarisation bands. The Sentinel-1 sensor can be operated in four different modes; the imagery obtained from the interferometric wide swath mode (IW) is recommended and available for land monitoring ([Prats-Iraola et al., 2015](https://doi.org/10.1109/IGARSS.2015.7327018)). This study used imagery from the IW mode that was already pre-processed to a ground range detected product (i.e., analysis ready Sentinel-1 data) by the ESA and was retrievable from the GEE data catalog. The pixel size of the ground range detected Sentinel-1 imagery is 10m, and this is created from single look complex imagery by applying a multi-look algorithm. Further preprocessing steps, such as thermal noise removal, radiometric calibration and terrain correction were performed before making the data available in GEE. Given the physical structure of the vegetation canopy is more sensitive to the VH polarisation, only this band was used in this study. The inherent speckle noise associated with the Sentinel-1 imagery was not filtered out, as spatial filtering algorithms lower the spectral and spatial variability required to differentiate pixels. 

#### Phenological variables extracted from the Sentinel-1

The biophysical conditions of plant species, including annual and perennial grasses, change through the growth calendar. While perennial grasses may be photosynthetically active throughout the year, annual grasses may disappear during the dry or low rainfall periods. The growth phenology of the plants can be vital information to differentiate between grass types. Sentinel-1, in contrast to the optical Sentinel-2 imagery, is not affected by cloud cover or shadow; thus, multitemporal Sentinel-1 data was anlysed to extract phenological information about the species. A Fourier harmonics function was applied to the Sentinel-1 time series data to compute amplitude and phase bands whereby the amplitude explains the variance in the original time series and the phase angle denotes the time associated with the peak of the curve ([Jakubauskas et al., 2001](https://www.asprs.org/wp-content/uploads/pers/2001journal/april/2001_apr_461-470.pdf)). The amplitude and phase bands were adjusted to spatially align with the regions of interest and the Sentinel-2 data and pixels that were not grassland were masked using the method discussed earlier. Annual composites of the Sentinel-1 imagery were created to extract the phenological information of the plants. Additional composites, including maximum, medoid, 20th, and 80th percentile of the phase and amplitude information, were created through the annual composites. [Poortinga et al., (2019)](https://doi.org/10.3390/rs11070831) used a similar approach in a land cover classification project conducted in Myanmar.


### Topographic variables

The ACT digital elevation model (DEM) derived from an aerial LiDAR survey was used to compute topographical variables, such as slope, aspect, and ruggedness index, in QGIS 3.10. The pixel size of the DEM was 1m, so all topographical variables were geometrically corrected to 10m using the bilinear interpolation method to match the Sentinel-2 pixels and for easy import into GEE. In GEE, the elevation, slope, aspect, and ruggedness index images were added to the composite images from Sentinel-2 and Sentinel-1 to compose a single image of several bands.


### Random forest classification

Random Forest (RF) is a decision tree ensemble machine learning algorithm widely used for land cover monitoring as the RF is not limited by data structure and minimises overfitting the data [Breiman, 2000](https://doi.org/10.1023/A:1010933404324). Additionally, the RF is computationally less expensive to implement as only a few hyperparameters require tuning.  The RF randomly selects a proportion of the instances to train a decision tree while replacing the samples to be re-used in the next iteration. Sampling a subset of the instances with replacement to create decision trees is called boostrap aggregating (i.e., bagging). The RF creates multiple decision trees to avoid overfitting; the final decision tree is obtained through majority voting. Fig. 3 summarises how the Random Forest classification algorithm functions. The RF classification algorithm in GEE was used, requiring the tuning for hyperparameters such as the number of trees to grow, the number of the predictor variables to use, and the proportion of instances to train a decision tree at every iteration. In GEE, these hyperparameters are the *numberOfTrees*, *variablesPerSplit*, and *bagFraction*. The *numberOfTrees* values tested ranged between 10 and 150 at an interval of 10, *variablesPerSplit* values ranged between 1 and 10. The *bagFraction* ranged between 10% and 90% at an interval of 10. The *numberOfTrees*, *variablesPerSplit*, and *bagFraction* with the highest accuracy were used as the optimal values for model training. 






![image](https://github.com/user-attachments/assets/0ed0f4bc-d2a9-4bda-a6b8-60d0ad633234)|
|:--:|
| *Fig. 3. A conceptual diagram summarising how the Random Forest algorithm functions.*|





#### Data partitioning, selecting optimal predictors and classification

The reference data was used to randomly sample pixels for each cover class, which was then split into two sets, with 80% of the samples representing the training set, while the remaining was used for evaluating the accuracy of the Random Forest model. A Random Forest classification model was trained using the predictor variables and optimal hyperparameter values in probability mode to predict cover classes. The predictor variables were assessed to remove redundant variables. Methods such as correlation analysis, principal component analysis and separability indices can be used to select the optimal predictor variables for RF models. However, in this study, we used the mean decrease impurity method ([Breiman, 2000](https://doi.org/10.1023/A:1010933404324)), which is built into the RF algorithm in the GEE and widely used in classification tasks. Once the top predictor variables were identified, a parsimonious RF model was created using these variables. 


#### Evaluation of the Random Forest model

The test set was used to evaluate the accuracy of the RF classifier in that the user's accuracy, prouducer's accuracy, and F-1 score were computed from a confusion matrix table. To quantify the uncertainty associated with the Random Forest model, Monte Carlo simulation and Conformal Prediction methods were explored. While the Monte Carlo method is widely used for uncertainty quantification ([Canters et al.,2002](https://doi.org/10.1080/13658810110099143)) and ([Cockx et al., 2014](https://doi.org/10.1016/j.jag.2014.03.016)), the Conformal Prediction is a recent method in Earth Observation, and in contrast to Monte Carlo the Conformal Prediction method makes no assumption about data distribution and is model agnostic, supporting all classical and deep learning artificial intelligence models ([Singh et al., 2024](https://doi.org/10.48550/arXiv.2401.06421)). The RF model produced class membership probabilities for each pixel and was used for the post-hoc Monte Carlo simulation and Conformal Prediction to report model uncertainty. 




## Results




## Discussion




## Conclusion




## References


1, Achanta, R., & Susstrunk, S. (2017). Superpixels and Polygons Using Simple Non-iterative Clustering. 2017 IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 4895–4904. https://doi.org/10.1109/CVPR.2017.520 <br>

2, ACT Government. (2024). ACTGOV Vegetation Map 2023. ACT Government Geospatial Data Catalogue. https://actmapi-actgov.opendata.arcgis.com/datasets/ACTGOV::actgov-vegetation-map-2023/about. Accessed on 11 January 2025 <br>

3, Badreldin, N., Prieto, B., & Fisher, R. (2021). Mapping Grasslands in Mixed Grassland Ecoregion of Saskatchewan Using Big Remote Sensing Data and Machine Learning. Remote Sensing, 13(24), 4972. https://doi.org/10.3390/rs13244972 <br>

4, Bazzo, C. O. G., Kamali, B., Dos Santos Vianna, M., Behrend, D., Hueging, H., Schleip, I., Mosebach, P., Haub, A., Behrendt, A., & Gaiser, T. (2024). Integration of UAV-sensed features using machine learning methods to assess species richness in wet grassland ecosystems. Ecological Informatics, 83, 102813. https://doi.org/10.1016/j.ecoinf.2024.102813 <br>

5, Bera, B., Saha, S., & Bhattacharjee, S. (2020). Estimation of Forest Canopy Cover and Forest Fragmentation Mapping Using Landsat Satellite Data of Silabati River Basin (India). KN - Journal of Cartography and Geographic Information, 70(4), 181–197. https://doi.org/10.1007/s42489-020-00060-1 <br>

6, Berra, E. F., Fontana, D. C., Yin, F., & Breunig, F. M. (2024). Harmonized Landsat and Sentinel-2 Data with Google Earth Engine. Remote Sensing, 16(15), 2695. https://doi.org/10.3390/rs16152695 <br>

7, Brawata, R., Stevenson, B., & Seddon, J. (2017). Conservation Effectiveness Monitoring Program: ACT Lowland Native Grasslands Ecosystem Condition Monitoring Plan [Technical]. Environment, Planning and Sustainable Development Directorate, ACT Government. https://www.act.gov.au/__data/assets/pdf_file/0009/2539629/lowland-native-grassland-ecosystem-condition-monitoring-plan-2017.pdf <br>

8, Breiman, L. (2001). Random Forests. Machine Learning, 45(1), 5–32. https://doi.org/10.1023/A:1010933404324 <br>

9, Canters, F., Genst, W. D., & Dufourmont, H. (2002). Assessing effects of input uncertainty in structural landscape classification. International Journal of Geographical Information Science, 16(2), 129–149. https://doi.org/10.1080/13658810110099143 <br>

10, Cockx, K., Van De Voorde, T., & Canters, F. (2014). Quantifying uncertainty in remote sensing-based urban land-use mapping. International Journal of Applied Earth Observation and Geoinformation, 31, 154–166. https://doi.org/10.1016/j.jag.2014.03.016 <br>

11, Conners, R. W., Trivedi, M. M., & Harlow, C. A. (1984). Segmentation of a high-resolution urban scene using texture operators. Computer Vision, Graphics, and Image Processing, 25(3), 273–310. https://doi.org/10.1016/0734-189X(84)90197-X <br>

12, Crabbe, R. A., Lamb, D., & Edwards, C. (2020). Discrimination of species composition types of a grazed pasture landscape using Sentinel-1 and Sentinel-2 data. International Journal of Applied Earth Observation and Geoinformation, 84, 101978. https://doi.org/10.1016/j.jag.2019.101978 <br>

13, Crabbe, R. A., Lamb, D. W., & Edwards, C. (2019). Discriminating between C3, C4, and Mixed C3/C4 pasture grasses of a grazed landscape using multi-temporal sentinel-1a data. Remote Sensing, 11(3). https://doi.org/10.3390/rs11030253 <br>

14, Fassnacht, F. E., Li, L., & Fritz, A. (2015). Mapping degraded grassland on the Eastern Tibetan Plateau with multi-temporal Landsat 8 data—Where do the severely degraded areas occur? International Journal of Applied Earth Observation and Geoinformation, 42, 115–127. https://doi.org/10.1016/j.jag.2015.06.005 <br>

15, Flood, N. (2013). Seasonal Composite Landsat TM/ETM+ Images Using the Medoid (a Multi-Dimensional Median). Remote Sensing, 5(12), 6481–6500. https://doi.org/10.3390/rs5126481 <br>

16, Gao, B. (1996). NDWI—A normalized difference water index for remote sensing of vegetation liquid water from space. Remote Sensing of Environment, 58(3), 257–266. https://doi.org/10.1016/S0034-4257(96)00067-3 <br>

17, Gitelson, A. A., Gritz †, Y., & Merzlyak, M. N. (2003). Relationships between leaf chlorophyll content and spectral reflectance and algorithms for non-destructive chlorophyll assessment in higher plant leaves. Journal of Plant Physiology, 160(3), 271–282. https://doi.org/10.1078/0176-1617-00887 <br>

18, Gorelick, N., Hancher, M., Dixon, M., Ilyushchenko, S., Thau, D., & Moore, R. (2017). Google Earth Engine: Planetary-scale geospatial analysis for everyone. Remote Sensing of Environment, 202, 18–27. https://doi.org/10.1016/j.rse.2017.06.031 <br>

19, Hall-Beyer, M. (2017). Practical guidelines for choosing GLCM textures to use in landscape classification tasks over a range of moderate spatial scales. International Journal of Remote Sensing, 38(5), 1312–1338. https://doi.org/10.1080/01431161.2016.1278314 <br>

20, Haralick, R. M., Shanmugam, K., & Dinstein, I. H. (1973). Textural features for image classification. IEEE Transactions on Systems, Man, and Cybernetics, 6, 610–621. https://doi.org/10.1109/TSMC.1973.4309314<br>

21, Huete, A., Didan, K., Miura, T., Rodriguez, E. P., Gao, X., & Ferreira, L. G. (2002). Overview of the radiometric and biophysical performance of the MODIS vegetation indices. The Moderate Resolution Imaging Spectroradiometer (MODIS): A New Generation of Land Surface Monitoring, 83(1), 195–213. https://doi.org/10.1016/S0034-4257(02)00096-2 <br>

22, Huete, A. R. (1988). A soil-adjusted vegetation index (SAVI). Remote Sensing of Environment, 25(3), 295–309. https://doi.org/10.1016/0034-4257(88)90106-X <br>

23, Melville, B., Lucieer, A., & Aryal, J. (2018). Object-based random forest classification of Landsat ETM+ and WorldView-2 satellite imagery for mapping lowland native grassland communities in Tasmania, Australia. International Journal of Applied Earth Observation and Geoinformation, 66, 46–55. https://doi.org/10.1016/j.jag.2017.11.006 <br>

24, Meng, B., Zhang, Y., Yang, Z., Lv, Y., Chen, J., Li, M., Sun, Y., Zhang, H., Yu, H., Zhang, J., Lian, J., He, M., Li, J., Yu, H., Chang, L., & Yi, S. (2022). Mapping Grassland Classes Using Unmanned Aerial Vehicle and MODIS NDVI Data for Temperate Grassland in Inner Mongolia, China. Remote Sensing, 14(9), 2094. https://doi.org/10.3390/rs14092094 <br>

25, Mohammadpour, P., Viegas, D. X., & Viegas, C. (2022). Vegetation Mapping with Random Forest Using Sentinel 2 and GLCM Texture Feature—A Case Study for Lousã Region, Portugal. Remote Sensing, 14(18), 4585. https://doi.org/10.3390/rs14184585 <br>

26, Petermann, J. S., & Buzhdygan, O. Y. (2021). Grassland biodiversity. Current Biology, 31(19), R1195–R1201. https://doi.org/10.1016/j.cub.2021.06.060 <br>

27, Poortinga, A., Tenneson, K., Shapiro, A., Nquyen, Q., San Aung, K., Chishtie, F., & Saah, D. (2019). Mapping Plantations in Myanmar by Fusing Landsat-8, Sentinel-2 and Sentinel-1 Data along with Systematic Error Quantification. Remote Sensing, 11(7), 831. https://doi.org/10.3390/rs11070831 <br>

28, Prats-Iraola, P., Nannini, M., Scheiber, R., De Zan, F., Wollstadt, S., Minati, F., Vecchioli, F., Costantini, M., Borgstrom, S., De Martino, P., Siniscalchi, V., Walter, T., Foumelis, M., & Desnos, Y.-L. (2015). Sentinel-1 assessment of the interferometric wide-swath mode. 2015 IEEE International Geoscience and Remote Sensing Symposium (IGARSS), 5247–5251. https://doi.org/10.1109/IGARSS.2015.7327018 <br>

29, Rouse, J. W., Haas, R. H., Schell, J. A., & Deering, D. W. (1974). Monitoring vegetation systems in the Great Plains with ERTS. NASA Spec. Publ, 351(1), 309. https://ntrs.nasa.gov/citations/19740022614<br>

30, Tassi, A., & Vizzari, M. (2020). Object-Oriented LULC Classification in Google Earth Engine Combining SNIC, GLCM, and Machine Learning Algorithms. Remote Sensing, 12(22), 3776. https://doi.org/10.3390/rs12223776 <br>

31, Saatchi, S. S., van Zyl, J. J., & Asrar, G. (1995). Estimation of canopy water content in Konza Prairie grasslands using synthetic aperture radar measurements during FIFE. Journal of Geophysical Research, 100(D12), 25481. https://doi.org/10.1029/95JD00852 <br>

32, Singh, G., Moncrieff, G., Venter, Z., Cawse-Nicholson, K., Slingsby, J., & Robinson, T. B. (2024). Uncertainty quantification for probabilistic machine learning in earth observation using conformal prediction (Version 1). arXiv. https://doi.org/10.48550/ARXIV.2401.06421 <br>

33, Wang, C., Guo, H., Zhang, L., Qiu, Y., Sun, Z., Liao, J., Liu, G., & Zhang, Y. (2015). Improved alpine grassland mapping in the Tibetan Plateau with MODIS time series: A phenology perspective. International Journal of Digital Earth, 8(2), 133–152. https://doi.org/10.1080/17538947.2013.860198 <br>

34, Wen, Q., Zhang, Z., Liu, S., Wang, X., & Wang, C. (2010). Classification of Grassland Types by MODIS Time-Series Images in Tibet, China. IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing, 3(3), 404–409. https://doi.org/10.1109/JSTARS.2010.2049001 <br>

35, Yin, F., Lewis, P. E., & Gómez-Dans, J. L. (2022). Bayesian atmospheric correction over land: Sentinel-2/MSI and Landsat 8/OLI. Geoscientific Model Development, 15(21), 7933–7976. https://doi.org/10.5194/gmd-15-7933-2022 







