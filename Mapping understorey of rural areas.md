# Mapping Understorey of Rural Areas in Australian Capital Territory

In this project, the grassland communities in rural areas of the ACT, Australia, were categorised into native/native high diversity/exotic and native species types for efficient management.


## Abstract

Grasslands are an important global terrestrial biome as they provide a range of ecosystem services, including a refugia for thretened plants, birds, mammals and reptiles. The lowland areas of the Australian Capital Territory are dominated by grassland communities that are important to Australian biodiversity. However, the expanse of the ACT grassland communities have decreased chiefly due to weed invasion, fire and feral animal attacks, inappropriate grazing regime, urbanisation, and agricultural expansion or improvements. The ACT Natural Temperate Grasslands is listed as a critically endangered ecological community under the Commonwealth legislation (EPBC Act 1999). Continous monitoring of the grasslands is an efficient management practice to minimise or prevent many of the threats and stresses of the grassland vegetation commnunities. This project utilised multitemporal satellite imagery from Sentinel-1 and Sentinel-2, elevation data, and a Random Forest classification algorithm in Google Earth Engine (a cloud-based geospatial analysis platform) to (1) differentiate between exotic, native and native high diversity grass; (2) differentiate between dominant native grass species, including kangaroo grass, spear grass and Phalaris; and (3) quantify the performance and uncertainty of a Random Forest classfication model. A range of predictors, relevant for both pixel-based and object-based analysis, including spectral indices, textural and segmentation variables derived from the Sentinel-2 data, phenological variables derived from the Sentinel-1, and topographical variables from the elevation data were used to teach a Random Forest algorithm to discriminate between grassland types. A Monte Carlo simulation was used to optimise the predictability of the Random Forest model. The accuracy of the Random Forest model was assessed using a separate data set from the one used to teach the model, while statistical metrics such as overall accuracy, user's accuracy, producer's accuracy, and F1-score were used to describe the performance of the model.


## Introduction

Grasslands are globally ubiquitous, excluding Antarctica and extreme desert areas and highest mountains, making it one of the dominant biomes covering approximately 40% of the Earth's terrestrial ecosystems ([Petermann and Buzhdygan, 2021](https://doi.org/10.1016/j.cub.2021.06.060)). Specifically, grasslands are found in temperate, tropical and subtropical environments, and this global distribution is driven by variations in temperature and precipitation. In Australia, grasslands are spatially varied, mimicking regional climatic patterns and fire regimes. The Australian grasslands, including temperate, alpine and Monaro grasslands spanning the southeastern part of the country, are a habitat for many flora and fauna species ([McIvor, 1994](https://www.fao.org/4/y8344e/y8344e0g.htm)). In the Australian Capital Territory (ACT), grassland communities predominate the lowland areas. The communities comprise the Natural Temperate Grasslands (NTG), native grassland and degraded native grassland under the ACT Native Grassland Conservation Strategy [ACT Government, 2017]. The ACT lowland grasslands are predominantly perennial tussock grasses, such as *Poa*, *Themeda*, *Austrodanthonia*, *Rytidosperma*, and *Austrosipa* ([Brawata et al., 2017](https://www.act.gov.au/__data/assets/pdf_file/0009/2539629/lowland-native-grassland-ecosystem-condition-monitoring-plan-2017.pdf)) and can be found mainly in nature reserves. The spatial extent of the ACT grasslands has considerably decreased due to urbanisation, invasion of exotic species and weeds, agricultural improvements, and inappropriate grazing and fire regimes. Consequently, the NTG is categorised as a critically endangered ecological community under the Environment Protection and Biodiversity Conservation Act (EPBC Act, 1999). Monitoring grassland conditions is required to address the threats and stressors in time. Although a field-based monitoring methods can be used for grassland management, the direct physical assessment methods can be expensive to sustain, especially monitoring at a landscape scale.

