---
layout: base
title: OpenSafely and NHSX - Learning from the first collaboration
permalink: synthetic.html
---

<h2> {{page.title}} </h2>
<h4> Feb-21 (covering work from Oct-20 till Jan-21) </h4>

The OpenSAFELY platform was created to support reproducible, privacy-first, best practice healthcare analytics for a wide range of users at the outset of the COVID-19 pandemic.

OpenSAFELY started as a collaboration between the DataLab at the University of Oxford, the EHR group at London School of Hygiene and Tropical Medicine, TPP and other electronic health record software companies and for most of 2020, the platform was under extremely fast development. As a consequence, close support from the core technical team was necessary and the user base was limited to members of the collaborative.

In October 2020, members of the NHSX Analytics Unit became the first external collaborators to work on the [OpenSAFELY](https://opensafely.org/) platform.  The objective was to learn from their experience and shape the next phase of the platform, as the platform opens up to a wider community.

This blog highlights what the NHSX team learned during the first three months of this onboarding exercise. 

## Interest/Motivation

At NHSX, we had several reasons to be intrigued by the OpenSAFELY platform.  The primary interest was to support analysis by NHS England and Improvement of Covid-19 in primary care records.  However, there is a wider strategic interest in the OpenSAFELY approach to sensitive data.   Finally, this was also an learning opportunity to work with an experienced team on a set of tools and a novel approach to securely handling healthcare data.  

## October: initial exploration

**Fast Start**: An excellent feature of the OpenSAFELY platform is that it's all coded in the open on Github and thus to dive into and explore the framework is as simple as being able to clone a github repo.   Additionally, the platform has been developed with the ability to generate some dummy data - each variable of interest is populated with fake data from user set distributions which contains no real patient information.  This means within a day of deciding we were going to investigate using OpenSAFELY I was able to have a version of the code and get some initial dummy outputs produced.   

*Hurdle: none*

*Learning: the power of building a framework with dummy data on a public facing repository*

**Documentation**: This was helped by the step-by-step technical documentation the Datalab team had made available, including not just how to use their framework, but also how to install any prerequisites.  The documentation at that time was based on a variety of Github repos and thus took a while to work out the reading order and find all the relevant materials.  As the OpenSAFELY framework has been developed at speed this means that the documentation was detailed in some places and non-existent in others. Since then the DataLab team, with NHSX help has established a new site to host all technical documentation in a single place and established a discussion forum on GitHub where users can ask questions or suggest improvements in documentation.

*Hurdle: Documentation stored across several github repos*

*Learning/Change: Documentation moved to mkdocs site and continues to be actively improved and developed.*

**Installation of development software**: At this point I’ll pause and note some of the technical setup required.  The reason for outlining this here is that unfortunately NHS analysts are often constrained in their IT, especially when it comes to using free and open source tools.  To run OpenSAFELY you need git, access to Github, python (+ R and STATA optionally), and to trial the server run, Docker Desktop.  A step by step guide to setting up and running your first study can be found here: [Getting Started guide](https://docs.opensafely.org/getting-started/)

*Hurdle: Full use of the OpenSAFELY platform requires access to tools that NHS analysts sometimes don’t have.*

*Learning/Change: NHSX has [endorsed the use of free and open source software](https://www.nhsx.nhs.uk/blogs/data-saves-lives-building-and-skilling-nhs-analytics-community/) in the NHS and we are preparing a report on the appropriate and secure way to implement free and open source software for NHS analysts to increase confidence around the use of these tools.*

## November: writing the first analysis

**Choosing a starter project**: Once onboarded, and when some dummy data had been successfully created, we moved to thinking about a demonstrative example.   Several were put forwards; vaccine eligibility seemed to be of most interest.  At that time the final JCVI categories hadn’t been decided and the Green Book section on Covid-19 was also yet to be published.  OpenSAFELY was in a great position to give a fast indication of the numbers involved and to highlight some of the potential inequalities that could be produced inadvertently.

*Hurdle: Choosing an initial use case that allows for learning but also fits into appropriate use of the data*

*Learning/Change: At first, keep the analysis simple with high level outputs in order to focus on understanding the framework rather than getting caught in information governance issues around complex analysis producing low numbers or disclosive outputs.*

**Working with Primary Care Data**: Data collected through electronic health recordscontains sensitive private information for everyone and thus, quite rightly, safeguarded in the NHS.  This means that even as an NHS analyst of six years I’d never had access to primary care records.  I, like many other potential users, have little experience of working with the specific primary care records and more importantly being aware of the coding intricacies involved.   This has in many ways been the steepest learning experience and one where we’ve had to heavily rely on the experience of the Datalab team for direction to help stop us from going down multiple dead ends.   

*Hurdle: Primary care coding requires a great deal of background knowledge*

*Learning/Change: The OpenSAFELY team created a [YouTube video](https://youtu.be/NEwSQ5-dWSg) to highlight some of the specific issues to be aware of when conducting analysis in OpenSAFELY*


## December: running the analysis on real data

**The right place to create a software repo**: I started out making a repository in my own github area, as to create one in the OpenSAFELY space would require membership, which would take time for approvals.   This worked well to begin with as I was able to develop the model and have full access to the repo.  However, we quickly hit various hurdles around easily testing our code which took a while to overcome. 

*Hurdle: Currently creating a project outside of OpenSAFELY Github causes unnecessary development friction* 

*Learning/Change: For the time being new projects should be created in the OpenSAFELY organisation from the start; at least until full “external repository” support is added to the platform.*

**Keeping the software up to date**: As the OpenSAFELY framework is developing at pace, keeping all the software required to develop code locally up to date is important.   It’s also important to keep abreast of the latest documentation.  Several times we hit problems that required several updates before we could work around them.

*Hurdle: Out of date code and understanding causing errors*

*Learning/Change: the Datalab team have made it easier to update local development software, but users also need to remember to take responsibility to keep it up-to-date as with all software in the NHS. There is a section on updating OpenSafely here: [OpenSAFELY CLI](https://docs.opensafely.org/en/latest/opensafely-cli/)*

**Unexpected Initial Outputs**: The first results to come out of our vaccine eligibility project included a variety of errors which hadn’t been picked up in local development, or the automated github action checks.  The OpenSAFELY privacy model means we couldn’t see the raw input data, so understanding the unexpected errors was difficult.  As a result the team developed a “cohort reporter” function to report non-disclosive, descriptive statistics for the raw data.  There are also plans to improve the accuracy of the dummy data that researchers get access to during development.

*Hurdle: The OpenSAFELY privacy model can make debugging errors difficult.*

*Learning/Change: Use of the cohort reporter function helps, and will be incorporated by default into all new studies in due course.  More realistic dummy data could make it possible to avoid any debugging against live data. Additionally, unit tests with non-sensitive outputs are useful.* 

## First Outputs and Publication

Process for releasing outputs: Whilst the framework is open, the data and results are closely monitored and checked to ensure any data released are appropriate.  This process requires a Datalab colleague (or someone with equivalent access rights) to check the disclosiveness of the results before releasing it to the end user.  As analysis can be quite iterative depending on initial results this process can cause delays and be burdensome on the OpenSAFELY developers.  

*Hurdle: Burdensome release process*

*Learning/Change: the Datalab is trialling a new release protocol whereby redaction happens to a predictable, weekly schedule.  They are also training up new staff in redaction skills to ensure the workload and expertise are shared more widely.*

## Conclusion

Our work has been published [on the OpenSAFELY github account](https://github.com/opensafely/OS_OC_v001-research);  it is published as a record but should not be used for onward development, decision making or analysis. This work was superseded by the "[SARS-CoV2 (COVID-19) Vaccine Uptake Reporting Specification](https://github.com/opensafely/primis-covid-vacc-uptake-spec)", for which a report has since been [pre-printed](https://doi.org/10.1101/2021.01.25.21250356).

We are continuing to work with the Datalab team on OpenSAFELY across a variety of Covid-19 projects. Our main focus is to increase the use of OpenSAFELY across NHSX and NHS England and Improvement.
