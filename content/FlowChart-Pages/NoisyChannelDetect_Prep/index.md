---
title: 7 Noisy channel detection with PREP pipeline approach.
summary: This page outlines the detection of noisy channels applied using an approach from the PREP pipeline.
date: 2024-10-14

placement: 3
---
There are three stages to the noisy channel detection stage of the pipeline. In rejecting channel-wise data, the follow criteria are applied: 

- In GUI: Maximum proportion of electrodes that can be deleted as bad: **RELAX_cfg.MaxProportionOfElectrodesThatCanBeDeleted** = **0.20** (20%)
- In GUI: Extreme noise proportion electrode deletion threshold: **RELAX_cfg.ProportionOfExtremeNoiseAboveWhichToRejectChannel** = **0.05** (5%)

## Initial bad channel detection using PREP pipeline function

The ***findNoisyChannels()*** function from the **PREP pipeline** is applied. 

This functions divides the data into time windows of a defined duration, which is set to **1 second** by default.

### This function detects noisy channels according to the following 3 criteria:

### Correlation with other channels or *predictability criterion:*

The signal is low pass filtered at 50Hz and divided into time windows of 1 second duration, and the correlation of each individual channel with other channels in each time window is calculated. The maximum absolute correlation is calculated as the 98th percentile of the absolute values of the correlations with other channels in each time window. A channel is marked as being bad by correlation if the maximum correlation is less than a defined correlation (default: 0.4) threshold for a given % of time windows (1%).  

### Unusual high frequency noise : *noisiness criterion*

The ratio of the power of the high frequency components compared to the low frequency components is estimated. The ratio, for each channel, of the median absolute deviation (MAD) of high frequency components and  low frequency components is the *noisiness*. Based on this, the robust z-score is calculated for each channel compared to all other channels. Channels are marked as being *bad-by-HF noise* if their robust z-score > 5. This is calculated for each channel and for each time window. 

### Extreme amplitude: a *deviation criterion*

The deviation criterion is effective in detecting unusual high frequency noise. It is computed as the robust z-score of the robust standard deviation for each channel. Channels are marked as *bad-by-deviation* if the robust z-score > 5. In addition, for each channel a robust amplitude-adjusted z score is calculated for each 1 second time window by using the overall robust median and the overall robust standard deviation in the z score calculation.