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

A plot is usually composed of exotic and native (i.e., low, moderate and high quality) species of different proportions. Plots dominated by a species are selected to improve the predictability. A dominant species must cover a minimum of 50% of the plot. For instance if a plot is composed of 50% exotic, 30% low-quality native, and 20% high-quality native grassland, the plot is assigned to the 'exotic' class. The high quality native and moderate quality native plots were merged to align with the interests of land managers, producing three grass classes- high quality native, low quality native and exotic. These grass classes were detected and mapped in this project. The labelled data was used to build, train and validate the machine learning classifier.

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


In this project, the Sentinel-2 spectral bands were used as they provide high resolution imagery and are suited for vegetation monitoring. The Sentinel-2 imagery over the study areas acquired from 2019 to 2023 was used as this date aligns with the field observation data. To ensure that the electromagnetic energy recorded by the sensor was reflected off the targets of interest, the Bottom of the Atmosphere (BoA) Sentinel-2 imagery retrieved from the Copernicus Open Access Hub via Google Earth Engine was used. A Sentinel-2 image tile is approximately 110km x 110km, the study area was completely covered by four different image tiles. The number of Sentinel-2 images varied between the annual vegetation growth calendars (Jun-May) in that 216, 216, 214, 212, and 222 images for 2019, 2020, 2021, 2022 and 2023, respectively, were used. Despite the Sentinel-2 BOA products are potentially free from atmospheric effects, additional imgage preprocessing was conducted to deal with cloud cover, cloud shadow and distortions due to sun-satellite viewing angle.   


#### Cloud and cloud shadow masking

