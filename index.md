---
layout: base 
title: Technical Storage
description: Who we are
permalink: 
---

**NHSX is now part of the NHS Transformation Directorate** - Learn more at <https://www.nhsx.nhs.uk>

<h1>Welcome</h1>

The NHS England Digital Analytics and Research Team *(formerly NHSX Analytics Unit)* sees open ways of working as pivotal to increasing innovation and efficiency in the NHS.  This site has been created so we can share some focussed technical thoughts and examples.  

Within the team we have analysts, data engineers, data scientists, developers, economists, and evaluation specialists.   Here we will advertise public projects from all these disciplines as well as publishing thoughts on how healthcare analysts can interact with the open tools and data.

## Innovation Research Areas   

Our <a href="https://nhsx.github.io/AnalyticsUnit/assets/AnnualReport22_Final_120123.pdf" target="_blank">DART Innovation Branch Annual Report 2022</a> describes our main activities over the last calendar year.

To get the most value out of our data, we need to understand how to access the data, what the content of the data is, and what techniques can extract insights for different cases.  All three of these areas have significant challenges such as sharing sensitive data, representing complex information into a data asset that can be analysed, and demonstrating confidence and robustness in the methods applied.  Our research aims to address some of these issues by building data foundations to enable innovation in the near future. 

The first of these foundations is to **increase the understanding of the appropriate representation of structured and unstructured data**.  When multiple sources and modalities of data are linked the intra and inter correlations become complex with the additional issues of unknown confounding variables and often poor quality data.  The complexity often makes it impossible to identify efficiently the causal insights.  To deal with these issues we need to have methods for representing data in appropriate formats which can then be analysed and used in models.  We've started to explore this area through understanding the appropriate application of large-scale language models, exploring multi-modal representations of text and images, and graph representations of data to capture entity relationships rather than ordered correlations.

The second foundation is centred around our belief that unstructured data (especially text data) has huge, unlocked potential for healthcare analysis.  A key blocker to using unstructured text data is the potential sensitivity within the data.  Often this is partially dealt with by anonymising for patient identifiable information but this can still leave content which is disclosive as contextual or domain specific - see the [Functional Anonymisation Paper](https://eprints.soton.ac.uk/417832/1/Functional_Anonymisation_and_the_Data_Environment_Final.pdf) for a nice overview of challenges with anonymisation in general.  We are therefore aiming to **highlight the privacy of unstructured data beyond Patient Identifiable Information** through creating a tool to calculate the "privacy fingerprint" for a text data source.  This fingerprint would be a structured way of addressing the risk of disclosure which could then be used in an Information Governance process to understand what masking/anonymisation is required or what limited terms of use need to be applied to the data.  By having a tangible way of addressing this issue we aim to increase the sharing of these data with confidence. 

The third foundation relates to accessing through the **use of synthetic data and Privacy Enhancing Technologies (PETs)**.  This area aims to support the wider working in NHS England regarding secure data environments but currently focusses on quick access through leaving data at source and either creating non-disclosive versions or using methods which allow the model to be applied without the data ever being seen or disclosed outside of the secure data-owner silo.  In this area we are aiming to create a tool to generate high fidelity private synthetic data that can include fairness and explainability; investigating the generation of patient pathways through an agent-based style simulation; exploring homomorphic encryption; and monitoring the current frameworks for federated learning.

Our fourth foundation is a common area for data science but still with large unmet need for healthcare - **increasing the available validation methods for model application**.  We have previously seen the value of having defined benchmarks and gold standard downstream tasks for evaluation and validation and we aim to investigate what currently available methods allow us to identify and discuss fairness across our different models.

The final foundation aims at **applying reproducible analysis** to our data.  Once the data is accessible, the data is in a useable format, there is a clear process for validating, then we need to be producing code which allows for reuse across the healthcare system. Here we are supporting reproducible analytical pipelines and open ways of working as well as creating reusable code bases for population health management analysis, forecasting and simulation published on Github.

Much of this work is progressed through our [PHD Data Science Internship](https://nhsx.github.io/AnalyticsUnit/phdinterns.html) Scheme which also aims to increase our connections with academia and other research bodies. 
