# Day_15_AM
Probability Theory Assignment (Python + SciPy)
This repository contains a Jupyter Notebook implementing several
probability theory problems using:
Python
NumPy
SciPy (`scipy.stats`)
Matplotlib
The notebook demonstrates practical applications of probability
distributions and the Central Limit Theorem using simulations and
visualizations.
---
Notebook Contents
1. Website Traffic --- Poisson Distribution
A website receives 200 requests per minute.
We compute:
P(X > 220)
assuming a Poisson distribution.
---
2. Quality Control --- Binomial Distribution
A batch contains 50 bolts, with 2% defective probability.
We compute:
P(X = 3)
using the Binomial distribution.
---
3. Delivery Times --- Normal Distribution
Delivery times follow:
N(45, 8²)
We compute:
P(X > 60)
P(40 < X < 50)
---
4. Customer Arrivals --- Poisson Process
Customers arrive at 10 per hour.
We compute the probability of no arrivals in 6 minutes.
---
5. Central Limit Theorem Simulation
A simulation demonstrates the Central Limit Theorem using:
Sample size: 35
Multiple simulations
Histogram of sample means
Normal approximation overlay
Function implemented:
simulate_clt(distribution, params, n_samples, n_simulations)
---
6. Beta Distribution Visualization
The notebook plots:
Beta(2,5)
Beta(5,5)
Beta(0.5,0.5)
---
Installation
Install dependencies:
pip install numpy scipy matplotlib jupyter
---
Running the Notebook
Start Jupyter:
jupyter notebook
Open:
probability_theory_assignment.ipynb
Run the cells sequentially.
---
Repository Structure
. ├── probability_theory_assignment.ipynb ├── README.md
---
Learning Goals
This assignment demonstrates:
Poisson, Binomial, Normal, and Beta distributions
Using scipy.stats for probability calculations
Visualization with matplotlib
Simulation of the Central Limit Theorem
---
License
This project is for educational purposes.
