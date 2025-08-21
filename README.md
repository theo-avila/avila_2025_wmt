# avila_2025_wmt
**Water Mass Transformation and Variability in the Nordic Seas** 

Theo C. Avila<sup>1*</sup>, Jacob M. Steinberg<sup>2</sup>, John P. Krasting<sup>2</sup>, Jan-Erik Tesdal<sup>2,3</sup>, Stephen M. Griffies<sup>3</sup><br> 

<sup>1</sup> Department of Physics, University of Illinois at Urbana-Champaign  
<sup>2</sup> Geophysical Fluid Dynamics Laboratory, NOAA  
<sup>3</sup> Program in Atmospheric and Oceanic Sciences, Princeton University    

<sup>*</sup> Correspondence should be addressed to: ctavila2@illinois.edu  

## Core Functionality:

  Compute transformations (λ=ρ) from model surface fluxes outputs for monthly climatologies, time average, and mapping back to **x**-space. Built-in support for analyzing certain basins, or by creating own basins. There is built-in subsetting by year, block bootstrapping functionality for internal variability, and for seasonal / yearly averages. This repo runs on `xwmt` (Drake et al, 2025), uses some code from Tesdal et al (2023), and borrows formalism from Groeskamp et al. (2019)

## Example Notebooks:

- [`notebooks/single_experiment.ipynb`](notebooks/single_experiment.ipynb):  
  **Single Experiment Analysis (IN PROGRESS)**  
  Walkthrough of a single experiment SWMT. (maybe just two? forced & not forced?)

- [`notebooks/comparison_notebook.ipynb`](notebooks/comparison_notebook.ipynb):  
  **Experiment Comparison**  
  WMT analysis across multiple experiments to evaluate differences in transformation rates, variability, and dense water formation.

- [`notebooks/single_experiment.ipynb`](notebooks/volume_transport_regionate/):  
  **Interior Volume Transport**  
  Interior Volume Transport in the Arctic, using regionate & sectionate but not esnb. These notebooks have issues on the `/nbhome/ogrp/python/envs/dev` environment, and instead users may use `/nbhome/Jacob.Steinberg/miniconda3/envs/mass_transport/`. These notebooks have certain parts of them hard-coded (reading models in / static files), and could benefit from esnb functionality, but many model variables are not in the catalogs. 

## Dependencies 

This repository is configured for use on GFDL’s **ppan** partition (post‑processing & analysis nodes) with the Conda environment at `/nbhome/ogrp/python/envs/dev`. If you can’t access that, recreate a minimal equivalent via `environment.yml` (note: the `esnb` notebook isn’t included). Volume Transport notebooks may use `/nbhome/Jacob.Steinberg/miniconda3/envs/mass_transport/`, as dependency conflicts currently cause issues with regionate and sectionate with the esnb package. 

## Tasks/Questions

- Shifts in Location of dense water formation in Arctic and relationship to Interior Transport (Årthun et al. 2025)
  - Can decreases (changes) in return flow in the Barents Sea be related to shifts in dense water formation? (Heukamp et al. 2025)
- How do mixing and eddy parameterizations affect uncertainty in time and space of dense water formation?
  - Shift in rho / SWMT plots exists for OM5_bXX models; spatially, how are model updates and mixing parameters affecting formation of dense water? 
- Is the seasonal-interannual variability representation of SWMT-induced interior transport in coupled models realistic (OSNAP, ECCO, Zou et al. 2024, ...)? 
- Do poleward shifts in dense water formation significantly impact Arctic Circulation (ArMOC)? (Bretones et al. 2022)
  
## References
- Årthun, M., et al. (2025). Atlantification drives recent strengthening of the Arctic overturning circulation. Science Advances, 11(28), eadu1794. https://doi.org/10.1126/sciadv.adu1794
- Bretones, A., et al. (2022). Transient Increase in Arctic Deep-Water Formation and Ocean Circulation under Sea Ice Retreat. Journal of Climate, 35(1), 109–124. https://doi.org/10.1175/JCLI-D-21-0152.1
- Drake, H. F., et al. (2025). Water mass transformation budgets in finite-volume generalized vertical coordinate ocean models. Journal of Advances in Modeling Earth Systems, 17(3), e2024MS004383. https://doi.org/10.1029/2024MS004383
- Groeskamp, S., et al. (2019). The Water Mass Transformation Framework for Ocean Physics and Biogeochemistry. Annual Review of Marine Science, 11(Volume 11, 2019), 271–305. https://doi.org/10.1146/annurev-marine-010318-095421
- Heukamp, F. O., et al. (2025). Atlantic water recirculation in the northern Barents Sea affects winter sea ice extent. Nature Communications, 16(1), 5148. https://doi.org/10.1038/s41467-025-59992-9
- Tesdal, J.-E., et al. (2023). Revisiting Interior Water Mass Responses to Surface Forcing Changes and the Subsequent Effects on Overturning in the Southern Ocean. Journal of Geophysical Research: Oceans, 128(3), e2022JC019105. https://doi.org/10.1029/2022JC019105
- Zou, S., Petit, T., Li, F., & Lozier, M. S. (2024). Observation-Based Estimates of Water Mass Transformation and Formation in the Labrador Sea. Journal of Physical Oceanography, 54(7), 1411–1429. https://doi.org/10.1175/JPO-D-23-0235.1

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

