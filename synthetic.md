---
layout: base
title: Synthetic Data in Health Overview
permalink: synthetic.html
---

<h2> {{page.title}} </h2>

*Updated December 2021*

The analytics team in NHSX is currently conducting research into best practice and examples for generating synthetic healthcare data for the purpose of enabling greater data sharing across the system.   This work will progress through our PhD internship scheme as well as through collaborating and commissioning small proof of concepts to create shareable tools and guidance.  Our aim is to make this work open through our github account and the NHSX website.   

This thought stream is focussed on the application of synthetic data in healthcare and targeted at analysts in the NHS considering if, and how to implement a synthetic data generation tool.

There are many articles online introducing synthetic data which should be researched for wider context first.  One really good general introduction to synthetic is the [ONS methodology working paper series number 16 - Synthetic data pilot](https://www.ons.gov.uk/methodology/methodologicalpublications/generalmethodology/onsworkingpaperseries/onsmethodologyworkingpaperseriesnumber16syntheticdatapilot).  I would also recommend spending some time looking through the resources and examples on the [synthetic data vault](https://sdv.dev/) project.

In health care, synthetic data has the potential to overcome many data access issues inherent when using personal data.  When created with the required level of privacy, it can enable research of restricted datasets, proof of concepts for analysis and tools, end to end software development, and vendor evaluations. 

However, there exists a significant disconnect between research and practical implementation/application of techniques for generating useable synthetic data.  The NHS currently needs robust processes, guidance and examples of how to create, assess and use synthetic data in a way which ensures complete privacy of the sensitive data being simulated.  

Often, the focus is on creating high fidelity datasets (where the generated synthetic data contains a high degree of the information present in the ground truth data) which in my experience often end up requiring specific data sharing agreements to be used and thus can’t be made widely available.  Thus, there are two considerations which may save a lot of time and effort if address right at the start:

* High-fidelity doesn’t always suit the use-case  - Many use-cases in the NHS only require low to medium fidelity data in order to support innovation and help knowledge share but get caught in the trap of chasing high-fidelity data.   
* Specific research may be more suited to other access routes - Research cases which require high-fidelity cuts of the ground truth data may be better suited to remote analysis or a trusted research environment rather than transferable synthetic datasets.  

This thought stream attempts to set out the current status of synthetic data in healthcare and highlight the challenges that need to be addressed in order to increase the value and usage of synthetic data in the NHS.
 
<hr>
<br>

## Describing the problem, fidelity and technique

Generally, there are two branches of synthetic data generation problem:

* Applying Learnt Relationships from Raw Data - A real data set exists and can be mined in a secure location. The learning from this is then used to build models that contain key insights without any disclosive information. These models are then sampled from to create a new synthetic database.
* Creating From Scratch - Through setting known/expert opinion based relationships, data is created from scratch. The resulting database is then checked for consistency against any known similar data.

Generally, when applying learnt relationships from raw data, the final product can have a very high level of quality and thus the main focus of the work switches to be on privacy and ensuring that there is no information leakage.  Whereas, creating from scratch is much easier to ensure the privacy is absolute and so the focus now needs to be on improving the quality through improving the implemented intelligence. 

It is useful to define and talk about the fidelity the project is aiming at from the beginning.  There is a spectrum of synthetic data which can be generated based on its fidelity (i.e. how much of the raw data relationships have been maintained in the generated data).  This spectrum is best described in the “Synthetic dataset spectrum” of the ONS working paper mentioned above.
<br>

### Techniques 

There are many current active areas of research for synthetic generation techniques including (authors categorisation): 

1. Data Erosion (not truly synthetic data)
    1. Auto Anonymisation
    2. Obfuscation
2. Statistical/Probabilistic models
    1. Sampling from independent marginals and probabilistic fitting
    2. Chi-Squared calculation of joint probabilities
    3. Bayesian Network calculation of joint probabilities
3. Simulations
    1. Use of clinical practice guidelines (CPGs) or clinical pathways
    2. Agent based simulations 
4. Perturbations of the manifold
    1. Synthetic Minority Over-Sampling Technique (SMOTE)
    2. Variational Autoencoders (VAEs)
5. Iterative Comparisons
    1. Generative adversarial neural networks (GANs) - in particular the PATE-GAN and CT-GAN.

NHSX are currently reviewing the use of variational autoencoders combined with differential privacy as a recommended solution with appropriate tests - see [Link](https://github.com/nhsx/Synthetic-Data-Exploration-VAE) for recent updates.

[A Review of Anonymization for Healthcare Data](https://arxiv.org/pdf/2104.06523.pdf) gives a good summary of this area defining the anonymisation through either k-anonymity or l-diversity or t-closeness and the discussing techniques such as: slicing, generalization, suppression, perturbation, bucketization, and microaggregation. The paper also gives some example tools for supporting anonymisation in healthcare (Section 7)

This paper includes a good overview of a variety of probabilistic and generative techniques: [Generation and evaluation of synthetic patient data](https://bmcmedresmethodol.biomedcentral.com/articles/10.1186/s12874-020-00977-1)

This ONS working paper is a good example of implementing GANs, VAEs and SMOTE: [Synthetic data for public good](https://datasciencecampus.ons.gov.uk/projects/synthetic-data-for-public-good/).  This [BAE systems paper](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/908629/ASC_0259_Study3_FinalReport_v1_2.pdf) also has a good literature review for applied GANs.
 
<hr>
<br>

## Specifying the Problem

At this point it’s useful to introduce the ideas of Utility, Quality and Privacy for Synthetic data as these will rule the implementation and final decision regarding using the product.   
**Utility** - is the data fit for it’s defined use
**Quality** - is the data a good enough representation of reality
**Privacy** - does the synthetic data leak any sensitive information about the source data

Essentially, these three aspects need to be well defined at the start of the work and then balanced to give a series of tests that can be used against the final output.   The balance depends on the specific use-case and source data.

A good example of creating and evaluating synthetic data for healthcare is [Generating and Evaluating Synthetic UK Primary Care Data: Preserving Data Utility & Patient Privacy](https://ieeexplore.ieee.org/document/8787436)
<br>

### Utility
Firstly, It is not currently advised to create generic synthetic healthcare data openly as the privacy constraints are likely to reduce the quality down to an useable state.  

Thus, to define the utility we should start with a specific use case and a specific data source.  It’s useful to ask:

* What decision taken, insight, or other use is expected off the back of the produced synthetic data?
* What level of synthetic data would do the minimum required and what level would be nice to have? For Example:
    * If using the data as an example extract for app development the quality does not need to be high but the privacy needs to be very high.  Thus a data model could be used on a reduced data set which loses some secondary relationships in the data but ensures complete privacy;
    * Whereas, a user case which relies on investigating a demographic dependence on a health condition in a research context may need a much higher quality extract and more granular data (including geographical data) and thus relies on a raw data erosion or state of the art technique with appropriate data sharing agreement.	
* Which data types are included in the source (demographic, health, time, transactional, longitudinal, geographical, …) and which are required for the use-case?
* How much would the use-case be affected by removing more variables?

At this point it is useful to again consider if synthetic data is the right solution or whether pushing for an alternative access to the real data will be more appropriate.  
<br>

### Quality
The quality of the data comes down to how much the synthetic data contains the ground truth contained in the source data.   The quality required depends on the use-case but we also need to be able to put some form of a value on the quality of the synthetic data produced to support appropriate use.

There are a few tests available for testing how much of the original value remains in the synthetic extract, although none are perfect:
* **Profile Comparison** and frequency statistics of combinations within the data (e.g. Pearson’s correlations and similarity matrices)
* **Statistical Distribtuion Comparisons** such as Gaussian mixture log liklihood; Kolmogoroc-Smirnov test for comparing the cumulative distribution function of two continuous variables and the chi-squared test for comparing discrete distributions.  
* **Statistical Outcome Comparisons** such as [Voas Williamson statistic](https://onlinelibrary.wiley.com/doi/abs/10.1002/1099-1220%28200009/10%296%3A5%3C349%3A%3AAID-IJPG196%3E3.0.CO%3B2-5) (measures variance versus degrees of freedom for various combinations within the data); and use of [propensity scores](https://journalprivacyconfidentiality.org/index.php/jpc/article/view/568) (This paper demonstrates the equivalency of these two approaches [Guidelines for Producing Useful Synthetic Data](https://arxiv.org/pdf/1712.04078.pdf)).  Kullback-Leiber divergenece, Gower distance and the Wasserstein metric can all be used to investigate an aggregate difference between the synthetic and ground truth data.
* **Off-Manifold and Latent Space checks** - consider using principal component analysis (PCA) or [t-distributed stochastic neighbor embedding](https://distill.pub/2016/misread-tsne/) (t-SNE) to visualise any new variable combinations created 
* **End Use Case Comparisons** - Running two statistical/machine learning models related to the end use-case on the raw and synthetic data to compare the resultant summary statistics 
* **Detection Metrics** - Running a classifer (e.g. Logistic of SVM) on both the synthetic and ground truth data to see how accurately this can distinguish the difference. 

The Synthetic Data Vault project has a section on [Evaluation Framework](https://sdv.dev/SDV/user_guides/evaluation/evaluation_framework.html) built in python which includes a small suite of functions which can be viewed separately or aggregated to give an overall score for the synthetic data.  These functions include some of the statistical tests above as well as likelihood and detection metrics which compare the real and synthetic data when probabilistic and machine learning models are applied.  This implementation is available for single data tables, multi table situations and time series data. 

The previously mentioned [BAE systems paper](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/908629/ASC_0259_Study3_FinalReport_v1_2.pdf) creates a framework with a range of defined metrics dependent on the data being tested as well as testing DP-GANs, SDV and Presidio as 

We are currently developing a generic testing notebook that applies many of these algorithms mostly using the SDV implmentations through python. 
<br>

### Privacy
By far the most challenging area but also the most important is to have a way of evaluating the privacy needed and the privacy contained within the synthetic data.

When thinking about the level of privacy needed we should consider:
* Who will have access to the final data?  What other information will they have access to?
* Who would be affected by a privacy leak (consider: personnel, financial, reputational)?
* What information could an adversary obtain through a privacy leak?

In most cases the privacy will need to be set exceptionally high for health data which is why it’s sometimes easier to go for a “creating from scratch” method and sacrifice some quality!

It can be useful to consider some possible data attacks at this point.  Some examples of anonymization attacks can be found in [Review of anonymization for healthcare](https://arxiv.org/pdf/2104.06523.pdf) paper - section 4 and 5:
* **Background knowledge attacks:** If the adversary already has some knowledge of an individual they are trying to find in the data (e.g. heard that a celebrity or family member had been to a certain hospital on a certain data) then they might be able to use this information to reconstruct the identifiable information within the dataset. 
* **Linkage attacks:** When an adversary has access to other sources of information which are linkable to the data in question.  This linkage can increase their knowledge of an individual in a way which allows for identifiable information to be reconstructed. 
* **Attribute disclosure attacks:** When an adversary infers knowledge about the specifics of a sensitive attribute such as the exact medical condition of a group of patients.  
* **Membership disclosure attacks:** When the adversary wants to know if a specific individual is in (or out) or a specific group.

Some tests for privacy include:
* **Collision testing:** Like for like comparison of raw and synthetic to establish if any record is the same.  However, if we ensure that no record is in the raw data then an adversary can actually use this information to reconstruct some sensitive information. 
* **Uniqueness:** Combinations of values within the data (similar to the l-diversity model).  Some algorithms may force unique records to re-create the outlier!
* **Can I find me?:** Practical test to see how much information a user would need to find a known subject 

Although all these tests are useful, none give a definitive metric which can be tested against.  **Differential Privacy** is the most established mathematical way of defining some level of privacy in the data.  This is a large field which won’t be covered here, but instead we refer the reader to an excellent set of resources and active research programme at the van der schaar-lab.  A summary article on their synthetic data thoughts can be found [here](https://www.vanderschaar-lab.com/synthetic-data-breaking-the-data-logjam-in-machine-learning-for-healthcare/).  We are currently reseaching the application of differential privacy using the established Stochastic gradient descent differential privacy and the more recent PATE (Private Aggregation of Teacher Ensembles) implementation. 

Alongside this research we are looking into building a synthetic data adversarial suite which would quantify the privacy through simulated model inference attacks using shadow models.   

[SmartNoise](https://github.com/opendp/smartnoise-core) - A pluggable open source library of differentially private algorithms and mechanisms for releasing privacy preserving queries and statistics, as well as APIs for defining an analysis and a validator for evaluating these analyses and composing the total privacy loss on a dataset.

<hr>
<br>

## Longitudinal, text and imaging synthetic data

Most of this thought stream has been addressing tabular electronic health records.  Whilst much of this thinking can be used to other data types, there are a few additional points to consider if trying to generate more complex data.
<br>

### Longitudinal data
A key use-case for healthcare would be to create patient pathways and other longitudinal data which would support understanding how systems work together as well as allowing outcomes analysis.  These data have the added level of complexity that we are no longer just interested in the static relationships between variables but now the time-dependent relationships (i.e. does a outpatient appointment booked 12 days after referral impact the outcome more than a 26 day waiting period and thus how do we include this time-dependent nature into out synthetic model whilst preserving privacy).  Longitudinal data generated from  source data will also have considerable privacy concerns as the time component will make any record very granular and thus easily identifiable.  We are currently investigating a simulation approach for longitudinal data through the SynPath project mentioned in the case studies below.    
<br>

### Imaging data
Whilst the field of generating synthetic images is booming (especially when using GANs), the issue we have in healthcare is the availability of the training data for these models.  Not only do we need a large amount of data but that data also needs to capture the range of issues that are brought about due to different imaging equipment and data recording practices across the NHS.  NHSX is investigating this area through the [National COVID-19 Chest Image Database (NCCID) — National COVID-19 Chest Image Database documentation](https://nhsx.github.io/covid-chest-imaging-database/).
<br>

### Text Data
Healthcare has a huge amount of free-text and structured-text data available in it’s records which is often vastly underused due to the privacy required.  Thus, this area is ripe for synthetic data generation and yet suffers from the issue of training data again.  There isn’t currently a source of NHS-specific text data which could be used to develop the algorithms needed for synthetic text generation.  NHSX is investigating this area through the [NHS Corpus project](https://github.com/nhsx/language-corpus-tools). 

<hr>
<br>

## Known Projects and Case Studies
Please see the contact us section to let us know of further work
<br>

### Datasets 
[The Simulacrum - healthdatainsight.org.uk](https://healthdatainsight.org.uk/project/the-simulacrum/)

Fidelity = Medium

Technique = Probabilistic Model - Chi-Squared

The Simulacrum is a dataset that contains artificial patient-like cancer data to help researchers gain insights. The Simulacrum imitates some of the data held securely by the Public Health England’s National Cancer Registration and Analysis Service. The data is synthetic and does not contain any information about real patients. It is free to use and allows anyone who wants to use record-level cancer data to do so, safe in the knowledge that while the data feels like the real thing, there is no danger of breaching patient confidentiality. 

[Synthetic data | CPRD](https://www.cprd.com/content/synthetic-data)

Fidelity = high

Technique = Probabilistic Model - Bayesian Network

CPRD has generated high-fidelity synthetic datasets using a synthetic data generation and evaluation framework 

[SynAE](https://data.england.nhs.uk/dataset/a-e-synthetic-data)

Fidelity = Medium

Technique = Probabilistic Model - Bayesian Network

The synthetic A&E extract, “SynAE”, is the result of an NHS England pilot project to widen data sharing without loss of privacy for patients.

[64 Generating synthetic electronic patient records](https://adc.bmj.com/content/104/Suppl_4/A25.3)

Fidelity = High

Technique = Generative algorithms

The GOSH DRE team have worked with collaborators in UCL and NHS Digital to develop generative statistical and deep learning (AI) models that learn the structure and statistical properties of EPR data. These models have the capability to generate synthetic EPR data without reproducing individual patient records. To facilitate this work, de-identified EPR data from all patients treated at GOSH between January 2016 and January 2019 were extracted from the DRE data lake and modelled using the PyTorch, TensorFlow, and Scikit learn Python libraries.

[MIMIC-III Clinical Database v1.4](https://physionet.org/content/mimiciii/1.4/)

Fidelity = High

Technique = Data Erosion

MIMIC-III is a large, freely-available database comprising deidentified health-related data associated with over forty thousand patients who stayed in critical care units of the Beth Israel Deaconess Medical Center between 2001 and 2012. The database includes information such as demographics, vital sign measurements made at the bedside (~1 data point per hour), laboratory test results, procedures, medications, caregiver notes, imaging reports, and mortality (including post-hospital discharge).
<br>

### Tools

[SynthVAE](https://github.com/nhsx/SynthVAE)

Fidelity = Medium/High

Technique = Perturbations of the manifold - Variational AutoEncoder with Differential Privacy

An NHSX Data Science Intern Project focussed on developing an open source tool for generating medium fidelity data with high privacy.  USes the PyTorch implmentation of SGD-DP.  

[Synthetic LS data :: CALLS-HUB](https://calls.ac.uk/guides-resources/synthetic-ls-data/)

Fidelity = Medium

Technique = Probabilistic Model - Sampling from independent marginals

The datasets contain synthetic data based on the ONS Longitudinal Study for England and Wales (ONS LS), the Scottish Longitudinal Study (SLS) and the Northern Ireland Longitudinal Study (NILS) and do not contain real ONS LS, SLS or NILS data. The synthetic datasets have been developed for teaching purposes and for researchers to familiarise themselves with longitudinal data..  Uses synthpop and proportional fitting algorithm to generate the data.

[synthetichealth/synthea: Synthetic Patient Population Simulator](https://github.com/synthetichealth/synthea)

Fidelity = Medium

Technique = Simulation - Use of clinical practice guidelines (CPGs) or clinical pathways

SyntheaTM is a synthetic patient generator that models the medical history of synthetic patients. Our mission is to output high-quality synthetic, realistic but not real, patient data and associated health records covering every aspect of healthcare. The resulting data is free from cost, privacy, and security restrictions.  There is a international setup repo with an example for shrewsbury. [Link](https://github.com/synthetichealth/synthea/wiki/Other-Areas#abridged-example-for-shrewsbury-shropshire-united-kingdom)


[synthetichealth/syntheticmass](https://github.com/synthetichealth/syntheticmass)

Fidelity = Medium

Technique = Probabilistic Model - Sampling from independent marginals

The synthetic population aims to statistically mirrors the real population in terms of demographics, disease burden, vaccinations, medical visits, and social determinants. SyntheticMass establishes a risk-free environment for experimenting with large-scale HL7 FHIR® data.

[SynSys: A Synthetic Data Generation System for Healthcare Applications](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6427177/)

Fidelity = Medium

Technique = Probabilistic Model - Markov models and Regressions to generate independent marginals.

A machine learning-based synthetic data generation method. We use this method to generate synthetic time series data that is composed of nested sequences using hidden Markov models and regression models which are initially trained on real datasets. We test our synthetic data generation technique on a real annotated smart home dataset. We use time series distance measures as a baseline to determine how realistic the generated data is compared to real data and demonstrate that SynSys produces more realistic data in terms of distance compared to random data generation, data from another home, and data from another time period.

[google/simhospital](https://github.com/google/simhospital)

Fidelity = Medium - depends on the details in the defined pathways

Technique = Simulation - Use of clinical practice guidelines (CPGs) or clinical pathways

The basic behavior of Simulated Hospital can be summarized as follows:
* Simulated Hospital creates patients at a configurable rate.
* When Simulated Hospital creates a patient, it associates the patient with a pathway.
* A pathway models the events that will occur to the patient.
* Simulated Hospital runs events when they are due, in real time.
* When events run, they generate HL7v2 messages.

[SDS-Architect/Synthetic_Data_System: The Alpha Build of the SDS for ideas gathering, testing and commentary](https://github.com/SDS-Architect/Synthetic_Data_System)

Fidelity = Medium

Technique = Probabilistic Model - Sampling from independent marginals

Healthcare specific generator - uses a mixture of traditional probability sampling, machine learning and noise injection safety methods.

[The Synthetic Data Vault. Put synthetic data to work!](https://sdv.dev/)

Fidelity = Medium

Technique = Range

A number of open-source libraries, tutorials and other useful resources

[nhsx/SynPath: Proof Of Concept - Open Patient Pathway Generator using and an agent based approach](https://github.com/nhsx/SynPath)

Fidelity = Medium

Technique = Agent Based Simulation

*Currently at Proof Of Concept Stage*
Open Patient Pathway Generator using and an agent based approach

[BorealisAI/private-data-generation: A toolbox for differentially private data generation](https://github.com/BorealisAI/private-data-generation)

Fidelity = High

Technique = Range of Generative techniques

Users can benchmark the models on the existing datasets or feed a new sensitive dataset as an input and get a synthetic dataset as the output which can be distributed to third parties with strong differential privacy guarantees.

<hr>
<br>

## Off the shelf solutions in R and Python
There are a large range of libraries/packages available which can implement some of the above techniques in a generalised way.  This are usually to be used for quick implementations but require robust testing before release of the produced data.   
<br>

### R
[Synthpop](https://www.r-bloggers.com/generating-synthetic-data-sets-with-synthpop-in-r/)
An initial variable is synthesised using random sampling with replacement before classification and regression trees are applied to generate the rest of the synthetic dataset. Variables are synthesised sequentially, preserving their conditional distributions. Different regression methods (such as linear and logistic) are offered.

[SimPop](https://www.jstatsoft.org/article/view/v079i10)
SimPop creates household structures from observed data (so not as to create unobserved, unrealistic households) via resampling. Then categorical variables are generated. These are allowed to have non-observed relationships to households, as the sample is unlikely to capture all possible (reasonable) relationships in the population. Users can also take into account within-household relationships when simulating categorical variables. Finally, continuous variables are generated. 

[Sms](https://www.jstatsoft.org/article/view/v068i02)
Individual data are randomly (with replacement) selected from a database and evaluated against the profile of a geographical area iteratively. This replaces individual records until small area constraints are satisfied. This procedure produces microdata for regions based on observed data and census macro data. The more overlap between dataset and census variables, the better fit can be achieved. 
<br>

### Python
 
[SDV](https://pypi.org/project/sdv/)
Already mentioned is the synthetic data vault which provide their code openly through github but have also released a python package. 

[Synthetic](https://pypi.org/project/synthetic/)
Produced off the back of a nature paper, this project attempts to create a generalised machine learning algorithm which picks the best decentralised network growth models from empirical data.

[Faker](https://github.com/joke2k/faker)
Faker is a Python package that generates fake data for you. This doesn’t claim to be synthetic and the name makes it clear that this is fake data but still a useful tool to be aware of. 

Finally, here is an [Article](https://towardsdatascience.com/synthetic-data-generation-a-must-have-skill-for-new-data-scientists-915896c0c1ae) covering use of SymPy and Pydbgen. 

<hr>
<br>

## Get in Contact
This thought stream does not get anywhere close to covering the area of synthetic data adequately but aims to give context and resources for synthetic projects.  We’d be very interested to hear about other examples, thoughts and suggestions to be included but also if there are projects where NHSX could support we’d be interested to discuss.  

Contact analytics-unit@nhsx.nhs.uk if you want to contribute or chat. 