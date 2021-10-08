---
layout: base
title: Open Source Tool Requests
permalink: toolstackrequests.html
---

<h2> {{page.title}} </h2>

**Date:** September 2021

**Post author:** Analytics Unit, NHSX

For developers in the NHS, getting new software installed on their IT estate machine has always been something of a challenge, but this is particularly true in the case of open-source, programming, and version control tools. Access to R, Python, Git, and Docker for example, is prohibited in many trusts. Naturally, this is often with good reason--these tools can be used in ways that might circumvent IT security policies and potentially lead to the leakage of sensitive data in a way standard office software should not. There also exists a gap between IT teams and developers in terms of which tools and workflows they are familiar with. This gap in knowledge, combined with a culture of risk-aversion has been said to greatly hamper the process of adoption of new software in the NHS, leading many developers to look for workarounds.

An issue that we hope to highlight here, is that there often is no clear request process for open-source software or that current software approval processes are not designed with open-source software in mind. Below we outline ways in which such a request process could be reformed as to leverage the pre-existing knowledge of our developers and the wider open-source community, as well as the security and infrastructure requirements best understood by IT estate departments:

- Be goal focused by discussing the problems to overcome, and not necessarily the tool itself. A goal focused approach can highlight user requirements more easily while allowing flexibility in terms of considering other options.
- Start the evaluation with a search for any known tools that may achieve the same goal. In a similar vein, check whether the request has been discussed with the whole development team, and potentially other technical teams. Leverage your developer teams’ existing knowledge and prior research to minimise unnecessary work.
- Make use of the open-source community. Various forums exist for all tool stacks and much information and experience can be gleaned from these discussions.
  - _Note: When interacting with public facing forums, we should suitably anonymise our request as not to include any identifiable information that may expose trust data or infrastructure._
- Finally, ensure that the tool fits within existing policies and procedures.

For those requesting new tools, it is recommended that the following questions are answered before making a request. This will assist the IT estate department to deal with such a request in a timely manner and identify similar tools using the process above.

### 1. What is the problem at hand?

- What is the issue that needs to be solved?
- What is the scope of the issue?
- What data is involved with the issue?
  - Aggregated data
  - Clinical Data
  - PII
  - Capacity information
- Is any of this data security controlled?
- Does it require credentials or an authenticated API to access?

### 2. What tool have you identified that may fit the issue?

- Tool Name
  - Environment
    - R
    - Python
    - C
    - Stand-alone
    - Operating System requirements
  - Version number
- Has this tool been evaluated before?
- What was the result of this analysis?
- Does the tool have any documentation available?
  - Is this good quality?
  - Does the documentation specifically show it will address this issue?
- Was this tool developed using accepted standards?
  - Is the tool selected tested rigorously by the developers?
  - Is the tool licensed appropriately for use within the NHS?
  - Is the tool actively developed?
  - Does the tool have any major security bugs or issues documented?
  - Is the tool likely to be supported in the future?
    - 1 month
    - 1 year
    - 5 years

### 3. Have you evaluated other tools for this issue?

- Details of those tools, including why they are not suitable or have not been selected

## A Recommended Process for Evaluating Open Source Tools

This process has been designed and developed based on industry standards [^1]. The process has been adapted for use within the NHS and the wider structure. In essence, the review process is split into three evaluation stages, basic, intermediate, and advanced and a finalization or deployment stage. The tool must be evaluated at the lower stages to advance to further analysis.

The process allows for the initial selection and evaluation of tools by a technical person, not necessarily a security expert [^2]. Evaluation of documentation, bugs and code can be shared between individuals and teams to reduce the workload on a single individual. Once the major suitability and technical reviews are complete, the tool can be, if necessary, passed to a dedicated security team for a final, complete security review.

## 1. Basics

This level of evaluation can be performed by any technical member of staff, prior to the deployment of the tool. It is suggested that this stage of the evaluation forms part of the initial user request. The aim of this evaluation is to establish the viability and initial quality of the selected tool.

