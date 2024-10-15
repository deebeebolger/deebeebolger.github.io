---
title: 5 Filtering Parameters 
summary: Here we describe the applied filters and their parameters.
date: 2024-10-15

reading_time: false  # Show estimated reading time?
share: false  # Show social sharing links?
profile: false  # Show author profile?
comments: false  # Show comments?

# Optional header image (relative to `assets/media/` folder).
header:
  caption: ""
  image: ""
---


## Notch filter

A **4th order Butterworth filter** is applied with cutoff 3Hz above and below 50Hz, which implies low and high cutoff of 47Hz and 53Hz, respectively. 

### High-pass filter

A 4th order Butterworth filter is applied with a high-pass cutoff of 0.25Hz. 

A lower cutoff ($\leq0.1Hz$) would be preferable, but given that ICA is carried out and that applying a higher high-pass filter facilitates ICA computation, a cutoff of 0.25Hz was considered a reasonable compromise.

### Low-pass filter

It is recommended not to carry out low pass filtering prior to Multi-channel Wiener Filtering (MWF) as this reduces the chance of rank deficiency. Therefore, in the current implementation of the pipeline, low-pass filtering is not carried at this stage.