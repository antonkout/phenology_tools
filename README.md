# PhenologyExtraction
A repository folder regarding phenology extraction scripts utilizing existing packages (i.e. TIMESAT, CropPhenology) and proposing new methodologies. 

PhenologyExtractionRodopi.ipynb, Phenology_Extraction_NOA.ipynb are written in python 3.7 where as TIMESAT&CropPhenology.ipynb, CreateAnimatedTimeseries.ipynb, TIMESAT, NDVI-NDWI-PSRI for komotini parcels.ipynb are wirtten in R.

PhenologyExtractionRodopi: Cotton phenology extraction from Sentinel-2 data, combined with ground truth data provided at parcel level from cotton farmers from Rodopi, Greece
Phenology_Extraction_NOA: Phenlogoy extraction methodology exteding existing phenology extraction approaches, proposing a fully automated prototype for phenology extraction escaping from the user-oriented limitations of the existing packages. The main steps of this procedure are outlier removal based on the gaussian distribution of values, temporal interpolation creating decadal dates, regression fitting with Savitzky-Golay fitting, moving average to define intersections between reference and moving average curves and finaly the phenology extraction of meaningful metrics.
TIMESAT&CropPhenology: Utilizes a first approach combing TIMESAT and CropPhenology packages, in order to combine output metrics.
CreateAnimatedTimeseries: An animation regarding the timeseries of NDVI, NDWI, PSRI calculated from Sentinel-2 imagery.
TIMESAT: Phenology Extraction with TIMESAT package. TIMESAT is a software package for analysing time-series of satellite sensor data, able to investigate the seasonality of satellite time-series data and their relationship with dynamic properties of vegetation, such as phenology and temporal development.
NDVI-NDWI-PSRI for komotini parcels: Exploring timeseries of NDVI, NDWI, PSRI indices at parcel level to investigate past farming practices and define key-moments in phenology extraction.

Phenology_Extraction_NOA in detail:
Based on an extended bibliographic research, this workflow was constructed in order to identify the critical phenological phases describing cotton crop, in order to evaluate the results of the developed phenology extraction service and improve the precision of the model. Within this framework, three phenological phases have been identified, apart from the germination phase, which are the vegetative, the reproducing and the ripening phase respectively. Each of these phases, are separated in individual phenological stages which describe the physiognomy of the plant. Moreover, the phenological development stages of plants, which is used in a variety of fields of application, such as in a number of scientific disciples and in the agricultural industry, use the BBCH-scale decimal code system, which is divided into primary and secondary growth stages, developed by Zadoks , to describe the stages of growth in plants. The following table presents the primary growth stages of cotton crop in the BBCH-scale among with the corresponding phenological stages and the phenological phases which are belong:

BBCH Code	Definition	Phenological Stage	Phenological Phase
0	Germination	Germination	Germination phase
1	Leaf Development (main shoot)	Tillering stage	Vegetative phase
2	Formation of side shoots		
3	Stem elongation (main shoot)	Stem elongation	
4	Development of harvestable vegetative plant parts	Panicle initiation	Reproductive phase
5	Inflorescence emergence	Booting/Heading stage	
6	Flowering	Flowering stage	
7	Development of fruits and seeds	Milk stage	Ripening phase
8	Ripening of fruits and seeds	Dough stage	
9	Senescence	Mature stage	

To begin with, germination starts as the seed absorbs water and oxygen through its chalaza after planting. The hypocotyl elongates from the radicle and form an arch that begins to push up through the soil. The seedling emergence normally takes place 4 to 14 days after sowing and after a week the first true leaf forms above cotyledons and shift from emergence to vegetative growth. At this point, the germination and seedlings emergence stages are finished, and the plant enters the vegetative phase. The vegetative phase starts when the first vegetative structures appear on the main stem. Main stem leaves and branches form points of attachment on the main stem called nodes. Generally, a new node is produced an average of every 3 days, although nodes develop more quickly early in the growing season than later in the season. The development of vegetative growth and fruiting in this phase is highly related to temperature if adequate moisture is available. The plant growth and development are functions of the sunlight interception and temperature and new leaves appear increasing the leaf area of cotton plant rapidly.  Furthermore, cotton has an indeterminate growth habit and can grow very tall under conditions of unrestrained growth. Unmanaged growth promotes diseases and makes the cultivation practice of harvesting very difficult. Subsequently, the reproductive phase follows when reproductive structures begin to appear on the plant and the carbohydrate supplies are slowly shifted from the production of roots and leaves (vegetative phase) to the development of fruits (reproductive phase). As the fruit load on the plant increases and ages, the development of new leaves steadily declines. As a result, fruit development can be identified when the leaf population is steadily decreases. Furthermore, the leaf photosynthesis does not remain constant as the leaf grows, where after 20 days of age, a cotton leaf reaches its maximum photosynthetic capacity and therefore declines. At the phenological stage of flowering, the squares are visible on nodes about 35 days after planting and the whole blooming time lasts approximately six weeks. Finally, the ripening phase follows, where the pollinated flowers form cotton bolls and around 5-7 days after bloom, flower dries and falls off, exposing the cotton boll. After pollination, it takes 50 days for the boll to fully develop and open. The three major phases of boll development are categorized as the enlargement, filling and maturation phase.  

The phenology extraction method relies on the investigation of satellite derived time-series and more precisely on the analysis of three different indices such as the Normalized Difference Vegetation Index (NDVI), the Normalized Difference Water Index (NDWI) and the Plant Senescence Reflectance Index (PSRI). NOA has already implemented a phenology extraction method combining the abovementioned indices for detecting phenological phases of paddy rice in South Korea, implementing the TIMESAT package. Extending the existing methodology and combining phenological processes and metrics from three different freely available packages, which are namely TIMESAT , CropPhenology  and FenicePhenolo , NOA has finalized its own generalized fully automated prototype for phenology extraction escaping from the user-oriented limitations of the TIMESAT package. 

![Picture1](https://user-images.githubusercontent.com/39597223/123802419-f55b8380-d8f3-11eb-83bc-575a59e02f8b.png)


