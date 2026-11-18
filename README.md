# Spatiotemporal PM2.5 Prediction Across Delhi
## **Work in Progress**

## Overview

This project extends my earlier Delhi air-quality forecasting research into a spatiotemporal prediction framework. The goal is to estimate hourly PM2.5 concentrations at locations without air-quality monitoring stations, using observations from the surrounding monitoring network and relevant environmental variables.

The initial phase focuses on PM2.5 across Delhi, with the longer-term objective of extending the framework to additional pollutants.

## Research Approach

The project investigates how well spatial and machine-learning methods can generalize to locations excluded from model training.

Current experiments include:

- **Inverse Distance Weighting (IDW):** A spatial interpolation baseline that estimates pollution concentrations using observations from nearby monitoring stations.
- **Generalized Additive Models (GAM):** Models used to examine potentially nonlinear relationships between environmental variables and PM2.5 concentrations.
- **LightGBM:** A gradient-boosting approach evaluated for capturing more complex relationships in the data.
- **Environmental features:** Exploration of meteorological and atmospheric variables, including temperature, wind, surface pressure, and planetary boundary-layer height (BLH).
- **Fire-related features:** Preliminary experiments examining whether fire activity provides additional predictive information.

## Validation

A central part of this work is evaluating spatial generalization rather than relying solely on randomly splitting observations.

I use **Leave-One-Station-Out (LOSO) validation**, where observations from one monitoring station are withheld during training and used to evaluate predictions. This process is repeated across the monitoring network.

The current evaluation covers 33 monitoring stations and approximately 2.23 million test predictions.

## Current Progress

### Inverse Distance Weighting (IDW)

I implemented IDW as a spatial interpolation baseline to estimate PM2.5 concentrations at monitoring stations excluded from the prediction process. Geographic distances between stations were calculated using the Haversine formula, and nearby stations were assigned greater influence through inverse-distance weights. I evaluated distance powers of 1.5 and 2.0, with a minimum distance threshold of 0.5 km to prevent excessively large weights.

For each prediction, the target station was excluded from the source network, and measurements unavailable at a given hour were excluded from the weighted average. I also tested modifications to the spatial weights using wind direction, wind speed, temperature, humidity and boundary-layer height to examine whether atmospheric conditions could improve spatial estimates.

### Generalized Additive Model (GAM)

I developed a Generalized Additive Model using PyGAM to capture nonlinear relationships between PM2.5 concentrations, atmospheric conditions, temporal patterns and spatial information.

The model incorporates long-term trends, daily and seasonal cycles, boundary-layer height, wind speed and wind direction. Cyclic smooth functions capture repeating daily and annual patterns, while a two-dimensional smooth term models the relationship between wind direction components.

To incorporate spatial information, I used IDW estimates from surrounding stations at the current hour and at 1-, 3- and 6-hour lags as additional model inputs. The smoothing parameter was selected through three-fold grouped cross-validation, with entire monitoring stations held out during validation. Training was subsampled at 12-hour intervals to reduce computational costs, while predictions were evaluated hourly.

I also conducted separate experiments incorporating fire radiative power and fire counts to investigate whether fire activity provided additional predictive information.

## Project Status

**Work in Progress.** Model development, feature evaluation, validation, and error analysis are ongoing. Results are preliminary and may change as the methodology develops.

The current focus is on improving spatial generalization, understanding prediction uncertainty, and determining the practical limits of hourly PM2.5 estimation across Delhi.
