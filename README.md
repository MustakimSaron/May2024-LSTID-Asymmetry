# Large-Scale Traveling Ionospheric Disturbances (May 2024 Superstorm)

Analysis pipeline for:  
**"Longitudinal Asymmetry of Large-Scale Traveling Ionospheric Disturbances During the May 2024 Superstorm: A Comparative Study of Eurasian and North American Sectors"**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/MustakimSaron/May2024-LSTID-Asymmetry/blob/main/May2024_LSTID_Analysis.ipynb)

## Code Overview
- `step1_space_weather.py`: Interplanetary drivers and storm timeline (Figure 1).
- `step3_keograms.py`: Detrended TEC extraction and meridional keograms (Figure 2).
- `step4_wave_tracking.py`: Linear regression wavefront tracking and damping (Figure 3).
- `step5_defense_analyses.py`: Baseline control and Welch power spectral density (Figure 4).

## Data Access
Observational HDF5 and CSV datasets are deposited on Zenodo: [https://doi.org/10.5281/zenodo.YOUR_ZENODO_ID](https://doi.org/10.5281/zenodo.YOUR_ZENODO_ID)
