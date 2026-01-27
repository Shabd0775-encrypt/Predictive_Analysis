
# Data Generation using Modelling and Simulation for Machine Learning

## Problem Statement
This project demonstrates synthetic data generation using modelling and simulation and its application to machine learning.

A discrete-event queueing system is simulated using SimPy, and the generated data is used to train and evaluate multiple ML models.

## Simulation Tool
SimPy – a Python-based discrete event simulation library suitable for modelling queueing systems.

## Input Parameters
- arrival_rate (0.2 – 2.0)
- service_rate (0.5 – 3.0)
- queue_capacity (5 – 50)
- simulation_time (50 – 300)

## Output Parameters
- avg_wait_time (Target variable)
- avg_system_time
- server_utilization

## ML Models Used
- Linear Regression
- Random Forest Regressor
- Support Vector Regressor
- KNN Regressor
- Decision Tree Regressor

## Evaluation Metrics
- MAE
- RMSE
- R² Score

## Conclusion
Random Forest Regressor produced the best performance for predicting average waiting time.

## Author
Shabd Sharma
