This part of the repository contains the Sichuan adaptation. The goal here is simply to see whether the idea from the original paper also appears in a different setting, using data that is actually available for China. I used the 1-km GDP raster from Figshare as a rough proxy for economic conditions, and I clipped it to the Sichuan boundary from GADM. For the satellite signal, I used the annual VIIRS night-light data from Google Earth Engine.

The workflow in this folder follows a simple structure: one notebook prepares the Sichuan data by sampling points across the province and matching each point with its GDP value and night-light value, and another notebook trains a small regression model to see how well the night-light signal explains the variation in GDP. The idea is not to build a perfect model but to check whether the core relationship described in the original paper still holds. The results suggest that it does: brighter places generally correspond to higher local GDP, although the strength of the pattern is smaller than in the DHS setting.

![Scatter plot of GDP vs NTL](results/gdp_vs_ntl_scatter.png)

The data folders here only include small files generated during the process (such as sample_points.csv). The larger datasets (GDP raster, shapefile) are not uploaded to GitHub, but the sources and download links are listed below so the workflow can be reproduced.
