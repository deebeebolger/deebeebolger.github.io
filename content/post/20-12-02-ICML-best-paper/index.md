---
title: EEG CeLaVie Project
date: 2024-10-14
image:
  focal_point: 'top'
---

Overview of resting-state EEG processing and analysis carried out in the context of the Celavie project.

<!--more-->

**Flowchart of RELAX pipeline applied to resting-state hdEEG data**

```mermaid
flowchart TD;

Config([Create RELAX config *.mat file]) --> BIDS([Prepare BIDS structure]);
BIDS --> Ld(Load current dataset, *.bdf or *.set formats);
Ld --> EXRej([Exclude external channels]);
EXRej --> AddRS(Calculate and add downsampling info to RELAX config);
AddRS --> AddChan(Add channel coordinate information to EEG structure);
AddChan --> ScalpRej([Delete scalp channels marked for rejection]);
ScalpRej --> Notch([Apply notch filter, 4th order Butterworth: 47Hz - 53Hz]);
Notch --> HPfilt([Apply high-pass filter, 4th order Butterworth : 0.25Hz]);
HPfilt --> RSamp([Downsample the data]);
RSamp -->|Plot Channel Spectra|Prep([Detect noisy channels: PREP pipeline function]);
Prep --> EpClean([Epoch data to detect extremely noisy time periods: 1second epochs]);
EpClean --> XtremeData([Delete channels exceeding threshold of proportion of data with extreme outliers: max. of 20% channels]);
XtremeData --> Blink([Eye-blink detection via IQR approach]);
Blink -->|Record artifact rejection details|SerArrChoice{Multi Wiener Filtering or MWF?};


```