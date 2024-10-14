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

Config([Create RELAX config *.mat file]):::blue -->
BIDS([Prepare BIDS structure]):::blue
click Config "https://www.notion.so/Create-RELAX-configuration-file-fff069b2d231816bacd1ec135d7fde60?pvs=4" "Link"
click BIDS "https://www.notion.so/Structure-data-in-BIDS-fff069b2d23181dba6aad4cc4e02c10b?pvs=4" "Link"
BIDS --> Ld(Load current dataset, *.bdf or *.set formats):::orange
--> EXRej([Exclude external channels]):::green
click EXRej "https://www.notion.so/Exclude-external-channels-105069b2d2318042886bd1ea5be2271a?pvs=4" _blank
EXRej --> AddRS(Calculate and add downsampling info to RELAX config)
click AddRS "https://www.notion.so/Downsampling-Calculate-and-record-parameters-ada35d3cf3654347936aba920a648537?pvs=4" "Link" _blank
AddRS --> AddChan(Add channel coordinate information to EEG structure)
click AddChan "https://www.notion.so/Add-channel-coordinates-105069b2d2318037ac85c298119f8eaa?pvs=4" "Link" _blank
AddChan --> ScalpRej([Delete scalp channels marked for rejection]):::green
ScalpRej --> Notch([Apply notch filter, 4th order Butterworth: 47Hz - 53Hz]):::green
click Notch "https://www.notion.so/Filtering-106069b2d23180d39265e28bfde0d607?pvs=4" "Link" _blank
Notch --> HPfilt([Apply high-pass filter, 4th order Butterworth : 0.25Hz]):::green
click HPfilt "https://www.notion.so/Filtering-106069b2d23180d39265e28bfde0d607?pvs=4" "Link" _blank
HPfilt --> RSamp([Downsample the data]):::green
RSamp -->|Plot Channel Spectra|Prep([Detect noisy channels: PREP pipeline function]):::mintgreen
Prep --> EpClean([Epoch data to detect extremely noisy time periods: 1second epochs]):::mintgreen
click Prep "https://www.notion.so/Noisy-channel-detection-106069b2d23180ea87fcd1d23694c031?pvs=4" "Link" _blank
EpClean --> XtremeData([Delete channels exceeding threshold of proportion of data with extreme
outliers: max. of 20% channels]):::mintgreen 
click EpClean "https://www.notion.so/Noisy-channel-and-time-interval-detection-MAD-106069b2d23180d58246de1234c9eba7?pvs=4" "Link" _blank
XtremeData --> Blink([Eye-blink detection via IQR approach]):::mandarine
click XtremeData "https://www.notion.so/Noisy-channel-and-time-interval-detection-MAD-106069b2d23180d58246de1234c9eba7?pvs=4" "Link" _blank
click Blink "https://www.notion.so/Eye-blink-detection-IQR-approach-106069b2d23180f39a05d888d86d14cc?pvs=4" "Link" _blank
Blink -->|Record artifact rejection details|SerArrChoice{Multi Wiener Filtering or MWF?}
click SerArrChoice "https://www.notion.so/Wiener-Filter-and-Multi-Channel-Wiener-Filter-Background-Information-78e411f8fb814be685872c22ae22aad1?pvs=4" "Link" _blank
SerArrChoice -->|No|DoSerArr([Calculate Signal-to-error Ratio and Artifact-to-residue ratio]):::mintgreen
SerArrChoice -->|Yes| MWF1([Carry out MWF Round 1: Detect and clean muscle artifacts]):::mintgreen
MWF1 -->|Record processing stats for MWF 1 in RELAX config| MWF2([Carry out MWF Round 2: Detect eye-blinks masked by muscle artifacts]):::mintgreen;
click MWF1 "https://www.notion.so/Multi-channel-Wiener-Filters-105069b2d23180eb83b4d3e1fe5aab00?pvs=4" "Link" _blank
MWF2 --> |Record processing stats for MWF 2 in RELAX config| MWF3([Carry out MWF Round 3: Detect drift-related and hEOG artifacts]):::mintgreen
click MWF2 "https://www.notion.so/Multi-channel-Wiener-Filters-Round-2-107069b2d2318016a8e9e994f9843d29?pvs=4" "Link" _blank
DoSerArr --> Reref([Perform robust average re-referencing]):::aubergine
MWF3 -->|Record processing stats for MWF 3 in RELAX config| Reref:::aubergine
click MWF3 "https://www.notion.so/Multi-channel-Wiener-Filters-Round-3-107069b2d2318009a868f8ed3df4cc03?pvs=4" "Link" _blank
Reref --> Nanrej([Reject data periods marked as NaN in noise masks]):::aubergine
click Reref "https://www.notion.so/Robust-average-re-referencing-107069b2d231806484a5e1df6c47df78?pvs=4" "Link" _blank
Nanrej --> ICAInfomax([Perform ICA using the Infomax algorithm]):::red
click ICAInfomax "https://www.notion.so/ICA-via-the-Infomax-algorithm-10c069b2d23180d0ba65c4cd8a973fc4?pvs=4" "Link" _blank
ICAInfomax --> wICA([Perform wavelet-enhanced ICA on artifact-related ICs
detected by ICLabel function]):::red
wICA --> CCM([Compute cleaned metrics]):::grey
CCM -->|Record warnings about potential issues in RELAX config|Interp([Interpolate
rejected channels using Spherical Spline Interpolation]):::grey
```