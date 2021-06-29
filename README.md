# PhenologyExtraction
A repository folder regarding phenology extraction scripts utilizing existing packages (i.e. TIMESAT, CropPhenology) and proposing new methodologies. 

PhenologyExtractionRodopi.ipynb, Phenology_Extraction_NOA.ipynb are written in python 3.7 where as TIMESAT&CropPhenology.ipynb, CreateAnimatedTimeseries.ipynb, TIMESAT, NDVI-NDWI-PSRI for komotini parcels.ipynb are wirtten in R.

### Description of scripts:
<b>PhenologyExtractionRodopi</b>: Cotton phenology extraction from Sentinel-2 data, combined with ground truth data provided at parcel level from cotton farmers from Rodopi, Greece

<b>Phenology_Extraction_NOA</b>: Phenlogoy extraction methodology exteding existing phenology extraction approaches, proposing a fully automated prototype for phenology extraction escaping from the user-oriented limitations of the existing packages. The main steps of this procedure are outlier removal based on the gaussian distribution of values, temporal interpolation creating decadal dates, regression fitting with Savitzky-Golay fitting, moving average to define intersections between reference and moving average curves and finaly the phenology extraction of meaningful metrics.

<b>TIMESAT&CropPhenology</b>: Utilizes a first approach combing TIMESAT and CropPhenology packages, in order to combine output metrics.

<b>CreateAnimatedTimeseries</b>: An animation regarding the timeseries of NDVI, NDWI, PSRI calculated from Sentinel-2 imagery.

<b>TIMESAT</b>: Phenology Extraction with TIMESAT package. TIMESAT is a software package for analysing time-series of satellite sensor data, able to investigate the seasonality of satellite time-series data and their relationship with dynamic properties of vegetation, such as phenology and temporal development.

<b>NDVI-NDWI-PSRI for komotini parcels</b>: Exploring timeseries of NDVI, NDWI, PSRI indices at parcel level to investigate past farming practices and define key-moments in phenology extraction.

## Phenology_Extraction_NOA in detail:
Based on an extended bibliographic research, this workflow was constructed in order to identify the critical phenological phases describing cotton crop, in order to evaluate the results of the developed phenology extraction service and improve the precision of the model. Within this framework, three phenological phases have been identified, apart from the germination phase, which are the vegetative, the reproducing and the ripening phase respectively. Each of these phases, are separated in individual phenological stages which describe the physiognomy of the plant. Moreover, the phenological development stages of plants, which is used in a variety of fields of application, such as in a number of scientific disciples and in the agricultural industry, use the BBCH-scale decimal code system, which is divided into primary and secondary growth stages, developed by Zadoks , to describe the stages of growth in plants. The following table presents the primary growth stages of cotton crop in the BBCH-scale among with the corresponding phenological stages and the phenological phases which are belong:

<b>BCH Code	Definition	Phenological Stage	Phenological Phase</b><br/>
0 -	Germination	Germination/	Germination phase<br/>
1 -	Leaf Development (main shoot)	Tillering stage/	Vegetative phase<br/>
2 -	Formation of side shoots<br/>		
3 -	Stem elongation (main shoot)<br/>
4 -	Development of harvestable vegetative plant parts	Panicle initiation/ Reproductive phase<br/>
5 -	Inflorescence emergence	Booting/ Heading stage<br/>	
6 -	Flowering/ Flowering stage<br/>	
7 -	Development of fruits and seeds	Milk stage/ Ripening phase<br/>
8 -	Ripening of fruits and seeds/ Dough stage<br/>
9 -	Senescence	Mature stage<br/>	

### Major Phenological Stages
To begin with, germination starts as the seed absorbs water and oxygen through its chalaza after planting. The hypocotyl elongates from the radicle and form an arch that begins to push up through the soil. The seedling emergence normally takes place 4 to 14 days after sowing and after a week the first true leaf forms above cotyledons and shift from emergence to vegetative growth. At this point, the germination and seedlings emergence stages are finished, and the plant enters the vegetative phase. The vegetative phase starts when the first vegetative structures appear on the main stem. Main stem leaves and branches form points of attachment on the main stem called nodes. Generally, a new node is produced an average of every 3 days, although nodes develop more quickly early in the growing season than later in the season. The development of vegetative growth and fruiting in this phase is highly related to temperature if adequate moisture is available. The plant growth and development are functions of the sunlight interception and temperature and new leaves appear increasing the leaf area of cotton plant rapidly.  Furthermore, cotton has an indeterminate growth habit and can grow very tall under conditions of unrestrained growth. Unmanaged growth promotes diseases and makes the cultivation practice of harvesting very difficult. Subsequently, the reproductive phase follows when reproductive structures begin to appear on the plant and the carbohydrate supplies are slowly shifted from the production of roots and leaves (vegetative phase) to the development of fruits (reproductive phase). As the fruit load on the plant increases and ages, the development of new leaves steadily declines. As a result, fruit development can be identified when the leaf population is steadily decreases. Furthermore, the leaf photosynthesis does not remain constant as the leaf grows, where after 20 days of age, a cotton leaf reaches its maximum photosynthetic capacity and therefore declines. At the phenological stage of flowering, the squares are visible on nodes about 35 days after planting and the whole blooming time lasts approximately six weeks. Finally, the ripening phase follows, where the pollinated flowers form cotton bolls and around 5-7 days after bloom, flower dries and falls off, exposing the cotton boll. After pollination, it takes 50 days for the boll to fully develop and open. The three major phases of boll development are categorized as the enlargement, filling and maturation phase.  

