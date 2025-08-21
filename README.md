# avila_2025_wmt
**Water Mass Transformation and Variability in the Nordic Seas** 

Theo C. Avila<sup>1*</sup>, Jacob M. Steinberg<sup>2</sup>, John P. Krasting<sup>2</sup>, Jan-Erik Tesdal<sup>2,3</sup>, Stephen M. Griffies<sup>3</sup><br> 

<sup>1</sup> Department of Physics, University of Illinois at Urbana-Champaign  
<sup>2</sup> Geophysical Fluid Dynamics Laboratory, NOAA  
<sup>3</sup> Program in Atmospheric and Oceanic Sciences, Princeton University    

<sup>*</sup> Correspondence should be addressed to: ctavila2@illinois.edu  

## Core Functionality:

  Compute transformations (λ=ρ) from model surface fluxes outputs for monthly climatologies, time average, and mapping back to **x**-space. Built-in support for analyzing certain basins, or by creating own basins. There is built in subsetting by year, and block bootstrapping functionality for internal variability.

## Example Notebooks:

- [`notebooks/single_experiment.ipynb`](notebooks/single_experiment.ipynb):  
  **Single Experiment Analysis (IN PROGRESS)**  
  Walkthrough of single experiment SWMT. (maybe just two? like forced & not forced?)

- [`notebooks/comparison_notebook.ipynb`](notebooks/comparison_notebook.ipynb):  
  **Experiment Comparison**  
  WMT analysis across multiple experiments and evaluate differences in transformation rates, variability, and dense water formation.

  - [`notebooks/single_experiment.ipynb`](notebooks/single_experiment.ipynb):  
  **Interior Volume Transport**  
  Interior Volume Transport in the Arctic, using regionate & sectionate but not esnb. These notebooks have issues on the `/nbhome/ogrp/python/envs/dev` environment, and instead users should may use `/nbhome/Jacob.Steinberg/miniconda3/envs/mass_transport/`. These notebooks have certain parts of them hard-coded (reading models in / static files), and could benefit from esnb functionality but many model variables are not in the catalogs. 

## Dependencies 

This repository is configured for use on GFDL’s **ppan** partition (post‑processing & analysis nodes) with the Conda environment at `/nbhome/ogrp/python/envs/dev`. If you can’t access that, recreate a minimal equivalent via `environment.yml` (note: the `esnb` notebook isn’t included).

## Important Notes / To Do

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
  SWMT should be calculated with the appropriate conventions, however a sign flip at the end is required such that positive values are increase in mass. It is not appropriate to flip the dictionary sign conventions before the transformation calculation. The sign flip is done within the notebooks already (so no change is needed), but for further development and use it is important to realize this convention. 

- **Ocean Only**  
  Salinity restoring terms must be added to the dictionaries if using ocean-only experiments.