### 1.1 Due-Diligence

Has anyone else, within the domain of the requester (i.e., within the same team, department or trust), made a request for this tool. The aim here is to establish if the work has already been conducted, or if an evaluation is in progress.

It should be possible to establish if a request is ongoing by reviewing the Wiki or the national repository. If a request has already been made then the requester should either assist with the ongoing evaluation (if the evaluation process is ongoing), request access to the tool (if the evaluation is complete and successful) or review the documentation for the evaluation to establish why the tool was rejected and make a request as appropriate.

### 1.2 Product documentation

Is product documentation available, up to date and usable? The quality of the product documentation should be publicly available, up to date with the latest version, recently updated (in line with any recent release of the product) and comprehensive.

### 1.3 Use of standards

Does the tool utilise accepted standards for code development and is the code well documented? Good development standards and coding practises fortifies the quality of a tool and makes updates, modifications, and reviews easier to conduct.

### 1.4 Test plan

Evaluate and review any test plan for the tool that is publicly available. In some instances, no test plan is available, but some testing strategy is described within the documentation.

### 1.5 Licenses

A review of the licenses and end user acceptance documentation is necessary to establish if the tool can be used by your organisation, department or for your use.

### 1.6 Environment

Can you facilitate the tool within your environment? What are the system requirements? Does the tool have any major dependencies? Can a suitable environment be provisioned?

### 1.7 Commits and bug reports

Does the project have active commits (maintainers and development) and does the Bug reports contain any show-stopping issues? If no active development is ongoing, why? Has the project been superseded? Is it no longer suitable for use?

### 1.8 Maintainability and sustainability

Is an LTS version available, what is the frequency of releases? How long are versions being supported for? Does the tool indicate a roadmap for development and support?

### 1.9 Requirements Management

Does the tool meet the requirements for the task at hand? Is it likely to continue to offer support for this task?

## 2. Intermediate

This level of evaluation should be conducted with involvement from IT Teams and with a small test group of users (maybe just the initial requester if appropriate). IT should review the previous evaluation and further document this stage.

### 2.1 Review of the Basic evaluation

IT Teams should review the information gathered and check that the analysis work done at the Basic Evaluation stage is completed and accurate. This gives IT teams a chance to review the formed request and establish and cross check the analysis and evolution already performed. If any aspect of the basic evaluation is found to be lacking, the requester should be contacted and asked to assist in the completion of that section.

### 2.2 Project Planning

This stage requires the IT team’s involvement to identify, from a technical viewpoint, what is required to allow this tool to be run. This should include dependencies, compute power and permissions.

### 2.3 Test planning – include rollback strategies

Establish a procedure and plan for testing and evaluating the tool in an operational environment (i.e., a sandbox test environment with no real clinical data) A plan should be compiled that includes testing for:

- Functionality of the tool
- Compatibility with existing infrastructure (hardware and software)
- Ability to monitor for network connections or unusual system activity
- Development of a rollback plan, how to remove the tool from systems

### 2.4 Quality Assurance – criteria for success

The IT team and the requester should work together to establish a set of criteria to be applied to the tool. This should include:

- Quantifiable criteria (i.e., processes 1,000 records in under 1 second)
- Positive and Negative tests (i.e., tool is capable of this task – Yes or No)

It is best to avoid subjective tests at this stage (i.e., tools are better at this task).
The aim of this is to confirm the full requirements of this tool, along with the development of a full plan for the viability of the tool under this use case.

At this stage in the evaluation, IT should be in a position where they are able to deploy this tool to a small test group, including the original requester, for a viability evaluation with synthetic data to confirm that the tool can perform as expected and required.

## 3. Advanced (pre-deployment)

This level of analysis is designed to ensure that the tool is suitable and effective for use, as well as to identify and combat any risk and security implications inherent within the tool.

### 3.1 Review of the Intermediate level evaluation