### Methodology
The phenology extraction method relies on the investigation of satellite derived time-series and more precisely on the analysis of three different indices such as the Normalized Difference Vegetation Index (NDVI), the Normalized Difference Water Index (NDWI) and the Plant Senescence Reflectance Index (PSRI). NOA has already implemented a phenology extraction method combining the abovementioned indices for detecting phenological phases of paddy rice in South Korea, implementing the TIMESAT package. Extending the existing methodology and combining phenological processes and metrics from three different freely available packages, which are namely TIMESAT , CropPhenology  and FenicePhenolo , NOA has finalized its own generalized fully automated prototype for phenology extraction escaping from the user-oriented limitations of the TIMESAT package. 

![pipeline](https://user-images.githubusercontent.com/39597223/123803197-bed23880-d8f4-11eb-8f05-a52aa4e5f6e9.jpg)

### Preprocess
The pipeline commences with creating a robust cloud free without noise dataset with even spaced time-series. For this purpose, several interpolation approaches are utilized until the finalization of the dataset. To begin with, an outlier detection method is applied using the assumption that the data from every acquisition derived from the Sentinel-2 platform, regarding the parcels of investigation follow a gaussian distribution. Accordingly, the values are reviewed in order to evaluate the 3-sigma rule and therefore lie within three standard deviations expressing the 99.7% of the entire data per acquisition. Furthermore, a weighted average interpolation follows to construct decadal time-series from the raw data acquisitions, filling the fixed timestamps that fall within a ten-day range of the acquisition. The remaining empty decadal timestamps that do not fall within the desired range are subsequently created employing second order polynomial interpolation. Anew, the previously mentioned outlier detection based on the 3-sigma-rule is applied to detect any anomalies created from the interpolation procedure.

### Regression Fitting
Major part of the phenology extraction pipeline is the regression fitting of the time-series curve using the signal Savitzky-Golay filter for smoothing the data in order to increase precision and of the data without distorting the signal tendency. Savitzky-Golay approach was selected among other fitting approaches, such as least-squares fitted asymmetric Gaussian or double logistic smooth functions, as it captures both subtle and rapid changes in the time-series, providing a better understanding for the beginning and for the ending of the growing season. Before applying the Savitzky-Golay filtering, linear interpolation is employed to the time-series to transfer the temporal scale from decadal timestep to daily values for generating results comparable between data sources with different time aggregation windows. Subsequently, the iterative Savitzky-Golay filter is employed to the interpolated time-series with 4th polynomial degrees and a length of 50 days, in order to remove short peaks and drop-offs, resulting in reference time-series on which phenological metrics can be computed. 

### Moving Average
Bearing in mind developing a general transferable model for phenology extraction without user-oriented limitations, the moving average calculation proposed by Reed et al. (1994)  for calculating the phenological and productivity variables, is applied finding the intersection points, as start and end of season, between the moving average and the reference curve. The rolling average is implemented with a forwards and backwards lag, which is the moving average window defined as the length of the non-growing season. For each individual input entity in the phenology extraction pipeline, the average length of the non-growing season that describe the moving average window, is calculated through estimating primary the growing season length from two subsequent NDVI signal minima and the signal describing the seasonal crop growth. On the assumption that the seasonal crop growth follows a normal distribution, two standard deviations computed from the barycenter of the area which describe the 68.2% of the statistical population define the Seasonal growing LEngth (SLE). Moreover, the desired lag for defining the moving average window was calculated based on the following formula:

![Capture](https://user-images.githubusercontent.com/39597223/123810482-1a072980-d8fb-11eb-824c-dde9c3f988ed.PNG)

where L is lag in days, N the number of years in the time-series and 365 the number of days in the year. In this way, the dynamics of each entity is incorporated in the derivation of phenological metrics in an objective and user-independent way. 

<p align="center">
  <b></b>
  <b>The moving average implementation for finding intersections with the reference curve </b>
  <img src="https://user-images.githubusercontent.com/39597223/123809942-b11fb180-d8fa-11eb-92a6-af26c3e64cf1.png" width="400" height="300" >
  </p>

### Phenological Metrics  
The final phenological products are eleven phenological metrics describing the phenological crop phases. The start, peak and end of season are determined, as mentioned before, as the intersections of the reference time-series and the forward and backward lagged moving average curves respectively measured in Days of Year (DOY). The rate of increase in NDVI during the beginning of the season is related to the physiognomy of the vegetation and the green up rate, as it describes the velocity at which the crop moves from the germination stage to the growth stage of the plant. On the other hand, the rate of decrease describes the rate of senescence at which the crop shifts from the flowering phase to the ripening stage, where the harvesting begins. Additionally, seven phenological integrals describing the productivity of the seasonal crop are calculated as expressed from the three abovementioned phenological packages (TIMESAT, CropPhenology, FenicePhenolo) and describe different phenological components. 

<p align="center">
  <b></b>
  <b>The large season integral and the small season integral as described in the TIMESAT package</b>
  <img src="https://user-images.githubusercontent.com/39597223/123808296-4a4dc880-d8f9-11eb-946b-8fe054b32d37.png" width="500" height="400" >
  </p>
  
The large season integral (LSI) can be used as a proxy of the relative amount of vegetation biomass without regarding the minimum values, whereas the small season integral (SSI) as a proxy of the relative amount of vegetation of biomass while regarding the minimum values . Furthermore, the cyclic fraction (CF) is directly related to the purely seasonal growth, whereas the permanent fraction (PF) describes the amount of vegetation that does not have a characteristic seasonal cycle within the growing season and the minimum permanent integral (MPI) describes the perennial vegetation component and depending on the vegetation index used may also contain components of soil substate. 

<p align="center">
  <b></b>
  <b>The cyclic fraction, the permanent fraction and the minimum permanent integral as described in the Phenolo package</b>
  <img src="https://user-images.githubusercontent.com/39597223/123809341-33f43c80-d8fa-11eb-8f18-708bcc74fe38.png" width="500" height="400" >
  </p>
  
As regards the TINDVIBeforeMax (BMI), describes the pre-anthesis crop growth, as pre-anthesis crop canopy growth is important for reducing evaporation of water from the soil surface and high values indicate high biomass accumulated before anthesis, which can indicate lower water evaporation from soil and high number of tillers and kernels being formed and can be used as a biomass proxy. Finally, the TINDVIAfterMax (AMI) describes the post-anthesis crop growth, where high values indicate smaller reductions in accumulated biomass during the post anthesis period, which relate to a slower and longer process of grain filling and is associated with low yield, can be used a yield proxy.

<p align="center">
  <b></b>
  <b>The TINDVIBeforeMax integral and TINDVIAfterMax integral as described in the CropPhenology package</b>
  <img src="https://user-images.githubusercontent.com/39597223/123809557-600fbd80-d8fa-11eb-82ed-9a2ae79b4b2b.png" width="500" height="400" >
  </p>

The following table presents the calculated phenological metrics jointly with the way calculated:<br/>

<b>Time of the start of season (SOS) </b>-	Time of the intersection point between the reference NDVI curve and the forward lagged moving average<br/>
<b>Time for the peak of the season (POS) </b>-	Time of the maximum NDVI value<br/>
<b>Time of the end of season (EOS) </b>-	Time of the intersection point between the reference NDVI curve and the backwards lagged moving average<br/>
<b>Rate of Increase (RoI) </b>-	Rate of difference between the SOS and the POS levels and the corresponding time difference<br/>
<b>Rate of Decrease (RoD) </b>-	Rate of difference between the POS and the EOS levels and the corresponding time difference<br/>
<b>Base level (BL) </b>-	Given as the average of the left and right minimum values<br/>
<b>Large seasonal integral (LSI) </b>-	Integral of the function describing the season from the season start to the season end<br/>
<b>Small seasonal integral (SSI) </b>-	Integral of the difference between the function describing the season and the base level from season start to season end<br/>
<b>Cyclic fraction (CF) </b>-	Integral defined from line above start (SOS) and end of season (POS) time and the line connecting SOS and POS<br/>
<b>Permanent fraction (PF) </b>-	Integral of area defined from the two subsequent local minima and the SOS and POS points<br/>
<b>Minimum permanent integral (MPI) </b>-	Integral of area defined from the line connecting the subsequent local minima and the time axis x<br/>
<b>TINDVIBeforeMax integral (BMI) </b>-	Numerical integration of NDVI between SOS and POS<br/>
<b>TINDVIAfterMax integral (AMI) </b>-	Numerical integration of NDVI between POS and EOS<br/>



