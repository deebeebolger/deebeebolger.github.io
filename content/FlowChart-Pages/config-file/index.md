---
title: Create RELAX configuration file 
summary: Here we describe how the RELAX configuration file is created.

reading_time: false  # Show estimated reading time?
share: false  # Show social sharing links?
profile: false  # Show author profile?
comments: false  # Show comments?
show_date: true
show_time: true

# Optional header image (relative to `assets/media/` folder).
header:
  caption: ""
  image: ""
---


The function **CLV_CreateRELAX()** creates the RELAX_cfg.mat. This is the configuration structure containing the parameters that need to be defined prior to running the RELAX preprocessing pipeline. The following is the link to the CLV_CreateRELAX() function on Github.

[Project_CeLaVie/CLV_CreateRELAX.m at 6fb78aeda84e7a4377ddd281e3f90b1d9c26e640 · deebeebolger/Project_CeLaVie](https://github.com/deebeebolger/Project_CeLaVie/blob/6fb78aeda84e7a4377ddd281e3f90b1d9c26e640/CLV_CreateRELAX.m)

### Take note !

To be able to run the pipeline on your own computer, you will need to change the following three paths defined at the beginning of this script:

- **Relax_cfg.caploc**: Path to the channel location *.mat files
- **Relax_cfg.myPath**: Path to the raw EEG data.
- **Relax_cfg.OutputPath**: Path to the folder in which the processed data will be saved. This directory will be automatically created if not already present.

This configuration file is saved as a *.json file for each subject and its title takes the following form:

**sub-XX_Relax_config.json**

<aside>
💡

If the user decides to change a parameter value, they should change the value within the **CLV_CreateRelax()** function and ensure that the same parameters are applied for all participants. 

</aside>