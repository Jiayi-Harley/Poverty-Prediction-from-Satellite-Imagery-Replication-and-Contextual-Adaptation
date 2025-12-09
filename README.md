# Poverty-Prediction-from-Satellite-Imagery-Replication-and-Contextual-Adaptation
This repository contains my replication of the baseline methodology from Jean et al. (2016), “Combining satellite imagery and machine learning to predict poverty,” Science.
The goal of this coursework is twofold:

Replicate the original AI method using the open dataset, achieving results within ±5% of the published metrics.

Adapt the same methodology to a new geographical context (Sichuan, China) to address SDG 1 – No Poverty.

## About the Data

1. The way of retrieving data that the author said is out of work, since the data has been archived and the google drive is out of use. Here's what we can still do: Download nightlights data from https://www.ngdc.noaa.gov/eog/viirs/download_dnb_composites.html. Use the 2015 annual composite in the 75N/060W tile and the 00N/060W tile. Choose the .tif file that has "vcm-orm-ntl" in the name. Save them to viirs_2015_<tile_descriptor>.tif, where tile_descriptor is 75N/060W or 00N/060W.
  
2. get the LSMS survey data from the world bank. Download the 2016-2017 Malawi survey data, 2015-2016 Ethiopia data, and the 2015-2016 Nigeria data from https://microdata.worldbank.org/index.php/catalog/lsms. Unzip the downloaded data into countries/<country name>/LSMS/. Country name should be either malawi_2016, ethiopia_2015, or nigeria_2015.
