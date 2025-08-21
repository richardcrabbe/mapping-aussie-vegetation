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







![image](https://github.com/user-attachments/assets/35a8af89-bb0b-4a1d-8448-46fba6726266)|
|:--:|
| *Fig. 2. An overview of the workflow, including the datasets and principal methods employed.*|





The methodology was adapted from similar studies, including [Poortinga et al., 2019](https://doi.org/10.3390/rs11070831); [Tassi and Vizzari, 2020](https://doi.org/10.3390/rs12223776); and [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) and was implemented using Google Earth Engine JavaScript API and R. The previous studies that implemented similar land cover classification workflow reported a prediction accuracy ranging from 82% to 91%. The Google Earth Engine (GEE) is a cloud-based platform offering a combination of satellite imagery (including Landsat, MODIS, and Sentinel) and other geospatial datasets, integrated development environment and algorithms to make planet-scale remote sensing analysis and sharing of results easy ([Gorelick et al., 2017](https://doi.org/10.1016/j.rse.2017.06.031)). The GEE entails large-scale computing resources accessible via JavaScript API and Python API, and is automatically synced with GitHub for easy project collaboration through code sharing and version control. 



### Software

Google Earth Engine (GEE) Java Script API, R and QGIS were employed in this study. The GEE was used for image preprocessing, postprocessing, analysis and classification; the R was used for model development and evaluation; and QGIS was used for the preparation of the final map for visualisation purposes only. 

### ACT data

#### Field survey data
Field survey data was collected from 2019 to 2023 (inclusive), in which experts from the ACT government conducted visual discrimination of grasses using the step point ecological survey method (Evans and Love, 1957). The field sampling plots were randomly selected with each plot size equivalent to $400m^2$ (i.e., 20m by 20m) to suit the nominal ground sampling distance of the Sentinel-2 satellite. The geographic coordinates of a plot were collected using a handheld GPS with a horizontal accuracy of approximately 5m. The observer recorded the botanical composition in each plot, including a fraction of vegetation cover, bare soil, and level of diversity categorised as low  quality native, moderate quality native and high quality native. TThe vegetation cover comprised proportions of native C3 and C4 plants and exotic annual and perennial plants. Not every plot was labelled in the field; thus, a post-field processing of the data was performed to remove bad data points, including the unlabelled plots. The vegetation cover of the plots was varied; the labelled plots with a minimum of 70% cover were retained for further analysis. 

#### Labelling

A plot is usually composed of exotic and native (i.e., low, moderate and high quality) species of different proportions. Plots dominated by a species are selected to improve the predictability. A dominant species must cover a minimum of 60% of the plot. For instance if a plot is composed of 60% exotic, 30% low-quality native, and 10% high-quality native grassland, the plot is assigned to the 'exotic' class. The high quality native and moderate quality native plots were merged to align with the interests of land managers, producing three grass classes- high quality native, low quality native and exotic. These grass classes were detected and mapped in this project. The labelled data was used to build, train and validate the machine learning classifier.

#### Canopy cover data
The ACT canopy cover raster layer, derived from high-resolution (1m) LiDAR data and classified into surface types including trees, shrubs and grass, was used to mask out all surface types except grasslands.

#### Elevation data
A digital elevation model, with a ground sampling distance of 1m, acquired through a LiDAR survey over the ACT in 2020, was used to characterise the topography of the study regions. Through the elevation data, slope, aspect, eastness and northness were derived.

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

Since the Sentinel-2 satellites acquire data at varied native spatial resolutions, the imagery obtained at spectral bands with 20m resolution was spatially downscaled to 10m using the nearest neighbourhood geometric resampling method to preserve the original reflectance values and harmonise the data. The Sentinel-2 has 13 spectral bands, but only the blue, green, red, nir, swir1 and swir2 were used. In this study, one year of images is regarded as a composite, thus, five different image composites were analysed since the study period spans 2019-2023.

#### Sentinel-2 covariates

The standard deviation and mediod were computed for the blue, green, red, nir, swir1, and swir2 bands. The medoid is analogous to the univariate median, however, it is more insensitive to outliers and applicable to multi-dimensional data such as multispectral imagery. Further details on medoid is given in ([Flood, 2013](https://doi.org/10.3390/rs5126481)). In this study, annual is defined as the period from June to May the following year to mark the phenological growth calendar of the plants. Given the growth pattern may vary between years, the medoid of the 20th and 80th percentile were included in the yearly compsite. The medoid was computed using the GEE composite module developed by [Principe (2019)](https://github.com/fitoprincipe/geetools-code-editor). Additionally, we computed the standard deviation of the normalised difference for the nir and swir2, green and swir, and nir and red. The bands in the Sentiel-2 composites were used to calculate additional covariates (Table 3). The ND prefixing some of the covariates represents the normalised difference between the first and second bands computed as |NDVI|$${band1-band2}\over{band1+band2}$$|, while  p20 and p80 refer to the 20th and 80th percentile respectively. Amongst the ND bands are widely used spectral indices, such as Normalised Difference Vegetation Index (NDVI, [Rouse et al., 1973](https://ntrs.nasa.gov/citations/19740022614)), Normalised Difference Water Index ([NDWI, McFeeters, 1996](https://doi.org/10.1080/01431169608948714)) and ([Gao, 1996](https://doi.org/10.1016/S0034-4257(96)00067-3)), and Normalised Burn Ratio ([NBR, Key and Benson, 199](https://www.frames.gov/catalog/3356)). The other spectral indices included were the soil-adjusted vegetation index (SAVI), enhanced vegetation index (EVI) and index-based built-up index (IBI). Table 2 details the formulae and principal references of these additional spectral indices.  


*Table 2. The equations and references for soil-adjusted vegetation index (SAVI), enhanced vegetation index (EVI) and index-based built-up index (IBI).*

|Index|Formula|Reference| 
|:----|:----|:---|
|SAVI|$$\left({NIR-Red}\over{NIR+Red+0.5}\right)×{1.5}$$|[Huete, 1998](https://doi.org/10.1016/0034-4257(88)90106-X)|
|EVI |$$\left({NIR-Red}\over{NIR+6×Red-7.5×Blue+1}\right)× {2.5}$$|[Huete et al., 2002](https://doi.org/10.1016/S0034-4257(02)00096-2)|
|IBI |$$\left({NIR}\over{NIR+Red}\right) + \left({Green}\over{Green+SWIR1}\right)$$|[Xu, 2008](https://doi.org/10.1080/01431160802039957)|



Sxity-three covariates were obtained from an annual Sentinel-2 composite. Table 3 shows these covariates for the 2019 composite only. The same number of covariates were obtained for 2020, 2021, 2022 and 2023, but have not been shown.

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


### Sentinel-1

Sentinel-1 is another Earth observation satellite mission operated by the ESA, launched into orbit in 2013, to monitor the environment from space regardless of atmospheric and weather conditions. The Sentinel-1 carries a sensor that transmits and records microwave energy that bounces off environmental targets, including grasslands. Sentinel-1 is a synthetic aperture radar system that measures the amplitude and phase of microwave energy in multiple polarisations. Because the Sentinel-1 uses artificial microwave energy, it can penetrate cloud cover and take photos of the Earth anytime. Thus, the Sentinel-1 complements the Sentinel-2 for continuous mapping of the environment while providing spectral information that characterises the variations in structural and moisture conditions of the vegetation ([Saatchi et al., 1995](https://doi.org/10.1029/95JD00852)). The Sentinel-1 typically transmits the microwave energy in vertical orientation and records the return signal in vertical and horizontal orientations, making the Sentinel-1 a dual-polarisation system in that the data comprises VV and VH polarisation bands. The Sentinel-1 sensor can be operated in four different modes; the imagery obtained from the interferometric wide swath mode (IW) is recommended and available for land monitoring ([Prats-Iraola et al., 2015](https://doi.org/10.1109/IGARSS.2015.7327018)). This study used imagery from the IW mode that was already pre-processed to a ground range detected product (i.e., analysis ready Sentinel-1 data) by the ESA and was retrievable from the GEE data catalog. The swath width of the Sentinel-1 is 250 km, so a total of 412 images were obtained for the five years (2019-2023). The pixel size of the ground range detected Sentinel-1 imagery is 10m, and this is created from single look complex imagery by applying a multi-look algorithm. Further preprocessing steps, such as thermal noise removal, radiometric calibration and terrain correction were performed before making the data available in GEE. Given the physical structure of the vegetation canopy is more sensitive to the VH polarisation, only this band was used in this study. The inherent speckle noise associated with the Sentinel-1 imagery was not filtered out, as spatial filtering algorithms lower the spectral and spatial variability required to differentiate pixels. 

#### Phenology covariates from the Sentinel-1

The biophysical conditions of plant species, including annual and perennial grasses, change through the growth calendar. While perennial grasses may be photosynthetically active throughout the year, annual grasses may disappear during the dry or low rainfall periods. The growth phenology of the plants can be vital information to differentiate between grass types. Sentinel-1, in contrast to the optical Sentinel-2 imagery, is not affected by cloud cover or shadow; thus, multitemporal Sentinel-1 data was anlysed to extract phenological information about the species. A Fourier harmonics function was applied to the Sentinel-1 time series data to compute amplitude and phase bands whereby the amplitude explains the variance in the original time series and the phase angle denotes the time associated with the peak of the curve ([Jakubauskas et al., 2001](https://www.asprs.org/wp-content/uploads/pers/2001journal/april/2001_apr_461-470.pdf)). The amplitude and phase bands were adjusted to spatially align with the regions of interest and the Sentinel-2 data. The Sentinel-1 pixels that were not grassland were masked using the methods discussed in section XXX. Annual composites of the Sentinel-1 imagery were created to extract the phenological information of the plants. Table 3 shows the amplitude and phase covariates indicative of plant phenology for 2019 only. [Poortinga et al., (2019)](https://doi.org/10.3390/rs11070831) used a similar approach in a land cover classification project conducted in Myanmar.



### Topographic covariates

The ACT digital elevation model (DEM) derived from an aerial LiDAR survey was used to compute topographical variables, such as slope, aspect, sine of aspect and cosine of aspect. The sine of aspect measures deviation from east (eastness) and the cosine aspect explains deviation from north (northness). The pixel size of the DEM was 1m, so all topographical variables were geometrically corrected to 10m using the bilinear interpolation method to match the Sentinel-2 pixels and for easy import into GEE. Table 3 shows the topographic covariates- elevation, slope, aspect, eastness and northness. Note that the topographic covariates remained same regardless of the study year. 


### Additional covariates

The spatial coordinates of the reference plots were included as additional covariates to account for the sensitivity of the RF to spatial autocorrelation. In this study, we assumed that the reference label for sampling plots remained unchaged between years, meaning if plot **A** was labelled class **X** in 2019, the class ID will remain same in other years. The longitude and latitude in decimal degrees were the covariates and these remained same regardless of the study year.

There were 65 covariates per the yearly composite of Sentinel-2 and Sentinel-1 imagery, making a total of 325 covariates for the five years. Plus, the topographic variables and spatial coordinates of the reference plots, 332 covariates were used for the image classification analysis.

### Image classification using Random Forest 

Random Forest (RF) is a decision tree ensemble machine learning algorithm widely used for land cover monitoring as the RF is not limited by data structure and minimises overfitting the data [Breiman, 2000](https://doi.org/10.1023/A:1010933404324). Additionally, the RF is computationally less expensive to implement as only a few hyperparameters require tuning.  The RF randomly selects a proportion of the instances to train a decision tree while replacing the samples to be re-used in the next iteration. Sampling a subset of the instances with replacement to create decision trees is called boostrap aggregating (i.e., bagging). The RF creates multiple decision trees to avoid overfitting; the final decision tree is obtained through majority voting. Fig. 3 summarises how the RF classification algorithm functions. 



![image](https://github.com/user-attachments/assets/0ed0f4bc-d2a9-4bda-a6b8-60d0ad633234)|
|:--:|
| *Fig. 3. A conceptual diagram summarising how the Random Forest algorithm functions.*|



#### Producing grassland layer


The RF classification algorithm was used to classify the remote sensing imagery. A hierarchical approach was adopted to classify the image pixels into exotic, high quality and low quality native grasses. There were diferent surface types in the imagery, including tree cover, grass cover, shrub cover, water bodies, roads, buildings and open land. This can increase the uncertainty in the RF model, while the model may perform well discriminating grassland pixels only. To this end, an initial RF classification was performed to classify the imagery into three broad themes- water, artificial and grassland. The artificial class includes buildings, roads and concrete surfaces. In this RF classification, only limited covariates were used to avoid computational memory issues in GEE. The medoid and the standard deviation and percentiles (20th and 80th) of the medoid derived from the Sentinel-2 and the phenological variables from the Sentinel-1 were the covariates used. The ACT LiDAR canopy cover data was used to mask out trees and shrubs, leaving behind grasslands only. With the aid of a high-resolution RGB Google imagery, ACT LiDAR canopy cover and the Sentinel-2 imagery, reference data for water, artificial and grassland were collected using GEE. The reference data were polygons of similar dimensions, but given the spatial variability 25 polygons defining water, 27 for aritificial and 50 for grassland were used. Through the RF classification algorithm in GEE, the covariates and reference data were used to classify the image pixels into water, artificial and grassland. Details of the RF classification have been sacrificed here as this is covered in section XXX. The accuracy of the RF classification on unseen reference data for grassland was 98%. The grassland pixels were retrieved, masking out all other pixels. The grassland layer was used to refine the region of interest for the main RF classification analysis in the sections below.



#### Classifying the grassland layer




##### Data partitioning


The reference data collected by the ACT were used to randomly sample pixels for exotic (EXO), high-quality (HQN) and low-quality (LQN) grassland. The reference sample size was 3137, and this was split into train and test sets with 90% of the samples for model training and the remaining was used for evaluating the accuracy of the model. The training and testing sample sizes were 2824 and 313, respectively (Table **X**).


*Table 3. The reference sample size for exotic, high-quality native and low-quality native grasses.*

|Grass|Training|Testing|Total|
|:----|:----|:---|:---|
|Exotic|1336|148|1484 |
|HQ native|1065|118|1183|
|LQ native|423|47|470|



##### Hyperparameter tuning 

The RF classification algorithm produces the best result and is more efficient if the optimal values for the hyperparameters are used. The RF classification algorithm in GEE was used, and despite this algorithm requires five hyperparameters (i.e, numberOfTrees, variablesPerSplit, minLeafPopulation, bagFraction and maxNodes) to run, the most important hyperparmeters requiring tuning are the number of trees to grow (*numberOfTrees*), and the number of covariates per split  (*variablesPerSplit*). Owing to computational reasons, the tuning of optimal values for *numberOfTrees* and *variablesPerSplit* were conducted in R environment. A grid search approach was used, the values for *variablesPerSplit* ranged from 1 to 332 while a set of values was specified for *numberOfTrees* (10,20,50,500). The *numberOfTrees* and *variablesPerSplit* values that produced an RF model with the highest accuracy were selected as the optimal values. The optimal vaalues for *variablesPerSplit* and *numberOfTrees* were 89 and 500, respectively.

##### Cross validation and training of RF model

A good-fit model is a model capable of generalising effectively well to data that was not used to teach the model, so to assess this a 10-fold cross-validation strategy was employed in the R environment. The training dataset was randomly partitioned into 10 equally sized sub-samples called folds (Kohavi, 1995) and for every run of the cross-validation, one fold was reserved for validation, while the model was trained on the remaining nine folds. This process was repeated 10 times, varying the one-fold data for model validation in each iteration. Each of the ten folds was used extacly once for model validation. The model results from the 10-iterations were averaged to assess the generalisability of the model to unseen data. <br>

The RF classification model was trained using the 332 covariates and optimal hyperparameter values in probability mode in R and also GEE for the spatial representation of the grasses. 


##### Ranking the covariates

The covariates were assessed to remove redundant ones. Methods such as correlation analysis, principal component analysis and separability indices can be used to select the optimal predictor variables for RF models. However, in this study, we used the mean decrease impurity method ([Breiman, 2000](https://doi.org/10.1023/A:1010933404324)), which is built into the RF algorithm in the GEE and widely used in classification tasks. Once the top covariates were identified, a parsimonious RF model was created using these covariates. 










##### Evaluation of the Random Forest model

- accuracy based on training set (cross validation)

- accuracy based on test set


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

14, Evans, R.A., and R.M. Love. 1957. The step-point method of sampling: A practical tool in range research

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



## Scripts from the Google Earth Engine (JavaScript API)

### Stage 1- Processing Datasets

```JavaScript
var CRACE_2 = 
    ee.Geometry.Polygon(
        [[[149.1119063550977, -35.21104403446435],
          [149.11731178442946, -35.22317830810074],
          [149.12632363455316, -35.235238912694896],
          [149.1434042451702, -35.23425589042167],
          [149.1436835232536, -35.223841600898176],
          [149.1433190971777, -35.21118383661413],
          [149.14469170371615, -35.18811277607007],
          [149.13138793612154, -35.18818364989447],
          [149.12134580359398, -35.18958583728357]]]),
    aoi_2 = 
    ee.Geometry.Polygon(
        [[[148.94836853016415, -35.219220491535644],
          [148.96004150379696, -35.276417837365265],
          [149.04175231922665, -35.3307739470321],
          [149.1001171873907, -35.27361498650361],
          [148.97034118641415, -35.208000594872935]]]),
    geometry = 
    ee.Geometry.Polygon(
        [[[148.82829009658553, -35.110536045139284],
          [148.67448150283553, -35.88866803378386],
          [148.98062637040647, -35.917974542761286],
          [149.28696929580428, -35.93983027031052],
          [149.44352447158553, -35.139739533100666],
          [148.92442046767928, -35.108289189306234]]]),
    geometry2 = 
    ee.Geometry.Polygon(
        [[[148.81479084916316, -35.28752016927877],
          [149.0207845015069, -35.72240002362171],
          [149.14026081986628, -35.71682526046451],
          [149.17047322221003, -35.42640071411601],
          [148.94525349564753, -35.21350253672814]]]),
    ACT_VEGBOUND = 
    ee.Geometry.Polygon(
        [[[148.80998433060847, -35.29704783012935],
          [149.05992329545222, -35.71403773262223],
          [149.09837544388972, -35.71961269079874],
          [149.09562886185847, -35.602456699024415],
          [149.17527974076472, -35.59799021561819],
          [149.15330708451472, -35.4683538180112],
          [149.2123585981866, -35.35307018749132],
          [149.35243428178035, -35.36874948969099],
          [149.41972554154597, -35.31049673610865],
          [149.29338276810847, -35.24322985703525],
          [149.22059834428035, -35.210697510363424],
          [149.20961201615535, -35.16580391048749],
          [149.12858784623347, -35.11526897213073],
          [148.87590229935847, -35.262294477952004]]]),
    LQN = ee.Geometry.Polygon(
        [[[149.10941487283642, -35.38969202031002],
          [149.10967236490185, -35.38970514004468],
          [149.1096830937379, -35.389490850778145],
          [149.1094470593446, -35.389490850778145]]]),
    HQN = ee.Geometry.Polygon(
        [[[149.0435720803087, -35.29604149005351],
          [149.0440548779314, -35.296032733418315],
          [149.0440548779314, -35.295673710559676],
          [149.04363645332506, -35.295673710559676]]]),
    EXO = ee.Geometry.Polygon(
        [[[149.2297814712063, -35.329886632792046],
          [149.22978147114125, -35.3299675978516],
          [149.23010333622304, -35.32999385673495],
          [149.23010870064107, -35.329740020505234],
          [149.2298082932314, -35.32971376153942]]]);
//-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
var ACT_boundary = ee.Geometry.Polygon(
        [[[148.82829009658553, -35.110536045139284],
          [148.67448150283553, -35.88866803378386],
          [148.98062637040647, -35.917974542761286],
          [149.28696929580428, -35.93983027031052],
          [149.44352447158553, -35.139739533100666],
          [148.92442046767928, -35.108289189306234]]]);


// FIELD was a manually created polygon containing majority of the reference data points
/*
var FIELD = ee.Geometry.Polygon(
        [[[149.1019590046573, -35.121758791187766],
          [148.9371640827823, -35.21774068699828],
          [149.1253049519229, -35.42894922912131],
          [149.30795265700104, -35.286710205738736],
          [149.14384438063385, -35.12288204113921]]]);
Map.addLayer(FIELD)
*/

//return to the "FIELD"above if this one below didnt work 
var FIELD =ACT_VEGBOUND
//set map center object
Map.centerObject(FIELD, 10)

//polygon limited to canopy cover data, used for clipping other data
//var polygonClip = ee.FeatureCollection("projects/ee-racrabbe3/assets/ACT_canopyCover_ROI")//.bounds(1000) 

//boundary of ACT
var ACT_boundOfficial =ee.FeatureCollection('projects/ee-racrabbe3/assets/ACT-BOUNDARY')          
//Map.addLayer(ACT_boundary, {}, 'ACT')
//Map.addLayer(ACT_boundOfficial)

//this is the ACT lowland vegetation shapefile, can be used to filter the satellite imagery
//created 2nd March 2025, more recent than the "FIELD" above. The "FIELD" was used to create the first probability maps
var fcol = ee.FeatureCollection("projects/ee-racrabbe3/assets/ACTGOV_Lowland_Vegetation_Map_2023")
//var fcol = fcol.bounds()
//Map.addLayer(fcol)

//second "FIELD" created more recently on 2 March 2025; so mute the first "FIELD" above
var fcol2 = fcol.map(function features(f){return f.convexHull()})
//Map.addLayer(fcol2)
var FIELD3 =fcol2.geometry()
//print(FIELD2)
//Map.addLayer(FIELD3)

//var FIELD = fcol.geometry().convexHull()
//Map.addLayer(FIELD)

//var fcol4 = fcol3.simplify({'maxError': 0.5})
//Map.addLayer(fcol4)

//Map.addLayer(DEM)
//Map.addLayer(DEM.clip(fcol3))

//var fcol5 = fcol.geometry().convexHull()
//Map.addLayer(fcol5)

//----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


//load up data and required libraries
var elevation = ee.Image("projects/ee-racrabbe3/assets/ACT_DEM_2020_10m_GDA20").select('b1').rename('elevation')
//var elevation = actLiDAR_DEM
//print(elevation, 'elevation')
var jrcImage = ee.Image("JRC/GSW1_0/GlobalSurfaceWater")
//var composite = require('users/fitoprincipe/geetools:composite')
//var funcHLS = require('users/geeberra/Modules:HLS_Module_v2');
//var dem = ee.Image('projects/ee-racrabbe3/assets/ACT_DEM_2020_10m_GDA20')

//image = covariates.addJRCAndTopo(image);
//image = covariates.addCovariates(image);

//********************************************************************************************************************


//****LOAD REQUIRED MODULES AND DATA*******************************************************************************************************************
var covariates = require("users/servirmekong/mrc:covariate_module");
var composite = require('users/fitoprincipe/geetools:composite')
var funcHLS = require('users/geeberra/Modules:HLS_Module_v2');


var bandIn_S2 = [ 'B2',  'B3',  'B4',  'B8', 'B11',    'B12'];
    
//BandOut will have the same name for all the sensors
var bandOut = ['blue','green','red','nir','swir1','swir2'];

//bands to use later to filter collection for reducer analysis
var bandOut_2 = ['blue','green','red','nir','swir1','swir2', 'ND_green_swir1','ND_nir_red','ND_nir_swir2'];

// Harmonized Sentinel-2 Level 2A collection.
var s2 = ee.ImageCollection('COPERNICUS/S2_SR_HARMONIZED');
var csPlus = ee.ImageCollection('GOOGLE/CLOUD_SCORE_PLUS/V1/S2_HARMONIZED');

var QA_BAND = 'cs_cdf';
var CLEAR_THRESHOLD = 0.70;

//**************************************************************************************************************************
//****GET IMAGE COLLECTION ******************************************************
//Make image collection for each year
var S2Col = s2
    .filterBounds(ACT_boundary)
    //.filterDate('2019-06-01', '2020-06-01')
    .filter(ee.Filter.eq('SPACECRAFT_NAME', 'Sentinel-2A'))//.eq('SPACECRAFT_NAME', 'Sentinel-2A')
    .linkCollection(csPlus, [QA_BAND])
    .map(function(img) {
      return img.updateMask(img.select(QA_BAND).gte(CLEAR_THRESHOLD).clip(FIELD));
      //return img.updateMask(img.select(QA_BAND).gte(CLEAR_THRESHOLD));
    }).select(bandIn_S2, bandOut);

var collection2019 = S2Col.filterDate('2021-06-01', '2022-06-01') //***
//Map.addLayer(collection2019, {min:0, max:2500, bands:['red', 'green', 'blue']}, 'collection2019')

//Map.addLayer(FIELD)
//Map.addLayer(ACT_VEGBOUND,{}, "ACT vegetation boundary drawn by Richard")
//Map.addLayer(FIELD3)

//***BRDF COLLECTION AND CLIP TO ROI***************************************************************************************

//make BRDF layers and clip To ROI
var imgS2019_BRDF = collection2019.map(funcHLS.applyBRDF);
//var imgS2020_BRDF = collection2020.map(funcHLS.applyBRDF);
//var imgS2021_BRDF = collection2021.map(funcHLS.applyBRDF);
//var imgS2022_BRDF = collection2022.map(funcHLS.applyBRDF);
//var imgS2023_BRDF = collection2023.map(funcHLS.applyBRDF);

//print(imgS2019_BRDF, 'imgS2019_BRDF')
//Map.addLayer(imgS2019_BRDF, {min:0, max:2500, bands:['red', 'green', 'blue']}, 'imgS2019_BRDF')

//---1.compute the medoid bands //'EPSG:7855'
var s2col2019_medoid = composite.medoid(imgS2019_BRDF).reproject({crs:'EPSG:32755',crsTransform:[10,0,600000,0,-10,6100000]}).select(bandOut)
//print(s2col2019_medoid, 's2col2019_medoid')
//Map.addLayer(s2col2019_medoid, {bands:['red', 'green', 'blue'], min:0, max:2500}, 's2col2019_medoid')




//---2. apply the covariates function to generate additional covariates
var imgS2019_BRDF_2 = imgS2019_BRDF.map(covariates.addCovariates).select(bandOut_2)
//print(imgS2019_BRDF_2, "imgS2019_BRDF_2")

//standard deviation composites for 2019
var s2col2019_sd = imgS2019_BRDF_2.reduce(ee.Reducer.stdDev())
.reproject({crs:'EPSG:32755',crsTransform:[10,0,600000,0,-10,6100000]});
//print(s2col2019_sd, 's2col2019_sd'); //***SELECT



//---3. the percentiles composite for 2019
//set up a list to select relevant bands only 
var list1 = ee.List.sequence(0,47) //list of bands to be selected out of the 72
//var s2col2019_percentiles2 = s2col2019_percentiles2.select(list1)
//print(s2col2019_percentiles2, 's2col2019_percentiles2')
var imgS2019_BRDF_ACT = imgS2019_BRDF.map(covariates.addCovariates)
var s2col2019_percentiles = imgS2019_BRDF_ACT.reduce(ee.Reducer.percentile([20,80]))
.reproject({crs:'EPSG:32755',crsTransform:[10,0,600000,0,-10,6100000]}).select(list1);
//print(s2col2019_percentiles, 's2col2019_percentiles')
//Map.addLayer(s2col2019_percentiles, {bands:["red_p80", "green_p80","blue_p80"]}, "s2col2019_percentiles")


/*
Export.image.toAsset({
  image: s2col2019_medoid,
  description: 's2col2021_medoid_2',
  assetId: 'users/racrabbe/covariate_s2col2021_medoid_2',  
  //scale:10,
  region: FIELD,
  crs: 'EPSG:7855',
  crsTransform: [1,0,658000,0,-1,6112000], //[10,0,600000,0,-10,6100000],
  maxPixels:1e13
  //shardSize: 2560
});

*/

//--------------------------------------------------------------------------------------------------------

//CANOPY COVER
//var canopyc = ee.Image("projects/ee-racrabbe3/assets/ACT_Canopy_Cover_2020_1m_GDA2020")
//print(canopyc, 'canopy cover')

//mask out the tree cover pixels
//var noCanopy = canopyc.updateMask(canopyc.select('b1').eq(0)).clip(ACT_boundOfficial)
//Map.addLayer(canopyc.clip(ACT_boundary), {min:0, max:1, palette:['blue', 'red']}, 'canopyc')
//Map.addLayer(noCanopy, null, 'canopyc')
//Map.addLayer(field_data)

//--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//*************************************************************************************************

//***TOPOGRAPHICAL VARIABLES
var topoBands = ["elevation","slope", "aspect","eastness","northness"]
var topo = covariates.addJRCAndTopo(elevation).select(topoBands)
//print(topo, 'topo')
Map.addLayer(topo)



//------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

//***PHENOLOGICAL VARIABLES FROM SENTINEL-1
//Aim: visualise the timeseries profile for EXO, HQN, LQN
var trSet = ee.FeatureCollection("projects/ee-racrabbe3/assets/ACT-GRASSLAND-TRAININGSET-UNEQUAL-CLASS-gee-use-only")
//Map.addLayer(trSet, {color:"red"}, "Training Set from R")

var trSet2 = trSet.remap(["EXO","HQN","LQN"], [0, 1,2], "class")

// function to conditionally set properties of feature collection
var featureProperties = function(f){ 
  var getProperty = f.get("class") 
  var mapColours = ee.List(['red', 'green', 'blue']); 
  
  // use the class as index to lookup the corresponding display color
  return f.set({style: {color: mapColours.get(getProperty)}})
}

// apply the function and view the results on map
var styled =  trSet2.map(featureProperties)
Map.addLayer(styled.style({styleProperty: "style"}), {}, 'Training Data Points in Colours')


//var tsSet = ee.FeatureCollection ("projects/ee-racrabbe3/assets/ACT-GRASSLAND-TESTINGSET-UNEQUAL-CLASS-gee-use-only")
//Map.addLayer(tsSet,{color:"yellow"}, "Testing Set from R")

//*****************************************************************************************************************************************************************************************************************************************
//Get S1 collection
var s1Col = ee.ImageCollection("COPERNICUS/S1_GRD_FLOAT")
.filterBounds(ACT_boundary)
.filterDate('2019-06-01', '2024-06-01')
.filter(ee.Filter.eq('instrumentMode', 'IW'))
.filter(ee.Filter.eq('orbitProperties_pass', 'DESCENDING'))
.map(function(image){return image.clip(LQN)})//FIELD
.select('VH');


//S1-Collection for each year
//var s1Col2018 =s1Col.filterDate('2018-06-01', '2019-06-01')
//var s1Col2019 =s1Col.filterDate('2019-06-01', '2020-06-01')
//var s1Col2020 =s1Col.filterDate('2020-06-01', '2021-06-01')
//var s1Col2021 =s1Col.filterDate('2021-06-01', '2022-06-01')
//var s1Col2022 =s1Col.filterDate('2022-06-01', '2023-06-01')
//var s1Col2023 =s1Col.filterDate('2023-06-01', '2024-06-01')

//print(s1Col2019, 's1Col2019')
//Map.addLayer(s1Col2019, null, 'Sentinel-1')

//-----TIME SERIES ANALYSIS OF SENTINEL-1 SAR IMAGERY 
// This field contains UNIX time in milliseconds.
var timeField = 'system:time_start';

// Use this function to add variables for VH, time and a constant to S1 imagery.
var addVariables = function(image) {
  // Compute time in fractional years since the epoch.
  var date = ee.Date(image.get(timeField));
  var years = date.difference(ee.Date('1970-01-01'), 'year');
  // Return the image with the added bands.
  return image
    // Add an NDVI band.
    //.addBands(image.normalizedDifference(['B5', 'B4']).rename('NDVI')).float()
    // Add a time band.
    .addBands(ee.Image(years).rename('t').float())
    // Add a constant band.
    .addBands(ee.Image.constant(1));
};

//****AMPLITUDE & PHASE 2019**************************************************************************************************

// Now add variables 
var filteredSentinel = s1Col//s1Col2023 
  //.filterBounds(roi)
  //.map(maskClouds)
  .map(addVariables);


// Plot a time series of VH at a single location.
var s1Chart = ui.Chart.image.series(filteredSentinel.select('VH'), LQN)//FIELD >> EXO
    .setChartType('ScatterChart')
    .setOptions({
      title: 'S1 VH time series at ROI',
      trendlines: {0: {
        color: 'CC0000'
      }},
      lineWidth: 1,
      pointSize: 3,
    });
print(s1Chart);



// Linear trend ----------------------------------------------------------------
// List of the independent variable names
var independents = ee.List(['constant', 't']);

// Name of the dependent variable.
var dependent = ee.String('VH');

// Compute a linear trend.  This will have two bands: 'residuals' and 
// a 2x1 band called coefficients (columns are for dependent variables).
var trend = filteredSentinel.select(independents.add(dependent))
    .reduce(ee.Reducer.linearRegression(independents.length(), 1));
// Map.addLayer(trend, {}, 'trend array image');

// Flatten the coefficients into a 2-band image
var coefficients = trend.select('coefficients')
  .arrayProject([0])
  .arrayFlatten([independents]);

// Compute a de-trended series.
var detrended = filteredSentinel.map(function(image) {
  return image.select(dependent).subtract(
          image.select(independents).multiply(coefficients).reduce('sum'))
          .rename(dependent)
          .copyProperties(image, [timeField]);
});


// Plot the detrended results, an example using CRACE
var detrendedChart = ui.Chart.image.series(detrended, LQN, null, 20) //FIELD >> EXO
    .setOptions({
      title: 'Detrended S1 time series at ROI',
      lineWidth: 1,
      pointSize: 3,
    });
print(detrendedChart);



// Harmonic trend ----------------------------------------------------------------
// Use these independent variables in the harmonic regression.
var harmonicIndependents = ee.List(['constant', 't', 'cos', 'sin']);

// Add harmonic terms as new image bands.
var harmonicS2 = filteredSentinel.map(function(image) {
  var timeRadians = image.select('t').multiply(2 * Math.PI);
  return image
    .addBands(timeRadians.cos().rename('cos'))
    .addBands(timeRadians.sin().rename('sin'));
});


// The output of the regression reduction is a 4x1 array image.
var harmonicTrend = harmonicS2
  .select(harmonicIndependents.add(dependent))
  .reduce(ee.Reducer.linearRegression(harmonicIndependents.length(), 1));
  
  // Turn the array image into a multi-band image of coefficients.
var harmonicTrendCoefficients = harmonicTrend.select('coefficients')
  .arrayProject([0])
  .arrayFlatten([harmonicIndependents]);

//print(harmonicTrendCoefficients, 'harmonicTrendCoefficients')

// Compute fitted values.
var fittedHarmonic = harmonicS2.map(function(image) {
  return image.addBands(
    image.select(harmonicIndependents)
      .multiply(harmonicTrendCoefficients)
      .reduce('sum')
      .rename('fitted'));
});



// Plot the fitted model and the original data, CRACE as an example.
print(ui.Chart.image.series(
  fittedHarmonic.select(['fitted','VH']), LQN, ee.Reducer.mean(), 10) //FIELD >>EXO
    .setSeriesNames(['VH', 'fitted'])
    .setOptions({
      title: 'Harmonic model: original and fitted values',
      lineWidth: 1,
      pointSize: 3,
}));



// Compute phase and amplitude.
var phase2019 = harmonicTrendCoefficients.select('cos').atan2(
            harmonicTrendCoefficients.select('sin')).rename('phase2019')//.reproject('EPSG:7855', [10,0,659891,0,-10,6111102]).rename('phase2019').clip(CRACE_2);
            
var amplitude2019 = harmonicTrendCoefficients.select('cos').hypot(
                harmonicTrendCoefficients.select('sin')).rename('amp2019')//.reproject('EPSG:7855', [10,0,659891,0,-10,6111102]).rename('amp2019').clip(CRACE_2); //may have to log transform for visualisation purposes

//print(amplitude2019, 'amplitude2019') 
var phAmp_2019 = phase2019.addBands(amplitude2019)
//print(phAmp_2019, 'phAmp_2019') //***SELECT
//Map.addLayer(phAmp_2019, {bands: ["phase2019", "phase2019", "amp2019"]}, 'phAmp2019')


//EXPORT S1 PHENOLOGY BANDS (PHASE AND AMPLITUDE) 
Export.image.toAsset({
  image: phAmp_2019,
  description: 'phAmp_2023_phaseAndAmplitude',
  assetId: 'projects/ee-racrabbe3/assets/covariate_phAmp2023',
  //scale:10,
  region: FIELD,
  crs: 'EPSG:7855',
  crsTransform: [1,0,658000,0,-1,6112000], //[10,0,600000,0,-10,6100000],
  maxPixels:1e13
  //shardSize: 2560
});


```





