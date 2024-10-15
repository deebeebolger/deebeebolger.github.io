---
title: Rereferencing
summary: This page details the re-referencing carried out after MWF rounds.
date: 2024-10-03
---
After Multi-channel Wiener Filter (MWF) stages, the continuous data is re-referenced to the average across the scalp channels, excluding those channels marked as bad. 

<aside>
❗

In the RELAX re-reference function, ***RELAX_average_rereference(EEG)**,* is described as applying the robust re-reference but this does not appear to be the case. This function applies EEGLAB’s ***pop_reref()*** function, which re-references to the average of the scalp electrodes. 

To apply the PREP pipeline’s robust re-referencing function, it is necessary to use the their ***performReference()*** or ***robustReference()*** function. 

</aside>