---
title: Multi-channel Wiener Filtering - round 1
summary: This page details the first round of MWF applied in this implementation of the RELAX pipeline.
date: 2024-10-15
---

Multi-channel Wiener Filters (MWF) (Borowicz, 2018; Somers et al., 2018) constitutes one of the key artifact reduction components of RELAX pipeline. The MWF are applied sequentially in three rounds to reduce:

1. Muscle artifacts
2. Blinks that may have been masked by muscle artifacts
3. Horizontal eye-movements (hEOG) and drift.

The aim is to reduce as much as possible these artifact-types while preserving as much as possible the neural signal. 

## Background

Wiener filters are data-dependent, linear, least square error filters. The coefficients of Wiener filters are calculated so as to minimize the average square distance between the filter output and a desired signal. In its most basic form, Wiener filters assume that signals are stationary processes but by periodically recalculating the filter coefficients for every block of N signal samples, the filter can adapt itself to the average characteristics of the signals within the block. 

Here, the activity underlying the EEG signal cannot be considered stationary and so blocks of N samples need to be defined. In the pipeline, these N samples define the **MWF delay period** and need this delay period is calculated as a function of the sampling frequency. 

If the desired delay period (D) is 40ms (0.04seconds) then N (the MWF delay period in samples) is given by $N = floor(D*F_s)$ where $F_s$ is the sampling frequency (512Hz).

In the current implementation of the pipeline, a delay period of 40 milliseconds is defined, which translates as a delay period (in samples) of **20 samples**.

MWF Delay Period : **RELAX_cfg.MWFDelayPeriod_ms** = 40;

<aside>
💡

For a delay period of 16 samples, we would need to define a delay period (in ms) of 31.2ms

</aside>

## Multi-channel Wiener Filtering (MWF) : Round 1

The **first round** concerns mainly **muscle artifact** cleaning. But eye-blink cleaning can be included in the first round if wished. This implies integrating the eye-blink mask into the noise-mask. The first round is carried out if **RELAX_cfg.Do_MWF_Once** = 1 .

### Muscle activity

Muscle artifacts are dealt with in the first round of MWF. To create a template for the detection of muscle activity for the MWF cleaning, the data is separated into 1second epochs with 500ms overlap.

The log frequency/log power slope above which to mark an artifact as a muscle artifact. The more negative the value, the more muscle artifact is removed. Less stringent = -0.31, medium stringency = -0.59 and high stringency = -0.72. The default value for this parameter is -0.59. 

- In GUI: Log-frequency Log-power slope muscle artifact threshold for MWF cleaning: Relax_cfg.MuscleSlopeThreshold = -0.31.

The function *RELAX_muscle()* creates a template of clean and muscle artefacted data to be used for cleaning using MWF.  Note that if data has been low pass filtered below 75Hz, muscle artifact slopes cannot be computed. In this template, muscle artifact periods are marked as 1 and clean periods are marked as 0; thus creating a mask. 

- In GUI: Max proportion marked as muscle for MWF cleaning: **RELAX_cfg.MaxProportionOfDataCanBeMarkedAsMuscle** = 0.05

The following function (below) creates a template of clean and artefacted data to be used for cleaning in MWF.

```matlab
[continuousEEG, epochedEEG] = RELAX_muscle(continuousEEG, epochedEEG, RELAX_cfg)
```

### Blink Activity

The blink activity is mainly dealt with in the second round of MWF. However, it is also possible to detect eye-blinks in the first round, in which case the eye-blink mask will be integrated into the noise mask. To allow eye-blink cleaning in round 1:

- **RELAX_cfg.MWFRoundToCleanBlinks** = 1