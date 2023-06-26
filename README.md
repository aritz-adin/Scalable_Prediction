# A scalable approach for short-term disease forecasting in high spatial resolution areal data

This repository contains the R code to fit the models described in the paper entitled _"A scalable approach for short-term disease forecasting in high spatial resolution areal data"_ [(Orozco-Acosta et al., 2023)](https://arxiv.org/abs/2303.16549), as well as to reproduce similar figures and tables to the ones presented in the paper. Note that due to confidentiality issues, simulated data sets has are provided and then, results are not fully reproducible.

All computations were performed using version 0.5.1 of the R package [**bigDM**](https://cran.r-project.org/web/packages/bigDM/index.html), which was released on CRAN on February 23, 2023. This version includes adaptations to the `STCAR_INLA()` function, making it compatible for short-term forecasting. 
The package also includes several univariate and multivariate spatial and spatio-temporal Bayesian models for high-dimensional areal count data based on the integrated nested Laplace approximation (INLA) estimation technique (http://www.r-inla.org/).

See [https://github.com/spatialstatisticsupna/bigDM](https://github.com/spatialstatisticsupna/bigDM) for details about installation and access to the vignettes accompanying this package.


## Table of contents

- [Cancer mortality data](#Cancer-mortality-data)
- [R code](#R-code)
- [Acknowledgements](#Acknowledgements)
- [References](#References)


## Cancer mortality data

The proposed methodology is applied to project male lung cancer and overall cancer (all sites) mortality data in the 7907 municipalities of continental Spain by considering three-year ahead predictions using the period 1991-2012 as reference.

The `Data_LungCancer` object available at the **bigDM** package, contains simulated data of male lung cancer mortality counts (modified in order to preserve the confidentiality of the original data). Specifically, the data set contains the following variables:
- ```ID```: character vector of geographic identifiers
- ```year```: numeric vector of years identifiers
- ```obs```: observed number of cases
- ```exp```: expected number of cases
- ```SMR```: standardized mortality ratios
- ```pop```: population at risk

Use the following commands to load the data
```r 
> library(bigDM)
> data("Data_LungCancer")

> head(Data_LungCancer)
     ID year obs        exp      SMR     pop
1 01001 1991   0 0.27554975 0.000000  483.77
2 01002 1991   3 2.72124997 1.102435 4948.98
3 01003 1991   0 0.49612295 0.000000  667.91
4 01004 1991   0 0.37040942 0.000000  591.11
5 01006 1991   0 0.06999827 0.000000   62.81
6 01008 1991   0 0.29240328 0.000000  354.80
```

Similarly, an Rdata containing simulated data of male overall cancer mortality counts can be loaded as:
```r 
> load(url("https://emi-sstcdapp.unavarra.es/bigDM/inst/Rdata/Data_OverallCancer.Rdata"))

> head(Data_OverallCancer)
     ID year obs       exp       SMR     pop
1 01001 1991   1 1.0125164 0.9876384  483.77
2 01002 1991  10 9.8199947 1.0183305 4948.98
3 01003 1991   1 1.8756597 0.5331458  667.91
4 01004 1991   1 1.4252320 0.7016401  591.11
5 01006 1991   0 0.2518388 0.0000000   62.81
6 01008 1991   2 1.0323942 1.9372445  354.80
```


## R code

The code of this paper is organized in self-contained folders, which are named according to the corresponding sections of the paper.


[**Section 4. Predictive validation study**](https://github.com/spatialstatisticsupna/Scalable_Prediction/tree/main/Section4_PredictiveValidationStudy)


[**Section 5. Illustration: projections of cancer mortality in Spain**](https://github.com/spatialstatisticsupna/Scalable_Prediction/tree/main/R/Section5_Illustration)

- [**Fit_models.R**](https://github.com/spatialstatisticsupna/Scalable_Prediction/tree/main/R/Section5_Illustration/Fit_models.R)

  This R script contains the necessary functions to replicate the fit of spatio-temporal *classical* and *partition* models considered in the illustration section of Orozco-Acosta et al. (2023) using the [bigDM](https://github.com/spatialstatisticsupna/bigDM) package. The code can be used with any other data sets with similar structure.
  
  It also computes the Logarithmic Score (based on both LOOCV and LGOCV approaches) and model selection criteria (DIC and WAIC) to reproduce the results shown in **Table 3**.
  
  **IMPORTANT NOTE**: In order to compute Logarithmic Score measures under the partition models (Disjoint or k-order neighbourhood models) the sub-models must be previously saved by setting the argument `STCAR_INLA(..., save.models=TRUE)`.


- [**LungCancer_Results.R**](https://github.com/spatialstatisticsupna/Scalable_Prediction/tree/main/R/Section5_Illustration/LungCancer_Results.R)



### Version info
``` {.r}
R version 4.2.1 (2022-06-23 ucrt)
Platform: x86_64-w64-mingw32/x64 (64-bit)
Running under: Windows 10 x64 (build 17763)
```


# Acknowledgements

This research has been supported by the project PID2020-113125RBI00/MCIN/AEI/10.13039/501100011033.

![image](https://github.com/spatialstatisticsupna/Scalable_Prediction/blob/main/micin-aei.jpg)


# References

[Liu, Z., and Rue, H. (2022). Leave-Group-Out Cross-Validation For Latent Gaussian Models. _arXiv preprint_.](https://doi.org/10.48550/arXiv.2210.04482)

[Orozco-Acosta, E., Riebler, A., Adin, A., and Ugarte, M.D. (2023). A scalable approach for short-term disease forecasting in high spatial resolution areal data. _arXiv preprint_.](https://arxiv.org/abs/2303.16549)
