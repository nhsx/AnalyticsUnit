---
layout: base
title: Generating high-fidelity tabular numeric/categorical data - SynthVAE
permalink: SynthVAE.html
---
 
<h2> {{page.title}} </h2>
 
[SyntheVAE](https://github.com/nhsx/SynthVAE) was produced off the back of one of our first [data science intern](https://nhsx.github.io/AnalyticsUnit/phdinterns.html) projects.  The final [report](https://github.com/nhsx/SynthVAE/blob/main/reports/report.pdf) gives the full details for this work.   The project focussed on one technique - the variational autoencoder, and asked if this is a suitable architecture as a synthetic generation tool in the context of the NHS and what privacy value can we demonstrate through the addition of differential privacy into this architecture.
 
Other architectures were considered and compared such as using a [Gaussian Copula](https://arxiv.org/pdf/2009.09471.pdf) or the [Conditional Tabular Generative Adversarial Network (CTGAN)](https://proceedings.neurips.cc/paper/2019/file/254ed7d2de3b23ab10936522dd547b78-Paper.pdf) approach.  However, the [variational autoencoder](https://arxiv.org/abs/1312.6114) was chosen as they have demonstrated similar performance to GANs on image generation but offer more interpretability.  
 
In a surprisingly short amount of time our intern was able to create a working variational autoencoder on our training data (the “[support](https://www.acpjournals.org/doi/10.7326/0003-4819-122-3-199502010-00007)” dataset) allowing the majority of the project to focus on incorporating functionality to optimise the data generation for privacy and to code evaluation metrics for quality and privacy.
 
## Incorporating Privacy through “Differential Privacy” (DP)
 
An immediate challenge when attempting to include privacy within machine learning models is to precisely define and evaluate the privacy of an algorithm. Differential Privacy (DP) addresses this challenge by providing a formal privacy metric using the intuition that if the model preserves privacy, then the removal of any single individual should not significantly affect the output of the model.  In general, a tradeoff must be made between complete privacy and optimal performance. Differential privacy (if it can be computed for the given procedure) allows the amount of privacy sacrificed during training to be quantified.
 
In order to incorporate differential privacy within a tool that would be able to optimise itself for a given training dataset we used a coupling of the differential privacy framework with a stochastic gradient descent algorithm (DP-SGD).  This works by editing the updates involved in gradient descent in two ways:
 
1. it clips the gradients corresponding to any particular example (intuitively this can be thought of as preventing the model overfitting to outliers, hence sacrificing their privacy) and
2. it adds noise to the gradients.  

An alternative approach would be to use Private Aggregation of Teacher Ensembles (PATE).  This involves the training of multiple “teacher” models, each trained on a separate partition of the dataset.  A “student” model is then trained using noised outputs of the teacher models.  This student model is the final output of the training procedure and has a calculable differential privacy budget.  
 
The benefits of DP-SGD over PATE is its conceptual and implementation simplicity but a valid future direction could be to investigate the application of PATE to SynthVAE. 
 
## Using Synthetic Data Vault Metrics to Evaluate out tool
 
[Synthetic Data Vault (SDV)](https://sdv.dev/) is an open-source project which provides synthetic data generation and evaluation functionality. In particular, it allows for numerous modern methods (e.g. Copulas, CTGAN) to be trained on a particular dataset and their performance compared, using a variety of metrics, with little code overhead.
 
SDV provides three types of metrics, namely:
 
- detection metrics - how easily synthetic data points can be distinguished from real data points using logistic regression models or support vector classifiers.
- distribution metrics - how similar the empirical distributions of the real and synthetic data are using gaussian mixture log-likelihood, chi-squared, kolmogorov-Smirnov, or Kullback-Leibler tests
- privacy metrics - empirical estimations by attempting to quantify how accurately the value of a sensitive variable within the real data can be predicted by a model trained on the synthetic data. 
 
See the project [report](https://github.com/nhsx/SynthVAE/blob/main/reports/report.pdf) for details of the evaluation results and comparison against the alternate architectures. 
 
The summary of this work was that the VAE is a viable synthetic health data generator and performs as well or better than other leading architectures on this simple training dataset.  It also allows for an easy adaptation to include differential privacy. 
 
However, it was seen that the measure of privacy provided by DP did not always correlate directly with the observed level of privacy according to SDV’s privacy metrics. This observation motivates further work. 
 
## Future Development
 
In early 2022 we have another intern taking up the development of this tool.  Possible areas of investigation include:
- Investigating the application of SynthVAE on large training datasets
- Incorporating further evaluation metrics to highlight quality,  privacy and fairness of the generated data
- Fine tuning of the model parameters
- Implementation in TensorFlow as well as the current PyTorch code
- Comparison against other model architectures to highlight the value of the approach
- Visualisation of the latent space through SNE or PCA
 
# Contact
 
Please get in contact through analytics-unit@nhsx.nhs.uk if you would like to discuss this specific project or to discuss the generation of synthetic data in general. 
