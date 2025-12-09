This part of the repository contains the Sichuan adaptation. The main idea here is to take the model from the original paper and see how far it can be pushed in a completely different setting, using data that is actually available for China. I use the 1-km GDP raster from Figshare as a rough proxy for local economic conditions and clip it to the Sichuan boundary from GADM. Around a set of sampled locations in the province, I collect two kinds of satellite-based signals: annual VIIRS night-light intensity and small Sentinel-2 RGB patches.

On the modelling side, the adaptation reuses the CNN trained in the baseline replication. Instead of training a new network from scratch on Chinese data, I feed the Sichuan Sentinel-2 patches through the existing night-light CNN and keep the feature vectors from the last layer before the classifier. These CNN features are then combined with the GDP values at the same locations, and a simple regression model is trained to predict GDP. This mirrors the final step in Jean et al. (2016), where CNN features are used as inputs to a regression model, but replaces the DHS wealth index with a gridded GDP proxy for Sichuan.

The goal is not to build a highly accurate GDP model, but to check whether the visual cues learned in the original setting still carry useful information in this new one. The results suggest that they do: locations with higher night-light intensity and more “built-up” looking patches tend to have higher local GDP, although the relationship is noisier than in the DHS countries.

The data folders here only include small files generated during the process (such as sample_points.csv). The larger datasets (GDP raster, shapefile) are not uploaded to GitHub, but the sources and download links are listed below so the workflow can be reproduced.

![Scatter plot of GDP vs NTL](results/gdp_vs_ntl_scatter.png)

This plot is just a quick check to see whether the night-light signal has any relationship with the GDP values we sampled across Sichuan. The points are fairly spread out, but there’s a general upward tendency: brighter locations usually match with higher local GDP. It’s not a tight pattern, which is expected given the noise in both datasets, but it’s enough to show that the basic idea still holds here and that the night-light intensity does carry some information about local economic conditions.

The Sentinel-2 patches and CNN feature arrays are not committed to the repository due to size, but the notebooks in `adaptation/code/` show how they were created.
