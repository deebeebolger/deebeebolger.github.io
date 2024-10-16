---
title: Wavelet thresholding of classified ICs 
summary: This page details the application of wavelet thresholding on ICs classified by ICLable and identified for rejection 
date: 2024-10-01
---

The computed ICs (Independent Components) are automatically classified using EEGLAB’s ICLabel plugin. The algorithms underlying the automatic classification of ICs is based on crowd sourcing run by the Swartz Center for Computational Neuroscience, University of California, which involves experts contributing to the ICLabel project by volunteering to label components. The ICLabel plugin automatically classifies ICs into broad categories based on their source:

- Brain
- Muscle
- Oculare
- Cardiac
- Channel noise
- Line noise
- Other

In the current implementation, an IC is considered for rejection if the probability of it corresponding to Muscle, Ocular, Cardiac, Channel or Line noise is equal to or above 80%. 
```matlab
% IC classes: Brain, Muscle, Eye, Heart, LineNoise, ChannelNoise, Other
 icThreshold    = [0 0.0; 0.8 1; 0.8 1; 0.8 1; 0.8 1; 0.8 1; 0 0];
```

![Classified ICs and wICA](classified_ICs.png "Figure 1: Example of ICs classified by ICLabel plugin according to the categories: Brain, Muscle, Other, Line Noise. In this case, no IC was marked for rejection. The ICs were computed by the infomax algorithm. ")
