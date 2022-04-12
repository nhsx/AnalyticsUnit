---
layout: base
title: Assessing Privacy of Generated Synthetic Data through Friendly Motivated Attacks - Synthetic Adversarial Suite
permalink: SynthAdvSuite.html
---
 
<h2> {{page.title}} </h2>
 
In the NHS, when synthetic datasets are generated, or synthetic data-producing models released, there is currently little support for validating the privacy of the data and benchmarking the product against any standards. This leads to a dependence on the party generating the data to prove the privacy, which creates a conflict of interest.
 
As assessing the privacy of generated synthetic data is a difficult task we have often found that this acts as a blocker to the data being finally shared and used for the very purpose it was created.
 
A common approach is to use adversarial attacks on the data to prove what information can be ascertained if the attack has different levels of information.  While many guides to carrying out adversarial attacks to recover real information from synthetic datasets are in the literature, the style of attacks are highly varied, and specific to particular cases.   To make a tool that could be applied across multiple projects and be used as a benchmark for privacy we needed to focus on membership inference attacks.   Two scenarios were identified that we aimed to address:
 
A proof of concept suite of extensible tools were built, with example attack scenarios which can be deployed against a range of synthetic data models.   By building for extensibility, additional attack scenarios can be built for and included in the suite in future. A set of high-level pipeline elements that handle stages common to synthetic data generation, attacks, or both, were developed. Each stage also included code-injection points, for generic deployability of the suite.  These stages included: Dataset preprocessing, model training, shadow dataset generation, attack model training. Keeping these elements at a high level should cover many synthetic data modelling approaches, but may not be back-compatible with all pipelines described in the literature.
 
The included scenarios in this commission were all membership inference (MI) attacks where an attacker has no information about any individuals they expect to be present in the training set of a synthetic data model, and seek to recover partial or complete data records of individuals in the training set.  Future work would need to consider other forms of attack such as linkage attacks.
 
Two specific scenarios were then developed
 
### Scenario 1: Clear Box
 
Situation: Access to the synthetic dataset and a description of the generative model’s architecture and training procedure. 
 
The rationale for this attack is that a particular model architecture and training procedure will lead to a particular level of overfitting on training data. A synthetic data model will then leave artefacts in its output synthetic data differently for input data that was and wasn’t in its training data.
 
However, each synthetic data model may leave different artefacts. It would be a simple exercise for an attacker to train an attack classifier against a single shadow model – essentially the classifier would only have to memorise that shadow model’s training set to achieve perfect accuracy.
 
Instead, by training against data produced by many instantiations of the same architecture and training procedure, the classifier must learn to recognise artefacts that differentiate ‘in training’ and ‘out of training’ data that generalise across the family of synthetic data models with the same architecture and training procedure, rather than seeking artefacts specific to a single shadow model.
 
This should then generalise to the artefacts left in the synthetic dataset by the original synthetic data model. There may be a compound effect, as the attacker has trained their shadow models on synthetic data – a higher number of artefacts may be expected in the attacker’s shadow dataset compared to the first synthetic dataset. However, the presence of some similar artefacts in the first synthetic dataset will mean that reducing a threshold on the classifier’s confidence of detecting ‘in training’ data may be the only change needed to begin identifying likely candidates of data leakage through the original synthetic data model. This threshold would be quite simple to determine if clustering methods showed clear separation in the confidence values returned by the classifier on the researchers’ synthetic dataset.
 
### Scenario 2: Black Box
 
Situation: Access to a black box model that can provide unlimited synthetic data, with data realistic of the training distribution gath
 
This attack scenario generates a single large shadow dataset, to be used to train a regressor that predicts the target model's output data distance from the input data - essentially predicting how much each datum in the dataset has been changed by the dataset. A final classifier may then take the form of a threshold.
 
The method relies on the premise that synthetic data models are often at risk of overfitting to their training data, both recreating their training data well and leaving dissimilar artefacts in the minor changes that are introduced (often including some stage of stochastic noise injection).
 
While the stochastic stage in many synthetic data models can mean that any data may pass through the network with little change, it is unlikely to pass through the network repeatedly with only small changes unless it was overfit to during training, and artefacts detectable in the small changes may still be dissimilar when compared between examples in and out of the training set.
 
The attacker can measure differences between the dataset in their possession and the anonymised data returned by the black box by any given metric they wish to define. By training a regressor to predict these differences, as well as being able to measure them precisely, an attacker can start to differentiate between synthetic data close to input data that has occurred by chance versus that occurring due to synthetic data model overfitting - this would be when both the measured difference and regressor's prediction of difference are low.
 
Additionally, the regressor can be used independently against example synthetic data released by the researchers on its own - a low prediction of difference as the only indicator still raises the odds that a given datum was overfit to during training.
 
## Code Release
 
The current version of the code and outputs are under review.
 
Further development work is expected including:
Extensions to the suite for further attack scenarios
Further validation of the current tooling through tuning and example use-cases
Development of functionality within the suite to aid accuracy and understanding
 
# Contact
 
Please get in contact through analytics-unit@nhsx.nhs.uk if you would like to discuss this specific project or to discuss the generation of synthetic data in general. 
