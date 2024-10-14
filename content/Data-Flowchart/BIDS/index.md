---
title: Structuring data in BIDS
summary: This page details how the raw and processed data are structured according to BIDS. 
date: 2024-10-14

---
The EEG along with its accompanying meta data has been used to structure the data in BIDS () format. The structuring applied is based on that described in Pernet et al (2019) and summarized in figure 1. 

The structuring of the data in BIDS is carried out by the matlab function:

CLV_createBIDS(). Below is a link to the function on Github.

![EEG-BIDS structure](BIDS_example.png)