Satellite remote sensing provides a more cost-efficient approach for continuous monitoring of grasslands at a large scale. Earth observation satellites take multispectral photographs for a detailed spectral analysis of terrestrial vegetation. Through spectral indices such as the normalised difference vegetation index (NDVI), soil-adjusted vegetation index (SAVI), enhaced vegetation index (EVI), and normalised difference water index (NDWI), spectral data from the satellite sensors can be used to track the health and vigour of vegetation. Earth observation satellites, such as Landsat and Moderate Resolution Imaging Spectroradiometer (MODIS), have been extensively used for grassland monitoring. [Meng et al., (2022)](https://doi.org/10.3390/rs14092094)  leveraged MODIS NDVI products, including maximum, mean and sum of NDVI for large-scale temperate grassland mapping in Inner Mongolia. In a different study, time series of MODIS NDVI was analysed to extract phenological metrics to differentiate between alpine meadows, steppes, and desert grasses in the Tibetan Plateau ([Wang et al., 2015](https://doi.org/10.1080/17538947.2013.860198)), while a similar study leveraged the MODIS EVI to classify grasslands into meadow steppe, typical steppe, desert steppe, high-cold meadow steppe, high-cold typical steppe and shrub herbosa ([Wen et al., 2010](https://doi.org/10.1109/JSTARS.2010.2049001)). Landsat 8 was used to map high-diversity grassland and degraded grassland with accuracy higher than 80% ([Fassnach et al., 2015](https://doi.org/10.1016/j.jag.2015.06.005)). The advent of the Sentinel satellites operated under the Copernicus Program by the European Space Agency complements the existing sensors to offer improved opportunities for grasslands monitoring from space as the Sentinel satellites provide higher spatial, spectral and temporal information about the environment. Integrating satellite sensors, including optical and synthetic aperture radar (SAR), and machine learning and deep learning techniques have been used for improvements in grassland mapping. [Badreldin et al., (2021)](https://doi.org/10.3390/rs13244972) combined MODIS, Sentinel-2 and Sentinel-1 data and Random Forest to classify grasslands into native, tame and mixed in the Canada. The study achieved prediction accuracies higher that 85% for the native grasslands. In Tasmania (Australia), [Meville et al.,(2015)](https://doi.org/10.1016/j.jag.2017.11.006) combined Landnsat ETM+ and WorldView-2 and Random Forest to differentiate lowland native grasslands of *Poa labillardierei* , *Themeda triandra* and lowland native graalsnad complex predominantly species form the *Danthonia* genus. The average prediction accuracies varied between 54% and 87%. [Crabbe et al., (2019)](https://doi.org/10.3390/rs11030253) explored multitemporal Sentinel-1 data to discriminate pastural grasses into C3, C4, and mixed, while in a different study a range of machine learning methods and a combination of Sentinel-1 and Sentinel-2 data were used to map species diversity for a grazing property in Australia ([Crabbe et al., 2020](https://doi.org/10.1016/j.jag.2019.101978)). 

The aim of this study is to differentiate grassland types in lowland ACT to support the ACT Native Grassland Conservation Strategy and Action Plans for efficient management of the Natural Temperate Grasslands. To achieve this aim, the following specific objectives were addressed: <br> 

- differentiate between exotic, native and native high diversity grass <br>

 - differentiate between dominant native grass species, including kangaroo grass, spear grass and Phalaris <br>

- quantify the performance and uncertainty of a Random Forest classfication model


## Materials and Methods







![image](https://github.com/user-attachments/assets/699429d5-d6a9-428f-8df8-a37b3cfe0a12)






### Study area



The location of the study area is the grasland areas of the ACT, Australia, represented by the figure below. 





![image](https://github.com/user-attachments/assets/aafaff09-ecf7-4569-a99e-c90376f47570)|
|:--:|
| *Fig. 1. The study location with red pixels showing grassland areas investigated.*|












The figure below is an overview of the cardinal workflow. The methodology was adapted from recent similar studies, including [Poortinga et al., 2019](https://doi.org/10.3390/rs11070831), [Tassi and Vizzari, 2020](https://doi.org/10.3390/rs12223776), and [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) and was implemented using Google Earth Engine JavaScript API. The previous studies that implemented similar land cover classification workflow reported a prediction accuracy ranging from 82% to 91%. The Google Earth Engine (GEE) is a cloud-based platform offering a combination of satellite imagery (including Landsat, MODIS, and Sentinel) and other geospatial datasets, integrated development environment and algorithms to make planet-scale remote sensing analysis and sharing of results easy ([Gorelick et al., 2017](https://doi.org/10.1016/j.rse.2017.06.031)). The GEE entails large-scale computing resources accessible via JavaScript API and Python API, and is automatically synced with GitHub for easy project collaboration through code sharing and version control. 





![image](https://github.com/user-attachments/assets/7bdb329b-5694-4768-87bd-c44d8e40fe3b)|
|:--:|
| *Fig. 2. An overview of the workflow, including the datasets and principal methods employed.*|





### Reference data

The ground reference data was collected from 2018 to 2023 (inclusisve), in which visual discrimination of grasses were conducted by experts from the ACT government. The field sampling plots were randomly selected with each plot size equivalent to $400m^2$ (i.e., 20m by 20m) to match the nominal ground sampling distance of the Sentinel-2 satellite. The geographic coorodinates of a plot were collected using a handheld GPS with a horizontal accuracy of approximately 5m. In each plot, the observer recorded the botanical composition including a fraction of vegetation cover and bare soil. Further, the grasses were separated into native/exotic, perennial/annual, and C3/C4 with the level of plant diversity recorded. Post-field processing of the data was done, removing bad rows and columns of data. The reference data was used to build, train and validate the machine learning classifier}.





### Sentinel-2 satellite imagery

Sentinel-2 is one of the Earth observation satellite missions operated through the Copernicus Program under the European Space Agency (ESA). The Sentinel-2, launched in 2015, on-board satellites that carry sensors collecting optical imagery of differing native resolutions at a planetary scale. The table below describes the spectral bands of Sentinel-2, including the key use and spatial resolution.



| *Table. 1. An overview of the workflow, including the datasets and principal methods employed.*|
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


In this project, the Sentinel-2 spectral bands were used as they provide high resolution imagery and suited for vegetation monitoring. The Sentinel-2 imagery over the study areas acquired from 2018 to 2013 was used as this date aligns with the field observation data. To ensure that the electromagnetic energy recorded by the sensor were those reflected off the targets of interest, the Bottom of Atmosphere (BoA) Sentinel-2 imagery retrieved from the Copernicus Open Access Hub via Google Earth Engine were used. However, there was not BoA product for 2018, so the Top of Atmposphere (ToA) product was collected and corrected for atmospheric influence using the sensor insentive radiative transfer model in GEE [(Yin et al., 2022)](https://doi.org/10.5194/gmd-15-7933-2022). Once the BoA imagery was obtained for all years, a bidirection reflectance distribution function was applied to minimise errors due to temporal variations in the sun-sensor viewing geometry. Image pixels affected by cloud and cloud shadow were masked using the quality assesssment bands. The project adapted the pre-analysis techniques, including cloud/shadow, atmospheric correction and BRDF methods by [Berra et al. (2024)](https://doi.org/10.3390/rs16152695) to convert the ToA or BoA imagery to analysis ready data (ARD).  Since the Sentinel-2 satellites acquire data at varied native spatial resolutions, the imagery obtained at spectral bands with 10m resolution were spatially upscaled to 20m using the nearest neighbourhood geometric resampling method to preserve the original reflecance values and harmonise the data. 


#### Spectral indices

The ARD was analysed to extract spectral indices that measure the biophysical conditions of the grasses. Spectral indices are obtained from the bands applying different arithmetric operations; despite there are many spectral indices only those that require the nominal resolution (20m) bands and relevant to the project were utilised. The spectral indices, include the normalised vegetation index (NDVI), normalised water index (NDWI), soil-adjusted vegetation index (SAVI), enhanced vegetation index (EVI), green chlorophyll vegetation index (GCVI), and bare soil index (BSI). The table below details the spectral indices, formulae and principal references.  


|Index|Formula|Reference| 
|:----|:----|:---|
|NDVI|$${NIR-Red}\over{NIR+Red}$$|[Rouse et al., 1973](https://ntrs.nasa.gov/citations/19740022614)|
|NDWI|$${NIR-SWIR2}\over{NIR+SWIR2}$$|[Gao, 1996](https://doi.org/10.1016/S0034-4257(96)00067-3)|
|SAVI|$$\left({NIR-Red}\over{NIR+Red+0.5}\right)×{1.5}$$|[Huete, 1998](https://doi.org/10.1016/0034-4257(88)90106-X)|
|EVI |$$\left({NIR-Red}\over{NIR+6×Red-7.5×Blue+1}\right)× {2.5}$$|[Huete et al., 2002](https://doi.org/10.1016/S0034-4257(02)00096-2)|
|GCVI|$$\left({NIR}\over{Green}\right)-{1}$$|[Gitelson et al., 2003](https://doi.org/10.1078/0176-1617-00887)|
|BSI |$${(SWIR2+Red)}-{(NIR+Blue)}\over\{(SWIR2+Red)}+{(NIR+Blue)}$$|[Bera et al., 2020](https://doi.org/10.1007/s42489-020-00060-1)|



The NDVI, BSI, a textural measure (i.e, GLCM contrast) derived from Sentinel-1 (see the section on Sentinel-1 for details) were combined using user-defined thresholds to mask out pixels that were not grassland.



#### Textural and segmentataion 

Naturally, spatial relationships exist between the grass types and this can be leveraged to improve discrimination between species. In image analysis, the spatial relationship between pixels can be described through a textural analysis of the brightness values recorded by the electromagnetic detector. In this project, the grey level co-occurrence metrics (GLCM) by [Haralick et al., 1973](https://doi.org/10.1109/TSMC.1973.4309314) were explored as the method is widely used in similar studies, including [Mohammadpour et al., 2022](https://doi.org/10.3390/rs14184585), [Zhang et al., 2024](https://doi.org/10.1080/15481603.2024.2385170), and [Bazzo et al., 2024](https://doi.org/10.1016/j.ecoinf.2024.102813). The GLCM, a second order statistical analysis of an image, is employed by identifying a pixel in a pre-determined moving window of pixels and comparing the relationships between the focal pixel and neighbouring pixels in a specific direction and distance. Through descriptive statistical methods, many textural metrics can be computed. In the GEE, eighteen GLCM metrics, sourced from the works of [Haralick et al., 1973](https://doi.org/10.1109/TSMC.1973.4309314) and [Conners et al., 1984](https://sdoi.org/10.1016/0734-189X(84)90197-X), can be computed. However, the relevance of the metrics is study-specific and for this reason only five of the metrics were explored in this study. These were sum average (AVG), variance (VAR), contrast (CON), inverse difference moment (IDM) and entropy (ENT). The formulae for the metrics are from [Hall-Beyer, 2017)](https://doi.org/10.1080/01431161.2016.1278314).




|Metric|Formula|Description|
|:----|:----|:---|
|CON|$$\sum_{i,j=0}^{N-1}  P_{i,j} \left( {i-j} \right)^2 $$|Measure local contrast|
|IDM|$$\sum_{i,j=0}^{N-1}  {P_{i,j}\over 1+ \left( {i-j} \right)^2} $$|Measure homogeneity|
|ENT |$$\sum_{i,j=0}^{N-1} P_{i,j} \left( {-lnP_{i,j}} \right)$$|Measure randomness in grey-levels|
|AVG|$$\sum_{i,j=0}^{N-1}  i\left(P_{i,j}\right)$$|Measure mean grey-levels|
|VAR  |$$\sum_{i,j=0}^{N-1}  P_{i,j} \left( {i-μ_i} \right)^2 $$|Measure the spread of grey-levels|



ASM = Angular Second Moment and IDM = Inverse Difference Moment. Pi,j refers to the probability of values i (labels of the columns) and j (labels of the rows) occurring in adjacent pixels in the original image within the pre-determined neighbourhood window. Regarding the GLCM Correlation, µ is mean and σ the standard deviation.


To compute the GLCM metrics in GEE, a 8-bit grey-scale imagery is required. Although many approaches for selecting a single-band imagery for the GLCM textural analysis exist, including using an NDVI layer, a recent method by [Tassi  and Vizzari., 2020](https://doi.org/10.3390/rs12223776) leveraging the NIR, Red, and Blue bands was used. A linear combination of the bands was used as: <br>




**$\(0.30×NIR)+(0.59×Red)+(0.11×Green)$** 




Image segmentation is another method to explore the capability of the Sentinel-2 to differentiate between the grasses as pixels with similar spatial and spectral attributes, such as colour, luminance and texture, are clustered together to form homogeneous superpixels referred to as spectral objects or clusters. Image segmentation methods perform object-based analysis of the pixels and can remove redundant data. The Simple Non-Iterative Clustering (SNIC) algorithm by [Achanta and Susstrunk, 2017](https://doi.org/10.1109/CVPR.2017.520) was used to segment the Sentinel-2 pixels into spectral clusters. The SNIC algorithm requires input variables such as compactness factor for spatial distance weighting and connectivity and neighbourhood size for efficient grouping of the pixels. The SNIC input parameters used by [Tassi and Vizzari, 2020](https://doi.org/10.3390/rs12223776) for a land cover classification study in Europe were replicated in this study. The SNIC clusters were used a predictor variable.


Annual image collection for the spectral indices, GLCM textural metrics and SNIC clusters were created and from which composites such as maximum, medoid, 20th and 80th percentile spectral information were computed. The medoid is analogous to univariate median, but it is more insensitive to outliers and applicable to multi-dimensional data such as multispectral imagery. Further details on medoid is provided in ([Flood, 2013](https://doi.org/10.3390/rs5126481)). Annual is defined as the period from June to May the following year to  mark the phenological growth calendar of the plants. 

### Sentinel-1

Sentinel-1 is another Earth observation satellite mission operated by the ESA, launchced into orbit in 2013, with the aim of monitoring the environment from space regardless of atmospheric and weather conditions. The Sentinel-1 carries a sensor that transmits and records microwave energy that bounced off environmental targets, including grasslands. Sentinel-1 is a synthetic aperture radar system, measuring the amplitude and phase of the microwave energy in multiple polarisations. Because the Sentinel-1 uses artificial microwave energy it is capable of  penetrating through cloud cover and taking photos of the Earth at any time. Thus, the Sentinel-1 complements the Sentinel-2 for continuous mapping of the environment, while providing spectral information that characterises the variations in structural and moisture conditions of the vegetation ([Saatchi et al., 1995](https://doi.org/10.1029/95JD00852)). The Sentinel-1 typically transmits the microwave energy in vertical orientation and records the return signal in vertical and horizontal orientations making the Sentinel-1 a dual-polarisation system in that the data comprises VV and VH polarisation bands.The Sentinel-1 sensor can be operated in four different modes, but the imagery obtained from the interferometric wide swath mode (IW) is recommended and available for land monitoring ([Prats-Iraola et al., 2015](https://doi.org/10.1109/IGARSS.2015.7327018)). This study used imagery from the IW mode that were already pre-processed to a ground range detected product (i.e., analysis ready data) by the ESA and were retrievable from the GEE data catalog. The pixel size of the ground range detected Sentinel-1 imagery is 10m and this is created from single look complex imagery by applying a multi-look algorithm. Further preprocessing steps such as thermal noise removal, radiometric calibration and terrain correction were performed before making the data available in GEE. Given the physical structure of vegetation canopy is more sensitive to the VH polarisation, only this band was used in this study. The inherent speckle noise associated with the Sentinel-1 imagery was not filtered out as this lowers the spectral and spatial variability required to differentiate pixels. 

#### Phenological variables extracted from the Sentinel-1

The biophysical conditions of plant species, including annual and perennial grasses, change through the growth calendar. While perennial grasses maybe photosynthetically active throughout the year, annual grasses may disappeear during the dry or low rainfall periods. The growth phenology of the plants can be an importantt information to differentiate between grass types. Sentinel-1, in contrast to the optical Sentinel-2 imagery, is not affected by cloud cover or shadow; thus, a multitemporal Sentinel-1 data was anlysed to extract phenological information about the species. A Fourier harmonics function was applied to the Sentinel-1 time series data to compute amplitude and phase bands whereby the amplitude explains the variance in original time series and the phase angle denotes the time associated with the peak of the curve ([Jakubauskas et al., 2001](https://www.asprs.org/wp-content/uploads/pers/2001journal/april/2001_apr_461-470.pdf)). The amplitude and phase bands were adjusted to spatially align with the regions of interest and the Sentinel-2 data and pixels that were not grassland were masked using the method discussed earlier. Annual composites of the Sentinel-1 imagery were created to extract the phenological information of the plants. Through the annual composites, additional composites including maximum, medoid, 20th and 80th percentile of the phase and amplitude information were created.  A similar approach was used by [Poortinga et al., 2019](https://doi.org/10.3390/rs11070831) in a land cover classification project conducted in Myanmar.


### Topographic variables

The NASA  Shuttle Radar Topography Mission (SRTM), a global topographic data, was obtained from the GEE data archive to compute elevation, slope, and aspect.  The NASA SRTM elevation data has a pixel size of approximately 30m, this was adjusted to match the Sentinel-2 pixels before computing the topographic variables. The elevation, slope and aspect images were added to the composite images from the Sentinel-2 and Sentinel-1 to compose a single image of several bands.


### Random forest classification

Random Forest (RF) is a decision tree ensemble machine learning algorithm widely used for land cover monitoring as it is not limited by data structure and minimises overfitting the data [Breiman, 2000](https://doi.org/10.1023/A:1010933404324). Additionally, the RF is computationally less expensive to implement as only few hyperparameters require tuning.  The RF operates by randomly selecting a proportion of the instances to train a decision tree, while replacing the samples to be re-used in the next iteration. Sampling a subset of instances with replacement to create decision trees is referred to as boostrap aggregating (i.e., bagging). The RF creates multiple decision trees to avoid overfitting; the final descision tree is obtained through majority voting. The figure below summarises how the Random Forest classification algorithm functions. The RF classification algorithm in GEE was used, requiring the tuning for hyperparameters such as the number of trees to grow, number of the predictor variables to use and the proportion of instances to train a decision tree at every iteration. In GEE, these hyperparameters are the *numberOfTrees*, *variablesPerSplit*, and *bagFraction*, respectively.  The *numberOfTrees* values tested ranged between 10 and 150 at an interval of 10, *variablesPerSplit* values ranged between 1-10, while *bagFraction* was by increment of 10 with the maximum limit being 90%. The *numberOfTrees*, *variablesPerSplit*, and *bagFraction* with the highest accuracy were used as the optimal values for model training. 






![image](https://github.com/user-attachments/assets/0ed0f4bc-d2a9-4bda-a6b8-60d0ad633234)|
|:--:|
| *Fig. 3. A schematic diagram summarising how the Random Forest algoirthm functions.*|





#### Data partitioning, selecting optimal predictors and classification

The reference data was used to randomly sample pixels for each cover class, which was then split into two sets with 80% of the samples representing the training set while the remaining was used for evaluating the accuracy of the Random Forest classifier. A Random Forest classification model was trained using the predictor variables and optimal hyperparameter values in probability mode to predict cover classes. The predictor variables were assessed to remove redundant variables. Methods such as correlation analysis, principal component analysis and separability indices have been used to select the optimal predictor variables for RF models. However, in this work, we used the mean decrease impurity method ([Breiman, 2000](https://doi.org/10.1023/A:1010933404324)), which is built-into the RF algorithm in the GEE. Once the top predictor variables were identified a parsimonius RF model was created using these variables. 


#### Evaluation of the Random Forest model

The test set was used to evaluate the accuracy of the RF classifier in that user's accuracy, prouducer's accuracy, and F-1 score were computed from a confusion matrix table. To quantify the uncertainty associated with the Random Forest model, Monte Carlo simulation (MC)  and Conformal prediction methods were explored. While the Monte Carlo method is widely used for uncertainty quantification ([Canters et al.,2002](https://doi.org/10.1080/13658810110099143)) and ([Cockx et al., 2014](https://doi.org/10.1016/j.jag.2014.03.016)), the Conformal prediction is a recent method in Remote Sensing and contrast to MC the conformal prediction method makes no assumpution about data distribution and is model agnostic, supporting all classical and deep learning artificial intelligence models ([Singh et al., 2024](https://doi.org/10.48550/arXiv.2401.06421)). The RF classifier produced class membership probabilities for each pixel and were used for the post-hoc Monte Carlo simulation and conformal prediction. 




## Results




## Discussion




## Conclusion




## References


1, Achanta, R., & Susstrunk, S. (2017). Superpixels and Polygons Using Simple Non-iterative Clustering. 2017 IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 4895–4904. https://doi.org/10.1109/CVPR.2017.520 <br>

2, Badreldin, N., Prieto, B., & Fisher, R. (2021). Mapping Grasslands in Mixed Grassland Ecoregion of Saskatchewan Using Big Remote Sensing Data and Machine Learning. Remote Sensing, 13(24), 4972. https://doi.org/10.3390/rs13244972 <br>

3, Bazzo, C. O. G., Kamali, B., Dos Santos Vianna, M., Behrend, D., Hueging, H., Schleip, I., Mosebach, P., Haub, A., Behrendt, A., & Gaiser, T. (2024). Integration of UAV-sensed features using machine learning methods to assess species richness in wet grassland ecosystems. Ecological Informatics, 83, 102813. https://doi.org/10.1016/j.ecoinf.2024.102813 <br>

4, Bera, B., Saha, S., & Bhattacharjee, S. (2020). Estimation of Forest Canopy Cover and Forest Fragmentation Mapping Using Landsat Satellite Data of Silabati River Basin (India). KN - Journal of Cartography and Geographic Information, 70(4), 181–197. https://doi.org/10.1007/s42489-020-00060-1 <br>

5, Berra, E. F., Fontana, D. C., Yin, F., & Breunig, F. M. (2024). Harmonized Landsat and Sentinel-2 Data with Google Earth Engine. Remote Sensing, 16(15), 2695. https://doi.org/10.3390/rs16152695 <br>

6, Brawata, R., Stevenson, B., & Seddon, J. (2017). Conservation Effectiveness Monitoring Program: ACT Lowland Native Grasslands Ecosystem Condition Monitoring Plan [Technical]. Environment, Planning and Sustainable Development Directorate, ACT Government. https://www.act.gov.au/__data/assets/pdf_file/0009/2539629/lowland-native-grassland-ecosystem-condition-monitoring-plan-2017.pdf <br>

7, Breiman, L. (2001). Random Forests. Machine Learning, 45(1), 5–32. https://doi.org/10.1023/A:1010933404324 <br>

8, Canters, F., Genst, W. D., & Dufourmont, H. (2002). Assessing effects of input uncertainty in structural landscape classification. International Journal of Geographical Information Science, 16(2), 129–149. https://doi.org/10.1080/13658810110099143 <br>

9, Cockx, K., Van De Voorde, T., & Canters, F. (2014). Quantifying uncertainty in remote sensing-based urban land-use mapping. International Journal of Applied Earth Observation and Geoinformation, 31, 154–166. https://doi.org/10.1016/j.jag.2014.03.016 <br>

10, Conners, R. W., Trivedi, M. M., & Harlow, C. A. (1984). Segmentation of a high-resolution urban scene using texture operators. Computer Vision, Graphics, and Image Processing, 25(3), 273–310. https://doi.org/10.1016/0734-189X(84)90197-X <br>

11, Crabbe, R. A., Lamb, D., & Edwards, C. (2020). Discrimination of species composition types of a grazed pasture landscape using Sentinel-1 and Sentinel-2 data. International Journal of Applied Earth Observation and Geoinformation, 84, 101978. https://doi.org/10.1016/j.jag.2019.101978 <br>

12, Crabbe, R. A., Lamb, D. W., & Edwards, C. (2019). Discriminating between C3, C4, and Mixed C3/C4 pasture grasses of a grazed landscape using multi-temporal sentinel-1a data. Remote Sensing, 11(3). https://doi.org/10.3390/rs11030253 <br>

13, Fassnacht, F. E., Li, L., & Fritz, A. (2015). Mapping degraded grassland on the Eastern Tibetan Plateau with multi-temporal Landsat 8 data—Where do the severely degraded areas occur? International Journal of Applied Earth Observation and Geoinformation, 42, 115–127. https://doi.org/10.1016/j.jag.2015.06.005 <br>

14, Flood, N. (2013). Seasonal Composite Landsat TM/ETM+ Images Using the Medoid (a Multi-Dimensional Median). Remote Sensing, 5(12), 6481–6500. https://doi.org/10.3390/rs5126481 <br>

15, Gao, B. (1996). NDWI—A normalized difference water index for remote sensing of vegetation liquid water from space. Remote Sensing of Environment, 58(3), 257–266. https://doi.org/10.1016/S0034-4257(96)00067-3 <br>

16, Gitelson, A. A., Gritz †, Y., & Merzlyak, M. N. (2003). Relationships between leaf chlorophyll content and spectral reflectance and algorithms for non-destructive chlorophyll assessment in higher plant leaves. Journal of Plant Physiology, 160(3), 271–282. https://doi.org/10.1078/0176-1617-00887 <br>

17, Gorelick, N., Hancher, M., Dixon, M., Ilyushchenko, S., Thau, D., & Moore, R. (2017). Google Earth Engine: Planetary-scale geospatial analysis for everyone. Remote Sensing of Environment, 202, 18–27. https://doi.org/10.1016/j.rse.2017.06.031 <br>

18, Hall-Beyer, M. (2017). Practical guidelines for choosing GLCM textures to use in landscape classification tasks over a range of moderate spatial scales. International Journal of Remote Sensing, 38(5), 1312–1338. https://doi.org/10.1080/01431161.2016.1278314 <br>

19, Haralick, R. M., Shanmugam, K., & Dinstein, I. H. (1973). Textural features for image classification. IEEE Transactions on Systems, Man, and Cybernetics, 6, 610–621. https://doi.org/10.1109/TSMC.1973.4309314<br>

20, Huete, A., Didan, K., Miura, T., Rodriguez, E. P., Gao, X., & Ferreira, L. G. (2002). Overview of the radiometric and biophysical performance of the MODIS vegetation indices. The Moderate Resolution Imaging Spectroradiometer (MODIS): A New Generation of Land Surface Monitoring, 83(1), 195–213. https://doi.org/10.1016/S0034-4257(02)00096-2 <br>

21, Huete, A. R. (1988). A soil-adjusted vegetation index (SAVI). Remote Sensing of Environment, 25(3), 295–309. https://doi.org/10.1016/0034-4257(88)90106-X <br>

22, Melville, B., Lucieer, A., & Aryal, J. (2018). Object-based random forest classification of Landsat ETM+ and WorldView-2 satellite imagery for mapping lowland native grassland communities in Tasmania, Australia. International Journal of Applied Earth Observation and Geoinformation, 66, 46–55. https://doi.org/10.1016/j.jag.2017.11.006 <br>

23, Meng, B., Zhang, Y., Yang, Z., Lv, Y., Chen, J., Li, M., Sun, Y., Zhang, H., Yu, H., Zhang, J., Lian, J., He, M., Li, J., Yu, H., Chang, L., & Yi, S. (2022). Mapping Grassland Classes Using Unmanned Aerial Vehicle and MODIS NDVI Data for Temperate Grassland in Inner Mongolia, China. Remote Sensing, 14(9), 2094. https://doi.org/10.3390/rs14092094 <br>

24, Mohammadpour, P., Viegas, D. X., & Viegas, C. (2022). Vegetation Mapping with Random Forest Using Sentinel 2 and GLCM Texture Feature—A Case Study for Lousã Region, Portugal. Remote Sensing, 14(18), 4585. https://doi.org/10.3390/rs14184585 <br>

25, Petermann, J. S., & Buzhdygan, O. Y. (2021). Grassland biodiversity. Current Biology, 31(19), R1195–R1201. https://doi.org/10.1016/j.cub.2021.06.060 <br>

26, Poortinga, A., Tenneson, K., Shapiro, A., Nquyen, Q., San Aung, K., Chishtie, F., & Saah, D. (2019). Mapping Plantations in Myanmar by Fusing Landsat-8, Sentinel-2 and Sentinel-1 Data along with Systematic Error Quantification. Remote Sensing, 11(7), 831. https://doi.org/10.3390/rs11070831 <br>

27, Prats-Iraola, P., Nannini, M., Scheiber, R., De Zan, F., Wollstadt, S., Minati, F., Vecchioli, F., Costantini, M., Borgstrom, S., De Martino, P., Siniscalchi, V., Walter, T., Foumelis, M., & Desnos, Y.-L. (2015). Sentinel-1 assessment of the interferometric wide-swath mode. 2015 IEEE International Geoscience and Remote Sensing Symposium (IGARSS), 5247–5251. https://doi.org/10.1109/IGARSS.2015.7327018 <br>

28, Rouse, J. W., Haas, R. H., Schell, J. A., & Deering, D. W. (1974). Monitoring vegetation systems in the Great Plains with ERTS. NASA Spec. Publ, 351(1), 309. https://ntrs.nasa.gov/citations/19740022614<br>

29, Tassi, A., & Vizzari, M. (2020). Object-Oriented LULC Classification in Google Earth Engine Combining SNIC, GLCM, and Machine Learning Algorithms. Remote Sensing, 12(22), 3776. https://doi.org/10.3390/rs12223776 <br>

30, Saatchi, S. S., van Zyl, J. J., & Asrar, G. (1995). Estimation of canopy water content in Konza Prairie grasslands using synthetic aperture radar measurements during FIFE. Journal of Geophysical Research, 100(D12), 25481. https://doi.org/10.1029/95JD00852 <br>

31, Singh, G., Moncrieff, G., Venter, Z., Cawse-Nicholson, K., Slingsby, J., & Robinson, T. B. (2024). Uncertainty quantification for probabilistic machine learning in earth observation using conformal prediction (Version 1). arXiv. https://doi.org/10.48550/ARXIV.2401.06421 <br>

32, Wang, C., Guo, H., Zhang, L., Qiu, Y., Sun, Z., Liao, J., Liu, G., & Zhang, Y. (2015). Improved alpine grassland mapping in the Tibetan Plateau with MODIS time series: A phenology perspective. International Journal of Digital Earth, 8(2), 133–152. https://doi.org/10.1080/17538947.2013.860198 <br>

33, Wen, Q., Zhang, Z., Liu, S., Wang, X., & Wang, C. (2010). Classification of Grassland Types by MODIS Time-Series Images in Tibet, China. IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing, 3(3), 404–409. https://doi.org/10.1109/JSTARS.2010.2049001 <br>

34, Yin, F., Lewis, P. E., & Gómez-Dans, J. L. (2022). Bayesian atmospheric correction over land: Sentinel-2/MSI and Landsat 8/OLI. Geoscientific Model Development, 15(21), 7933–7976. https://doi.org/10.5194/gmd-15-7933-2022 







