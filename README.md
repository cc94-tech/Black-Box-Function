# Black-Box-Function
Repository for my capstone project focused on using ML to optimise high-dimensional black box function. This involves Bayesian optimisation techniques and visualisations to explore and evaluate query points.  
# Bayesian Optimization Capstone Project

**Author:** Can Chatan  
**Institution:** Imperial College London  
**Course:** Professional Certificate in Machine Learning and AI  
**Date:** December 2025

## Overview
This repository documents my Bayesian Optimization capstone project applying GP-UCB to Personal Independence Payment (PIP) assessment strategy optimization for Citizens Advice Richmond.

## Documentation
- **[DATASHEET.md](DATASHEET.md)** - Complete dataset documentation
- **[MODELCARD.md](MODELCARD.md)** - Bayesian optimization strategy details

## Methodology
**Approach:** Gaussian Process Upper Confidence Bound (GP-UCB)  
**Functions:** 8 black-box functions (1D to 8D)  
**Rounds:** 10 optimization iterations  
**Application:** Social service resource allocation under uncertainty

## Key Technical Details
- **Acquisition Function:** Upper Confidence Bound (UCB)
- **β Evolution:** 2.0 (Rounds 1-3) → 3.5 (Rounds 9-10)
- **Kernel:** Matérn 5/2 with learned lengthscales (0.15-0.25)
- **Strategy:** Adaptive exploration-exploitation balancing for social service constraints

## Citizens Advice Context
This optimization framework addresses resource allocation challenges for vulnerable populations, balancing efficiency with fairness and interpretability requirements essential for nonprofit deployment.

## Reproducibility
See MODELCARD.md for complete technical specifications, hyperparameters, and decision rules enabling independent replication.

## Contact
Can Chatan  
Imperial College London
Sent from my iPad
