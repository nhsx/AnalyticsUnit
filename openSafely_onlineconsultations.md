---
layout: base
title: Increasing understanding of online consultation coding activity through OpenSAFELY (onboarding pilot project)
permalink: openSafely_onlineconsultations.html
---

<h2> {{page.title}} </h2>

**Date:** September 2021 (Covering work from Jan-21 till Jun-21)

**Post author:** Martina Fonseca - Senior Analyst, NHSX

**Research team:** NHSX Analytics Unit, NHSE/I Digital First Primary Care - in collaboration with OpenSAFELY

**Git repository:** [opensafely/OS_OC_v001-research](https://github.com/opensafely/OS_OC_v001-research) (to be made open)

*note 1: this study and its outputs have been approved by NHSE/I as meeting the stated project purpose - including open release* 

*note 2: as the open Safely framework is continually developing, some of the technical detail and issues discussed here may be out of date*

*note 3: the work carried out was a collaboration between NHSX AU, NHSE/I Digital First Primary Care and OpenSAFELY but the narrative in this piece is personal rather than organisational*

## OpenSAFELY

[OpenSAFELY](https://www.opensafely.org/about/) is a new secure analytics platform for electronic health records (EHR) in the NHS. The platform, developed by the Data Lab at the U. Oxford and partners at the start of the pandemic, uses a novel approach for enhanced security and timely data access that means there is no need to migrate outside of, or view at an individual record level, large volumes of disclosive pseudonymised patient data hosted in secure environments managed by the EHR software companies (e.g. TPP, EMIS); instead, it relies on trusted analysts to run arms-length computations and analysis on near real-time on records still held inside these secure environments.

Late last year, NHSX and the Analytics Unit were given the opportunity to become the first external collaborators to work on the OpenSAFELY platform. Our lead data scientist Jonny Pearson wrote about the [journey and main learnings from this first collaboration](https://nhsx.github.io/AnalyticsUnit/openSafely_learning.html).

Earlier in the year, we were given the opportunity to take part in the **[OpenSAFELY pilot for onboarding external approved users and researchers](https://www.opensafely.org/onboarding-new-users/)**. To continue the shared learning while also supporting the wider digital transformation agenda that NHSX is leading, we made use of OpenSAFELY to **better understand the implementation and adoption of online consultations (OC) in primary care**, in particular its coded activity in primary care records.
This piece outlines some of the main learnings, takeaways and outputs from this pilot project.


## Roll-out of online consultations

NHSE/I, through its Digital First Primary Care (DFPC) programme, has been working on enabling the adoption and use of online consultation systems as a means to increase choice and flexibility for patients in accessing and receiving care and supporting practices to signpost and triage patients to the correct member of staff or service, prioritising care on need and optimising use of wider primary care roles.

An online consultation enables a patient to contact their GP, other health professional or GP practice staff over the internet, typically by using a smartphone, tablet or computer. It may, among other outcomes, also result in a written-form consultation.

The NHS Long Term plan (pre Covid) committed to every patient having the right to digital first primary care by 2023/24 with a commitment in the GP contract for 21/22 for all practices to offer online and video consultations. OC capability is believed to stand close to 95%.

An evaluation of the digital first approach in response to Covid-19 has been commissioned and is ongoing. Wider efforts on improving intelligence for operational, research and evaluation purposes are also underway.

OpenSAFELY was identified as a means of providing rapid and rich intelligence on the OC landscape, in particular during the pandemic. In this initial discovery piece, we looked at:

- understanding coding use and prevalence in primary care records by codes of interest, over time and in terms of national variation
- understanding broad demographics and past clinical history of those associated with online consultation-relevant codes


## Piloting and using OpenSAFELY - the external collaborator view

One of the main strengths of OpenSAFELY is the richness of the [documentation](https://docs.opensafely.org/) provided, covering both ‘Getting Started’ guides, ‘How To’ tutorials and extensive reference material.

The OpenSAFELY team also provides active and timely support via the GitHub Q&A forum and a dedicated researcher Slack channels.

The first step in this discovery piece was defining the set of primary care codes relevant to online consultations to be queried. After initial desktop research and stakeholder input, the [OpenCodelists builder](https://www.opencodelists.org/) was used to define an 18-item codelist. This tool can be used by anyone to create, curate and re-use codelists.

Made easier by the documentation as well as other existing study repositories available on the Github, open-source tools were used, including:
- **Python**: for defining the cohort and generating dummy data to test the code;
- **Github**: to host the full study repository, so that it can be accessed and run in the EHR secure environments servers when required, but also crucially for version-control and promotion of open, collaborative and transparent ways working;
- **R**: for data analysis and visualisation, though other tools including Stata or Python can also be used.

The dedicated jobs server was then used to request for the code to be run against the real data - always at arms-length within the server. All these [request logs are shown transparently](https://jobs.opensafely.org/nhsx/online-consultations/). The outputs of interest (trendlines, summary statistics, model outcomes) were then made available to the research team, after review for disclosure by an Accredited ONS Safe Researcher.

### Tips ###
Some tips for analysts, from current experience:
- Define a fixed scope question and check feasibility based on available coding practices and literature;
- Make full use of the rich documentation and Q&A forums;
- Look into other public OpenSAFELY repositories and publications to understand the art of the possible and how to implement these. Many of the approaches are easily transferable and adaptable!
- Though running code on dummy data can already help maximise chances that the code is fit for purpose when run on real data, breaking up the code, actions and jobs into smaller chunks and ensuring that the code produces informative logs and has fail-safes can really help when it comes to running and debugging code on the actual data, at ‘arms-length’.
- Generate summary outputs as editables - that is, SVG images, html tables - so that these can be re-designed outside of the server if need be.


## Insights from the discovery piece


All the direct outputs can be found on [Github](https://github.com/opensafely/OS_OC_v001-research) (to be made open) and a more comprehensive report has also been shared with stakeholders. Some highlights are shown in the Appendix below.

Some insights include:

- More needs to be done to consolidate and harmonise coding practices for online consultations in primary care
- Six of the eighteen codes defined were in active use in TPP practices. The ones used by more practices were, in order, eConsultation via online application, Telemedicine consultation with patient and E-mail sent to patient - in 70% or more of practices (Figure 1). EMIS practices also had registered activity for these codes, but their volumes were quite different, indicating likely differences in digital supplier systems, coding approaches or population served.
- As expected, contrary to overall GP consultations, which dwindled at the start of the pandemic, coding activity related to digital forms of interaction picked up rapidly from March 2020. In the second semester of 2020, over nine monthly eConsultation coding events per 1,000 registered population were registered, compared to less than one per 1,000 a year prior (Figure 2).
- When compared to the full practice population, or to those that had consulted their GP at all, the cohort of patients that had any recorded online consultation activity in 2019-2020 tended to (Table 1):
    - Has a higher preponderance of female patients;
    - Has a higher relative preponderance of those aged 18-40, followed by those aged 40-50 and 50-60;
    - Skews more towards white patients;
    - Skews more towards those least deprived 
- We also found early indications that patients with online consultation coding activity were more likely to have a clinical history of asthma, depression or heart conditions than other patients with any overall GP consultation activity in the same period of time - it is important to note though that the OC systems user profile may not be generalisable and may be very dependent on the practice-by-practice implementation model


## Final thoughts

Insights from this discovery pilot study help build the picture around the implementation and use of online consultations and can support ongoing discussions on differential patterns of uptake as well as conversations with practices, OC system suppliers and EHR suppliers on ensuring consistent and widespread coding practices. Areas of interest for future exploration include:
- Development of coding activity metrics as proxies for wider coding quality and primary care activity (including sources of variation by organisation or patient sociodemographics);
- Facilitation of research and evaluation studies. For instance, for those with eConsultation events, how many need to re-consult within a month?

More than anything, this project was a great opportunity to collaborate and learn new stretching skills and techniques from DataLab and OpenSAFELY collaborative colleagues as well as subject knowledge from NHSE/I DFPC. It is also a great blueprint for the wider Data Strategy:
- OpenSAFELY is a powerful tool for researchers and analysts to generate insights from healthcare data, while ensuring appropriate data protection. This contributes to aspirations set out in [Chapter 5 of the DHSC Data Strategy](https://www.gov.uk/government/publications/data-saves-lives-reshaping-health-and-social-care-with-data-draft/data-saves-lives-reshaping-health-and-social-care-with-data-draft#empowering-researchers-with-the-data-they-need-to-develop-life-changing-treatments-models-of-care-and-insights), on empowering researchers with the data they need to develop life-changing treatments, models of care and insights.
- Its use of open source tools, version control, web user interfaces and rich documentation is also in line with the [desired direction of travel for ways of working in the NHS and for health and social care analysts across](https://www.nhsx.nhs.uk/blogs/data-saves-lives-building-and-skilling-nhs-analytics-community/), namely with ambitions set out in [Chapter 3 of the draft DHSC Data Strategy](https://www.gov.uk/government/publications/data-saves-lives-reshaping-health-and-social-care-with-data-draft/data-saves-lives-reshaping-health-and-social-care-with-data-draft#supporting-local-and-national-decision-makers-with-data), on building analytical and data science capability, working transparently and in the open, encouraging sharing practices and collaborations with partners.

## Appendix - Highlight figures and graphs

**Figure 1. Portion of practices with any recorded activity for online consultation relevant codes in general practice (January 2019 -  December 2020). Codes with no activity at all omitted. Only for practices using the TPP supplier system**
![Barchart showing portion of TPP practices that have a certain online-consultation relevant code recorded](/assets/sc03_fig05_pracnatcoverage_REWORKED.png){:height="700px" }

**Figure 2. Monthly code instance rates per 1,000 registered population of SNOMED codes in TPP general practice (January 2019 -  December 2020). March 2020 indicated in pink. Codes with no activity at all omitted. Only for practices using the TPP supplier system**
![Barchart showing monthly trend in use of specific online-consultation relevant codes](/assets/sc03_fig01_nattrends_REWORKED.png){:height="700px" }

<br>
<b>Table 1. Characteristics of the studied cohort (TPP system), both overall and by a) patients with any form of GP consultation in 2019-2020; b) patients with any OC code instance in 2019-2020</b>

<table>
<tbody>
<tr>
<td rowspan="2">
<p><strong>Characteristic</strong></p>
</td>
<td>
<p><strong>Overall</strong></p>
</td>
<td>
<p><strong>Had any GP consultation</strong></p>
</td>
<td>
<p><strong>Had OC coding instance</strong></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;"> N = 20,651,036</span></p>
</td>
<td>
<p><span style="font-weight: 400;">N = 17,166,765</span></p>
</td>
<td>
<p><span style="font-weight: 400;">N = 1,087,919</span></p>
</td>
</tr>
<tr>
<td>
<p><strong>sex</strong></p>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Female</span></p>
</td>
<td>
<p><span style="font-weight: 400;">9,599,496 (49%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">9,172,833 (53%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">661,235 </span><strong>(61%)</strong></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Male</span></p>
</td>
<td>
<p><span style="font-weight: 400;">9,963,322 (51%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">7,993,645 (47%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">426,654 (39%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Other/Unknown</span></p>
</td>
<td>
<p><span style="font-weight: 400;">299 (&lt;0.1%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">287 (&lt;0.1%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">30 (&lt;0.1%)</span></p>
</td>
</tr>
<tr>
<td>
<p><strong>age [2]</strong></p>
</td>
<td>
<p><span style="font-weight: 400;">41 (21, 59)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">44 (24, 61)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">43 (27, 58)</span></p>
</td>
</tr>
<tr>
<td>
<p><strong>Age group</strong></p>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">(0,18]</span></p>
</td>
<td>
<p><span style="font-weight: 400;">4,151,378 (21%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,279,485 (19%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">147,313 (14%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">(18,40]</span></p>
</td>
<td>
<p><span style="font-weight: 400;">5,388,980 (28%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">4,295,711 (25%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">349,162 (32%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">(40,50]</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,665,869 (14%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,353,934 (14%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">176,261 (16%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">(50,60]</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,735,067 (14%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,577,374 (15%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">178,461 (17%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">(60,70]</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,144,742 (11%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,137,624 (13%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">124,470 (12%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">(70,80]</span></p>
</td>
<td>
<p><span style="font-weight: 400;">1,598,702 (8.2%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">1,627,530 (9.6%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">74,886 (6.9%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">(80,Inf]</span></p>
</td>
<td>
<p><span style="font-weight: 400;">716,706 (3.7%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">729,284 (4.3%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">30,036 (2.8%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Unknown</span></p>
</td>
<td>
<p><span style="font-weight: 400;">161,673</span></p>
</td>
<td>
<p><span style="font-weight: 400;">165,823</span></p>
</td>
<td>
<p><span style="font-weight: 400;">7,330</span></p>
</td>
</tr>
<tr>
<td>
<p><strong>ethnicity</strong></p>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Asian</span></p>
</td>
<td>
<p><span style="font-weight: 400;">1,209,218 (6.2%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">995,568 (5.8%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">43,196 (4.0%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Black</span></p>
</td>
<td>
<p><span style="font-weight: 400;">398,242 (2.0%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">318,858 (1.9%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">14,157 (1.3%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Mixed</span></p>
</td>
<td>
<p><span style="font-weight: 400;">238,762 (1.2%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">189,299 (1.1%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">10,708 (1.0%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Other</span></p>
</td>
<td>
<p><span style="font-weight: 400;">5,737,108 (29%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">4,775,182 (28%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">289,469 (27%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">White</span></p>
</td>
<td>
<p><span style="font-weight: 400;">11,979,787 (61%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">10,887,858 (63%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">730,389</span><strong> (67%)</strong></p>
</td>
</tr>
<tr>
<td>
<p><strong>living alone</strong></p>
</td>
<td>
<p><span style="font-weight: 400;">5,466,461 (28%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">4,733,553 (28%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">316,542 (29%)</span></p>
</td>
</tr>
<tr>
<td>
<p><strong>region</strong></p>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">East</span></p>
</td>
<td>
<p><span style="font-weight: 400;">4,623,066 (24%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">4,014,256 (23%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">200,338 (18%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">East Midlands</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,458,477 (18%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,036,933 (18%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">160,425 (15%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">London</span></p>
</td>
<td>
<p><span style="font-weight: 400;">1,277,438 (6.5%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">940,810 (5.5%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">62,586 (5.8%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">North East</span></p>
</td>
<td>
<p><span style="font-weight: 400;">960,313 (4.9%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">812,460 (4.7%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,494 (0.3%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">North West</span></p>
</td>
<td>
<p><span style="font-weight: 400;">1,722,626 (8.8%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">1,587,452 (9.2%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">120,462 (11%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">South East</span></p>
</td>
<td>
<p><span style="font-weight: 400;">1,236,531 (6.3%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">1,119,208 (6.5%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">121,340 (11%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">South West</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,586,842 (13%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,410,816 (14%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">251,541 (23%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">West Midlands</span></p>
</td>
<td>
<p><span style="font-weight: 400;">840,558 (4.3%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">699,715 (4.1%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">21,112 (1.9%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Yorkshire &amp; The Humber</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,851,255 (15%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,540,057 (15%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">146,558 (13%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Unknown</span></p>
</td>
<td>
<p><span style="font-weight: 400;">6,011</span></p>
</td>
<td>
<p><span style="font-weight: 400;">5,058</span></p>
</td>
<td>
<p><span style="font-weight: 400;">63</span></p>
</td>
</tr>
<tr>
<td>
<p><strong>deprivation quintile</strong></p>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Q1 (most)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,989,883 (21%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,376,403 (20%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">167,889 </span><strong>(16%)</strong></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Q2</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,822,954 (20%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,297,000 (20%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">209,375 (20%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Q3</span></p>
</td>
<td>
<p><span style="font-weight: 400;">4,023,228 (21%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,545,312 (21%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">236,391 (22%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Q4</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,817,032 (20%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,409,747 (20%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">235,705 (22%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Q5 (least)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,577,294 (19%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,238,612 (19%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">219,527 (21%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Unknown</span></p>
</td>
<td>
<p><span style="font-weight: 400;">332,726</span></p>
</td>
<td>
<p><span style="font-weight: 400;">299,691</span></p>
</td>
<td>
<p><span style="font-weight: 400;">19,032</span></p>
</td>
</tr>
<tr>
<td>
<p><strong>rural urban</strong></p>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Other</span></p>
</td>
<td>
<p><span style="font-weight: 400;">310,706 (1.6%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">281,603 (1.6%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">18,154 (1.7%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Rural</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,896,532 (20%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">3,578,049 (21%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">216,578 (20%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Urban</span></p>
</td>
<td>
<p><span style="font-weight: 400;">15,355,879 (78%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">13,307,113 (78%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">853,187 (78%)</span></p>
</td>
</tr>
<tr>
<td>
<p><strong>care home</strong></p>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Yes</span></p>
</td>
<td>
<p><span style="font-weight: 400;">34,545 (0.2%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">35,080 (0.2%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">2,592 (0.2%)</span></p>
</td>
</tr>
<tr>
<td>
<p><span style="font-weight: 400;">Non</span></p>
</td>
<td>
<p><span style="font-weight: 400;">19,528,572 (100%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">17,131,685 (100%)</span></p>
</td>
<td>
<p><span style="font-weight: 400;">1,085,327 (100%)</span></p>
</td>
</tr>
<tr>
<td colspan="3">
<p><em><span style="font-weight: 400;"></span></em><span style="font-weight: 400;">Showing n (%) except for [2] which shows Median (IQR)</span></p>
</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>