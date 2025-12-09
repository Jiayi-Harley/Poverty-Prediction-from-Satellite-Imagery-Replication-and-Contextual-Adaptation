# Poverty-Prediction-from-Satellite-Imagery-Replication-and-Contextual-Adaptation
This repository contains my replication of the baseline methodology from Jean et al. (2016), “Combining satellite imagery and machine learning to predict poverty,” Science.
The goal of this coursework is twofold:

Replicate the original AI method using the open dataset, achieving results within ±5% of the published metrics.

Adapt the same methodology to a new geographical context (Sichuan, China) to address SDG 1 – No Poverty.

## About the Data

1. The way of retrieving data that the author said is out of work, since the data has been archived and the google drive is out of use. Here's what we can still do: Download nightlights data from https://www.ngdc.noaa.gov/eog/viirs/download_dnb_composites.html. Use the 2015 annual composite in the 75N/060W tile and the 00N/060W tile. Choose the .tif file that has "vcm-orm-ntl" in the name. Save them to viirs_2015_<tile_descriptor>.tif, where tile_descriptor is 75N/060W or 00N/060W.
  
2. get the LSMS survey data from the world bank. Download the 2016-2017 Malawi survey data, 2015-2016 Ethiopia data, and the 2015-2016 Nigeria data from https://microdata.worldbank.org/index.php/catalog/lsms. Unzip the downloaded data into countries/<country name>/LSMS/. Country name should be either malawi_2016, ethiopia_2015, or nigeria_2015.

## Running the baseline replication
Once the data is in place, the replication mostly follows the structure of the original repository. The notebooks are already set up to process the survey data, download the satellite patches, train the night-light classifier, extract features, and fit the final regression model. As long as the files are in the paths described above, the notebooks should run without major changes. The main thing is to check that the night-light tiles and the LSMS folders are named correctly so the scripts can find them. After that, training the CNN and running the prediction notebook should reproduce the results within a few percentage points of the numbers in the paper.

## Adapting to the Sichuan China Data

For the Sichuan part, I needed something that could stand in for the DHS wealth index, since we obviously don’t have that kind of survey data for China. The 1-km GDP raster from Figshare turned out to be a good fit, because it gives a fairly detailed view of local economic activity and can be treated as a rough indicator of development levels. I clipped it to the Sichuan boundary from GADM so I could focus on the province. To keep the idea close to Jean et al. (2016), I still used nighttime lights as the main signal, pulling the annual VIIRS values for points across Sichuan. Once I had GDP and night-light matched for a large set of locations, the question was simply whether the same kind of relationship the original paper relies on also appears here. The final results suggested that it does: brighter areas generally show higher local GDP, and even a simple model can capture that pattern. It’s not a perfect setup, but it’s enough to show that the original approach transfers reasonably well to this new context.

## Repository structure

The repo is split into two parts. The first part is the replication, which stays close to the layout of the original project and includes the notebooks for processing the survey data, training the CNN, extracting features, and fitting the regression model. The second part contains the Sichuan adaptation, where I worked with the GDP raster, the province boundary, and the night-light data. I kept both sections separate so the original method and the adapted version don’t get mixed up, but they share the same general idea and the same style of workflow.

## Notes on results

The replication behaves pretty much the way the original paper describes, and the numbers land close to what was reported. The Sichuan model is less accurate, which is expected, but it still shows a clear relationship between night-light intensity and local GDP. It’s enough to show that the basic idea transfers, even though the data sources are different.

## Environment

I ran everything in Python 3.10 with PyTorch, GeoPandas, Rasterio, and the Earth Engine Python API. There’s nothing special about the setup, but I added a requirements file so the environment can be recreated easily. Most of the work was done in Google Colab, which already includes the main pieces I needed. The only extra step was installing Rasterio and enabling Earth Engine.
