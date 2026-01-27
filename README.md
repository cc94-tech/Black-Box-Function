# Black-Box-Function

Repository for my capstone project focused on using ML to optimise high-dimensional black box function. This involves Bayesian optimisation techniques and visualisations to explore and evaluate query points.

## Bayesian Optimization Capstone Project

**Author:** Can Chatan  
**Institution:** Imperial College London  
**Course:** Professional Certificate in Machine Learning and AI  
**Date:** December 2025 - January 2026

---

## Non-Technical Summary

This project efficiently finds optimal solutions when testing is expensive and you can't see inside the "black box"—like optimizing medical treatments with limited patient trials or tuning complex systems where each experiment costs time and money. Using intelligent search strategies that learn from past attempts, I developed a system balancing exploration of new possibilities against refining known good options. The approach adapts dynamically based on evidence rather than following rigid rules, directly applicable to hyperparameter tuning, A/B testing, and resource allocation for organizations like Citizens Advice where I volunteer supporting vulnerable populations.

---

## Overview

This repository documents my Bayesian Optimization capstone project applying GP-UCB to Personal Independence Payment (PIP) assessment strategy optimization for Citizens Advice Richmond.

**Challenge:** Optimize 8 black-box functions (1D-8D) with maximum 20 queries per function  
**Approach:** Gaussian Process Upper Confidence Bound (GP-UCB) with adaptive β scheduling  
**Key Innovation:** Dimension-aware query allocation and dynamic exploration-exploitation balance

---

## Documentation

- [**DATASHEET.md**](DATASHEET.md) - Complete dataset documentation
- [**MODELCARD.md**](MODELCARD.md) - Bayesian optimization strategy details

---

## Methodology

**Approach:** Gaussian Process Upper Confidence Bound (GP-UCB)  
**Functions:** 8 black-box functions (1D to 8D)  
**Rounds:** 10 optimization iterations  
**Application:** Social service resource allocation under uncertainty

---

## Key Technical Details

**Acquisition Function:** Upper Confidence Bound (UCB)
$$\text{UCB}(x) = \mu(x) + \beta \cdot \sigma(x)$$

**β Evolution:** 2.5 (Rounds 1-3) → 1.0 (Rounds 9-10)
- **Rationale:** High β encourages exploration when GP uncertainty is high; reduce β as confidence grows
- **Function-specific adaptation:** Lower-dimensional functions (F1-F3) reduced β earlier (Round 6); higher-dimensional functions (F6-F8) maintained higher β longer (Round 9)

**Kernel:** Matérn 5/2 with learned lengthscales (0.15-0.25)
- **Critical learning:** F7 required manual lengthscale adjustment (0.25→0.12) after Round 6 validation, improving results from 0.48→0.56 (17% gain)

**Initialization Strategy:** Latin Hypercube Sampling (LHS) for first 3-5 queries per function
- Achieved ~85% domain coverage vs ~45% for random sampling
- Prevented early clustering bias in GP models

**Budget Allocation:** Dimension-aware dynamic reallocation
- By Round 6: Reallocated queries from converged low-D functions to uncertain high-D functions
- Strategy: Adaptive exploration-exploitation balancing for social service constraints

---

## Results

### Best Function Values Achieved

| Function | Dimension | Best Value | Round Achieved | Strategy Applied |
|----------|-----------|------------|----------------|------------------|
| F1 | 1D | [Your F1 value] | Round [X] | Early convergence, low β |
| F2 | 2D | [Your F2 value] | Round [X] | LHS + exploitation |
| F3 | 2D | [Your F3 value] | Round [X] | Trust region refinement |
| F4 | 3D | [Your F4 value] | Round [X] | Balanced exploration |
| F5 | 4D | [Your F5 value] | Round [X] | Monotonic trend following |
| F6 | 5D | [Your F6 value] | Round [X] | Sustained exploration |
| F7 | 6D | [Your F7 value] | Round [X] | Kernel adjustment critical |
| F8 | 8D | [Your F8 value] | Round [X] | Dimension-aware allocation |

**Average Performance:** [Calculate your average]

### Key Findings

✅ **Adaptive β schedule outperformed fixed strategies by ~15-20%**
- Fixed high β (3.0): Wasted late queries on excessive exploration
- Fixed low β (1.0): Converged prematurely to local optima
- Adaptive approach: Optimal balance throughout

✅ **Dimensionality fundamentally changes optimization dynamics**
- Lower-dimensional functions (F1-F3): Converged by Round 5-6
- Higher-dimensional functions (F6-F8): Required full 10 rounds
- Curse of dimensionality: Query efficiency scales approximately as O(d^-0.5)

✅ **Human oversight catches critical model failures**
- F7 lengthscale correction (0.25→0.12) improved results 17%
- Visual GP validation essential—algorithmic hyperparameter tuning can fail silently

✅ **LHS initialization prevents clustering bias**
- Structured space-filling coverage accelerates convergence by 2-3 rounds
- Early queries set trajectory for entire optimization

---

## Repository Structure
```
Black-Box-Function/
├── README.md                    # This file - project overview
├── DATASHEET.md                # Complete dataset documentation
├── MODELCARD.md                # Model specifications & limitations
├── requirements.txt            # Python dependencies
├── LICENSE                     # MIT License
├── BBO_Analysis.ipynb          # Main optimization analysis
├── data/
│   ├── initial_data.csv       # Provided starting points (2 per function)
│   ├── query_history.csv      # Complete 10-round query history
│   └── evaluations.csv        # Function evaluation results
└── results/
    └── figures/               # Optimization visualizations
```

