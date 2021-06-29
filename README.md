# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
**In 1-2 sentences, explain the problem statement: e.g "This dataset contains data about... we seek to predict..."**
In this scenario, a bank would like to predict the types of customers who will subscribe to one of its products, a term deposit. The dataset in use contains data about the bank's clients in terms of their demographics, their current products/situation and various financial variables.

**In 1-2 sentences, explain the solution: e.g. "The best performing model was a ..."**
##################################################

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**
The pipeline used a very simple architecture. It started with the import of a simple 2 dimensional dataset with 20 feature and 1 label columns of mixed types. The first step was to clean and transform the data including dropping records with null values (dropna), codifying/encoding values along with creating new features. Step 2 included randomly splitting the dataset into an 80/20 ratio for training and testing data. 2 parameters  were included (inverse of regularization strength and max_iteration) for use with a Logistics Regression Model, that was scored primarily on accuracy. This is a non-linear model that is used to model the probability of a class or event existing, in this case, applying for a term deposit. Using hyperdrive, I ran the scenario for 50 runs (1 failed), allowing the application to try different random permutations (randomparametersampling) of the 2 parameters (C - uniform from 0.05 to 1 and max_iter-6 choices ranging from 10 to 250) and allowing for early termination based on a banditpolicy. At the end, we used the best run to save the model for future use.

**What are the benefits of the parameter sampler you chose?**
Random Sampling was used for this model. One of its main benefits is that it allows you to quickly (but randomly) cover the search space in an initial run. With those results, the user could then refine their parameters for narrowed hyperparameter tuning. Other than that, it supports discrete (choice) and continuous (uniform) hyperparameters, which were used in this exercise. 

**What are the benefits of the early stopping policy you chose?**
A bandit policy was used to ensure efficient use of time and resources. This policy actively monitors the various runs. Once the best run so far has been established according to the specified primary performance metric, the policy monitors subsequent runs to determine their suitability. If a subsequent run's performance metric is outside a certain range (slack factor) at the specified evaluation interval, it is then terminated. This prevents time waste. 

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**
Data source improvement - this dataset was heavily imbalanced which could result in bias. There were ~33k samples, with a 89-11 percent split on the 2 classes. Generally, we could either get more balanced data, or reduce the samples in favor of balance. Of course, that would be experimental, as it might not be a huge issue.
On another note, we could also look at different metrics to understand their pros and cons and to determine suitability in this business case.

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
**Image of cluster marked for deletion**
