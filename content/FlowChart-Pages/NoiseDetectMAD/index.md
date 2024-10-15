---
title: Detection of noisy channels and time intervals via MAD
summary: This page details the parameters applied for the detection of noisy channels and time intervals by computing MAD.
date: 2024-10-15
---

Extreme outlier detection is carried out using the **Median Absolute Deviation (MAD)**, which is more robust to outliers. The continuous data is segmented into 1 second epochs with a 50% overlap (500ms) and in each time segment the following is identified **to detect both electrodes and time segments** to mark for rejection:

- extreme amplitudes having a low probability of corresponding to brain activity. This is estimated by MAD from the median.
- extreme drift
- extreme kurtosis
- very improbable voltage distributions
- log-power log-frequency slopes, which can indicate muscle activity.

For each time window, a channel is deleted if the proportion of its data presenting extreme values exceeds a defined percentage, here **5%**. 

A maximum proportion of channels that can be deleted based on the above criterion is defined; here this proportion is 20%.

In the **RELAX config** file, the above parameters are defined as follows. 

### **MAD (mean absolute deviation) from median voltage shift within 1 second epoch**.

It is the threshold MAD from the median in all epochs for each electrodes against the same electrode in different epochs. If set lower than 20MAD, it would catch less severe voltage shifts.

- In GUI: MAD from median voltage shift: **RELAX_cfg.ExtremeVoltageShiftThreshold** = 20 MAD

### **MAD from within blink affected epochs**.

How many MAD from the median across blink affected epochs should be excluded as extreme data. 

- In GUI: MAD from median voltage shift in blink affected epochs: **RELAX_cfg.ExtremeBlinkShiftThreshold** = 8 MAD

### **Absolute Voltage Threshold**.

Min and max voltage (microVolts) threshold beyond which data will be excluded from cleaning and deleted. 

- In GUI: Absolute voltage shift: **RELAX_cfg.ExtremeAbsoluteVoltageThreshold** =   $500\mu$V

Other criteria applied in the ***findNoisyChannels()*** to detect noisy electrodes:

- In GUI: Single channel kurtosis: **RELAX_cfg.ExtremeSingleChannelKurtosisThreshold** = 8
- In GUI: All channel kurtosis: **RELAX_cfg.ExtremeChannelKurtosis** = 8

### **Log-power,  log-frequency slopes.**

Slope of log frequency, log power below which to reject as drift without neural activity. 

- In GUI: Log-frequency Log-power for detecting drift threshold: **RELAX_cfg.ExtremeDriftSlopeThreshold** = -4

<aside>
❗

Detected time periods with extreme artifacts are marked with **NaN**  in the cleaning templates applied in the Multi-channel Wiener filtering stage of pre-processing. These time periods are ignored when the MWF constructs the cleaning templates. These time periods are also excluded from the data prior to ICA decomposition. 

</aside>