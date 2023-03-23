---
layout: base
title: NHS Language Corpus - Discovery
permalink: languagecorpusdiscovery.html
---

<h2> {{page.title}} </h2>

**Date:** Easter 2022

**Post author:** Dan Schofield - Senior Data Scientist, NHS Transformation Directorate.

**GitHub repository:** <https://github.com/nhsx/language-corpus-tools>

*This blog discusses our discovery project on building a language corpus with a focus on the NHS, looking at useful open source tools which can help with ingestion, enrichment, and sharing of the text data.  The project looks to help address a current lack of NHS-specific text resources available for supporting development of Natural Language Processing (NLP) tools through various stages, such as training, benchmarking, and evaluation.*

Utilising free-text as a data source in both clinical and non-clinical settings in the NHS comes with many challenges, but it can contain information which is not available elsewhere, and thus helping develop NLP techniques to harness this information at scale is highly desirable.

It is also known that language tasks in various settings require different labelled training data or fine-tuned solutions: Mental Health notes are often long form and very descriptive, the NHS.UK website uses accessible language, Electronic Health Record entries may be of variable length depending on speciality and contain local technical abbreviations, and feedback can often contain a mix of clinical and colloquial terms.  

On the other hand, many modern large-scale language models (see [BERT-101](https://huggingface.co/blog/bert-101) for an explaination of BERT) have gained success from initially being exposed to large amounts of unlabelled data with various styles and sources, and then fine-tuned to solve one (or more) domain specific NLP tasks on much smaller amounts of labelled data.

With this in mind, in March 2021 we decided to run a short four-week discovery project, looking at how to build an NHS-focussed collection of texts and explore some of the considerations in doing so, which could help developers build better NLP tools for the healthcare system.

## The Vision

The initial vision around the [NHS Language Corpus](https://nhsx.github.io/nhsx-internship-projects/nhs-language-corpus/) was broken down into four high-level goals:

1. **Open** - it is important to make this resource easily available and accessible to innovators and researchers in NLP healthcare space

2. **Representative** - it would need to contains a range of sources and capture the variability in language used in a given setting

3. **Extensible** - it should be designed such that it can be used to collect a dataset that has a wide coverage as well as a large number of examples over time

4. **Useful** - it must be sure to add to the currently available resources constructively

## Testing the Water… Starting Small

During the discovery, we started by collecting together some user stories that reflected the different viewpoints of those likely to interact with the corpus.  These fit into groups like those responsible for the infrastructure of the corpus, those involved in the enrichment activities on the collected texts, and those looking to use the outputs.  

An example generated user story was “As a data scientist, I want to be able to integrate different NLP approaches or engines into the pipeline, so that I can compare across different techniques and evaluate them robustly” which focuses on an internal team member, and their need for flexibility in the solution.  

Many of these user stories helped shape how we broke up the time available to us during the project.  From this, we then broke the initial framework into three sections: ingest, enrich, and share.

### Ingest

The need to build out a corpus from different sources led us initially to look at those which were available in open forums on the web, or through accessible APIs due to the short timeframes of the project.  We decided on [Scrapy](https://scrapy.org/) as a framework which allowed us to automate the collection and was extensible and flexible.

We collected content from the following areas:
- NHS.UK Conditions pages e.g. <https://www.nhs.uk/conditions/allergies/>
- NHS Data Dictionary Definitions e.g. <https://www.datadictionary.nhs.uk/attributes/organisation_site_name.html>
- NHS Trust News or Blogs
- NHS Feedback Data e.g. <https://www.nhs.uk/services/hospital/barnsley-hospital/X539/ratings-and-reviews>

We would look to extend these in future iterations of the project, with additional considerations around ingestion of data from sources that are not open, such as the introduction of user credentials to control access or robust de-identification where required.

### Enrich

As well as collecting together various data sources, we recognised the need for enrichment of the texts through labelling, to help with training of downstream tasks.  This could be to manually or automatically perform entity recognition, and then to link to concepts in clinical terminologies such as SNOMED-CT, or classification codes in ICD-10 or OPCS-4, which can be accessed via [TRUD](https://isd.digital.nhs.uk/trud/)). Other enrichment could include the need to label other attributes of the texts like sentiment, the presence of negation, perform coreference resolution, or look into relation extraction.

We were keen to explore two avenues here, frameworks that allow for human annotation, but also those that can perform or integrate some automated annotation as well.  For this we identified a selection of three open source tools, two of which had a biomedical/healthcare focus, and the other which was a more general tool.

- **brat** (<https://github.com/nlplab/brat>) - “brat (brat rapid annotation tool) aims to provide an intuitive and fast way to create text-bound and relational annotations.  It is based on the [stav visualiser](https://github.com/nlplab/stav/) which was originally made in order to visualise [BioNLP'11 Shared Task data](https://sites.google.com/site/bionlpst/)”.

- **doccano** (<https://github.com/doccano/doccano>) - “doccano is an open source text annotation tool for humans. It provides annotation features for text classification, sequence labelling and sequence-to-sequence tasks. So, you can create labelled data for sentiment analysis, named entity recognition, text summarization and so on. Just create a project, upload data and start annotating. You can build a dataset in hours”.  This tool is still under active development.

- **MedCAT Trainer** (<https://github.com/CogStack/MedCATtrainer>) - “MedCAT Trainer is an interface for building, improving and customising a given Named Entity Recognition and Linking (NER+L) model ([MedCAT - Medical Concept Annotation Tool](https://github.com/CogStack/MedCAT)) for biomedical domain text”.  It is part of the [CogStack](https://github.com/CogStack) framework and is still under active development.

Each framework was set up to allow for manual annotation of the collected data sources, further offering different amounts of flexibility in areas such as cross-document labelling and introducing automated labelling models, but no single setup was appropriate for all of our use-cases, and each would require some further customisation or development.  

Positively, for our use-case, all of the above frameworks did allow us to enrich our ingested data in various ways, and through our deployment setup we were able to compare the different workflows of using each.  This set the foundations for a number of future projects exploring and enriching the ingested data, some of which we highlight later.

*N.B. After the initial discovery project concluded, we became aware of another framework with healthcare focus which would have been useful to add as another example to our “Enrich” pipeline stage.  It looks to introduce active learning techniques into the annotation cycle to help reduce the need for manual labelling further. The framework is called [markup](https://github.com/SwanseaUniversityMedical/markup) and has an online demo available [here](https://getmarkup.com/demo).*

### Share

One key goal of the corpus highlighted above is that it will be as open as possible to users such that they can use it in the development of new NLP tools.  This led us to consider a number of possible approaches for sharing the corpus with users.

The use of a public cloud storage would allow for easy access for users, flexibility in terms of storage size allowances, and alleviate concerns over maintenance.  It would also provide us with challenges around controlling access, versioning of the corpus as it grows or changes over time, and long-term cost considerations.

Some popular model sharing and NLP frameworks have begun offering hosted sharing of datasets and metadata through their managed platforms (see for example [HuggingFace Datasets and Hub](https://huggingface.co/docs/datasets/index)).  This approach would again remove concern around ongoing maintenance and support, but does limit control over the access to the corpus, as well as security considerations of where the data will be stored.

Another sharing approach would be to consider building out a credentialed service like that of [PhysioNet](https://physionet.org/).  This service (where datasets like [MIMIC-III](https://physionet.org/content/mimiciii/1.4/) are hosted) requires a user to sign up for an account, a data access agreement to be signed, associated training to be completed, and sign-off from the data owners for each dataset project application (containing a short description of the project).  This option would require much more support, but gives a robust way to control access to the data, whilst keeping to a minimum the number of hoops a user must jump through to gain access.

## Next Steps

Much of what we have described above is just scratching the surface of available data sources, open tooling, and approaches to managing access, but aims to give an idea of the types of considerations which would be required when trying to build an NHS-specific corpus of different text sources.

For us, this initial discovery gave us a framework to compare these different tools and will feed into our thinking going forward for the wider project, whilst also providing a starting point for other projects exploring and evaluating emerging techniques on NHS text data.

Lastly, we highlight some related projects we are undertaking which may be of interest: 

- A project over summer 2021 with a visiting Data Science Master’s degree student, exploring using open source frameworks to build pipelines which automatically label NHS.UK conditions pages collected as part of this discovery to different clinical coding ontologies, and identifying tasks for evaluating the success of these tools.

- An on-going internal exploration project investigating using modern large-scale language models (such as [GPT-2](https://openai.com/blog/better-language-models/), [GPT-Neo](https://github.com/EleutherAI/gpt-neo), or [T0](https://github.com/bigscience-workshop/t-zero)) to generate synthetic texts with relevant healthcare domain content, using approaches like fine-tuning, [prompting](https://arxiv.org/abs/2107.13586), and controlled generation (like those described in [Controllable Neural Text Generation - Lil'Log](https://lilianweng.github.io/posts/2021-01-02-controllable-text-generation/)).  We will also be considering how to make sure any generated synthetic text is protected from any training data leakage which could violate privacy.