Cloud cover, cloud shadow and other atmospheric effects in the imagery were corrected by identifying and masking the affected pixels using the Sentinel-2-specific quality assessment, Cloud Score+ product develoed by Google [Pasquarella et al. (2023)](https://ieeexplore.ieee.org/document/10208818). The cumulative distribution function of possible cloud score values not lower than 70% were used as the threshold for retaining cloud-free pixels. The Harmonized Landsat and Sentinel-2 (HLS) GEE module by [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) was used for further image processing. 

#### BRDF correction

The nadir view angles of the Sentinel-2 satellites is not temporally invariant, causing directional reflection on surface materials which can be accounted for via a bidirectional reflectance distribution function (BRDF) [Roy et al. (2017)](https://doi.org/10.1016/j.rse.2017.06.019). The BRDF within the HLS module [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) was applied to minimise errors in the imagery due to temporal variations in the sun-sensor viewing geometry. 

#### Sentinel-2 image composites 

Since the Sentinel-2 satellites acquire data at varied native spatial resolutions, the imagery obtained at spectral bands with 20m resolution was spatially downscaled to 10m using the nearest neighbour geometric resampling method to preserve the original reflectance values and harmonise the data. The Sentinel-2 has 13 spectral bands, but only the blue, green, red, nir, swir1 and swir2 were used. In this study, one year of images is regarded as a composite, thus, five different image composites were analysed since the study period spans 2019-2023.

#### Sentinel-2 covariates

The standard deviation and mediod were computed for the blue, green, red, nir, swir1, and swir2 bands. The medoid is analogous to the univariate median, however, it is more insensitive to outliers and applicable to multi-dimensional data such as multispectral imagery. Further details on medoid is given in ([Flood, 2013](https://doi.org/10.3390/rs5126481)). In this study, annual is defined as the period from June to May the following year to mark the phenological growth calendar of the plants. Given the growth pattern may vary between years, the medoid of the 20th and 80th percentiles were included in the yearly compsite. The medoid was computed using the GEE composite module developed by [Principe (2019)](https://github.com/fitoprincipe/geetools-code-editor). Additionally, we computed the standard deviation of the normalised difference for the nir and swir2, green and swir, and nir and red. The bands in the Sentiel-2 composites were used to calculate additional covariates (Table 3). The ND prefixing some of the covariates represents the normalised difference between the first and second bands computed as |NDVI|$${band1-band2}\over{band1+band2}$$|, while  p20 and p80 refer to the 20th and 80th percentiles, respectively. Amongst the ND bands are widely used spectral indices, such as Normalised Difference Vegetation Index (NDVI, [Rouse et al., 1973](https://ntrs.nasa.gov/citations/19740022614)), Normalised Difference Water Index ([NDWI, McFeeters, 1996](https://doi.org/10.1080/01431169608948714)) and ([Gao, 1996](https://doi.org/10.1016/S0034-4257(96)00067-3)), and Normalised Burn Ratio ([NBR, Key and Benson, 199](https://www.frames.gov/catalog/3356)). The other spectral indices included were the soil-adjusted vegetation index (SAVI), enhanced vegetation index (EVI) and index-based built-up index (IBI). Table 2 details the formulae and principal references of these additional spectral indices.  


*Table 2. The equations and references for soil-adjusted vegetation index (SAVI), enhanced vegetation index (EVI) and index-based built-up index (IBI).*

|Index|Formula|Reference| 
|:----|:----|:---|
|SAVI|$$\left({NIR-Red}\over{NIR+Red+0.5}\right)×{1.5}$$|[Huete, 1998](https://doi.org/10.1016/0034-4257(88)90106-X)|
|EVI |$$\left({NIR-Red}\over{NIR+6×Red-7.5×Blue+1}\right)× {2.5}$$|[Huete et al., 2002](https://doi.org/10.1016/S0034-4257(02)00096-2)|
|IBI |$$\left({NIR}\over{NIR+Red}\right) + \left({Green}\over{Green+SWIR1}\right)$$|[Xu, 2008](https://doi.org/10.1080/01431160802039957)|



Sixty-three covariates were obtained from an annual Sentinel-2 composite. Table 3 shows these covariates for the 2019 composite only. The same number of covariates were obtained for 2020, 2021, 2022 and 2023, but have not been shown.

*Table 3. Covariates for 2019 only. The cohorts of the covariates derived from the Sentinel-2 imagery are spectral features (SP), spectral indices (SI), and statistic (STA). The phenology covariates (PHE) were derived from Sentinel-1, topographical covariates (TOP) were from the ACT LiDAR data and the spatial coordinates of the reference data representing the longitude and latitude (LL) covariates were used to account for spatial autocorrelation.*

|Covariate|Cohort|
|:----|:----|
|blue|SP|
|green |SP|
|red|SP|
|nir|SP|
|swir1|SP|
|siwr2 |SP|
|blue_p20|SP|
|blue_p80 |SP|
|green_p20|SP|
|green_p80|SP|
|red_p20|SP|
|red_p80|SP|
|nir_p20 |SP|
|nir_820 |SP|
| swir1_p20|SP|
| swir1_p80|SP|
|swir2_p20 |SP|
| swir2_p80|SP|
|ND_blue_green_p20 |SI|
| ND_blue_green_p80|SI|
|ND_blue_red_p20 |SI|
| ND_blue_red_p80|SI|
|ND_blue_nir_p20 |SI|
|ND_blue_nir_p80 |SI|
| ND_blue_swir1_p20|SI|
|ND_blue_swir1_p80 |SI|
| ND_blue_swir2_p20|SI|
|ND_blue_swir2_p80 |SI|
|ND_green_red_p20 |SI|
|ND_green_red_p80 |SI|
| ND_green_nir_p20|SI|
| ND_green_nir_p80|SI|
| ND_green_swir1_p20|SI|
|ND_green_swir1_p80 |SI|
|ND_green_swir2_p20 |SI|
|ND_green_swir2_p80 |SI|
|ND_red_swir1_p20 |SI|
| ND_red_swir1_p80|SI|
| ND_red_swir2_p20|SI|
| ND_red_swir2_p80|SI|
| ND_nir_red_p20|SI|
|ND_nir_red_p80 |SI|
| ND_nir_swir1_p20|SI|
|ND_nir_swir1_p80 |SI|
|ND_nir_swir2_p20 |SI|
|ND_nir_swir2_p80 |SI|
|ND_swir1_swir2_p20 |SI|
| ND_swir1_swir2_p80|SI|
|EVI_p20 |SI|
|EVI_p80 |SI|
| SAVI_p20|SI|
| SAVI_p80|SI|
| IBI_p20|SI|
|IBI_p80 |SI|
|blue_stdDev |STA|
| green_stdDev|STA|
|red_stdDev|STA|
| nir_stdDev|STA|
| swir1_stdDev|STA|
|swir2_stdDev |STA|
| ND_green_swir1_stdDev|STA|
|ND_nir_red_stdDev |STA|
| ND_nir_swir2_stdDev|STA|
| phase2019|PHE|
| amp2019|PHE|
| elevation|TOP|
|slope |TOP|
|aspect |TOP|
| eastness|TOP|
| northness|TOP|
|longitude |LL|
| latitude|LL|



### Sentinel-1

Sentinel-1 is another Earth observation satellite mission operated by the ESA, launched into orbit in 2013, to monitor the environment from space regardless of atmospheric and weather conditions. The Sentinel-1 carries a sensor that transmits and records microwave energy that bounces off environmental targets, including grasslands. Sentinel-1 is a synthetic aperture radar system that measures the amplitude and phase of microwave energy in multiple polarisations. Because the Sentinel-1 uses artificial microwave energy, it can penetrate cloud cover and take photos of the Earth anytime. Thus, the Sentinel-1 complements the Sentinel-2 for continuous mapping of the environment while providing spectral information that characterises the variations in structural and moisture conditions of the vegetation ([Saatchi et al., 1995](https://doi.org/10.1029/95JD00852)). The Sentinel-1 typically transmits the microwave energy in vertical orientation and records the return signal in vertical and horizontal orientations, making the Sentinel-1 a dual-polarisation system in that the data comprises VV and VH polarisation bands. The Sentinel-1 sensor can be operated in four different modes; the imagery obtained from the interferometric wide swath mode (IW) is recommended and available for land monitoring ([Prats-Iraola et al., 2015](https://doi.org/10.1109/IGARSS.2015.7327018)). This study used imagery from the IW mode that was already pre-processed to a ground range detected product (i.e., analysis ready Sentinel-1 data) by the ESA and was retrievable from the GEE data catalog. The swath width of the Sentinel-1 is 250 km, so a total of 412 images were obtained for the five years (2019-2023). The pixel size of the ground range detected Sentinel-1 imagery is 10m, and this is created from single look complex imagery by applying a multi-look algorithm. Further preprocessing steps, such as thermal noise removal, radiometric calibration and terrain correction were performed before making the data available in GEE. Given the physical structure of the vegetation canopy is more sensitive to the VH polarisation, only this band was used in this study. The inherent speckle noise associated with the Sentinel-1 imagery was not filtered out, as spatial filtering algorithms lower the spectral and spatial variability required to differentiate pixels. 

#### Phenology covariates from the Sentinel-1

The biophysical conditions of plant species, including annual and perennial grasses, change through the growth calendar. While perennial grasses may be photosynthetically active throughout the year, annual grasses may disappear during the dry or low rainfall periods. The growth phenology of the plants can be vital information to differentiate between grass types. Sentinel-1, in contrast to the optical Sentinel-2 imagery, is not affected by cloud cover or shadow; thus, multitemporal Sentinel-1 data was anlysed to extract phenological information about the species. A Fourier harmonics function was applied to the Sentinel-1 time series data to compute amplitude and phase bands in which the amplitude explains the variance in the original time series and the phase angle denotes the time associated with the peak of the curve ([Jakubauskas et al., 2001](https://www.asprs.org/wp-content/uploads/pers/2001journal/april/2001_apr_461-470.pdf)). The amplitude and phase bands were adjusted to spatially align with the regions of interest and the Sentinel-2 data. The Sentinel-1 pixels that were not grassland were masked using the methods discussed in the section below (i.e., producing grassland layer). Annual composites of the Sentinel-1 imagery were created to extract the phenological information of the plants. Table 3 shows the amplitude and phase covariates indicative of plant phenology for 2019 only. [Poortinga et al., (2019)](https://doi.org/10.3390/rs11070831) used a similar approach in a land cover classification project conducted in Myanmar.



### Topographic covariates

The ACT digital elevation model (DEM) derived from an aerial LiDAR survey was used to compute topographical variables, such as slope, aspect, sine of aspect and cosine of aspect. The sine of aspect measures deviation from east (eastness) and the cosine aspect explains deviation from north (northness). The pixel size of the DEM was 1m, so all topographical variables were geometrically corrected to 10m using the bilinear interpolation method to match the Sentinel-2 pixels and for easy import into GEE. Table 3 shows the topographic covariates- elevation, slope, aspect, eastness and northness. Note that the topographic covariates remained same regardless of the study year. 


### Additional covariates

The spatial coordinates of the reference plots were included as additional covariates to account for the sensitivity of the RF to spatial autocorrelation. In this study, we assumed that the reference label for sampling plots remained unchaged between years, meaning if plot **A** was labelled class **X** in 2019, the class ID will remain same in other years. The longitude and latitude in decimal degrees were the covariates and these remained same regardless of the study year.

There were 65 covariates per the yearly composite of Sentinel-2 and Sentinel-1 imagery, making a total of 325 covariates for the five years. Plus, the topographic variables and spatial coordinates of the reference plots, 332 covariates were used for the image classification analysis.

### Image classification using Random Forest 

Random Forest (RF) is a decision tree ensemble machine learning algorithm widely used for land cover monitoring as the RF is not limited by data structure and minimises overfitting the data [Breiman, 2000](https://doi.org/10.1023/A:1010933404324). Additionally, the RF is computationally less expensive to implement as only a few hyperparameters require tuning.  The RF randomly selects a proportion of the instances to train a decision tree while replacing the samples to be re-used in the next iteration. Sampling a subset of the instances with replacement to create decision trees, known as bootstrap aggregating (i.e., bagging). The RF creates multiple decision trees to avoid overfitting; the final decision tree is obtained through majority voting. Fig. 3 summarises how the RF classification algorithm functions. 



![image](https://github.com/user-attachments/assets/0ed0f4bc-d2a9-4bda-a6b8-60d0ad633234)|
|:--:|
| *Fig. 3. A conceptual diagram summarising how the Random Forest algorithm functions.*|



#### Producing grassland layer


The RF classification algorithm was used to classify the remote sensing imagery. A hierarchical approach was adopted to classify the image pixels into exotic, high quality and low quality native grasses. There were diferent surface types in the imagery, including tree cover, grass cover, shrub cover, water bodies, roads, buildings and open land. This can increase the uncertainty in the RF model, while the model may perform well discriminating grassland pixels only. To this end, an initial RF classification was performed to classify the imagery into three broad themes- water, artificial and grassland. The artificial class includes buildings, roads and concrete surfaces. In this RF classification, only limited covariates were used to avoid computational memory issues in GEE. The medoid and the standard deviation and percentiles (20th and 80th) of the medoid derived from the Sentinel-2 and the phenological variables from the Sentinel-1 were the covariates used. The ACT LiDAR canopy cover data was used to mask out trees and shrubs, leaving behind grasslands only. With the aid of a high-resolution RGB Google imagery, ACT LiDAR canopy cover and the Sentinel-2 imagery, reference data for water, artificial and grassland were collected using GEE. The reference data were polygons of similar dimensions, but given the spatial variability 25 polygons defining water, 27 for aritificial and 50 for grassland were used. Through the RF classification algorithm in GEE, the covariates and reference data were used to classify the image pixels into water, artificial and grassland. Details of the RF classification have been sacrificed here as this is covered in the sections below. The accuracy of the RF classification on unseen reference data for grassland was 98%. The grassland pixels were retrieved, masking out all other pixels. The grassland layer was used to refine the region of interest for the main RF classification analysis in the sections below.



#### Classifying the grassland layer




##### Data partitioning


The reference data collected by the ACT were used to randomly sample pixels for exotic (EXO), high-quality (HQN), and low-quality (LQN) grassland. The reference sample size was 3137, split into train and test sets, with 90% of the samples allocated for model training and the remaining 10% for evaluating the model's accuracy. The training and testing sample sizes were 2824 and 313, respectively (Table **4**).


*Table 4. The reference sample size for exotic, high-quality native and low-quality native grasses.*

|Grass|Training|Testing|Total|
|:----|:----|:---|:---|
|Exotic|1336|148|1484 |
|HQ native|1065|118|1183|
|LQ native|423|47|470|



##### Hyperparameter tuning 

The RF classification algorithm produces the best result and is more efficient if the optimal values for the hyperparameters are used. The RF classification algorithm in GEE was used, and despite this algorithm requires five hyperparameters (i.e, numberOfTrees, variablesPerSplit, minLeafPopulation, bagFraction and maxNodes) to run, the most important hyperparmeters requiring tuning are the number of trees to grow (*numberOfTrees*), and the number of covariates per split  (*variablesPerSplit*). Owing to computational reasons, the tuning of optimal values for *numberOfTrees* and *variablesPerSplit* were conducted in R environment. A grid search approach was used, the values for *variablesPerSplit* ranged from 1 to 332 while a set of values was specified for *numberOfTrees* (10,20,50,500). The *numberOfTrees* and *variablesPerSplit* values that produced an RF model with the highest accuracy were selected as the optimal values. The optimal values for *variablesPerSplit* and *numberOfTrees* were 89 and 500, respectively.

##### Cross validation and training of RF model

A good-fit model is a model capable of generalising effectively well to data that was not used to teach the model, so to assess this a 10-fold cross-validation strategy was employed in the R environment. The training dataset was randomly partitioned into 10 equally sized sub-samples called folds (Kohavi, 1995) and for every run of the cross-validation, one fold was reserved for validation, while the model was trained on the remaining nine folds. This process was repeated 10 times, varying the one-fold data for model validation in each iteration. Each of the ten folds was used exactly once for model validation. The model results from the 10-iterations were averaged to assess the generalisability of the model to unseen data. <br>

The RF classification model was trained using the 332 covariates and optimal hyperparameter values in probability mode in R and also GEE for the spatial representation of the grasses. 


##### Ranking the covariates

The covariates were assessed to remove redundant ones. Methods such as correlation analysis, principal component analysis and separability indices can be used to select the optimal predictor variables for RF models. However, in this study, we used the mean decrease impurity method ([Breiman, 2000](https://doi.org/10.1023/A:1010933404324)), which is built into the RF algorithm in the GEE and widely used in classification tasks. Once the top covariates were identified, a parsimonious RF model was created using these covariates. 










##### Evaluation of the Random Forest model

- accuracy based on training set (cross validation)

- accuracy based on test set


The test set was used to evaluate the accuracy of the RF classifier in that the user's accuracy, prouducer's accuracy, and F-1 score were computed from a confusion matrix table.  




## Results




## Discussion

### Phenogical growth profile of the grassland

Fig. 4 illustrates the potential of Sentinel-1 for monitoring the temporal changes in grassland growth. The different grassland classes showed variation in maximum growth and this was captured by the Sentinel-1. The exotic grassland showed consistenly high backscatter values, especially at maximum growth, than the native vegetation. The backscatter for high-quality native, at the maximum growth, was consistenly higher than the low-quality natives. This suggests the Sentinel-1 alone can be used to discriminate exotic grassland from low-quality and high-quality natives.



<img width="1108" height="592" alt="image" src="https://github.com/user-attachments/assets/d42afe98-634d-428f-95e0-f607d6dd1e04" />|
|:--:|
| *Fig. 4. A phenological growth profile for exotic, low-quality native and high-quality native grasslands. The profile was derived from the Sentinel-data.*|







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


## Stage 2- Random Forest CLASSIFICATION 1- Detecting grassland only areas 

```JavaScript
//this "FIELD" is a larger polygon of the one above as it includes all the vegetation zones of the ACT
var ACT_VEGBOUND = 
    /* color: #0b4a8b */
    /* shown: false */
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
          [148.87590229935847, -35.262294477952004]]]);

 Map.addLayer(ACT_VEGBOUND)         

var FIELD = ACT_VEGBOUND

//surface types of interest for the preliminary classification
var water = /* color: #0b4a8b */ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Polygon(
                [[[149.10842890405985, -35.29258035551193],
                  [149.10872931146952, -35.29254532746762],
                  [149.10879368448587, -35.292352672952994],
                  [149.1084718194041, -35.29233515888346]]]),
            {
              "class": 0,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.14485019415554, -35.305149093596164],
                  [149.14521497458156, -35.3050615370567],
                  [149.14519351690944, -35.3048514009754],
                  [149.14485019415554, -35.30483388961066]]]),
            {
              "class": 0,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.06717342108425, -35.23146305804654],
                  [149.0679029819363, -35.23146305804654],
                  [149.06777423590358, -35.230797020478384],
                  [149.06730216711696, -35.230797020478384]]]),
            {
              "class": 0,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.10778713877232, -35.18990379465765],
                  [149.10838795359166, -35.18983364980105],
                  [149.10847378428014, -35.18937770675717],
                  [149.10783005411656, -35.18937770675717]]]),
            {
              "class": 0,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1745686457025, -35.307819694346406],
                  [149.1754698679315, -35.30778467289809],
                  [149.1754698679315, -35.30746947918086],
                  [149.17461156104673, -35.30736441433555]]]),
            {
              "class": 0,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.99039853806823, -35.2613368400033],
                  [148.99051387305587, -35.26134122019718],
                  [148.99050850863784, -35.2612930380515],
                  [148.9904092669043, -35.26128865785501]]]),
            {
              "class": 0,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.0525729099697, -35.34118384397505],
                  [149.05310935502655, -35.341218851171085],
                  [149.05313081282878, -35.34076375644005],
                  [149.05268019898108, -35.34072874904687]]]),
            {
              "class": 0,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.04598900421638, -35.27061733209741],
                  [149.0461526189663, -35.27063266101907],
                  [149.0461928521015, -35.270531928052236],
                  [149.0460641060688, -35.27052535850657]]]),
            {
              "class": 0,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.13034214309755, -35.2924266145863],
                  [149.13042797378603, -35.29333734014752],
                  [149.13180126480165, -35.29333734014752],
                  [149.13171543411318, -35.292286502052]]]),
            {
              "class": 0,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.08006255390478, -35.22459885759561],
                  [149.08057753803564, -35.224668972426656],
                  [149.08072774174047, -35.22433592643962],
                  [149.08023421528173, -35.224248282531626]]]),
            {
              "class": 0,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.04990873155066, -35.32545432635777],
                  [149.05059537705847, -35.325559367704344],
                  [149.05050954637, -35.325174215433016],
                  [149.04986581620642, -35.32513920149919]]]),
            {
              "class": 0,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.05274114427039, -35.32398373317555],
                  [149.05317029771277, -35.32398373317555],
                  [149.05317029771277, -35.32352854415036],
                  [149.0526553135819, -35.3234585148421]]]),
            {
              "class": 0,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.044852591868, -35.32052446910592],
                  [149.04506716858918, -35.32052446910592],
                  [149.0451422704416, -35.32041066722115],
                  [149.0449062360483, -35.32037565122438]]]),
            {
              "class": 0,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.04424217116411, -35.321547425260086],
                  [149.0443092263895, -35.32154304832286],
                  [149.04430386197146, -35.3214970904676],
                  [149.04424485337313, -35.32150146740733]]]),
            {
              "class": 0,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.02866897544106, -35.29446309060955],
                  [149.02907667121133, -35.29453314502316],
                  [149.02922687491616, -35.294305467957216],
                  [149.02896938285073, -35.29418287234875],
                  [149.02867970427712, -35.2943492520581]]]),
            {
              "class": 0,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.14354363844643, -35.30680753952044],
                  [149.14560357496987, -35.30680753952044],
                  [149.14560357496987, -35.30442601670279],
                  [149.14371529982338, -35.30442601670279]]]),
            {
              "class": 0,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.07728234694252, -35.29924246001403],
                  [149.07985726759682, -35.29952266075695],
                  [149.08002892897377, -35.29812164734038],
                  [149.07762566969643, -35.29784144174647]]]),
            {
              "class": 0,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.21138789794634, -35.207404547403755],
                  [149.21128060958574, -35.20768506577805],
                  [149.21151664397905, -35.207676299593516],
                  [149.2116132035036, -35.20750974190768]]]),
            {
              "class": 0,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.20268901272573, -35.20156567698582],
                  [149.20287140293874, -35.20156567698582],
                  [149.20287140293874, -35.20146047478189],
                  [149.20267291947164, -35.20146047478189]]]),
            {
              "class": 0,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.21166773410323, -35.33676601224101],
                  [149.21185012431624, -35.336774764466846],
                  [149.2118233022261, -35.3366259764988],
                  [149.2116784629393, -35.336643480979845]]]),
            {
              "class": 0,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.21581821047482, -35.33466924199428],
                  [149.21604351603207, -35.33465173708561],
                  [149.21605424486813, -35.33453795508684],
                  [149.21586112581906, -35.33452482638435]]]),
            {
              "class": 0,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.21391384207425, -35.335579492020464],
                  [149.2140694101971, -35.335579492020464],
                  [149.21407477461514, -35.33545258277611],
                  [149.21393529974637, -35.33546571132788]]]),
            {
              "class": 0,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.08943051558225, -35.289303277279636],
                  [149.09097546797483, -35.28902304115614],
                  [149.09088963728635, -35.288042207084544],
                  [149.08943051558225, -35.28839250633143]]]),
            {
              "class": 0,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.10548085432737, -35.28671105612296],
                  [149.10711163740842, -35.286640994939745],
                  [149.10728329878538, -35.2855900699162],
                  [149.1057383463928, -35.28552000776293]]]),
            {
              "class": 0,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.0373215909034, -35.313151751246586],
                  [149.03779365969, -35.31308171295163],
                  [149.0376649136573, -35.3128190688054],
                  [149.03725721788703, -35.31287159770288]]]),
            {
              "class": 0,
              "system:index": "24"
            })]),
    artificial = /* color: #ffc82d */ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1647055225548, -35.19459268106922],
                  [149.16543508340686, -35.19452254026075],
                  [149.16543508340686, -35.19399648226698],
                  [149.16474843789905, -35.194031552905884]]]),
            {
              "class": 1,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1519167499718, -35.200037176517114],
                  [149.15215278436511, -35.200037176517114],
                  [149.15215278436511, -35.199870603163184],
                  [149.15193820764392, -35.199853069106055]]]),
            {
              "class": 1,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.14988899995654, -35.20050182669886],
                  [149.15013576318592, -35.20047552581617],
                  [149.15015722085803, -35.20032648731991],
                  [149.14993191530078, -35.20034402127485]]]),
            {
              "class": 1,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1901879981142, -35.3067465841972],
                  [149.19054204970416, -35.3067465841972],
                  [149.1905313208681, -35.3065364524925],
                  [149.19016654044208, -35.30656271898543]]]),
            {
              "class": 1,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.0449289694552, -35.27216599962112],
                  [149.0462593451266, -35.27216599962112],
                  [149.04634517581508, -35.27164044488575],
                  [149.04510063083217, -35.27157037066341]]]),
            {
              "class": 1,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.160102628588, -35.18414570948751],
                  [149.16008117091587, -35.1843561586057],
                  [149.16042449366978, -35.1843386212],
                  [149.16053178203038, -35.18416324693484]]]),
            {
              "class": 1,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.00040098399654, -35.2070258775798],
                  [149.00093742579952, -35.207078475094086],
                  [149.00095888347164, -35.20669275919818],
                  [149.0004653570129, -35.206657694025886]]]),
            {
              "class": 1,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.9940005105325, -35.22379175232757],
                  [148.99520214017116, -35.22379175232757],
                  [148.99533088620387, -35.222985419396544],
                  [148.99425800259792, -35.222985419396544]]]),
            {
              "class": 1,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.97990516388074, -35.21126612924336],
                  [148.97981933319227, -35.211792075385404],
                  [148.98089221679822, -35.21193232711451],
                  [148.9807634707655, -35.21140638188104]]]),
            {
              "class": 1,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.98256591522352, -35.21761231852491],
                  [148.9833383914198, -35.21768243939207],
                  [148.9833383914198, -35.21729677387304],
                  [148.98269466125623, -35.2171565314118]]]),
            {
              "class": 1,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1976574448454, -35.303102101092584],
                  [149.19881615913982, -35.30313712456792],
                  [149.19885907448406, -35.30275186550548],
                  [149.19808659828777, -35.30261177084615]]]),
            {
              "class": 1,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.0856061586029, -35.228220979318145],
                  [149.08614260040588, -35.22827356309976],
                  [149.08614260040588, -35.22788794790979],
                  [149.08567053161926, -35.22788794790979]]]),
            {
              "class": 1,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.0915499337799, -35.23252397273247],
                  [149.0918396123535, -35.23254149973384],
                  [149.09186107002563, -35.232374993067886],
                  [149.0916035779602, -35.232357466030535]]]),
            {
              "class": 1,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.17789847710856, -35.336917012602584],
                  [149.17901427605875, -35.33712706536842],
                  [149.17892844537027, -35.33607679607935],
                  [149.17781264642008, -35.335866740583576]]]),
            {
              "class": 1,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.20690924981363, -35.34062786441559],
                  [149.20793921807535, -35.34132800602468],
                  [149.2085400328947, -35.34048783536575],
                  [149.20716674187906, -35.339927716739645]]]),
            {
              "class": 1,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.201931069882, -35.35455954146718],
                  [149.20257480004557, -35.35448953904665],
                  [149.2024889693571, -35.354139526033805],
                  [149.20197398522623, -35.35410452464908]]]),
            {
              "class": 1,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.02783608865104, -35.30047897439929],
                  [149.02908063363395, -35.30072414635605],
                  [149.028908972257, -35.29988355369742],
                  [149.028007750028, -35.29974345407206]]]),
            {
              "class": 1,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.16134453190318, -35.39813148966216],
                  [149.1621599234437, -35.398166471955236],
                  [149.1621599234437, -35.39774668343664],
                  [149.16130161655894, -35.397641735965486]]]),
            {
              "class": 1,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.16426277531139, -35.39424836078767],
                  [149.16524982822887, -35.39459819988235],
                  [149.16533565891734, -35.393933504304826],
                  [149.16426277531139, -35.39361864659264]]]),
            {
              "class": 1,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.16992760075084, -35.391239681923274],
                  [149.17035675419322, -35.39141460818635],
                  [149.17082882297984, -35.391099740639646],
                  [149.17027092350475, -35.390574958663386],
                  [149.1696701086854, -35.39071490085761]]]),
            {
              "class": 1,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1327134475353, -35.27986272284499],
                  [149.1331426009777, -35.27988023961276],
                  [149.1331426009777, -35.27949486984638],
                  [149.13262761684683, -35.279599970873626]]]),
            {
              "class": 1,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.06520155908152, -35.237953345884044],
                  [149.0659740352778, -35.237953345884044],
                  [149.0659740352778, -35.237567776703955],
                  [149.06524447442575, -35.237567776703955]]]),
            {
              "class": 1,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.0777328395991, -35.232388703934674],
                  [149.07801178933664, -35.23239746745044],
                  [149.07795814515634, -35.23225725108446],
                  [149.07774356843515, -35.23227477814346]]]),
            {
              "class": 1,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.17787088684145, -35.323928260440866],
                  [149.17776359848085, -35.32417336133035],
                  [149.17819275192323, -35.324313418647876],
                  [149.1782785826117, -35.324050810978484]]]),
            {
              "class": 1,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.16688455871645, -35.32641424929541],
                  [149.1668201857001, -35.32660682270662],
                  [149.16722788147035, -35.326711862555754],
                  [149.16724933914247, -35.32650178272102]]]),
            {
              "class": 1,
              "system:index": "24"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.13330548836348, -35.36590916691213],
                  [149.1336702687895, -35.36594416317997],
                  [149.13369172646162, -35.36555920339932],
                  [149.13331621719954, -35.365576701611005]]]),
            {
              "class": 1,
              "system:index": "25"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.13245254589674, -35.36340689443884],
                  [149.13304263188002, -35.36338939575685],
                  [149.13309627606031, -35.36307441883244],
                  [149.13255983425734, -35.36305692007838]]]),
            {
              "class": 1,
              "system:index": "26"
            })]),
    vegetation = /* color: #00ffff */ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Polygon(
                [[[149.18869673349485, -35.27840233589061],
                  [149.18989836313352, -35.278297233309075],
                  [149.18989836313352, -35.27756151141914],
                  [149.18895422556028, -35.27752647687672]]]),
            {
              "class": 2,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.19719397165403, -35.27290178424585],
                  [149.19826685526, -35.272866747687836],
                  [149.19822393991575, -35.272306160698385],
                  [149.19740854837522, -35.27237623428423]]]),
            {
              "class": 2,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1820233974658, -35.286652462908215],
                  [149.18251692392454, -35.28668749350244],
                  [149.18245255090818, -35.28633718687814],
                  [149.1820233974658, -35.28637221760878]]]),
            {
              "class": 2,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.18356834985838, -35.28337703538722],
                  [149.18391167261228, -35.28339455139481],
                  [149.18391167261228, -35.28313181088317],
                  [149.18361126520261, -35.28313181088317]]]),
            {
              "class": 2,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.19052063562498, -35.282448681563004],
                  [149.19084250070676, -35.282466197771406],
                  [149.19084250070676, -35.28211587288334],
                  [149.19049917795286, -35.28206332401941]]]),
            {
              "class": 2,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.18959795572385, -35.28614451758871],
                  [149.19002710916624, -35.28614451758871],
                  [149.1900914821826, -35.28591681692827],
                  [149.18972670175657, -35.28591681692827]]]),
            {
              "class": 2,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.18262421228513, -35.271833162408406],
                  [149.18318211176023, -35.27188571791035],
                  [149.18318211176023, -35.271552865822194],
                  [149.1827100429736, -35.271552865822194]]]),
            {
              "class": 2,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.18376146890745, -35.26913526750913],
                  [149.1841477070056, -35.26913526750913],
                  [149.1841691646777, -35.268907519022115],
                  [149.18378292657957, -35.2688199232797]]]),
            {
              "class": 2,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.03475145310324, -35.21878620354976],
                  [149.0354810139553, -35.21889138330662],
                  [149.03556684464377, -35.218190182353105],
                  [149.03496602982443, -35.218085001687605]]]),
            {
              "class": 2,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.01483873337668, -35.21482433345392],
                  [149.01548246354025, -35.21482433345392],
                  [149.0155253788845, -35.21440359252834],
                  [149.01479581803244, -35.21436853068611]]]),
            {
              "class": 2,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.01393751114767, -35.22071447743533],
                  [149.01458124131125, -35.22074953653647],
                  [149.01458124131125, -35.22036388559094],
                  [149.01410917252463, -35.22036388559094]]]),
            {
              "class": 2,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.04028753250998, -35.22355421555835],
                  [149.0411029240505, -35.223519157668804],
                  [149.04101709336203, -35.22316857794039],
                  [149.0404162785427, -35.22299328750824]]]),
            {
              "class": 2,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1202163083708, -35.36203323636527],
                  [149.1206669194853, -35.362068234313334],
                  [149.1206669194853, -35.361630758871996],
                  [149.12015193535444, -35.361630758871996]]]),
            {
              "class": 2,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.99415374971932, -35.19510894278711],
                  [148.99561287142342, -35.19496866200111],
                  [148.9956987021119, -35.19363598245255],
                  [148.9942395804078, -35.1939165483848]]]),
            {
              "class": 2,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.9965999243409, -35.19907177490753],
                  [148.99758697725838, -35.19910684335533],
                  [148.9977157232911, -35.19851067768366],
                  [148.99702907778328, -35.19837040277206]]]),
            {
              "class": 2,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.96194668351112, -35.21204684765906],
                  [148.96278353376286, -35.21218709912218],
                  [148.96282644916036, -35.21169621794122],
                  [148.96222563359504, -35.21157349718223]]]),
            {
              "class": 2,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.2366925774249, -35.252005943169856],
                  [149.23705735785092, -35.252040988748576],
                  [149.23710027319515, -35.251778146538925],
                  [149.23664966208065, -35.25172557799474]]]),
            {
              "class": 2,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.22467628103817, -35.254073606391046],
                  [149.22506251913632, -35.254073606391046],
                  [149.2250410614642, -35.2538282931731],
                  [149.22467628103817, -35.253810770771985]]]),
            {
              "class": 2,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.22183313948238, -35.257840823277476],
                  [149.22205844503964, -35.257832062511106],
                  [149.2220691738757, -35.257674368554355],
                  [149.22186532599056, -35.257674368554355]]]),
            {
              "class": 2,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.22637143713558, -35.25719252400764],
                  [149.22661820036495, -35.257227567344],
                  [149.22667184454525, -35.25704358965911],
                  [149.22642508131588, -35.25704358965911]]]),
            {
              "class": 2,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.15716335210493, -35.30942920108417],
                  [149.15905162725142, -35.30949924254178],
                  [149.15905162725142, -35.30830852951456],
                  [149.15716335210493, -35.30809840186689]]]),
            {
              "class": 2,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1740719977348, -35.3436074602485],
                  [149.17604610356977, -35.3436074602485],
                  [149.17578861150434, -35.342697300651984],
                  [149.17398616704634, -35.34262728795062]]]),
            {
              "class": 2,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.16832134160688, -35.35389855140213],
                  [149.16960880193403, -35.353828548408636],
                  [149.1693513098686, -35.3528485001287],
                  [149.16814968022993, -35.35291850397167]]]),
            {
              "class": 2,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.19066087969736, -35.363888191562424],
                  [149.19143335589365, -35.36402818004724],
                  [149.19177667864756, -35.36357321658408],
                  [149.1909183717628, -35.363363232582465]]]),
            {
              "class": 2,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1875709749122, -35.36602298958003],
                  [149.18825762042002, -35.366162974362965],
                  [149.1883434511085, -35.36553304092813],
                  [149.1877855516334, -35.36546304802083]]]),
            {
              "class": 2,
              "system:index": "24"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.19555322894053, -35.36882263911575],
                  [149.19645445116953, -35.3689276240844],
                  [149.1964115358253, -35.36843769306242],
                  [149.19572489031748, -35.36829771222422]]]),
            {
              "class": 2,
              "system:index": "25"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.17626278193802, -35.36995996878476],
                  [149.17703525729698, -35.36995996878475],
                  [149.17703525729698, -35.36950503924612],
                  [149.17617695134254, -35.369540033917055]]]),
            {
              "class": 2,
              "system:index": "26"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1722072816749, -35.36602298958003],
                  [149.17319433459238, -35.36602298958003],
                  [149.17319433459238, -35.36560303377475],
                  [149.1725506044288, -35.36542805154441]]]),
            {
              "class": 2,
              "system:index": "27"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.11514349780782, -35.355388372610356],
                  [149.11559410892232, -35.35549337504971],
                  [149.11574431262716, -35.35523086869534],
                  [149.11529370151266, -35.35500336249797]]]),
            {
              "class": 2,
              "system:index": "28"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.12089415393575, -35.36135579462564],
                  [149.12123747668966, -35.361425791093936],
                  [149.1212803920339, -35.36116330402493],
                  [149.1209585269521, -35.36112830568458]]]),
            {
              "class": 2,
              "system:index": "29"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1230828364919, -35.35673589354867],
                  [149.12269659839376, -35.35685839433715],
                  [149.12293263278707, -35.35708589530845],
                  [149.1234047015737, -35.35699839501072],
                  [149.12312575183614, -35.356893394528306]]]),
            {
              "class": 2,
              "system:index": "30"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.09905656115814, -35.13230274363447],
                  [149.10021527545257, -35.13261861835107],
                  [149.100472767518, -35.132021965079886],
                  [149.09952862994476, -35.131776283050414]]]),
            {
              "class": 2,
              "system:index": "31"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1151498152475, -35.14009396229259],
                  [149.11489232318206, -35.14062036909377],
                  [149.11553605334564, -35.14083093086108],
                  [149.11592229144378, -35.14051508800586]]]),
            {
              "class": 2,
              "system:index": "32"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1317398945945, -35.1503214559539],
                  [149.13255528613502, -35.1503916349045],
                  [149.13259820147925, -35.14983020160507],
                  [149.13182572528297, -35.149795111895244]]]),
            {
              "class": 2,
              "system:index": "33"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.11071137591773, -35.1495845733185],
                  [149.1116984288352, -35.14954948350275],
                  [149.1116984288352, -35.14912840453351],
                  [149.11071137591773, -35.14916349453084]]]),
            {
              "class": 2,
              "system:index": "34"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.1297228734153, -35.15376015335321],
                  [149.13070992633277, -35.153654889262576],
                  [149.13070992633277, -35.153163655038966],
                  [149.12993745013648, -35.15319874329615]]]),
            {
              "class": 2,
              "system:index": "35"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.94254132670721, -35.220587882555705],
                  [148.9427559034284, -35.22069305997776],
                  [148.94327088755927, -35.22051776419861],
                  [148.94329234523138, -35.22039505692794],
                  [148.9427344457563, -35.220324938404254]]]),
            {
              "class": 2,
              "system:index": "36"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.94530936641058, -35.22221811728042],
                  [148.9456526891645, -35.22234082179473],
                  [148.9459960119184, -35.222112941834766],
                  [148.94571706218085, -35.22206035406083]]]),
            {
              "class": 2,
              "system:index": "37"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.94681140345892, -35.22025481981999],
                  [148.94719764155707, -35.220237290164455],
                  [148.94726201457343, -35.220026934002775],
                  [148.94691869181952, -35.21995681516105]]]),
            {
              "class": 2,
              "system:index": "38"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.94674703044257, -35.22293681251094],
                  [148.94709035319647, -35.22298939971694],
                  [148.94709035319647, -35.22272646334618],
                  [148.94681140345892, -35.22272646334618]]]),
            {
              "class": 2,
              "system:index": "39"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.94232674998602, -35.21948351139494],
                  [148.94269153041205, -35.21948351139494],
                  [148.9426271573957, -35.21922056366558],
                  [148.94234820765814, -35.21922056366558]]]),
            {
              "class": 2,
              "system:index": "40"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.93777772349677, -35.21773051044165],
                  [148.93773480815253, -35.21794087255508],
                  [148.9381639615949, -35.21790581224071],
                  [148.9381639615949, -35.21764285940014]]]),
            {
              "class": 2,
              "system:index": "41"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.94447659649467, -35.223865977866055],
                  [148.9439616123638, -35.22418149697824],
                  [148.94447659649467, -35.224707359439044],
                  [148.94503449596976, -35.224286669743016]]]),
            {
              "class": 2,
              "system:index": "42"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[148.94778107800101, -35.226109642674416],
                  [148.94773816265678, -35.22642515306276],
                  [148.94846772350883, -35.22642515306276],
                  [148.94846772350883, -35.22596941544138]]]),
            {
              "class": 2,
              "system:index": "43"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.24485737410868, -35.31543219562755],
                  [149.24584442702616, -35.31550223188711],
                  [149.24597317305887, -35.31504699511593],
                  [149.24494320479715, -35.31497695846216]]]),
            {
              "class": 2,
              "system:index": "44"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.243103209413, -35.311343723871595],
                  [149.24367183772415, -35.311396253727196],
                  [149.24373084632248, -35.311212398853975],
                  [149.24381131259287, -35.31101978900821],
                  [149.24327487078995, -35.310945371356354]]]),
            {
              "class": 2,
              "system:index": "45"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.0824479019842, -35.20077295419784],
                  [149.0823191559515, -35.201106096862894],
                  [149.08296288611507, -35.201211299525866],
                  [149.08283414008235, -35.200930758788466]]]),
            {
              "class": 2,
              "system:index": "46"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.08517302634334, -35.20082555576211],
                  [149.0850013649664, -35.201123630649526],
                  [149.08540906073665, -35.201158698211415],
                  [149.08555926444149, -35.2009132249602]]]),
            {
              "class": 2,
              "system:index": "47"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.08000172736263, -35.19928256238658],
                  [149.07965840460872, -35.199615711164775],
                  [149.08000172736263, -35.199791052078126],
                  [149.08032359244442, -35.19954557469345]]]),
            {
              "class": 2,
              "system:index": "48"
            }),
        ee.Feature(
            ee.Geometry.Polygon(
                [[[149.07708348395442, -35.19204062233911],
                  [149.07669724585628, -35.19246147913837],
                  [149.0775126373968, -35.19249655043991],
                  [149.07764138342952, -35.192145836743315]]]),
            {
              "class": 2,
              "system:index": "49"
            })]);


//clip the TERRAIN covariates
var terrain = ee.Image("projects/ee-racrabbe3/assets/covariate_ACT_TERRAIN").clip(FIELD)
print(terrain, 'terrain')
Map.addLayer(terrain.select('elevation'), {min:200, max:1000, palette:['cyan', 'yellow', 'brown']}, 'Elevation')

//---load up the covariates

//for 2019
var m01 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2019_medoid")
//print(m01,"cov2019Medoid")
Map.addLayer(m01, {min:200, max:1200, bands:['nir', 'red', 'green']}, 'Medoid-2019')
var m02 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2019_percentiles")
//print(m02, 'cov2019Perc')
var m03 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2019_sd")
var m04 = ee.Image("projects/ee-racrabbe3/assets/covariate_phAmp2019")

//for 2020
var m05 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2020_medoid")
var m06 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2020_percentiles")
var m07 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2020_sd")
var m08 = ee.Image("projects/ee-racrabbe3/assets/covariate_phAmp2020").rename(['phase2020', 'amp2020'])

//for 2021
var m09 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2021_medoid")
var m10 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2021_percentiles")
var m11 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2021_sd")
var m12 = ee.Image("projects/ee-racrabbe3/assets/covariate_phAmp2021").rename(['phase2021', 'amp2021'])

//for 2022
var m13 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2022_medoid")
var m14 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2022_percentiles")
var m15 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2022_sd")
var m16 = ee.Image("projects/ee-racrabbe3/assets/covariate_phAmp2022").rename(['phase2022', 'amp2022'])

//for 2023
var m17 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2022_medoid")
var m18 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2022_percentiles")
var m19 = ee.Image("projects/ee-racrabbe3/assets/covariate_s2col2022_sd")
var m20 = ee.Image("projects/ee-racrabbe3/assets/covariate_phAmp2022").rename(['phase2023', 'amp2023'])

//merge the images up
var sentCov = m01.addBands(m02).addBands(m03).addBands(m04)
.addBands(m05).addBands(m06).addBands(m07).addBands(m08)
.addBands(m09).addBands(m10).addBands(m11).addBands(m12)
.addBands(m13).addBands(m14).addBands(m15).addBands(m16)
.addBands(m17).addBands(m18).addBands(m19).addBands(m20)

print(sentCov, 'sentCov')
Map.addLayer(sentCov, {min:200, max:1200, bands:['nir', 'red', 'green']}, 'sentCov')

//select the first 18 bands from the sentCov layer
//this data is required for the preliminary RF classification
var list=ee.List.sequence(0,17)
var sentCov2 = sentCov.select(list)
print(sentCov2, 'sentinel covariates')




//LiDAR-derived canopy cover layer 
var treeCover = ee.Image("projects/ee-racrabbe3/assets/ACT_Canopy_Cover_2020_1m_GDA2020")
//print(treeCover, 'canopy cover')
//Map.addLayer(treeCover.clip(FIELD), null, 'treeCover')

//Mask trees cover using the LiDAR-derived canopy cover layer 
//mask out the tree cover pixels
var noCanopy = sentCov2.updateMask(treeCover.select('b1').eq(0)).clip(FIELD)
//Map.addLayer(canopyc.clip(ACT_boundary), {min:0, max:1, palette:['blue', 'red']}, 'canopyc')
Map.addLayer(noCanopy, null, 'canopyc')
//Map.addLayer(field_data)

//classification for a vegetation layer
var refClass = water.merge(artificial).merge(vegetation)
//print(refClass.size())


// sample training areas
var landcover2 = noCanopy.sampleRegions({
  collection: refClass,
  properties: ['class'],
  scale: 10
  //tileScale: 16
});
//print(landcover2.size(), 'landcover2')



// partition training areas into training and test sets: apply 80-20 rule
landcover2 = landcover2.randomColumn()
var trainingSample = landcover2.filter('random <= 0.8') //80% of the data would be for model training
var testSample = landcover2.filter('random > 0.8')  //20% of data for model testing


// Use the optimal parameters in a model and perform final classification
var optimalModel = ee.Classifier.smileRandomForest({
  numberOfTrees: 100,
  bagFraction: 0.6
}).train({
  features: trainingSample,  
  classProperty: 'class',
  inputProperties: noCanopy.bandNames()
});


// classify the image
var finalClassification = noCanopy.classify(optimalModel);
print(finalClassification, 'finalClassification')
Map.addLayer(finalClassification, {min: 0, max: 2, palette: ['blue', 'purple', 'green']}, 'Random Forest Classification 1'); 


// assesss performance of the optimal model 
var accuracy2 = testSample
      .classify(optimalModel)
      .errorMatrix('class', 'classification')


//Print the user's accuracy to the console
print('Validation Overall accuracy: ', accuracy2.accuracy())
print('Validation Consumer accuracy: ', accuracy2.consumersAccuracy())
print('Validation Producer accuracy: ', accuracy2.producersAccuracy())
print('Validation Kappa: ', accuracy2.kappa())
print('Validation fscore: ', accuracy2.fscore(1))

//select the pixels classified as vegetation and use this to mask
//the image required for the grassland classification

//select the vegetation class as this would be the mask
var vegMask = finalClassification.select('classification').eq(2)
Map.addLayer(vegMask, null, 'vegetation')

//mask the image to be classified
var sentCov3 = sentCov.updateMask(vegMask)
print(sentCov3,"sentCov3")
Map.addLayer(sentCov3, {min:200, max:1200, bands:['nir', 'red', 'green']}, 'sentCov3')

//add the topographic bands
var img2classify = sentCov3.addBands(terrain)
print(img2classify, 'img2classify')

//export the "image to classify" to asset

Export.image.toAsset({
  image: img2classify,
  description: 'compositeLayer2',
  assetId: 'projects/ee-racrabbe3/assets/compositeLayer2',  
  //scale:10,
  region: FIELD,
  crs: 'EPSG:7855',
  crsTransform: [10,0,658000,0,-10,6112000], //[10,0,600000,0,-10,6100000],
  maxPixels:1e13
  //shardSize: 2560
});
```





