# PhenologyExtraction
A repository folder regarding phenology extraction scripts utilizing existing packages (i.e. TIMESAT, CropPhenology) and proposing new methodologies. 

PhenologyExtractionRodopi.ipynb, Phenology_Extraction_NOA.ipynb are written in python 3.7 where as TIMESAT&CropPhenology.ipynb, CreateAnimatedTimeseries.ipynb, TIMESAT, NDVI-NDWI-PSRI for komotini parcels.ipynb are wirtten in R.

PhenologyExtractionRodopi: Cotton phenology extraction from Sentinel-2 data, combined with ground truth data provided at parcel level from cotton farmers from Rodopi, Greece

Phenology_Extraction_NOA: Phenlogoy extraction methodology exteding existing phenology extraction approaches, proposing a fully automated prototype for phenology extraction escaping from the user-oriented limitations of the existing packages. The main steps of this procedure are outlier removal based on the gaussian distribution of values, temporal interpolation creating decadal dates, regression fitting with Savitzky-Golay fitting, moving average to define intersections between reference and moving average curves and finaly the phenology extraction of meaningful metrics.

TIMESAT&CropPhenology: Utilizes a first approach combing TIMESAT and CropPhenology packages, in order to combine output metrics.

CreateAnimatedTimeseries: An animation regarding the timeseries of NDVI, NDWI, PSRI calculated from Sentinel-2 imagery.

TIMESAT: Phenology Extraction with TIMESAT package. TIMESAT is a software package for analysing time-series of satellite sensor data, able to investigate the seasonality of satellite time-series data and their relationship with dynamic properties of vegetation, such as phenology and temporal development.

NDVI-NDWI-PSRI for komotini parcels: Exploring timeseries of NDVI, NDWI, PSRI indices at parcel level to investigate past farming practices and define key-moments in phenology extraction.
