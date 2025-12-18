 Datasheet: BBO Capstone Query Dataset

## Motivation

### Why was this dataset created?
This dataset was created to support Bayesian Optimization research applied to Personal Independence Payment (PIP) assessment strategy optimization for Citizens Advice Richmond. 
The dataset demonstrates GP-UCB optimization under severe query budget constraints typical of nonprofit resource allocation scenarios.

### What tasks does it support?
- Sequential black-box optimization with limited evaluation budgets (10-20 queries per function)
- Multi-objective optimization balancing accuracy, fairness, and interpretability
- Resource allocation strategy development for vulnerable populations
- Teaching and research in constrained Bayesian optimization

### Who created this dataset?
**Creator:** Can Chatan 
**Institution:** Imperial College London  
**Date:** December 2025  
**Context:** BBO Capstone Project  

---

## Composition

### What does the dataset contain?
**Size:** 80 query-evaluation pairs (10 rounds × 8 functions)  
**Structure:** Sequential Bayesian optimization data across 8 black-box functions of varying dimensionality  
**Dimensions:** Functions range from 1D (F1) to 8D (F8)  
**Format:** Structured data with query coordinates and corresponding function evaluations

### Instance breakdown:
- 10 evaluations per function
- 8 functions representing different complexity levels
- Generated over 10 optimization rounds using adaptive strategy

### Missing data:
**No missing evaluations:** All 80 queries successfully completed  
**Sparse spatial coverage:** High-dimensional functions (F6-F8) have limited coverage (~0.08 queries per unit hypercube in 8D space)  
**Boundary undersampling:** Less than 20% of queries explore domain edges

---

## Collection Process

### How was the data collected?
**Method:** Iterative Bayesian Optimization using Gaussian Process Upper Confidence Bound (GP-UCB)  
**Platform:** Imperial College BBO portal system  
**Duration:** November-December 2025

### Strategy evolution across rounds:
- **Rounds 1-3:** Broad exploration (β=2.0) with space-filling initialization
- **Rounds 4-6:** Balanced exploration-exploitation (β=2.5)
- **Rounds 7-10:** Targeted exploitation with safety exploration (β=3.0-3.5)

### Human oversight:
Approximately 5-8% of algorithmically suggested queries were manually reviewed with the following intervention criteria:
- Redundancy filter: Reject queries within Euclidean distance < 0.01 of previous queries
- Diversity promotion: Force boundary exploration if >80% queries clustered centrally
- Deployment feasibility: Avoid high-curvature regions difficult to explain to stakeholders

### Sampling characteristics:
- **Adaptive sequential design:** Later queries conditioned on all previous evaluations
- **Path-dependent:** Alternative initialization would yield different query sequences
- **Quality controlled:** Visual inspection for out-of-bounds or duplicate proposals

---

## Preprocessing and Uses

### Preprocessing applied:
**Input normalization:** All dimensions scaled to [0,1] domain bounds  
**Output treatment:** Raw function evaluations preserved without scaling  
**No imputation:** Not applicable as no missing values exist

### Intended uses:
- Research benchmark for constrained Bayesian optimization algorithms
- Educational case study demonstrating exploration-exploitation trade-offs
- Framework for social service resource allocation optimization
- Teaching adaptive hyperparameter strategies in sequential decision-making

### Inappropriate uses:
- Direct deployment without validation (synthetic functions, not real PIP data)
- Claiming global optimality given limited query budgets
- Generalization to other populations without domain-specific adaptation
- Automated decision-making without human oversight in high-stakes contexts

---

## Distribution and Maintenance

### Availability:
**Location:** GitHub repository https://github.com/cc94-tech/Black-Box-Function  
**Access:** Publicly available  
**License:** MIT License

### Maintenance:
**Maintainer:** Can Celik  
**Version:** 1.0 (December 2024)  
**Status:** Final dataset after Round 10; no further optimization planned  
**Updates:** No ongoing updates planned post-project completion  
**Issue reporting:** Via GitHub Issues in repository

### Retention:
Dataset maintained through at least December 2025 for academic and portfolio purposes.

---

## Ethical Considerations

### Privacy and confidentiality:
- No personally identifiable information included
- Synthetic optimization problem (not real client data)
- Framework designed with GDPR compliance for future real-world deployment

### Fairness and bias:
- Central clustering bias acknowledged: 85% of queries in [0.3, 0.7] range per dimension
- High-dimensional functions representing intersectional vulnerabilities remain under-explored
- Strategy prioritized safety (finding missed populations) over pure optimization efficiency

### Deployment considerations:
- Human oversight mandatory for real-world applications
- Citizens Advice context requires interpretable recommendations for volunteer staff
- Regular fairness audits required across protected characteristics if deployed
- Client consent essential for any AI-assisted PIP assessment

---
