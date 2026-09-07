# Longitudinal Asymmetry of Large-Scale Traveling Ionospheric Disturbances During the May 2024 Superstorm

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/MustakimSaron/May2024-LSTID-Asymmetry/blob/main/May2024_LSTID_Analysis.ipynb)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.YOUR_ZENODO_ID.svg)](https://doi.org/10.5281/zenodo.YOUR_ZENODO_ID)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Official Google Colab replication notebook and data processing pipeline for the research paper:

> **"Longitudinal Asymmetry of Large-Scale Traveling Ionospheric Disturbances During the May 2024 Superstorm: A Comparative Study of Eurasian and North American Sectors"**  
> *Author:* Md Mustakim Bin Alam  
> *Affiliation:* Department of Physics, Novosibirsk State University, Russia  
> *Journal:* *Solar-Terrestrial Physics* (Solnechno-Zemnaya Fizika)

---

## Overview

This repository contains the complete interactive Google Colab notebook (`May2024_LSTID_Analysis.ipynb`) used to analyze the May 10–12, 2024 extreme geomagnetic superstorm (minimum $SYM\text{-}H = -518.0\text{ nT}$, peak $AE = 4098.0\text{ nT}$). 

The pipeline fetches 1-minute solar wind/interplanetary magnetic field (IMF) parameters via the NASA CDAWeb API, processes global GNSS vertical Total Electron Content (vTEC) grids from the CEDAR Madrigal database, constructs detrended meridional keograms across the Eurasian ($30^\circ\text{E}$–$40^\circ\text{E}$) and North American ($75^\circ\text{W}$–$85^\circ\text{W}$) sectors, calculates wavefront phase velocities ($V_p$), and conducts Welch Power Spectral Density (PSD) diagnostics.

---

## Key Experimental Discoveries

| Parameter | Eurasian Sector (30°E–40°E) | North American Sector (75°W–85°W) | Physical Mechanism / Asymmetry |
| :--- | :--- | :--- | :--- |
| **Local Time Regime** | Dusk / Night (~20:00–23:00 LT) | Afternoon / Dusk (~13:00–16:00 LT) | Diurnal solar EUV photoionization contrast |
| **Apparent Phase Speed ($V_p$)** | **$419.3\text{ m/s}$** ($R^2 = 0.991$) | **$635.2\text{ m/s}$** ($R^2 = 0.998$) | **$+215.9\text{ m/s}$ (+51.5%)** Doppler boost in NA |
| **Dominant Wave Period ($T$)** | **$53.3\text{ min}$** | **$48.0\text{ min}$** | Fundamental AGW resonance mode (Welch PSD) |
| **Horizontal Wavelength ($\lambda_h$)** | **$1340.9\text{ km}$** | **$1829.4\text{ km}$** | Confirms large-scale acoustic-gravity waves |
| **Storm/Quiet Power Ratio** | **$12.9\times$** ($+11.1\text{ dB}$) | **$11.3\times$** ($+10.5\text{ dB}$) | Statistically rules out ambient noise ($p < 0.001$) |
| **Spatial Coherence** | Damps sharply below $55^\circ\text{N}$ | Traverses cleanly $70^\circ\text{N} \to 30^\circ\text{N}$ | Nighttime trough vs. daytime plasma sheet |
| **Geomagnetic Latitude (at 50°N Geo.)** | **$46.4^\circ\text{N}$ MLAT** | **$59.4^\circ\text{N}$ MLAT** | Dipole tilt places NA $13.0^\circ$ closer to auroral oval |

---

## Notebook Structure (`May2024_LSTID_Analysis.ipynb`)

1. **Environment Setup & Dependencies:** Installs required packages (`numpy`, `scipy`, `pandas`, `matplotlib`, `requests`, `h5py`).
2. **Space Weather Drivers (NASA CDAWeb API):**
   * Connects to CDAWeb HAPI service (`OMNI_HRO_1MIN`).
   * Downloads 1-minute IMF $B_z$, solar wind velocity $V_{sw}$, dynamic pressure $P_{dyn}$, auroral electrojet $AE$, and ring current $SYM\text{-}H$.
   * Filters unphysical missing-value flags (`Pdyn >= 90.0 nPa`).
   * Generates **Figure 1** (`Figure_1_Clean.png`) and outputs `omni_drivers_may2024.csv`.
3. **GNSS Corridor Filtering & Detrending:**
   * Reads May 9–11 CEDAR Madrigal gridded HDF5 files.
   * Isolates meridional corridors: Eurasia ($30^\circ\text{E}$–$40^\circ\text{E}$) and North America ($75^\circ\text{W}$–$85^\circ\text{W}$) from $30^\circ\text{N}$ to $70^\circ\text{N}$.
   * Applies a 60-minute running-average high-pass filter: $\Delta\text{TEC} = \text{TEC} - \langle\text{TEC}\rangle_{1\text{h}}$.
   * Generates **Figure 2** (`Figure_2_TID_Keograms.png`).
4. **Wave Kinematics & Damping Analysis:**
   * Tracks primary equatorward crests launched post-SSC (~17:40 UT on May 10).
   * Performs least-squares linear regression to yield $V_p = 419.3\text{ m/s}$ (EU) vs. $635.2\text{ m/s}$ (NA).
   * Calculates latitudinal peak-to-peak amplitude attenuation profiles.
   * Generates **Figure 3** (`Figure_3_Wave_Dynamics.png`).
5. **Quiet Baseline Control & Welch PSD:**
   * Compares undisturbed baseline (00:00–12:00 UT) against main-phase disturbance (16:00–23:55 UT) at $50^\circ\text{N}$.
   * Evaluates Welch periodogram spectra to confirm peak frequencies ($53.3\text{ min}$ vs. $48.0\text{ min}$).
   * Generates **Figure 4** (`Figure_4_Defense_Spectral_Control.png`).

---

## Data Availability (Zenodo Repository)

The raw observation grids and pre-computed driver tables are permanently archived on Zenodo:

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.YOUR_ZENODO_ID.svg)](https://doi.org/10.5281/zenodo.YOUR_ZENODO_ID)

* `gps240509g.002.hdf5`: World-wide GNSS vTEC grid (May 9, 2024 — quiet reference day).
* `gps240510g.003.hdf5`: World-wide GNSS vTEC grid (May 10, 2024 — shock arrival & primary wave packet).
* `gps240511g.003.hdf5`: World-wide GNSS vTEC grid (May 11, 2024 — storm peak & secondary pulse).
* `omni_drivers_may2024.csv`: 1-minute NASA OMNI driver series.
* `Figure_1_Clean.png`, `Figure_2_TID_Keograms.png`, `Figure_3_Wave_Dynamics.png`, `Figure_4_Defense_Spectral_Control.png`: High-resolution 300 DPI figures.

---

## How to Run

### Option 1: Run in Google Colab (Recommended)
Click the badge below to open the notebook directly in your browser:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/MustakimSaron/May2024-LSTID-Asymmetry/blob/main/May2024_LSTID_Analysis.ipynb)

*Note:* When executing the GNSS processing cells in Colab, ensure the HDF5 data files from the [Zenodo repository](https://doi.org/10.5281/zenodo.YOUR_ZENODO_ID) are uploaded to your Colab session runtime directory (`/content/`).

### Option 2: Run Locally
Clone the repository and install requirements:

```bash
git clone [https://github.com/MustakimSaron/May2024-LSTID-Asymmetry.git](https://github.com/MustakimSaron/May2024-LSTID-Asymmetry.git)
cd May2024-LSTID-Asymmetry

pip install numpy scipy pandas matplotlib requests h5py jupyter
jupyter notebook May2024_LSTID_Analysis.ipynb
