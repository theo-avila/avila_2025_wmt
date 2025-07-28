# avila_2025_wmt
**Water Mass Transformation and Variability in the Nordic Seas** 

Theo C. Avila<sup>1*</sup>, Jacob Steinberg<sup>2</sup>, John Krasting<sup>2</sup>, Jan-Erik Tesdal<sup>2,3</sup>, Stephen Griffies<sup>3</sup><br> 

<sup>1</sup> Department of Physics, University of Illinois at Urbana-Champaign  
<sup>2</sup> Geophysical Fluid Dynamics Laboratory, NOAA  
<sup>3</sup> Program in Atmospheric and Oceanic Sciences, Princeton University    

<sup>*</sup> Corresponding author: ctavila2@illinois.edu  

## Description

This repository contains code, analysis scripts, and Jupyter Notebooks for **Water Mass Transformation and Variability in the Nordic Seas**. We look at λ = ρ, within coupled gfdl models. There is built in functionality for looking at certain regions, or with reference to some density class. There is also functionality for block bootstrap sampling to get a sense of the internal variability within the systems. This repo includes two worked Jupyter Notebooks:

- **Single experiment analysis** (`notebooks/single_experiment.ipynb`)  
  A walkthrough of the WMT pipeline on one model run, showing how to compute and plot λ=ρ for a single experiment. This notebook is focuse

- **Experiment comparison** (`notebooks/comparison_notebook.ipynb`)  
  Demonstrates how to compare multiple runs with similar functionality as the single_experiment notebook. 

## Dependencies 

This repository uses the environment available at /nbhome/ogrp/python/envs/dev. If unable to access this environment, a minimal installation might include environment.yml, however this is missing the esnb notebook. Fluxes may be name

### To Do

