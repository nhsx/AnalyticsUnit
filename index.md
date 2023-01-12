---
layout: base 
title: Technical Storage
description: Who we are
permalink: 
---

**NHSX is now part of the NHS Transformation Directorate** - Learn more at <https://www.nhsx.nhs.uk>

<h1>Welcome</h1>

The NHS England Digitial Analytics and Research Team *(formerly NHSX Analytics Unit)* sees open ways of working as pivotal to increasing innovation and efficiency in the NHS.  This site has been created so we can share some focussed technical thoughts and examples.  

Within the unit we have analysts, data engineers, data scientists, developers, economists, and evaluation specialists.   Here we will advertise public projects from all these disciplines as well as publishing thoughts on how healthcare analysts can interact with the open tools and data.

## Innovation Research Areas   

Our <a href="https://nhsx.github.io/AnalyticsUnit/assets/AnnualReport22_Final.pdf" target="_blank">DART Innovation Branch Annual Report 2022</a> describes our main activities over the last calendar year.

If we want to get the most value out of our data then we need to understand how we can access the data, what the content of the data is and what techniques can extract insights for different cases.  All three of these areas have significant challenges such as sharing sensitive data, representing complex information from multiple sources into a data asset that can be ingested and analysed, and demonstrating confidence and robustness in the methods applied. 

Our research aims to address some of these issues by building data foundations to enable innovation in the near future. The first of these foundations is to **increase the understanding of the appropriate representation of structured and unstructured data**.  When multiple points of healthcare data and/or different modalities of data are linked it becomes complex with both intra and inter correlations, unknown confounding variables and often poor quality.  The complexity often makes it impossible to deal with directly in an efficient manner and the variable relationships and quality make causal insights difficult to identify.  To deal with these issues we need to have methods for representing this data in appropriate formats which can then be analysed or used in a model.  We've started to explore this area through understanding the appropriate application of large-scale language models, exploring multi-modal representations of text and images together and graph representations of data to capture entity relationships rather than ordered correlations.

The second pillar is centred around our belief that unstructured data (especially text data) has huge unlocked potential for healthcare analysis.  A key blocker to using unstructured text data is the potential sensitivity within the data.  Often this is partially dealt with by anonymising for patient identifiable information but this can still leave content which is contextual or domain specific and therefore still disclosive.  We are therefore aiming to **highlight the privacy of unstructured data beyond PII** through understanding the problem and currently available options and then creating tool to calculate a privacy fingerprint for a data base or piece of text.  This fingerprint would be a structured way of addressing the risk of disclosure which could then be used in an IG process to understand what masking/anonymisation is required or what limited terms of use need to be applied to the data.  By having a tangible way of addressing this issue we aim to increase the sharing of these data with confidence. 

The third pillar relates to accessing through the **use of synthetic data and Privacy Enhancing Technologies (PETs)**.  This would aim to support the wider working in NHS England regarding secure data environments but focusses on quick access through leaving data at source and either creating non-disclosive versions or using methods which allow the model to be applied without the data ever being seen or disclosed outside of the secure data silo.  In this area we are aiming to create a tool to generate high fidelity private synthetic data that can include fairness and explainability; investigating the generation of patient pathways through an agent-based style simulation; exploring homomorphic encryption on two disparate secure data silos; and monitoring the current frameworks for federated learning.

our fourth research area is a common area for data science but still with large unmet need for healthcare - **increasing the available validation methods for model application**.  We have previously seen the value of having defined benchmarks and gold standard downstream tasks for evaluation and validation and we aim to investigate what currently available methods allow us to identify and discuss fairness across our different models.

The final pillar aims at **applying reproducible analysis** to our data.  Once the data is accessible, the data is in a useable format, there is a clear process for validating, then we need to be producing code which allows for reuse across the healthcare system. Here we are supporting reproducible analytical pipelines and open ways of working as well as creating reusable code bases for population health management analysis, forecasting and simulation published on Github.

Much of this work is progressed through our PHD Data Science Internship Scheme which also aims to increase our connections with academia and other research bodies. 
