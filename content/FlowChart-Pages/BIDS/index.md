---
title: Structuring data in BIDS
summary: This page details how the raw and processed data are structured according to BIDS. 

show_date: true
show_time: true

---
The EEG along with its accompanying meta data has been used to structure the data in BIDS (Brain Imaging Data Structure) format. The structuring applied is based on that described in Pernet et al (2019) and summarized in figure 1. 

The structuring of the data in BIDS is carried out by the matlab function:

CLV_createBIDS(). Below is a link to the function on Github.
[Github link to CLV_createBIDS() function](https://github.com/deebeebolger/Project_CeLaVie/blob/938baacd3ff18d6b7692148880f2faee183fe051/CLV_createBIDS.m)

![EEG-BIDS structure](BIDS_example.png "Figure 1: From Pernet, C.R., Appelhoff, S., Gorgolewski, K.J. et al. EEG-BIDS, an extension to the brain imaging data structure for electroencephalography. Sci Data 6, 103 (2019).")

![EEG-BIDS structure in RELAX pipeline](Celavie_BIDS_structure.png "Figure 2: Overview of BIDS structure applied with resting-state data for three post-test participants, sub-018, sub-020 and sub-021. ")