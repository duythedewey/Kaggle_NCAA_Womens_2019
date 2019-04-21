# Kaggle_NCAA_Womens_2019

## Description
Solution for 3rd place finish in Kaggle's NCAA March Madness 2019 Tournament

## Data Files
All input data files were sourced from https://www.kaggle.com/c/womens-machine-learning-competition-2019/data

## Model Overview
A linear regression model was put together using pymc3. All data pre-processing and post-processing steps were handled using both numpy and pandas.
- FG attempts as team-level Gammas vs Normals (or Poissons for counts) to allow using loc/scale parameters instead of mu/sd 
- FG percentages as team-level Betas vs Bounded (0,1) Normals to allow using loc/scale parameters instead of mu/sd
- League-level Half-Cauchy error term to soak up some variance 
- Assume team's scoring propensity is normally-distributed and treat as observed variable
- Assume points spread between two teams is normally-distributed and treat as observed variable

Evaluation of odds of one team winning over another was done via simulation of team-level posterior scoring propensities (calculated from above).
- Simulation for each match up produces an output distribution representing the spread of each simulated match
- The win probability is determined by the number of simulated matches won over the total number of simulated matches
- 5000 simulations were run for each potential match up
