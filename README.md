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

Initial experiments show that IDW currently performs slightly better than the tested GAM and LightGBM approaches, with an R² of approximately 0.814.

This raises an important research question: how much of the remaining prediction error comes from model limitations, monitoring-network geometry, and short-term pollution variability that is not captured by the available features?

Further experiments are underway to investigate these limitations, particularly during periods of elevated pollution and rapidly changing atmospheric conditions.

## Project Status

**Work in Progress.** Model development, feature evaluation, validation, and error analysis are ongoing. Results are preliminary and may change as the methodology develops.

The current focus is on improving spatial generalization, understanding prediction uncertainty, and determining the practical limits of hourly PM2.5 estimation across Delhi.
