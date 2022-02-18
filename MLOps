layout	title	permalink
base
MLOps
MLOps.html
{{page.title}}
Date: February 2021

Post author: Paul Carroll - Senior Data Scientist, NHS Transformation Directorate (formally NHSX)

Purpose
Examine and explore the difficulties and possibilites in setting up a MLOps framework as a Data Scientist, and leave resources for other NHS Data Scientists to follow, should they not have a developer at hand for this work. 
There will be a series of potentially weekly updates as I explore the means and methods of pipelines and Machine Learning Operations for Data Science.


Sources
A whole range of excellent github pages, books, webpage resources and online video guides. 


Week One - Initial Task

The first task in MLOps to set up a Continuous Integration (CI) pipeline. 
This is a github repo where your model, your running code, shell scripts, gitignores, and yml files can be stored.
With these set up, the process can be run and tested using Github actions. 
Any updates or changes can be branched, run and tested, before pushing to the main branch. 
The CI process is vital in MLOps as this allows code to be run and tested ahead of deployment.

Spreading expertise and success
Decreases wasted time on solving problems that has already solutions elsewhere
Creates consistency and allows for comparison of work
Enforces a transparent way of working increasing quality and assurance
Showcases insightful ways of working to inspire others
Increases the ability to collaborate
Distributed workloads for larger development pieces and ability to get external test and assurance
Mandate for making code open
Public services are built with public money. So unless there's a good reason not to, the code they're based on should be made available for other people to reuse and build on. Open source code can be reused by developers working in government, avoiding duplication of work and reducing costs for the government as a whole. And publishing source code under an open licence means that you’re less likely to get locked in to working with a single supplier.

The 12th service standard set out in the government service manual states that service teams should:

Write code in the open from the start, and publish it in an open repository - minus any sensitive information, like secret keys and credentials;
Keep ownership of the intellectual property of new source code that’s created as part of the service, and make it available for reuse under an open licence.
Furthermore,

Making code open and reusable was added as point 12 of the NHS service standard too.

Point 3 of the Technology code of Practice requires equal consideration to be given to open source solutions when procuring software and states that your plans must show you’ve considered using open source and publishing your code openly.

The Open Data Charter was signed by G8 leaders on 18 June 2013. This sets out 5 strategic principles that all G8 members will act on. These include an expectation that all government data will be published openly by default, alongside principles to increase the quality, quantity and re-use of the data that is released. G8 members have also identified health as one of the 14 high-value areas from which they will release data. Their stated aim is to unlock the economic potential of open data, support innovation and provide greater accountability.

Checks and best practice
When sharing code there are a variety of potential issues to avoid and thus a code sharing way of working is useful to ensure the sharing is appropriate and useful. These issues include:

Accidental leakage of data, secrets or intellectual property.
Ownership and use
Dependencies and versioning
The tools and connected library versions of the developed code will likely be different from that being implemented by the end-user.
Freshness
The code will very quickly become out of date regarding library versions and possibly data connections (i.e. API endpoints changing) and thus ideally a shared code repo requires some regular maintenance and updating.
Alternatively, if the code isn’t to be constantly maintained then clear documentation is required to describe the locked down versions required.
Git Branch Stability
If developing code in a live environment then a branching strategy (such as feature or release branching) may need to be considered in order to avoid multiple developers creating conflicting branches simultaneously.
Alongside this a clear way of working for reviewing the code and pull requests is needed.
To address these issues and setup a best practice way of working for code sharing, consider implementing:

Sensitive content checks
Sensitive, personal, secret or top secret data/information: If so, you’ll need to consider not publishing or removing these elements and then clearing the git history (see below)
Keys and credentials: You must keep code that uses secrets away from the secrets themselves. This includes storing secret keys and credentials separately (e.g. a secret management system or secure config file). You can then open the code while keeping the secrets closed and secure.
Unreleased policy: If the code makes clear details of a policy that has not yet been announced, you should keep the code closed until the policy is announced.
Git History content and commit messages:
If keys or credentials were included previously and thus are contained within the git history, then just removing them will not solve the issue. In this case all keys and credentials should be rotated/renewed so that those being published are no longer valid. This needs to be documented clearly.
If your team feels that the commit history is not suitable for publication, there is an alternative. After reviewing the code to make sure it’s safe to open, you can either rewrite history to remove or improve some commits, or squash all previous commits into one. This approach loses a lot of value from the git history and so is only recommended when absolutely required.
One final less recommended option is to create a new repo and move the latest secure version of the code to this. This is not recommended as it not only loses the git history value but also can be time-consuming and can end up with dual runs of the code.
Has written permission been obtained for any data stored from the data owner?
Are any data transfers conducted safely and securely? See Implementing the Cloud Security Principles - NCSC.GOV.UK to read about checking adherence of third party tools.
Have any notebook outputs been removed/checked for sensitive information?
Coding in the open
Some projects are developed in private and then made open for the sake of sharing, whilst others are developed in the open from the start.
These projects need the developer to stick to the best practice and follow a more structured approach to programming but come with the benefits of increased scrutiny and collaboration through other interested parties contributing with code, ideas, or bug reports.
Documentation
Add Readme (Example) and contributing guides to all repositories to help everyone understand the basic usage and set way of working. Consider including in the README:
Overview of the required software/package/library versions and how to get them.
Notes on upgrading the environment and dependencies
Description of major packages and techniques used
Description of each file, including working files, log files, configs.
Be clear about who is responsible for maintaining the code and how often this occurs (including if this isn’t actively maintained)
Add a License and appropriate copyright:
Consider using MIT for code and OGLv3 or GPLv3 for documentation as default. However, other open licenses may be more appropriate for the individual case.
Note: when setting up a new github repo with an MIT license it will automatically insert the github username against the © - you’ll often want to change this.
Contributions guidelines:
The GOV.UK Frontend contribution guidelines
The GOV.UK style guide for pull requests
requirements.txt file:
This can be used, along with components such as setup.sh, to quickly facilitate the installations of specific dependencies and package versions.
This increases the portability of the developed code and provides a source of information for security evaluations.
Version control
Even if you think you’ll be the only person to ever use the code or that it will remain static, still use a versioning system either locally or through a repo hosting service.
Consider Semantic Versioning - Given a version number MAJOR.MINOR.PATCH, increment the: - MAJOR version when you make incompatible API changes, - MINOR version when you add functionality in a backwards compatible manner, and - PATCH version when you make backwards compatible bug fixes.
Clear branching and review guidance
This facilitates good code review practices
Better quality code
Better oversight for security issues
Can also assist with reduction in duplication of effort
Regular commits whilst developing
Strive for good commit notes which explain the change independent of the context the developer has at the time. See Maintaining version control in coding - Service Manual
Best practice is to include what the change is, and why it was necessary in the subject line with how the change has resolved the issue in the body of the commit message if needed.
This assists in attributing the code to a developer (Git Blame) and can help in tracing and code review processes.
Publish bug reports and resolutions (where appropriate)
Including bug report and issue tracking will assist others in establishing if the tool is suitable for their use case.
It will also assist others in identification and correction of any known bugs or issues.
Document your code
Including creation dates, script summaries and input/output descriptions at the start of a code is incredibly useful for context.
Additionally, in-line comments should be used to describe any chunks imported from elsewhere, any business decisions (e.g. why values less than 7 have been suppressed), and to support a reader in understanding the logic flow of the code.
