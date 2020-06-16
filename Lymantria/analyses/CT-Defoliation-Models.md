CT Defoliation Model Comparison
================
James Mickley and Audrey Barker Plotkin
June 16, 2020



  - [Overview](#overview)
      - [Summary of Results](#summary-of-results)
  - [Burlap Larva](#burlap-larva)
      - [Models](#models)
      - [AIC](#aic)
      - [R<sup>2</sup>](#r2)
      - [Plots from Top Baselines](#plots-from-top-baselines)
          - [sr\_2000-2010\_h13\_16d](#sr_2000-2010_h13_16d)
          - [tcg\_2000-2010\_h13\_full](#tcg_2000-2010_h13_full)
  - [Egg Mass Models](#egg-mass-models)
      - [AIC](#aic-1)
      - [R<sup>2</sup>](#r2-1)
      - [Plots from Top Baselines](#plots-from-top-baselines-1)
          - [sr\_2000-2010\_h13\_16d](#sr_2000-2010_h13_16d-1)
          - [tcg\_2000-2010\_h13\_full](#tcg_2000-2010_h13_full-1)
      - [Egg Mass Predictor](#egg-mass-predictor)
          - [AIC](#aic-2)
          - [R<sup>2</sup>](#r2-2)
          - [Plots](#plots)
  - [Graphs](#graphs)
      - [Compare condition scores between
        baselines](#compare-condition-scores-between-baselines)
      - [Condition Score Distributions](#condition-score-distributions)

## Overview

This analysis compares Val Pasquarella’s defoliation data from Landsat
satellite to

Here, we examine how varying the following components of the Landsat
change-in-condition model affect how well that predicts defoliation on
the ground: \* Spectral index (TGC, NDVI, SR, EVI) \* Baseline period
(2000-2010, 2005-2015) \* Harmonic periods (12- and -6 month, 12- and
4-month) \* Data included (all available data which varies over time,
consistent 16d interval)

We evaluate the predictive ability of the following: \* Landsat
condition scores predicting larval Lymantria abundance \* Landsat
condition scores predicting Lymantria egg mass abundance \* Egg mass
abundance predicting larval Lymantria abundance

### Summary of Results

  - For both larval abundance and egg masses, the baseline
    sr\_2000\_2010\_h13\_16d is the best predictor
  - All of the best models are SR (top 6 models). NDVI does
  - Condition score can account for 58-67% of the variation in larval
    abundance and 6-32% of the variation in egg masses
  - By comparison, egg masses only predict 55% of the variation in
    larval abundance, and condition scores outperform it as a predictor.
  - Predictive ability of Landsat condition scores weakens in 2018, the
    non-outbreak year, but there is still a pattern.
  - Egg masses only predict larval abundance during the outbreak, no
    relationship in 2018

<!-- end list -->

    'data.frame':   192 obs. of  48 variables:
     $ PointID                  : chr  "BB_BBL_5" "BB_BBL_6" "BB_BBL_7" "BB_BBS_5" ...
     $ Year                     : chr  "2017" "2017" "2017" "2017" ...
     $ m_evi_2000_2010_h12_16d  : num  -1.91 -2.98 -2.19 -2.45 -2.03 ...
     $ m_evi_2000_2010_h12_full : num  -2.22 -2.53 -2.41 -2.33 -1.98 ...
     $ m_evi_2000_2010_h13_16d  : num  -1.72 -2.76 -2.22 -2.11 -1.3 ...
     $ m_evi_2000_2010_h13_full : num  -1.95 -2.44 -2.29 -1.92 -1.1 ...
     $ m_evi_2005_2015_h12_16d  : num  -2.6 -3.46 -2.76 -2.57 -2.69 ...
     $ m_evi_2005_2015_h12_full : num  -2.2 -2.85 -2.09 -2.47 -2.15 ...
     $ m_evi_2005_2015_h13_16d  : num  -2.68 -3.59 -2.83 -2.31 -2.11 ...
     $ m_evi_2005_2015_h13_full : num  -2.15 -2.75 -1.98 -2.07 -1.78 ...
     $ m_ndvi_2000_2010_h12_16d : num  -1.44 -1.36 -1.33 -1.62 -1.01 ...
     $ m_ndvi_2000_2010_h12_full: num  -1.56 -1.79 -1.46 -1.63 -1.34 ...
     $ m_ndvi_2000_2010_h13_16d : num  -1.412 -1.723 -1.606 -1.609 -0.462 ...
     $ m_ndvi_2000_2010_h13_full: num  -1.535 -1.594 -1.236 -1.429 -0.725 ...
     $ m_ndvi_2005_2015_h12_16d : num  -2.15 -2.15 -1.96 -2.43 -1.87 ...
     $ m_ndvi_2005_2015_h12_full: num  -1.71 -2.18 -1.51 -1.98 -1.44 ...
     $ m_ndvi_2005_2015_h13_16d : num  -2.57 -2.57 -1.98 -2.44 -1.61 ...
     $ m_ndvi_2005_2015_h13_full: num  -1.87 -2.42 -1.95 -1.77 -1.26 ...
     $ m_reanalysis             : num  -2.82 -3.71 -3.06 -3.48 -3.12 ...
     $ m_sr_2000_2010_h12_16d   : num  -2.41 -2.6 -3.03 -2.14 -1.89 ...
     $ m_sr_2000_2010_h12_full  : num  -2.51 -2.66 -3.06 -2.21 -2.15 ...
     $ m_sr_2000_2010_h13_16d   : num  -2.14 -2.25 -2.57 -1.72 -1.25 ...
     $ m_sr_2000_2010_h13_full  : num  -1.98 -2.23 -2.39 -1.65 -1.41 ...
     $ m_sr_2005_2015_h12_16d   : num  -3.5 -4.39 -3.61 -3.26 -2.59 ...
     $ m_sr_2005_2015_h12_full  : num  -3.03 -3.17 -3.2 -3.05 -2.52 ...
     $ m_sr_2005_2015_h13_16d   : num  -3.38 -3.43 -3.33 -3.04 -2.15 ...
     $ m_sr_2005_2015_h13_full  : num  -2.79 -2.98 -2.8 -2.52 -1.91 ...
     $ m_tcg_2000_2010_h12_16d  : num  -3.26 -3.56 -2.95 -2.02 -1.5 ...
     $ m_tcg_2000_2010_h12_full : num  -2.75 -3.08 -3.04 -2.81 -2.38 ...
     $ m_tcg_2000_2010_h13_16d  : num  -3.12 -3.5 -2.55 -2.68 -1.25 ...
     $ m_tcg_2000_2010_h13_full : num  -2.91 -3.14 -2.15 -1.95 -1.45 ...
     $ m_tcg_2005_2015_h12_16d  : num  -2.55 -3.08 -3.07 -2.63 -2.9 ...
     $ m_tcg_2005_2015_h12_full : num  -2.55 -3.11 -2.26 -2.44 -2.29 ...
     $ m_tcg_2005_2015_h13_16d  : num  -3.25 -3.77 -2.92 -2.2 -2.25 ...
     $ m_tcg_2005_2015_h13_full : num  -2.1 -2.6 -2.62 -2.09 -1.7 ...
     $ BlockID                  : Factor w/ 13 levels "BB","BL","BS",..: 1 1 1 1 1 1 2 2 2 2 ...
     $ SiteID                   : Factor w/ 32 levels "BBL","BBS","BRL",..: 1 1 1 2 2 2 20 20 20 21 ...
     $ FragSize                 : num  388.8 388.8 388.8 26.9 26.9 ...
     $ ForestProp1km            : num  0.71 0.71 0.71 0.751 0.751 0.751 0.655 0.655 0.655 0.59 ...
     $ FragRatio1km             : num  1.81 1.81 1.81 1.5 1.5 ...
     $ Hunted                   : Factor w/ 2 levels "no","yes": 2 2 2 1 1 1 2 2 2 2 ...
     $ BrowseProb               : num  0.14 0.14 0.14 0.165 0.165 0.165 0.193 0.193 0.193 0.177 ...
     $ SiteDefoliation          : num  -2.57 -2.57 -2.57 -2.98 -2.98 ...
     $ EggMasses                : num  2 0 41 97 0 90 19 57 6 1 ...
     $ Abundance                : int  365 328 353 140 173 241 282 354 277 295 ...
     $ Alive                    : int  51 36 47 60 124 60 43 35 51 42 ...
     $ Pathogen                 : int  314 292 306 80 49 181 202 277 182 217 ...
     $ Mortality                : num  0.86 0.89 0.867 0.571 0.283 ...

## Burlap Larva

### Models

### AIC

Here we compare all of the baselines using
[AIC](https://en.wikipedia.org/wiki/Akaike_information_criterion) model
selection.

Models are ranked according to how good they are at predicting Lymantria
abundance from burlap traps.

The column to pay attention to is dAIC, or the difference in AIC between
models. A rule of thumb is that models with a dAIC less than 2 are not
notably different in their quality, and that models within 6 are
similar.

| model                          |     AIC |  dAIC | df | weight |
| :----------------------------- | ------: | ----: | -: | -----: |
| m\_sr\_2000\_2010\_h13\_16d    | 2097.97 |  0.00 |  7 |   0.79 |
| m\_sr\_2000\_2010\_h12\_16d    | 2102.15 |  4.18 |  7 |   0.10 |
| m\_sr\_2000\_2010\_h13\_full   | 2102.90 |  4.93 |  7 |   0.07 |
| m\_sr\_2005\_2015\_h13\_full   | 2104.64 |  6.68 |  7 |   0.03 |
| m\_sr\_2000\_2010\_h12\_full   | 2107.11 |  9.15 |  7 |   0.01 |
| m\_sr\_2005\_2015\_h12\_full   | 2107.29 |  9.32 |  7 |   0.01 |
| m\_sr\_2005\_2015\_h13\_16d    | 2111.07 | 13.10 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_full | 2111.37 | 13.40 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_16d  | 2111.64 | 13.67 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_full | 2111.95 | 13.99 |  7 |   0.00 |
| m\_reanalysis                  | 2113.65 | 15.68 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h13\_full  | 2114.00 | 16.03 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h13\_full  | 2114.00 | 16.03 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_16d  | 2114.33 | 16.36 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_16d  | 2114.56 | 16.59 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h12\_full  | 2116.26 | 18.29 |  7 |   0.00 |
| m\_sr\_2005\_2015\_h12\_16d    | 2116.61 | 18.64 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h13\_full  | 2119.09 | 21.12 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h13\_16d   | 2119.24 | 21.27 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h13\_full  | 2119.28 | 21.31 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h12\_16d   | 2119.79 | 21.82 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h12\_full  | 2121.20 | 23.23 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h13\_16d   | 2121.45 | 23.48 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h12\_full  | 2121.53 | 23.57 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h12\_16d   | 2121.84 | 23.87 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h12\_16d   | 2122.40 | 24.43 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_full | 2122.67 | 24.70 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h12\_full  | 2122.82 | 24.85 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h13\_16d   | 2122.82 | 24.86 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_full | 2123.18 | 25.21 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h13\_16d   | 2123.53 | 25.56 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h12\_16d   | 2126.95 | 28.98 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_16d  | 2128.81 | 30.84 |  7 |   0.00 |

### R<sup>2</sup>

Here, we are calculating the proportion of variance in the Lymantria
abundance data that is explained by each model.

We actually get two R<sup>2</sup> numbers for these models, a marginal
and a conditional R<sup>2</sup>:

  - **conditional R<sup>2</sup>**: the proportion of variance explained
    by the whole model: year, defoliation score, block, and site
  - **marginal R<sup>2</sup>**: the proportion of variance explained by
    just year and defoliation score (just fixed factors)

In our case, we’re mostly interested in the marginal R<sup>2</sup>. This
is going to tell us how well that particular defoliation score explains
the abundance of Lymantria.

    Random effect variances not available. Returned R2 does not account for random effects.

| baseline                       | R2\_marginal | R2\_conditional |
| :----------------------------- | -----------: | --------------: |
| m\_sr\_2005\_2015\_h12\_full   |         0.74 |              NA |
| m\_sr\_2005\_2015\_h13\_full   |         0.67 |            0.78 |
| m\_sr\_2000\_2010\_h13\_16d    |         0.66 |            0.79 |
| m\_ndvi\_2005\_2015\_h13\_full |         0.66 |            0.76 |
| m\_sr\_2000\_2010\_h13\_full   |         0.65 |            0.79 |
| m\_sr\_2000\_2010\_h12\_full   |         0.65 |            0.78 |
| m\_ndvi\_2005\_2015\_h13\_16d  |         0.65 |            0.76 |
| m\_sr\_2000\_2010\_h12\_16d    |         0.65 |            0.79 |
| m\_reanalysis                  |         0.65 |            0.76 |
| m\_sr\_2005\_2015\_h13\_16d    |         0.64 |            0.77 |
| m\_ndvi\_2005\_2015\_h12\_full |         0.64 |            0.73 |
| m\_ndvi\_2000\_2010\_h13\_16d  |         0.63 |            0.76 |
| m\_ndvi\_2000\_2010\_h12\_full |         0.63 |            0.74 |
| m\_sr\_2005\_2015\_h12\_16d    |         0.63 |            0.76 |
| m\_ndvi\_2000\_2010\_h13\_full |         0.62 |            0.77 |
| m\_ndvi\_2000\_2010\_h12\_16d  |         0.62 |            0.76 |
| m\_evi\_2005\_2015\_h13\_16d   |         0.61 |            0.76 |
| m\_evi\_2005\_2015\_h12\_16d   |         0.61 |            0.76 |
| m\_tcg\_2005\_2015\_h13\_16d   |         0.61 |            0.77 |
| m\_evi\_2005\_2015\_h12\_full  |         0.61 |            0.76 |
| m\_tcg\_2000\_2010\_h13\_full  |         0.61 |            0.76 |
| m\_tcg\_2005\_2015\_h12\_16d   |         0.61 |            0.74 |
| m\_tcg\_2005\_2015\_h13\_full  |         0.61 |            0.76 |
| m\_evi\_2000\_2010\_h12\_full  |         0.60 |            0.77 |
| m\_evi\_2000\_2010\_h12\_16d   |         0.60 |            0.75 |
| m\_evi\_2005\_2015\_h13\_full  |         0.60 |            0.76 |
| m\_evi\_2000\_2010\_h13\_full  |         0.60 |            0.78 |
| m\_evi\_2000\_2010\_h13\_16d   |         0.60 |            0.76 |
| m\_ndvi\_2005\_2015\_h12\_16d  |         0.60 |            0.74 |
| m\_tcg\_2000\_2010\_h12\_16d   |         0.59 |            0.76 |
| m\_tcg\_2000\_2010\_h13\_16d   |         0.59 |            0.76 |
| m\_tcg\_2005\_2015\_h12\_full  |         0.59 |            0.76 |
| m\_tcg\_2000\_2010\_h12\_full  |         0.58 |            0.76 |

### Plots from Top Baselines

#### sr\_2000-2010\_h13\_16d

![](CT-Defoliation-Models_files/figure-gfm/Burlap_sr_Param-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Burlap_sr_Pred-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Burlap_sr_Combined-1.png)<!-- -->

#### tcg\_2000-2010\_h13\_full

![](CT-Defoliation-Models_files/figure-gfm/Burlap_tcg_Param-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Burlap_tcg_Pred-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Burlap_tcg_Combined-1.png)<!-- -->

## Egg Mass Models

### AIC

| model                          |     AIC |  dAIC | df | weight |
| :----------------------------- | ------: | ----: | -: | -----: |
| m\_sr\_2000\_2010\_h13\_16d    | 1037.17 |  0.00 |  7 |   0.56 |
| m\_sr\_2000\_2010\_h12\_16d    | 1039.02 |  1.85 |  7 |   0.22 |
| m\_sr\_2000\_2010\_h13\_full   | 1040.61 |  3.44 |  7 |   0.10 |
| m\_sr\_2005\_2015\_h13\_full   | 1041.22 |  4.05 |  7 |   0.07 |
| m\_sr\_2000\_2010\_h12\_full   | 1042.64 |  5.48 |  7 |   0.04 |
| m\_sr\_2005\_2015\_h12\_full   | 1045.85 |  8.69 |  7 |   0.01 |
| m\_reanalysis                  | 1045.95 |  8.79 |  7 |   0.01 |
| m\_ndvi\_2005\_2015\_h13\_full | 1048.95 | 11.78 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h13\_full  | 1052.78 | 15.62 |  7 |   0.00 |
| m\_sr\_2005\_2015\_h13\_16d    | 1052.91 | 15.75 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h13\_16d   | 1053.15 | 15.98 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_16d  | 1054.02 | 16.86 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_full | 1054.80 | 17.63 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_16d  | 1055.06 | 17.89 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h12\_full  | 1056.09 | 18.93 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h12\_16d   | 1056.13 | 18.97 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h12\_full  | 1056.52 | 19.35 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h13\_16d   | 1056.54 | 19.38 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h12\_16d   | 1056.63 | 19.47 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h13\_16d   | 1056.81 | 19.64 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h13\_16d   | 1056.81 | 19.65 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_full | 1058.46 | 21.30 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h12\_16d   | 1059.09 | 21.92 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_16d  | 1059.17 | 22.01 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h13\_full  | 1059.94 | 22.78 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h12\_16d   | 1060.04 | 22.88 |  7 |   0.00 |
| m\_sr\_2005\_2015\_h12\_16d    | 1060.70 | 23.53 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h12\_full  | 1061.49 | 24.33 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h13\_full  | 1061.90 | 24.74 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h13\_full  | 1062.11 | 24.95 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h12\_full  | 1062.27 | 25.11 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_16d  | 1064.92 | 27.76 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_full | 1065.42 | 28.25 |  7 |   0.00 |

### R<sup>2</sup>

| baseline                       | R2\_marginal | R2\_conditional |
| :----------------------------- | -----------: | --------------: |
| m\_sr\_2005\_2015\_h13\_full   |         0.32 |            0.80 |
| m\_sr\_2000\_2010\_h13\_16d    |         0.30 |            0.81 |
| m\_sr\_2000\_2010\_h13\_full   |         0.29 |            0.81 |
| m\_sr\_2000\_2010\_h12\_16d    |         0.29 |            0.80 |
| m\_sr\_2000\_2010\_h12\_full   |         0.29 |            0.81 |
| m\_sr\_2005\_2015\_h12\_full   |         0.29 |            0.79 |
| m\_reanalysis                  |         0.19 |            0.81 |
| m\_ndvi\_2005\_2015\_h13\_full |         0.19 |            0.81 |
| m\_sr\_2005\_2015\_h13\_16d    |         0.19 |            0.78 |
| m\_ndvi\_2005\_2015\_h13\_16d  |         0.14 |            0.81 |
| m\_ndvi\_2000\_2010\_h13\_16d  |         0.13 |            0.79 |
| m\_sr\_2005\_2015\_h12\_16d    |         0.13 |            0.78 |
| m\_evi\_2000\_2010\_h13\_full  |         0.13 |            0.81 |
| m\_tcg\_2005\_2015\_h13\_16d   |         0.13 |            0.81 |
| m\_evi\_2000\_2010\_h13\_16d   |         0.13 |            0.80 |
| m\_evi\_2005\_2015\_h12\_16d   |         0.13 |            0.81 |
| m\_evi\_2005\_2015\_h13\_16d   |         0.12 |            0.81 |
| m\_evi\_2000\_2010\_h12\_full  |         0.11 |            0.80 |
| m\_tcg\_2005\_2015\_h12\_16d   |         0.11 |            0.81 |
| m\_ndvi\_2000\_2010\_h13\_full |         0.11 |            0.80 |
| m\_tcg\_2000\_2010\_h12\_full  |         0.10 |            0.80 |
| m\_ndvi\_2000\_2010\_h12\_full |         0.10 |            0.79 |
| m\_tcg\_2000\_2010\_h13\_16d   |         0.10 |            0.80 |
| m\_tcg\_2000\_2010\_h12\_16d   |         0.09 |            0.79 |
| m\_ndvi\_2000\_2010\_h12\_16d  |         0.09 |            0.79 |
| m\_evi\_2000\_2010\_h12\_16d   |         0.09 |            0.79 |
| m\_tcg\_2000\_2010\_h13\_full  |         0.09 |            0.80 |
| m\_evi\_2005\_2015\_h12\_full  |         0.09 |            0.79 |
| m\_evi\_2005\_2015\_h13\_full  |         0.08 |            0.80 |
| m\_tcg\_2005\_2015\_h12\_full  |         0.08 |            0.79 |
| m\_tcg\_2005\_2015\_h13\_full  |         0.08 |            0.80 |
| m\_ndvi\_2005\_2015\_h12\_16d  |         0.07 |            0.79 |
| m\_ndvi\_2005\_2015\_h12\_full |         0.06 |            0.79 |

### Plots from Top Baselines

#### sr\_2000-2010\_h13\_16d

![](CT-Defoliation-Models_files/figure-gfm/Egg_sr_Param-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Egg_sr_Pred-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Egg_sr_Combined-1.png)<!-- -->

#### tcg\_2000-2010\_h13\_full

![](CT-Defoliation-Models_files/figure-gfm/Egg_tcg_Param-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Egg_tcg_Pred-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Egg_tcg_Combined-1.png)<!-- -->

### Egg Mass Predictor

#### AIC

| model                             |     AIC |  dAIC | df | weight |
| :-------------------------------- | ------: | ----: | -: | -----: |
| m\_sr\_2000-2010\_h13\_16d        | 2097.97 |  0.00 |  7 |      1 |
| m\_tcg\_2000-2010\_h13\_full      | 2114.00 | 16.03 |  7 |      0 |
| Predict abundance with egg masses | 2123.20 | 25.23 |  7 |      0 |

#### R<sup>2</sup>

    Abundance ~ EggMasses * Year + (1 | BlockID/SiteID)
    # R2 for Mixed Models
    
      Conditional R2: 0.760
         Marginal R2: 0.555

#### Plots

![](CT-Defoliation-Models_files/figure-gfm/Egg_Predictor_Param-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Egg_Predictor_Pred-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/Egg_Predictor_Combined-1.png)<!-- -->

## Graphs

Let’s compare the old baseline model (reanalysis) to the new model with
the same parameters (tasseled cap greenness, 2000-2010, h13 harmonics,
full dataset), and see what has changed in the distribution of scores

![](CT-Defoliation-Models_files/figure-gfm/New_Baseline_Comparison_2017-1.png)<!-- -->

![](CT-Defoliation-Models_files/figure-gfm/New_Baseline_Comparison_2018-1.png)<!-- -->

#### Compare condition scores between baselines

Here we are looking at how well condition scores for individual plots
agree between the original reanalysis data product and the new condition
scores.

A lot of scatter means that at a point level, things are substantially
different.

Red lines are slope = 1. In both cases, Val’s new models have less
negative condition scores (values shifted up relative to the reanalysis
ones). There’s not much change in slope, which is good.

![](CT-Defoliation-Models_files/figure-gfm/Baseline_Comp-1.png)<!-- -->

#### Condition Score Distributions

Another interesting comparison is to compare the distribution of
condition scores for the same year between Val’s models

There’s some variation in distribution shape, spread, and how negative
scores are between baselines. NDVI is consistently less negative.

![](CT-Defoliation-Models_files/figure-gfm/Score_Distributions-1.png)<!-- -->