A review of the previous stages by another member of IT or management to confirm the work to date is accurate, comprehensive, and suitable.

### 3.2 Risk management

Analysis and risk assessment for the new tool should be conducted here. Teams should identify what data is going to be accessed with the tool and do a suitable risk assessment against the tool, its level of access to the data, the type of data the tool has access to, the processing to the data the tool is likely to do. This should cover security events that are possible, including impacts to the availability, accuracy, and confidentiality of the data.

This risk assessment should include a treatment plan, to remove, mitigate or transfer the identified risks. A common methodology to use is laid out below:

- **Risk Description** is a description of the anticipated risk.
- **Risk Subject** is who, or what is going to impacted by that risk
- **Likelihood** is a 1-10 score based on the anticipated likelihood of the event occurring where 1 is almost impossible and 10 is certain.
- **Severity** is a 1-10 score based on the severity of the impact of the risk, where 1 is very minimal impact (for example if data access was delayed by seconds) and 10 is serious harm (for example exposure of sensitive clinical and personal data to the public).
- **Risk Score** is the product of Likelihood and Severity (likelihood X Severity) and so is a scale of 1-100.
- **Treatment** describes what steps are taken to reduce the impact of the risk.
- **New Likelihood**, New Severity and New Score are as above, but for the risk following the treatment.

The aim of this risk assessment is to document the identifiable risks and the steps to take to reduce them.

### 3.3 Testing

Feedback from the initial test group should be used to supplement and inform how the tool is going to be used, what its feature sets and capabilities are. Any bugs or issues can be investigated and resolved prior to a wider release.

### 3.4 Design

Any changes based on community feedback should be evaluated, implemented, and tested. Risk assessments should be updated, and the documentation changed to reflect any necessary changes.

### 3.5 3rd Party Assessment

It is strongly recommended that the process of evaluating tools incorporates a continual review process that includes a regular review of all identified Common Vulnerabilities and Exposures (CVEs). A number of resources are available for these searches, including, but not limited to the following:

- https://nvd.nist.gov/vuln/search
- https://cve.mitre.org/cve/search_cve_list.html
- https://www.cvedetails.com/

By way of an example, the following links are for a search for ‘JupyterLab’:

- https://nvd.nist.gov/vuln/search/results?form_type=Basic&results_type=overview&query=JupyterLab&queryType=phrase&search_type=all
- https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=JupyterLab
- https://www.cvedetails.com/vulnerability-list/vendor_id-15653/JupyterLab.html

It is important that these searches are completed and that any vulnerability is reviewed. It is common for vulnerabilities to only apply to certain versions, and it is observable that most tools, under active development develop and release a patch for disclosures within 9 days [^3].

## 4. Finalization (deployment)

This final section of the evaluation process will complete the documentation and employability for the selected tool. It is applicable for any evaluation process, whether successful or not.

### 4.1 Document the reasons for success / failure of the request

Should the request and evaluation be successful, all documentation used, developed, and completed should be compiled and placed within the most suitable repository. This will allow any other team, department, or requester to review the previous requests.

The above is equally important for tools that have failed the evaluation for any reason. Proper documentation for the failures will quickly allow future requesters to see what issues were identified and prevent a fruitless process.

### 4.2 Deploy and distribute the tool

Assuming the tool is successful, the tool should be distributed via appropriate channels, such as a national level repository. This will allow others access to the tool and streamline future analysis.

### 4.3 Maintain updates, documentation, and notifications

Following the successful evaluation of a tool, the documentation notes and analysis should be maintained for future updates and releases. The main section to keep updated is the risk assessment and to consider if a formal Penetration Test is necessary and viable for major updates.

[^1]: https://owasp.org/www-pdf-archive/OWASP_Code_Review_Guide_v2.pdf
[^2]: http://qualipso.icmc.usp.br/OMM/
[^3]: https://www.fireeye.com/blog/threat-research/2020/04/time-between-disclosure-patch-release-and-vulnerability-exploitation.html