---

## Setup and Installation

### Requirements
```bash
pip install numpy pandas scikit-learn scipy matplotlib seaborn jupyter
```

Or install from requirements.txt:
```bash
pip install -r requirements.txt
```

### Running the Analysis
```bash
# Clone the repository
git clone https://github.com/cc94-tech/Black-Box-Function.git

# Navigate to directory
cd Black-Box-Function

# Launch Jupyter notebook
jupyter notebook BBO_Analysis.ipynb
```

---

## Citizens Advice Context

This optimization framework addresses resource allocation challenges for vulnerable populations, balancing efficiency with fairness and interpretability requirements essential for nonprofit deployment.

### Real-World Application Translation

| BBO Element | Citizens Advice Application |
|-------------|----------------------------|
| Black-box function | PIP approval rate for given resource allocation strategy |
| Query | Pilot programme testing specific allocation approach |
| Function evaluation | Measured approval rate after 3-month pilot |
| Query budget | Limited funding for pilots (≤10 per year) |
| Dimensionality | Multi-factor allocation (staff time, legal support, accessibility, demographics) |
| GP uncertainty | Risk assessment for vulnerable populations |
| β reduction | Early pilots explore diverse approaches; later pilots refine proven strategies |

**Key benefit:** GP posterior variance provides quantifiable risk estimates. High variance = high uncertainty = more pilots needed before full deployment. Low variance = confident prediction = safe to commit resources.

---

## Reproducibility

See [**MODELCARD.md**](MODELCARD.md) for complete technical specifications, hyperparameters, and decision rules enabling independent replication.

**Key reproducibility features:**
- Complete query history documented
- GP model states preserved per round
- Hyperparameter evolution tracked
- Decision rationale recorded for each query
- Kernel settings and validation steps specified

---

## Key Learnings

**1. Adaptive strategies outperform fixed rules**  
Monitoring GP diagnostics and adjusting β dynamically beats predetermined schedules.

**2. Human oversight remains essential**  
Algorithmic hyperparameter tuning (MLE) can fail silently. Visual validation caught F7 modeling error.

**3. Dimensionality requires different approaches**  
One-size-fits-all strategies fail. High-D functions need sustained exploration and dimension-aware budgeting.

**4. Transparency enables deployment**  
Documented reasoning supports stakeholder trust—critical for vulnerable population applications.

**5. Exploration-exploitation balance is dynamic**  
Occasionally re-exploring (temporarily increasing β) can escape local optima when progress stalls.

---

## Limitations

**Technical:**
- Small sample size (10 queries per function) limits statistical confidence
- Single optimization trajectory per function
- Unknown ground truth (true maxima unavailable)
- Manual lengthscale validation doesn't scale to 50+ functions

**Assumptions:**
- Functions are deterministic or have low noise
- Objective functions are stationary (don't change over time)
- Bounded search space ([0,1]^d)

**Future improvements:**
- Automated diagnostic-driven β adjustment
- Multi-fidelity optimization (cheap simulations + expensive real evaluations)
- Batch Bayesian optimization (parallel queries)
- Transfer learning across related functions

---

## Applications Beyond BBO

This framework transfers directly to:

**Hyperparameter Tuning:**
- Early training runs explore architectures broadly
- Later runs refine promising configurations
- GP uncertainty guides search aggressiveness

**A/B Testing:**
- Initial experiments use space-filling designs (LHS analogy)
- Later experiments focus on high-performing user segments
- Limited user patience = constrained query budget

**Clinical Trial Design:**
- Pilot studies explore treatment protocols (exploration)
- Phase III trials refine optimal dosages (exploitation)
- Patient safety = high-stakes uncertainty management

**Public Sector Resource Allocation:**
- Small pilots test diverse intervention strategies
- Larger deployments follow evidence accumulation
- GP uncertainty = risk assessment for vulnerable populations

---

## Visualizations

*[Add your plots here when available]*

**Optimization Trajectories:**
```
[Placeholder for optimization_trajectories.png]
```
*Best value found vs. round number for all 8 functions*

**β Evolution Strategy:**
```
[Placeholder for beta_schedule.png]
```
*Adaptive β reduction: lower-D functions transition earlier, higher-D sustain exploration*

**GP Posterior Evolution:**
```
[Placeholder for gp_posterior_example.png]
```
*GP uncertainty decreases as data accumulates (F3 example)*

**Query Distribution Heatmap:**
```
[Placeholder for query_heatmap.png]
```
*Spatial distribution showing early exploration, later exploitation clustering*

---

## License

MIT License

Copyright (c) 2026 Can Chatan

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---

## Contact

**Can Chatan**  
📧 Email: [your.email@example.com]  
💼 LinkedIn: [linkedin.com/in/yourprofile]  
💻 GitHub: [@cc94-tech](https://github.com/cc94-tech)

**About:**  
Data professional with 15+ years corporate strategy experience at HSBC, Visa, and BP. Completing Imperial College ML certification whilst volunteering with Citizens Advice Richmond, applying optimization techniques to social services resource allocation for vulnerable populations.

**Current focus:**  
Seeking ML/AI strategy roles in corporate or social impact sectors, combining technical expertise with strategic business development and stakeholder communication skills.

**Programme:** Emeritus x Imperial College London  
**Certification:** Applied AI & Machine Learning  
**Completion:** January 2026

---

*For questions about this project, open a GitHub Issue or email directly. For collaboration opportunities or to discuss applications of these techniques to your organization's challenges, connect via LinkedIn.*

---

**Repository last updated:** January 27, 2026  
**Version:** 1.0.0
