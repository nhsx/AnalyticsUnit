---
layout: base
title: Model Class Reliance for Demonstrating Variable Importance 
permalink: MCR.html
---

<h2> {{page.title}} </h2>

One of our data science intern projects looked into applying a novel variable importance technique, MCR (model class reliance), to machine learning models in order to assess the [Value of Commercial Product Sales Data in Healthcare Prediction](https://github.com/nhsx/commercial-data-healthcare-predictions).  See the write up in the report folder.  

Here, we’ll just focus on the variable importance component of the project and where else this technique could be used. 

## Variable Importance tools

Variable importance tools can, in the main, be broken down into three types: coefficient, decision split, or permutation.   
- **Coefficient feature importance** investigates the model outputs from models such as linear or logistic regressions to see if the feature fits.  
- **Decision split feature importance** attempts to minimise the split points for algorithms such as random forests, classification and regression trees of some stochastic gradient boosted algorithms.  
- **Permutation feature importance** runs the same predictive model many times over different subsets of features and compares the predictive power to understand the mean importance score for each feature. 

Whilst permutation techniques can be more resource intensive and require a performance metric to be defined, they are recommended as they are model agnostic, can be applied to complex or opaque models, and can be used to compare features across multiple models. 

During the first phase of the project a standard permutation importance tool within the scikit-learn python library was used - the [permutation importance function](https://scikit-learn.org/stable/modules/permutation_importance.html).    

In addition to this a [SHAP (SHapley Additive exPlanations)](https://papers.nips.cc/paper/2017/file/8a20a8621978632d76c43dfd28b67767-Paper.pdf) Analysis was completed, which attributes to each feature the change in the expected model prediction when conditioning on that feature.  

By running these variable importance tools on one arbitrary model, misleading results can be given due to the stochastic nature of the model’s machine learning algorithms. This is a problem because different instances of an optimised model class can use different variables (features) and in different ways to achieve the same model predictive performance. 

To address the problem of standard variable importance tools only evaluating one instance of a model, MCR (Model Class Reliance) was applied and compared.  

## Model Class Reliance

MCR was developed by [Fisher et al.](https://arxiv.org/abs/1801.01489) to compute the feature importance bounds across all optimal models called the Rashomon set for Kernel (SVM) Regression (polynomial run-time). [Smith, Mansilla and Goulding](https://papers.nips.cc/paper/2020/hash/fd512441a1a791770a6fa573d688bff5-Abstract.html) introduced a new technique that extends the computation of MCR to Random Forest classifiers and regressors.  This new technique is being developed as part of the [UKRI CIVIC project](https://gtr.ukri.org/projects?ref=EP%2FV053922%2F1).

MCR builds on permutation importance for a single model, computing the permutation feature importance bounds (MCR-, MCR+) for an input variable across all instances of the predictive model; calculating the minimum and maximum impact a variable could have on the predictions across all instances of the model. 

![Diagrammatic representation of the difference between other variable importance tools and
MCR](assets/img/MCR.png)

The base MCR analysis evaluates each feature individually for its importance, for example the importance of ‘minimum temperature’. It does not assess how important a dataset type used to create a number of the models’ features was to predictions as a whole, for example ‘weather’.  A [Group-MCR](https://ieeexplore.ieee.org/abstract/document/9671559?casa_token=F3GX0kqkGr0AAAAA:A4dT_VksM3_eSvrIaUJv8Y2OBp08bwH1wcZvRQxU4K017UkddLRkKdKFBLMVLCRRr4dcTDCCZMw) version has also been created in order to calculate the effects of variable groups, measuring the importance of a collection of features together on the predictions (See main project report for more details).

## Use in Healthcare Predictions

MCR can be used to establish the value of using a variable in a model being created for healthcare predictions, by suggesting which data types must be acquired for a predictive model to work effectively. In a healthcare setting it must be considered whether it is worth the investment in acquiring a type of data if another dataset works equally well, and is more affordable, or easier to access. MCR highlights which data types could be irreplaceable and which could be interchangeable. 

MCR results can also be used to guide the reduction of variables in order to create more transparent models for healthcare predictions.

GroupMCR offers us further information by implying how groups of variables may be working together in the model’s algorithms. By enabling the reduction of the number of variables, MCR can also be used to help decrease the dimensionality of the model leading to a more manageable global surface area to search for optimized meta-parameters. Creating the most accurate model possible using the chosen variables, would further evidence the value of their inclusion.

