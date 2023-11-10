---
date: "2023-11-02T00:00:00Z"
external_link: ""
image:
  caption: 
  focal_point: Smart
links:
- icon: 
  icon_pack: fab
  name: 
  url:
slides:
authors: ["BolgerD", "PitchoulinG"]
summary: A CNN trained on frequency-band data extracted from EEG (DEAP dataset) is used for real-time classification of the emotional valence of climate change images.  
tags:
- Deep Learning
- Time-frequency
- BCI
- Visual Communication
- Image databases
- DEAP
- FAICC
title: "Images of Climate Change: A Deep Learning Model"
url_code: ""
url_pdf: ""
url_slides: ""
url_video: "https://amubox.univ-amu.fr/s/iNjAwPxCii7ZEmi"
---

The urgency of the climate crises is no longer a subject of debate, the urgency is real and this is increasingly acknowledged both at the levels of public administrations and at the individual level. But despite this universal acknowledgement, positive and effective action is not always quick to follow and inciting people to take effective action is not an easy task. Therefore, the question of how to encourage people towards positive action is an increasingly crucial one. In todays world, visual communication through images has a central role and increasingly, research on the effective communication of Climate Change (CC) is addressing how to exploit this visual world to incite people to act. Studies on the cognitive, affective and behavioral effects of images is playing a central role in this work with the emergence of databases of images, including a small number specificalluy dedicated to CC, in which images have been rated in terms of emotional valence and arousal. Such research and image databases constitute a precious resource for testing, in an objective manner, the effect of images and their potential to encourage postiive CC action. One such database is the **French Affective Images of Climate Change** (FAICC) data (Otavi, Roussel & Syssau, 2021); this database is particularly useful in that images have been rated in terms of their **arousal** and **valence**.

The aim of the present work is to test the images from the FAICC with a model of emotion recognition. The emotion recognition model is built by training and testing a CCN (Convolutional Neural Network) on electroencephalography (EEG) data from the DEAP database (Koelstra et al, 2012). This EEG data was recorded while participants viewed 40, 1 minute music video excerpts that had been rated in terms of their **arousal**, **emotional valence**, **dominance** and **familiarity**. These ratings were attributed according to a 9-point Likert scale. 
