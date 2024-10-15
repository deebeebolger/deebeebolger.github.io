---
title: Add channel coordinates
summary: This page details how channel coordinates are added to the participant-level data.

show_date: true
show_time: true
---
The channel coordinates are provided by 4 coordinates files; each coordinates file corresponds to a specific cap size. The four coordinates files are the following:

- Biosemi_128_Taille_Large.mat
- Biosemi_128_Taille_XLarge.mat
- Biosemi_128_Taille_Medium.mat
- Biosemi_128_Taille_MLarge.mat
- Biosemi_128_Taille_Small.mat

For each participant, the cap size is extracted from “**participants.csv**” file and, based on this, the corresponding coordinates *.mat file is automatically applied. The coordinates in the *.mat file is added to **EEG.chanlocs** structure of the participant’s EEG structure.

![128-channel layout](channel_coordinates.png "Figure 1: Plot of the channel layout of 128-channel 10-20 configuration for a small Biosemi 12-channel cap.")