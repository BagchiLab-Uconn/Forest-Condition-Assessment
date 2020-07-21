Defoliation Model Comparison
================
James Mickley and Audrey Barker Plotkin
July 21, 2020



  - [Overview](#overview)
      - [Summary of Results](#summary-of-results)
  - [Quabbin](#quabbin)
      - [Models](#models)
      - [AIC](#aic)
      - [R<sup>2</sup>](#r2)
  - [CT Burlap Larva](#ct-burlap-larva)
      - [Models](#models-1)
      - [AIC](#aic-1)
          - [Both Years](#both-years)
          - [2017 Only](#only)
      - [R<sup>2</sup>](#r2-1)
      - [Plots from Top Baselines](#plots-from-top-baselines)
          - [sr\_2000-2010\_h13\_16d](#sr_2000-2010_h13_16d)
          - [tcg\_2000-2010\_h13\_full](#tcg_2000-2010_h13_full)
  - [Egg Mass Models](#egg-mass-models)
      - [AIC](#aic-2)
          - [Both Years](#both-years-1)
          - [2017 Only](#only-1)
      - [R<sup>2</sup>](#r2-2)
      - [Plots from Top Baselines](#plots-from-top-baselines-1)
          - [sr\_2000-2010\_h13\_16d](#sr_2000-2010_h13_16d-1)
          - [tcg\_2000-2010\_h13\_full](#tcg_2000-2010_h13_full-1)
      - [Egg Mass Predictor](#egg-mass-predictor)
          - [AIC](#aic-3)
          - [R<sup>2</sup>](#r2-3)
          - [Plots](#plots)
  - [Graphs](#graphs)
      - [Compare condition scores between
        baselines](#compare-condition-scores-between-baselines)
      - [Condition Score Distributions](#condition-score-distributions)

## Overview

This analysis compares Val Pasquarella’s defoliation data from Landsat
satellite to the following:

1 Defoliation data collected in late September 2017 from 483 points
within 6 ‘hotspots’ in the Quabbin Watershed Forest (Rich MacLean, DCR
Watershed Forester field data lead). 2 Lymantria larval and egg mass
abundance data collected in 2017 and 2018 from 12 trees each in 32
forest fragments of varying size in Eastern Connecticut.

Here, we examine how varying the following components of the Landsat
change-in-condition model affect how well that predicts defoliation or
Lymantria abundance on the ground:

  - Spectral index (TGC, NDVI, SR, EVI)
  - Baseline period (2000-2010, 2005-2015)
  - Harmonic periods (12- and -6 month, 12- and 4-month)
  - Data included (all available data which varies over time, consistent
    16d interval)

We evaluate the predictive ability of the following: \* Landsat
condition scores predicting the proportion of canopy defoliated \*
Landsat condition scores predicting larval Lymantria abundance \*
Landsat condition scores predicting Lymantria egg mass abundance \* Egg
mass abundance predicting larval Lymantria abundance

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
     $ m_evi_2000_2010_h12_16d  : num  -2.87 -3.37 -2.99 -3.39 -3.01 ...
     $ m_evi_2000_2010_h12_full : num  -2.61 -3.13 -2.79 -2.95 -2.75 ...
     $ m_evi_2000_2010_h13_16d  : num  -2.62 -3.05 -2.57 -2.87 -2.27 ...
     $ m_evi_2000_2010_h13_full : num  -2.26 -2.8 -2.3 -2.28 -1.98 ...
     $ m_evi_2005_2015_h12_16d  : num  -3.11 -3.4 -3.1 -3.06 -2.82 ...
     $ m_evi_2005_2015_h12_full : num  -2.54 -2.92 -2.37 -2.83 -2.73 ...
     $ m_evi_2005_2015_h13_16d  : num  -3.08 -3.4 -2.91 -3.01 -2.36 ...
     $ m_evi_2005_2015_h13_full : num  -2.62 -2.93 -2.35 -2.61 -2.21 ...
     $ m_ndvi_2000_2010_h12_16d : num  -2.05 -2.06 -1.97 -2.86 -1.77 ...
     $ m_ndvi_2000_2010_h12_full: num  -1.89 -1.96 -1.77 -2.55 -1.75 ...
     $ m_ndvi_2000_2010_h13_16d : num  -2.03 -1.92 -1.81 -2.6 -1.37 ...
     $ m_ndvi_2000_2010_h13_full: num  -1.79 -1.91 -1.57 -2.09 -1.33 ...
     $ m_ndvi_2005_2015_h12_16d : num  -2.45 -2.37 -1.93 -2.95 -1.83 ...
     $ m_ndvi_2005_2015_h12_full: num  -2.07 -2.15 -1.65 -2.54 -1.78 ...
     $ m_ndvi_2005_2015_h13_16d : num  -2.95 -2.76 -2.25 -3.1 -1.83 ...
     $ m_ndvi_2005_2015_h13_full: num  -2.42 -2.49 -1.91 -2.42 -1.67 ...
     $ m_reanalysis             : num  -2.82 -3.71 -3.06 -3.48 -3.12 ...
     $ m_sr_2000_2010_h12_16d   : num  -3.35 -3.38 -3.32 -3.3 -2.12 ...
     $ m_sr_2000_2010_h12_full  : num  -2.62 -3.03 -2.95 -2.79 -2.13 ...
     $ m_sr_2000_2010_h13_16d   : num  -2.62 -2.7 -2.57 -2.69 -1.56 ...
     $ m_sr_2000_2010_h13_full  : num  -2.07 -2.44 -2.28 -2.09 -1.58 ...
     $ m_sr_2005_2015_h12_16d   : num  -4.18 -3.82 -3.89 -4.08 -2.7 ...
     $ m_sr_2005_2015_h12_full  : num  -3.32 -3.43 -3.06 -3.67 -2.69 ...
     $ m_sr_2005_2015_h13_16d   : num  -3.57 -3.32 -3.14 -3.54 -2.28 ...
     $ m_sr_2005_2015_h13_full  : num  -2.9 -2.99 -2.58 -2.89 -2.13 ...
     $ m_tcg_2000_2010_h12_16d  : num  -3.02 -3.54 -3.12 -3.49 -3.07 ...
     $ m_tcg_2000_2010_h12_full : num  -2.71 -3.32 -2.97 -3.09 -2.82 ...
     $ m_tcg_2000_2010_h13_16d  : num  -2.87 -3.38 -2.82 -3.14 -2.39 ...
     $ m_tcg_2000_2010_h13_full : num  -2.44 -3.05 -2.52 -2.52 -2.1 ...
     $ m_tcg_2005_2015_h12_16d  : num  -3.51 -3.76 -3.53 -3.34 -3.06 ...
     $ m_tcg_2005_2015_h12_full : num  -2.82 -3.34 -2.71 -3.1 -2.95 ...
     $ m_tcg_2005_2015_h13_16d  : num  -3.62 -3.97 -3.52 -3.5 -2.72 ...
     $ m_tcg_2005_2015_h13_full : num  -3.04 -3.51 -2.81 -3.08 -2.55 ...
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
    'data.frame':   483 obs. of  64 variables:
     $ system.index             : Factor w/ 477 levels "0","0.00E+00",..: 14 391 392 393 394 395 396 397 398 399 ...
     $ BAft2acre.x              : int  100 110 120 100 100 100 80 80 110 90 ...
     $ Defol17abs               : num  -1.914 -1.197 -1.108 -0.929 -1.747 ...
     $ DefolMean                : num  1.6 1.73 1.92 1.4 2.8 ...
     $ DefolSD                  : num  0.699 1.104 1.24 0.699 1.033 ...
     $ DefolSD3x3               : num  0.293 0.394 0.408 0.305 0.238 ...
     $ HotSpot                  : int  1 1 1 1 1 1 1 1 1 1 ...
     $ OakDefolMe               : num  1.86 2.33 2.83 2.33 3 ...
     $ OakDefolSD               : num  0.69 1.528 1.169 0.577 0.866 ...
     $ PropOak.x                : num  0.7 0.273 0.5 0.3 0.9 ...
     $ SmplPnt                  : int  0 1 2 3 4 5 6 7 8 9 ...
     $ TYPE_ABREV               : Factor w/ 9 levels "BbRm","NrHd",..: 6 6 3 3 3 3 3 3 3 3 ...
     $ YEAR_COMPL               : int  1998 1998 0 0 0 0 0 0 0 0 ...
     $ harv                     : Factor w/ 2 levels "N","Y": 2 2 1 1 1 1 1 1 1 1 ...
     $ hotplot                  : chr  "1 0" "1 1" "1 2" "1 3" ...
     $ latitude                 : num  42.3 42.3 42.3 42.3 42.3 ...
     $ longitude                : num  -72.4 -72.4 -72.4 -72.4 -72.4 ...
     $ m_evi_2000_2010_h12_16d  : num  -2.107 -1.532 -0.707 -0.705 -1.048 ...
     $ m_evi_2000_2010_h12_full : num  -2.111 -1.55 -1.006 -0.925 -1.291 ...
     $ m_evi_2000_2010_h13_16d  : num  -1.317 -0.989 -0.227 -0.402 -0.645 ...
     $ m_evi_2000_2010_h13_full : num  -1.515 -1.029 -0.767 -0.658 -0.944 ...
     $ m_evi_2005_2015_h12_16d  : num  -1.98 -2.26 -1.22 -1.66 -2.06 ...
     $ m_evi_2005_2015_h12_full : num  -1.7 -1.92 -1.21 -1.34 -1.73 ...
     $ m_evi_2005_2015_h13_16d  : num  -1.738 -1.806 -0.813 -1.358 -1.612 ...
     $ m_evi_2005_2015_h13_full : num  -1.533 -1.632 -0.923 -1.105 -1.442 ...
     $ m_ndvi_2000_2010_h12_16d : num  -0.51055 -0.00355 0.18549 0.05526 -0.10191 ...
     $ m_ndvi_2000_2010_h12_full: num  -0.4565 0.0718 0.313 0.221 -0.1444 ...
     $ m_ndvi_2000_2010_h13_16d : num  -0.0194 0.306 0.4187 0.3406 0.2741 ...
     $ m_ndvi_2000_2010_h13_full: num  -0.0664 0.3188 0.3537 0.3974 0.1205 ...
     $ m_ndvi_2005_2015_h12_16d : num  -1.37 -1.39 -0.74 -1.26 -1.33 ...
     $ m_ndvi_2005_2015_h12_full: num  -1.229 -1.291 -0.661 -0.923 -1.038 ...
     $ m_ndvi_2005_2015_h13_16d : num  -1.336 -1.331 -0.577 -1.195 -1.175 ...
     $ m_ndvi_2005_2015_h13_full: num  -1.188 -1.225 -0.531 -0.846 -0.92 ...
     $ m_reanalysis             : num  -1.914 -1.197 -1.108 -0.929 -1.747 ...
     $ m_sr_2000_2010_h12_16d   : num  -1.133 -0.664 -0.288 -0.19 -0.452 ...
     $ m_sr_2000_2010_h12_full  : num  -1.243 -0.717 -0.246 -0.207 -0.619 ...
     $ m_sr_2000_2010_h13_16d   : num  -0.5762 -0.2628 0.0437 0.0907 -0.0649 ...
     $ m_sr_2000_2010_h13_full  : num  -0.8343 -0.3922 -0.1597 -0.0075 -0.3255 ...
     $ m_sr_2005_2015_h12_16d   : num  -2.47 -2.55 -1.65 -2.02 -2.23 ...
     $ m_sr_2005_2015_h12_full  : num  -2.03 -2.17 -1.42 -1.63 -1.74 ...
     $ m_sr_2005_2015_h13_16d   : num  -2.36 -2.41 -1.45 -1.84 -1.86 ...
     $ m_sr_2005_2015_h13_full  : num  -1.8 -1.93 -1.16 -1.3 -1.34 ...
     $ m_tcg_2000_2010_h12_16d  : num  -2.307 -1.781 -0.871 -0.708 -1.256 ...
     $ m_tcg_2000_2010_h12_full : num  -2.171 -1.684 -1.004 -0.876 -1.34 ...
     $ m_tcg_2000_2010_h13_16d  : num  -1.624 -1.205 -0.389 -0.397 -0.845 ...
     $ m_tcg_2000_2010_h13_full : num  -1.68 -1.172 -0.829 -0.608 -1.003 ...
     $ m_tcg_2005_2015_h12_16d  : num  -2.23 -2.65 -1.67 -1.96 -2.33 ...
     $ m_tcg_2005_2015_h12_full : num  -1.96 -2.26 -1.44 -1.62 -2.04 ...
     $ m_tcg_2005_2015_h13_16d  : num  -2.06 -2.29 -1.25 -1.69 -1.96 ...
     $ m_tcg_2005_2015_h13_full : num  -1.85 -2.03 -1.18 -1.4 -1.8 ...
     $ .geo                     : Factor w/ 486 levels "{\"type\":\"Point\",\"coordinates\":[-72.23140206880488,42.42868481418561]}",..: 477 480 414 412 396 394 407 410 386 393 ...
     $ hotspot                  : int  1 1 1 1 1 1 1 1 1 1 ...
     $ point                    : int  0 1 2 3 4 5 6 7 8 9 ...
     $ type                     : Factor w/ 9 levels "black birch/red maple/cherry",..: 6 6 4 4 4 4 4 4 4 4 ...
     $ BAft2acre.y              : int  100 110 120 100 100 100 80 80 110 90 ...
     $ n.trees                  : int  10 11 12 10 10 10 8 8 11 9 ...
     $ MeanDef                  : num  0.275 0.307 0.354 0.225 0.575 ...
     $ BAft2acre.conifer        : int  30 80 50 40 0 0 0 10 0 0 ...
     $ MeanDef.conifer          : num  0.125 0.25 0.125 0.125 0 0 0 0.125 0 0 ...
     $ BAft2acre.oak            : int  70 30 60 30 90 100 40 40 110 90 ...
     $ MeanDef.oak              : num  0.339 0.458 0.583 0.458 0.625 ...
     $ BAft2acre.otherhd        : int  0 0 10 30 10 0 40 30 0 0 ...
     $ MeanDef.otherhd          : num  0 0 0.125 0.125 0.125 0 0.125 0.125 0 0 ...
     $ PropOak.y                : num  0.7 0.273 0.5 0.3 0.9 ...

## Quabbin

### Models

    MeanDef ~ m_evi_2000_2010_h12_16d + (1 | HotSpot)
    MeanDef ~ m_evi_2000_2010_h12_full + (1 | HotSpot)
    MeanDef ~ m_evi_2000_2010_h13_16d + (1 | HotSpot)
    MeanDef ~ m_evi_2000_2010_h13_full + (1 | HotSpot)
    MeanDef ~ m_evi_2005_2015_h12_16d + (1 | HotSpot)
    MeanDef ~ m_evi_2005_2015_h12_full + (1 | HotSpot)
    MeanDef ~ m_evi_2005_2015_h13_16d + (1 | HotSpot)
    MeanDef ~ m_evi_2005_2015_h13_full + (1 | HotSpot)
    MeanDef ~ m_ndvi_2000_2010_h12_16d + (1 | HotSpot)
    MeanDef ~ m_ndvi_2000_2010_h12_full + (1 | HotSpot)
    MeanDef ~ m_ndvi_2000_2010_h13_16d + (1 | HotSpot)
    MeanDef ~ m_ndvi_2000_2010_h13_full + (1 | HotSpot)
    MeanDef ~ m_ndvi_2005_2015_h12_16d + (1 | HotSpot)
    MeanDef ~ m_ndvi_2005_2015_h12_full + (1 | HotSpot)
    MeanDef ~ m_ndvi_2005_2015_h13_16d + (1 | HotSpot)
    MeanDef ~ m_ndvi_2005_2015_h13_full + (1 | HotSpot)
    MeanDef ~ m_reanalysis + (1 | HotSpot)
    MeanDef ~ m_sr_2000_2010_h12_16d + (1 | HotSpot)
    MeanDef ~ m_sr_2000_2010_h12_full + (1 | HotSpot)
    MeanDef ~ m_sr_2000_2010_h13_16d + (1 | HotSpot)
    MeanDef ~ m_sr_2000_2010_h13_full + (1 | HotSpot)
    MeanDef ~ m_sr_2005_2015_h12_16d + (1 | HotSpot)
    MeanDef ~ m_sr_2005_2015_h12_full + (1 | HotSpot)
    MeanDef ~ m_sr_2005_2015_h13_16d + (1 | HotSpot)
    MeanDef ~ m_sr_2005_2015_h13_full + (1 | HotSpot)
    MeanDef ~ m_tcg_2000_2010_h12_16d + (1 | HotSpot)
    MeanDef ~ m_tcg_2000_2010_h12_full + (1 | HotSpot)
    MeanDef ~ m_tcg_2000_2010_h13_16d + (1 | HotSpot)
    MeanDef ~ m_tcg_2000_2010_h13_full + (1 | HotSpot)
    MeanDef ~ m_tcg_2005_2015_h12_16d + (1 | HotSpot)
    MeanDef ~ m_tcg_2005_2015_h12_full + (1 | HotSpot)
    MeanDef ~ m_tcg_2005_2015_h13_16d + (1 | HotSpot)
    MeanDef ~ m_tcg_2005_2015_h13_full + (1 | HotSpot)

### AIC

| model                          |      AIC |   dAIC | df | weight |
| :----------------------------- | -------: | -----: | -: | -----: |
| m\_tcg\_2005\_2015\_h13\_full  | \-687.86 |   0.00 |  4 |   0.95 |
| m\_reanalysis                  | \-681.69 |   6.17 |  4 |   0.04 |
| m\_evi\_2005\_2015\_h13\_full  | \-677.19 |  10.67 |  4 |   0.00 |
| m\_tcg\_2005\_2015\_h13\_16d   | \-653.95 |  33.90 |  4 |   0.00 |
| m\_tcg\_2005\_2015\_h12\_full  | \-651.38 |  36.48 |  4 |   0.00 |
| m\_tcg\_2000\_2010\_h13\_full  | \-647.89 |  39.96 |  4 |   0.00 |
| m\_sr\_2000\_2010\_h12\_16d    | \-645.60 |  42.26 |  4 |   0.00 |
| m\_sr\_2000\_2010\_h13\_16d    | \-644.92 |  42.93 |  4 |   0.00 |
| m\_tcg\_2000\_2010\_h13\_16d   | \-644.62 |  43.23 |  4 |   0.00 |
| m\_evi\_2005\_2015\_h13\_16d   | \-644.11 |  43.75 |  4 |   0.00 |
| m\_evi\_2005\_2015\_h12\_full  | \-643.58 |  44.27 |  4 |   0.00 |
| m\_evi\_2000\_2010\_h13\_full  | \-631.06 |  56.80 |  4 |   0.00 |
| m\_evi\_2000\_2010\_h13\_16d   | \-627.33 |  60.53 |  4 |   0.00 |
| m\_sr\_2000\_2010\_h13\_full   | \-626.61 |  61.25 |  4 |   0.00 |
| m\_sr\_2000\_2010\_h12\_full   | \-625.84 |  62.02 |  4 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_full | \-623.91 |  63.94 |  4 |   0.00 |
| m\_tcg\_2000\_2010\_h12\_full  | \-622.31 |  65.55 |  4 |   0.00 |
| m\_tcg\_2005\_2015\_h12\_16d   | \-617.21 |  70.65 |  4 |   0.00 |
| m\_tcg\_2000\_2010\_h12\_16d   | \-615.55 |  72.30 |  4 |   0.00 |
| m\_evi\_2005\_2015\_h12\_16d   | \-612.69 |  75.17 |  4 |   0.00 |
| m\_sr\_2005\_2015\_h13\_full   | \-609.01 |  78.85 |  4 |   0.00 |
| m\_sr\_2005\_2015\_h13\_16d    | \-607.97 |  79.88 |  4 |   0.00 |
| m\_sr\_2005\_2015\_h12\_16d    | \-604.16 |  83.69 |  4 |   0.00 |
| m\_evi\_2000\_2010\_h12\_full  | \-602.13 |  85.73 |  4 |   0.00 |
| m\_sr\_2005\_2015\_h12\_full   | \-601.03 |  86.83 |  4 |   0.00 |
| m\_evi\_2000\_2010\_h12\_16d   | \-598.74 |  89.12 |  4 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_16d  | \-593.56 |  94.30 |  4 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_16d  | \-585.95 | 101.91 |  4 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_full | \-585.14 | 102.72 |  4 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_full | \-584.38 | 103.48 |  4 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_16d  | \-574.99 | 112.87 |  4 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_full | \-573.68 | 114.18 |  4 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_16d  | \-556.78 | 131.08 |  4 |   0.00 |

### R<sup>2</sup>

| baseline                       | R2\_marginal | R2\_conditional |
| :----------------------------- | -----------: | --------------: |
| m\_tcg\_2005\_2015\_h13\_full  |         0.60 |            0.63 |
| m\_reanalysis                  |         0.59 |            0.64 |
| m\_evi\_2005\_2015\_h13\_full  |         0.57 |            0.61 |
| m\_tcg\_2005\_2015\_h13\_16d   |         0.55 |            0.58 |
| m\_tcg\_2000\_2010\_h13\_full  |         0.55 |            0.57 |
| m\_tcg\_2000\_2010\_h13\_16d   |         0.54 |            0.59 |
| m\_tcg\_2005\_2015\_h12\_full  |         0.53 |            0.57 |
| m\_evi\_2005\_2015\_h13\_16d   |         0.52 |            0.55 |
| m\_evi\_2000\_2010\_h13\_full  |         0.51 |            0.53 |
| m\_evi\_2005\_2015\_h12\_full  |         0.51 |            0.55 |
| m\_evi\_2000\_2010\_h13\_16d   |         0.49 |            0.55 |
| m\_sr\_2000\_2010\_h13\_16d    |         0.47 |            0.60 |
| m\_tcg\_2000\_2010\_h12\_full  |         0.47 |            0.52 |
| m\_sr\_2000\_2010\_h12\_16d    |         0.46 |            0.61 |
| m\_tcg\_2000\_2010\_h12\_16d   |         0.46 |            0.55 |
| m\_ndvi\_2005\_2015\_h13\_full |         0.46 |            0.48 |
| m\_tcg\_2005\_2015\_h12\_16d   |         0.45 |            0.52 |
| m\_sr\_2000\_2010\_h13\_full   |         0.44 |            0.56 |
| m\_evi\_2005\_2015\_h12\_16d   |         0.43 |            0.49 |
| m\_sr\_2000\_2010\_h12\_full   |         0.42 |            0.58 |
| m\_evi\_2000\_2010\_h12\_full  |         0.41 |            0.45 |
| m\_evi\_2000\_2010\_h12\_16d   |         0.40 |            0.50 |
| m\_sr\_2005\_2015\_h13\_full   |         0.40 |            0.46 |
| m\_sr\_2005\_2015\_h13\_16d    |         0.40 |            0.45 |
| m\_sr\_2005\_2015\_h12\_full   |         0.38 |            0.44 |
| m\_sr\_2005\_2015\_h12\_16d    |         0.37 |            0.45 |
| m\_ndvi\_2005\_2015\_h13\_16d  |         0.36 |            0.39 |
| m\_ndvi\_2005\_2015\_h12\_full |         0.33 |            0.37 |
| m\_ndvi\_2000\_2010\_h13\_16d  |         0.30 |            0.42 |
| m\_ndvi\_2000\_2010\_h13\_full |         0.29 |            0.42 |
| m\_ndvi\_2000\_2010\_h12\_16d  |         0.25 |            0.41 |
| m\_ndvi\_2000\_2010\_h12\_full |         0.24 |            0.42 |
| m\_ndvi\_2005\_2015\_h12\_16d  |         0.18 |            0.26 |

## CT Burlap Larva

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

#### Both Years

| model                          |     AIC |  dAIC | df | weight |
| :----------------------------- | ------: | ----: | -: | -----: |
| m\_ndvi\_2000\_2010\_h13\_16d  | 2097.77 |  0.00 |  7 |   0.80 |
| m\_ndvi\_2000\_2010\_h13\_full | 2102.60 |  4.83 |  7 |   0.07 |
| m\_sr\_2000\_2010\_h13\_16d    | 2102.96 |  5.19 |  7 |   0.06 |
| m\_sr\_2000\_2010\_h13\_full   | 2105.31 |  7.54 |  7 |   0.02 |
| m\_evi\_2000\_2010\_h13\_full  | 2107.22 |  9.45 |  7 |   0.01 |
| m\_sr\_2000\_2010\_h12\_16d    | 2107.25 |  9.48 |  7 |   0.01 |
| m\_sr\_2005\_2015\_h13\_16d    | 2107.65 |  9.88 |  7 |   0.01 |
| m\_tcg\_2000\_2010\_h13\_full  | 2107.89 | 10.12 |  7 |   0.01 |
| m\_tcg\_2000\_2010\_h13\_16d   | 2108.08 | 10.31 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h13\_16d   | 2108.32 | 10.55 |  7 |   0.00 |
| m\_sr\_2000\_2010\_h12\_full   | 2109.32 | 11.55 |  7 |   0.00 |
| m\_sr\_2005\_2015\_h12\_16d    | 2110.05 | 12.28 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h12\_16d   | 2112.11 | 14.34 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h13\_16d   | 2112.16 | 14.39 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_16d  | 2112.34 | 14.57 |  7 |   0.00 |
| m\_tcg\_2000\_2010\_h12\_full  | 2112.38 | 14.61 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h12\_full  | 2112.40 | 14.63 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_full | 2112.70 | 14.93 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h12\_full  | 2112.90 | 15.13 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h13\_full  | 2112.93 | 15.16 |  7 |   0.00 |
| m\_sr\_2005\_2015\_h13\_full   | 2112.98 | 15.21 |  7 |   0.00 |
| m\_evi\_2000\_2010\_h12\_16d   | 2113.12 | 15.35 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h13\_full  | 2113.20 | 15.43 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h13\_16d   | 2113.28 | 15.51 |  7 |   0.00 |
| m\_reanalysis                  | 2113.65 | 15.88 |  7 |   0.00 |
| m\_sr\_2005\_2015\_h12\_full   | 2113.92 | 16.15 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_16d  | 2113.97 | 16.20 |  7 |   0.00 |
| m\_tcg\_2005\_2015\_h12\_16d   | 2114.54 | 16.77 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h12\_full  | 2114.59 | 16.82 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h12\_16d   | 2116.99 | 19.22 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_full | 2117.62 | 19.85 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_full | 2124.26 | 26.49 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_16d  | 2125.18 | 27.41 |  7 |   0.00 |

#### 2017 Only

| model                          |     AIC |  dAIC | df | weight |
| :----------------------------- | ------: | ----: | -: | -----: |
| m\_sr\_2000\_2010\_h13\_16d    | 1239.92 |  0.00 |  5 |   0.15 |
| m\_sr\_2000\_2010\_h13\_full   | 1240.84 |  0.92 |  5 |   0.10 |
| m\_sr\_2000\_2010\_h12\_16d    | 1241.35 |  1.43 |  5 |   0.07 |
| m\_tcg\_2000\_2010\_h13\_full  | 1241.96 |  2.05 |  5 |   0.06 |
| m\_evi\_2000\_2010\_h13\_full  | 1242.02 |  2.10 |  5 |   0.05 |
| m\_sr\_2005\_2015\_h13\_16d    | 1242.06 |  2.15 |  5 |   0.05 |
| m\_tcg\_2000\_2010\_h12\_16d   | 1242.07 |  2.15 |  5 |   0.05 |
| m\_tcg\_2000\_2010\_h13\_16d   | 1242.11 |  2.19 |  5 |   0.05 |
| m\_tcg\_2005\_2015\_h12\_full  | 1242.28 |  2.36 |  5 |   0.05 |
| m\_sr\_2005\_2015\_h12\_16d    | 1242.36 |  2.45 |  5 |   0.05 |
| m\_evi\_2000\_2010\_h13\_16d   | 1242.58 |  2.66 |  5 |   0.04 |
| m\_evi\_2000\_2010\_h12\_16d   | 1242.58 |  2.67 |  5 |   0.04 |
| m\_sr\_2000\_2010\_h12\_full   | 1242.84 |  2.92 |  5 |   0.04 |
| m\_ndvi\_2000\_2010\_h13\_16d  | 1242.92 |  3.00 |  5 |   0.03 |
| m\_sr\_2005\_2015\_h12\_full   | 1243.51 |  3.59 |  5 |   0.03 |
| m\_tcg\_2000\_2010\_h12\_full  | 1243.75 |  3.83 |  5 |   0.02 |
| m\_tcg\_2005\_2015\_h12\_16d   | 1244.05 |  4.13 |  5 |   0.02 |
| m\_evi\_2005\_2015\_h12\_full  | 1244.16 |  4.24 |  5 |   0.02 |
| m\_evi\_2000\_2010\_h12\_full  | 1244.34 |  4.43 |  5 |   0.02 |
| m\_sr\_2005\_2015\_h13\_full   | 1245.02 |  5.11 |  5 |   0.01 |
| m\_ndvi\_2000\_2010\_h12\_16d  | 1245.51 |  5.59 |  5 |   0.01 |
| m\_tcg\_2005\_2015\_h13\_16d   | 1245.69 |  5.77 |  5 |   0.01 |
| m\_ndvi\_2000\_2010\_h13\_full | 1246.07 |  6.15 |  5 |   0.01 |
| m\_tcg\_2005\_2015\_h13\_full  | 1246.16 |  6.24 |  5 |   0.01 |
| m\_evi\_2005\_2015\_h12\_16d   | 1246.43 |  6.51 |  5 |   0.01 |
| m\_reanalysis                  | 1246.61 |  6.69 |  5 |   0.01 |
| m\_evi\_2005\_2015\_h13\_full  | 1246.99 |  7.08 |  5 |   0.00 |
| m\_evi\_2005\_2015\_h13\_16d   | 1247.57 |  7.66 |  5 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_16d  | 1250.06 | 10.14 |  5 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_full | 1250.92 | 11.01 |  5 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_full | 1251.07 | 11.16 |  5 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_full | 1253.60 | 13.69 |  5 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_16d  | 1254.74 | 14.82 |  5 |   0.00 |

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

| baseline                       | R2\_marginal | R2\_conditional |
| :----------------------------- | -----------: | --------------: |
| m\_ndvi\_2000\_2010\_h13\_16d  |         0.69 |            0.78 |
| m\_ndvi\_2000\_2010\_h13\_full |         0.69 |            0.76 |
| m\_evi\_2000\_2010\_h13\_16d   |         0.68 |            0.75 |
| m\_tcg\_2000\_2010\_h13\_16d   |         0.68 |            0.75 |
| m\_sr\_2000\_2010\_h13\_16d    |         0.67 |            0.77 |
| m\_sr\_2000\_2010\_h13\_full   |         0.67 |            0.76 |
| m\_tcg\_2000\_2010\_h13\_full  |         0.67 |            0.75 |
| m\_evi\_2000\_2010\_h13\_full  |         0.67 |            0.75 |
| m\_sr\_2000\_2010\_h12\_full   |         0.66 |            0.75 |
| m\_tcg\_2000\_2010\_h12\_full  |         0.66 |            0.74 |
| m\_evi\_2000\_2010\_h12\_16d   |         0.66 |            0.73 |
| m\_tcg\_2000\_2010\_h12\_16d   |         0.66 |            0.74 |
| m\_sr\_2005\_2015\_h13\_16d    |         0.66 |            0.77 |
| m\_evi\_2000\_2010\_h12\_full  |         0.66 |            0.74 |
| m\_sr\_2000\_2010\_h12\_16d    |         0.66 |            0.76 |
| m\_tcg\_2005\_2015\_h12\_full  |         0.66 |            0.75 |
| m\_ndvi\_2005\_2015\_h13\_16d  |         0.66 |            0.76 |
| m\_ndvi\_2000\_2010\_h12\_full |         0.66 |            0.74 |
| m\_sr\_2005\_2015\_h12\_16d    |         0.65 |            0.77 |
| m\_tcg\_2005\_2015\_h13\_full  |         0.65 |            0.75 |
| m\_sr\_2005\_2015\_h13\_full   |         0.65 |            0.76 |
| m\_ndvi\_2005\_2015\_h13\_full |         0.65 |            0.76 |
| m\_sr\_2005\_2015\_h12\_full   |         0.65 |            0.76 |
| m\_evi\_2005\_2015\_h13\_full  |         0.65 |            0.75 |
| m\_evi\_2005\_2015\_h12\_full  |         0.65 |            0.74 |
| m\_tcg\_2005\_2015\_h13\_16d   |         0.65 |            0.76 |
| m\_ndvi\_2000\_2010\_h12\_16d  |         0.65 |            0.75 |
| m\_reanalysis                  |         0.65 |            0.76 |
| m\_tcg\_2005\_2015\_h12\_16d   |         0.65 |            0.76 |
| m\_evi\_2005\_2015\_h13\_16d   |         0.64 |            0.76 |
| m\_evi\_2005\_2015\_h12\_16d   |         0.63 |            0.75 |
| m\_ndvi\_2005\_2015\_h12\_full |         0.63 |            0.73 |
| m\_ndvi\_2005\_2015\_h12\_16d  |         0.62 |            0.74 |

### Plots from Top Baselines

#### sr\_2000-2010\_h13\_16d

![](Defoliation-Models_files/figure-gfm/Burlap_sr_Param-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Burlap_sr_Pred-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Burlap_sr_Combined-1.png)<!-- -->

#### tcg\_2000-2010\_h13\_full

![](Defoliation-Models_files/figure-gfm/Burlap_tcg_Param-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Burlap_tcg_Pred-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Burlap_tcg_Combined-1.png)<!-- -->

## Egg Mass Models

### AIC

#### Both Years

| model                          |     AIC |  dAIC | df | weight |
| :----------------------------- | ------: | ----: | -: | -----: |
| m\_reanalysis                  | 1045.95 |  0.00 |  7 |   0.30 |
| m\_tcg\_2005\_2015\_h13\_16d   | 1047.48 |  1.53 |  7 |   0.14 |
| m\_tcg\_2005\_2015\_h12\_16d   | 1048.48 |  2.52 |  7 |   0.08 |
| m\_tcg\_2000\_2010\_h12\_full  | 1048.58 |  2.63 |  7 |   0.08 |
| m\_sr\_2000\_2010\_h12\_16d    | 1048.85 |  2.90 |  7 |   0.07 |
| m\_tcg\_2000\_2010\_h12\_16d   | 1049.41 |  3.46 |  7 |   0.05 |
| m\_sr\_2000\_2010\_h13\_16d    | 1049.60 |  3.64 |  7 |   0.05 |
| m\_tcg\_2000\_2010\_h13\_16d   | 1050.13 |  4.17 |  7 |   0.04 |
| m\_evi\_2005\_2015\_h13\_16d   | 1050.13 |  4.17 |  7 |   0.04 |
| m\_tcg\_2000\_2010\_h13\_full  | 1050.46 |  4.51 |  7 |   0.03 |
| m\_sr\_2005\_2015\_h13\_16d    | 1051.75 |  5.79 |  7 |   0.02 |
| m\_evi\_2000\_2010\_h13\_16d   | 1051.86 |  5.91 |  7 |   0.02 |
| m\_evi\_2005\_2015\_h12\_16d   | 1052.01 |  6.05 |  7 |   0.01 |
| m\_evi\_2000\_2010\_h12\_16d   | 1052.13 |  6.17 |  7 |   0.01 |
| m\_evi\_2000\_2010\_h12\_full  | 1052.55 |  6.59 |  7 |   0.01 |
| m\_tcg\_2005\_2015\_h12\_full  | 1052.81 |  6.86 |  7 |   0.01 |
| m\_evi\_2000\_2010\_h13\_full  | 1052.95 |  7.00 |  7 |   0.01 |
| m\_tcg\_2005\_2015\_h13\_full  | 1053.07 |  7.12 |  7 |   0.01 |
| m\_sr\_2000\_2010\_h12\_full   | 1053.37 |  7.42 |  7 |   0.01 |
| m\_sr\_2005\_2015\_h13\_full   | 1053.96 |  8.01 |  7 |   0.01 |
| m\_sr\_2000\_2010\_h13\_full   | 1054.41 |  8.46 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_16d  | 1054.92 |  8.97 |  7 |   0.00 |
| m\_sr\_2005\_2015\_h12\_full   | 1055.00 |  9.04 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h13\_full  | 1055.40 |  9.45 |  7 |   0.00 |
| m\_sr\_2005\_2015\_h12\_16d    | 1055.44 |  9.48 |  7 |   0.00 |
| m\_evi\_2005\_2015\_h12\_full  | 1056.48 | 10.52 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_16d  | 1058.34 | 12.39 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_16d  | 1058.49 | 12.54 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_full | 1059.88 | 13.93 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_full | 1060.49 | 14.53 |  7 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_full | 1062.51 | 16.56 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_full | 1065.71 | 19.76 |  7 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_16d  | 1066.11 | 20.15 |  7 |   0.00 |

#### 2017 Only

| model                          |    AIC |  dAIC | df | weight |
| :----------------------------- | -----: | ----: | -: | -----: |
| m\_tcg\_2000\_2010\_h12\_full  | 542.95 |  0.00 |  5 |   0.25 |
| m\_reanalysis                  | 543.55 |  0.60 |  5 |   0.19 |
| m\_tcg\_2000\_2010\_h13\_full  | 544.02 |  1.07 |  5 |   0.15 |
| m\_tcg\_2000\_2010\_h12\_16d   | 545.61 |  2.66 |  5 |   0.07 |
| m\_evi\_2000\_2010\_h12\_full  | 546.23 |  3.28 |  5 |   0.05 |
| m\_evi\_2000\_2010\_h13\_full  | 546.32 |  3.37 |  5 |   0.05 |
| m\_sr\_2005\_2015\_h13\_16d    | 546.74 |  3.79 |  5 |   0.04 |
| m\_sr\_2000\_2010\_h12\_16d    | 546.84 |  3.89 |  5 |   0.04 |
| m\_tcg\_2000\_2010\_h13\_16d   | 546.87 |  3.92 |  5 |   0.04 |
| m\_evi\_2000\_2010\_h12\_16d   | 547.39 |  4.44 |  5 |   0.03 |
| m\_sr\_2000\_2010\_h13\_16d    | 548.14 |  5.19 |  5 |   0.02 |
| m\_evi\_2000\_2010\_h13\_16d   | 548.42 |  5.46 |  5 |   0.02 |
| m\_tcg\_2005\_2015\_h13\_16d   | 548.69 |  5.74 |  5 |   0.01 |
| m\_evi\_2005\_2015\_h13\_16d   | 549.96 |  7.00 |  5 |   0.01 |
| m\_sr\_2005\_2015\_h13\_full   | 550.13 |  7.18 |  5 |   0.01 |
| m\_sr\_2005\_2015\_h12\_16d    | 550.43 |  7.48 |  5 |   0.01 |
| m\_tcg\_2005\_2015\_h13\_full  | 550.51 |  7.56 |  5 |   0.01 |
| m\_tcg\_2005\_2015\_h12\_full  | 550.64 |  7.69 |  5 |   0.01 |
| m\_sr\_2005\_2015\_h12\_full   | 550.98 |  8.03 |  5 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_16d  | 551.27 |  8.32 |  5 |   0.00 |
| m\_tcg\_2005\_2015\_h12\_16d   | 551.42 |  8.47 |  5 |   0.00 |
| m\_evi\_2005\_2015\_h13\_full  | 551.60 |  8.64 |  5 |   0.00 |
| m\_sr\_2000\_2010\_h13\_full   | 551.64 |  8.68 |  5 |   0.00 |
| m\_sr\_2000\_2010\_h12\_full   | 551.71 |  8.76 |  5 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_16d  | 552.05 |  9.10 |  5 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_16d  | 553.07 | 10.12 |  5 |   0.00 |
| m\_evi\_2005\_2015\_h12\_full  | 553.14 | 10.19 |  5 |   0.00 |
| m\_evi\_2005\_2015\_h12\_16d   | 553.55 | 10.60 |  5 |   0.00 |
| m\_ndvi\_2000\_2010\_h13\_full | 555.23 | 12.27 |  5 |   0.00 |
| m\_ndvi\_2005\_2015\_h13\_full | 556.17 | 13.22 |  5 |   0.00 |
| m\_ndvi\_2000\_2010\_h12\_full | 557.51 | 14.56 |  5 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_full | 561.32 | 18.37 |  5 |   0.00 |
| m\_ndvi\_2005\_2015\_h12\_16d  | 561.96 | 19.01 |  5 |   0.00 |

### R<sup>2</sup>

| baseline                       | R2\_marginal | R2\_conditional |
| :----------------------------- | -----------: | --------------: |
| m\_sr\_2000\_2010\_h12\_16d    |         0.21 |            0.79 |
| m\_sr\_2000\_2010\_h13\_16d    |         0.20 |            0.79 |
| m\_tcg\_2005\_2015\_h12\_16d   |         0.20 |            0.81 |
| m\_tcg\_2005\_2015\_h13\_16d   |         0.20 |            0.81 |
| m\_sr\_2005\_2015\_h13\_16d    |         0.19 |            0.79 |
| m\_reanalysis                  |         0.19 |            0.81 |
| m\_sr\_2005\_2015\_h13\_full   |         0.19 |            0.78 |
| m\_tcg\_2000\_2010\_h12\_full  |         0.18 |            0.80 |
| m\_sr\_2005\_2015\_h12\_full   |         0.18 |            0.78 |
| m\_sr\_2000\_2010\_h12\_full   |         0.18 |            0.78 |
| m\_tcg\_2000\_2010\_h13\_16d   |         0.17 |            0.80 |
| m\_tcg\_2005\_2015\_h12\_full  |         0.17 |            0.79 |
| m\_evi\_2005\_2015\_h13\_16d   |         0.17 |            0.81 |
| m\_tcg\_2000\_2010\_h13\_full  |         0.17 |            0.80 |
| m\_sr\_2005\_2015\_h12\_16d    |         0.17 |            0.79 |
| m\_sr\_2000\_2010\_h13\_full   |         0.17 |            0.78 |
| m\_tcg\_2005\_2015\_h13\_full  |         0.17 |            0.79 |
| m\_tcg\_2000\_2010\_h12\_16d   |         0.17 |            0.80 |
| m\_evi\_2005\_2015\_h12\_16d   |         0.16 |            0.81 |
| m\_evi\_2000\_2010\_h13\_16d   |         0.16 |            0.81 |
| m\_ndvi\_2000\_2010\_h13\_16d  |         0.15 |            0.80 |
| m\_evi\_2000\_2010\_h12\_16d   |         0.14 |            0.80 |
| m\_evi\_2000\_2010\_h12\_full  |         0.14 |            0.80 |
| m\_evi\_2000\_2010\_h13\_full  |         0.14 |            0.80 |
| m\_evi\_2005\_2015\_h13\_full  |         0.14 |            0.79 |
| m\_evi\_2005\_2015\_h12\_full  |         0.13 |            0.79 |
| m\_ndvi\_2000\_2010\_h12\_16d  |         0.11 |            0.78 |
| m\_ndvi\_2005\_2015\_h13\_16d  |         0.10 |            0.80 |
| m\_ndvi\_2005\_2015\_h13\_full |         0.10 |            0.79 |
| m\_ndvi\_2000\_2010\_h13\_full |         0.09 |            0.79 |
| m\_ndvi\_2000\_2010\_h12\_full |         0.08 |            0.79 |
| m\_ndvi\_2005\_2015\_h12\_full |         0.06 |            0.79 |
| m\_ndvi\_2005\_2015\_h12\_16d  |         0.06 |            0.80 |

### Plots from Top Baselines

#### sr\_2000-2010\_h13\_16d

![](Defoliation-Models_files/figure-gfm/Egg_sr_Param-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Egg_sr_Pred-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Egg_sr_Combined-1.png)<!-- -->

#### tcg\_2000-2010\_h13\_full

![](Defoliation-Models_files/figure-gfm/Egg_tcg_Param-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Egg_tcg_Pred-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Egg_tcg_Combined-1.png)<!-- -->

### Egg Mass Predictor

#### AIC

| model                             |     AIC |  dAIC | df | weight |
| :-------------------------------- | ------: | ----: | -: | -----: |
| m\_sr\_2000-2010\_h13\_16d        | 2102.96 |  0.00 |  7 |   0.92 |
| m\_tcg\_2000-2010\_h13\_full      | 2107.89 |  4.93 |  7 |   0.08 |
| Predict abundance with egg masses | 2123.20 | 20.24 |  7 |   0.00 |

#### R<sup>2</sup>

    Abundance ~ EggMasses * Year + (1 | BlockID/SiteID)
    # R2 for Mixed Models
    
      Conditional R2: 0.760
         Marginal R2: 0.555

#### Plots

![](Defoliation-Models_files/figure-gfm/Egg_Predictor_Param-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Egg_Predictor_Pred-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/Egg_Predictor_Combined-1.png)<!-- -->

## Graphs

Let’s compare the old baseline model (reanalysis) to the new model with
the same parameters (tasseled cap greenness, 2000-2010, h13 harmonics,
full dataset), and see what has changed in the distribution of scores

![](Defoliation-Models_files/figure-gfm/New_Baseline_Comparison_2017-1.png)<!-- -->

![](Defoliation-Models_files/figure-gfm/New_Baseline_Comparison_2018-1.png)<!-- -->

#### Compare condition scores between baselines

Here we are looking at how well condition scores for individual plots
agree between the original reanalysis data product and the new condition
scores.

A lot of scatter means that at a point level, things are substantially
different.

Red lines are slope = 1. In both cases, Val’s new models have less
negative condition scores (values shifted up relative to the reanalysis
ones). There’s not much change in slope, which is good.

![](Defoliation-Models_files/figure-gfm/Baseline_Comp-1.png)<!-- -->

#### Condition Score Distributions

Another interesting comparison is to compare the distribution of
condition scores for the same year between Val’s models

There’s some variation in distribution shape, spread, and how negative
scores are between baselines. NDVI is consistently less negative.

![](Defoliation-Models_files/figure-gfm/Score_Distributions-1.png)<!-- -->
