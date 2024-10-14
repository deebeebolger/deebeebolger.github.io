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
flowchart TD
%% Colors %%

classDef blue fill:#2374f7, stroke:#000, stroke-width: px, color:#fff
classDef orange fill:#fc822b,stroke:#000,stroke-width:2px,color:#fff
classDef green fill:#16b522,stroke:#000,stroke-width:2px,color:#fff
classDef mintgreen fill:#4DAB9A,stroke:#000,stroke-width:2px,color:#fff
classDef mandarine fill:#FFA344,stroke:#000,stroke-width:2px,color:#fff
classDef aubergine fill:#9A6DD7,stroke:#000,stroke-width:2px,color:#fff
classDef red fill:#D44C47,stroke:#000,stroke-width:2px,color:#fff
classDef grey fill:#979A9B,stroke:#000,stroke-width:2px,color:#fff

Config([Create RELAX config *.mat file]):::blue --> BIDS([Prepare BIDS structure]):::blue;
BIDS --> Ld(Load current dataset, *.bdf or *.set formats):::orange;
Ld --> EXRej([Exclude external channels]):::green;
EXRej --> AddRS(Calculate and add downsampling info to RELAX config);
AddRS --> AddChan(Add channel coordinate information to EEG structure);
AddChan --> ScalpRej([Delete scalp channels marked for rejection]):::green;
ScalpRej --> Notch([Apply notch filter, 4th order Butterworth: 47Hz - 53Hz]):::green;
Notch --> HPfilt([Apply high-pass filter, 4th order Butterworth : 0.25Hz]):::green;
HPfilt --> RSamp([Downsample the data]):::green;
RSamp -->|Plot Channel Spectra|Prep([Detect noisy channels: PREP pipeline function]):::mintgreen;
Prep --> EpClean([Epoch data to detect extremely noisy time periods: 1second epochs]):::mintgreen;
EpClean --> XtremeData([Delete channels exceeding threshold of proportion of data with extreme;outliers: max. of 20% channels]):::mintgreen;
XtremeData --> Blink([Eye-blink detection via IQR approach]):::mandarine;
Blink -->|Record artifact rejection details|SerArrChoice{Multi Wiener Filtering or MWF?};
SerArrChoice -->|No|DoSerArr([Calculate Signal-to-error Ratio and Artifact-to-residue ratio]):::mintgreen;
SerArrChoice -->|Yes| MWF1([Carry out MWF Round 1: Detect and clean muscle artifacts]):::mintgreen;
MWF1 -->|Record processing stats for MWF 1 in RELAX config| MWF2([Carry out MWF Round 2: Detect eye-blinks masked by muscle artifacts]):::mintgreen;
MWF2 --> |Record processing stats for MWF 2 in RELAX config| MWF3([Carry out MWF Round 3: Detect drift-related and hEOG artifacts]):::mintgreen;
DoSerArr --> Reref([Perform robust average re-referencing]):::aubergine;
MWF3 -->|Record processing stats for MWF 3 in RELAX config| Reref:::aubergine;
Reref --> Nanrej([Reject data periods marked as NaN in noise masks]):::aubergine;
Nanrej --> ICAInfomax([Perform ICA using the Infomax algorithm]):::red;
ICAInfomax --> wICA([Perform wavelet-enhanced ICA on artifact-related ICs detected by ICLabel function]):::red;
wICA --> CCM([Compute cleaned metrics]):::grey;
CCM -->|Record warnings about potential issues in RELAX config|Interp([Interpolate rejected channels using Spherical Spline Interpolation]):::grey;
```