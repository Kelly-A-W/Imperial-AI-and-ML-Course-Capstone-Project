# Model card for BBO capstone project

## Overview: name of your approach, type and version.

Name: BBO Capstone project
Type: Bayesian optimisation using Guassian process surrogate models and UCB acquisition functions
Version: V10.0 

## Intended use: what tasks is it suitable for? What use cases should be avoided?

This approach is suitable when you need to find the location of the maximum of a target function without doing an exhaustive grid search. An example of this is trying to find the hyperparameters that optimise the loss function of a high-dimensional model. This method should not be used in cases where there are very few locations were the maximum could be (in which case an exhaustive grid search is feasible), or when the data available to fit the surrogate model is very noisy.  

## Details:

I have started by focusing on fitting my Gaussian process surrogate model with Matern kernel to the data, and adjusting hyperparameters until a achieved an appropriate fit. Once my surrogate fit the data well, I kept the hyperparameters the same throughout the following weeks and focused instead on adjusting the kappa value for the UCB acquisition function in order to balance exploration and exploitation. I do this by looking at the posterior standard deviations relative to the posterior mean by calculating the posterior coefficient of variation (CV), as well as looking at the performance of previous query points. If I notice that the CV has increased, then I choose kappa to favour exploration over exploitation. I also look at previous performance, and if I notice that, say, decreasing kappa has resulted in worse performance, I will then try to increase kappa to improve performance. 

## Performance: 

The key measure of performance used was the posterior CVs, as well as the target values of previous query points, and whether they were a new maximum and if so by how much. These metrics helped me adjust the kappa value each week to select a new query point. So far, I have found new maximums for all functions except function 1. 

## Assumptions and limitations: 

I am assuming that my surrogate models fit my data well and that it does not need any further tuning, and I am assuming that comparing the distribution of the posterior means to the distribution of the target variable is a good measure of model fit. This assumption allows me to focus more on adjusting the acquisition function, and by keeping my surrogate consistent, I know that any big changes in the performance of my query point is due to changes in kappa, rather than being unsure whether it is due to changes in kappa or changes in my surrogate model. A key limitation of this approach is that if the distribution of my posterior means is not a good measure of model fit and my surrogate model is in fact fitting my data badly, changes in kappa is unlikely help find a good query point. 

## Ethical considerations: 

I have made sure to documnet my work and my decision making process clearly so that the methods can be repoduced by future researchers reviewing my work. Good documentation also ensures that my methods are not applied inappropriately when being adpated to real-world problems. 
