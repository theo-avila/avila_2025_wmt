# avila_2025_wmt
**Water Mass Transformation and Variability in the Nordic Seas** 

Theo C. Avila<sup>1*</sup>, Jacob M. Steinberg<sup>2</sup>, John P. Krasting<sup>2</sup>, Jan-Erik Tesdal<sup>2,3</sup>, Stephen M. Griffies<sup>3</sup><br> 

<sup>1</sup> Department of Physics, University of Illinois at Urbana-Champaign  
<sup>2</sup> Geophysical Fluid Dynamics Laboratory, NOAA  
<sup>3</sup> Program in Atmospheric and Oceanic Sciences, Princeton University    

<sup>*</sup> Correspondence should be addressed to: ctavila2@illinois.edu  

## Description

This repository contains code, analysis scripts, and Jupyter Notebooks for **Water Mass Transformation and Variability in the Nordic Seas**. We analyze λ = ρ transformations within coupled GFDL models.

---

## Core Functionality:

- **Water Mass Transformation (WMT) pipeline**:  
  Compute and visualize transformations (λ=ρ) from surface fluxes and model outputs.

- **Regional analysis**:  
  Built-in support for analyzing certain basins, or by creating own basins. 

- **Internal variability estimation**:  
  Block-bootstrap sampling tools to look at internal variability in the WMT results. 

---

## Example Notebooks:

- [`notebooks/single_experiment.ipynb`](notebooks/single_experiment.ipynb):  
  **Single Experiment Analysis**  
  Walkthrough of single experiment SWMT. (maybe just two? like forced & not forced?)

- [`notebooks/comparison_notebook.ipynb`](notebooks/comparison_notebook.ipynb):  
  **Experiment Comparison**  
  WMT analysis across multiple experiments and evaluate differences in transformation rates, variability, and dense water formation. 

## Dependencies 

This repository uses the environment available at /nbhome/ogrp/python/envs/dev. If unable to access this environment, a minimal installation might be similar to environment.yml, however this is missing the esnb notebook. 

### Important Notes / To Do

this repository is still being developed.

- **Limited compatibility with non-MOM6 models:**  
  Most of the functionality provided here relies explicitly on MOM6 outputs and conventions.

- **Check dictionaries for required fluxes:**  
  These notebooks use dictionaries to define WMT calculations. Users should verify that all necessary fluxes are provided; additional warnings would be useful.

- **Regridding resolution caution:**  
  When mapping transformations back to **x**-space, regridding is fixed at ¼°, which is appropriate only for ¼° experiments. If using different resolutions new functionality will need to be developed for mapping to **x**-space.

- **Fallback variables for missing fluxes:**  
  The notebooks sum transformations using individual fluxes. If those are unavailable in your `diag_table`, users can default to the net responses: `wfo`, `hfds`, and `sfdsi`. This requires change in dictionaries, probably should be built in, or use xbudget auto-dictionary(?)

- **Mapping to *x*-space is very slow:**  
  Always test mapping procedures first on short periods (1–3 years). For longer jobs, use `sbatch` or run processes in the background. 

- **Sign Convention Flip**
  SWMT should be calculated with the appropriate conventions, however a sign flip at the end is required such that positive values are increase in mass. It is not appropriate to flip the dictionary sign conventions before the transformation calculation.

