---
layout: base
title: Experiences of using open source in the NHS
permalink: experiences.html
---

<h2> {{page.title}} </h2>

**Date:** August 2021

**Post author:** Summarised by the Analytical Unit, NHSX with thanks to all contributors.

During March 2021, we put out a call for analysts and IT professionals in the NHS to be interviewed regarding their experience of using open source software in the NHS.  This post aims to capture some of the key points and suggestions raised during these interviews but this is not to be read as a recommendation or endorsement or a particular approach or opinion.

### Need to access open-source tools
All respondents said there was a large unmet need for access to tools which allow coding, sharing and version control in the NHS.  Access to these would be of great benefit to the NHS analyst/developer.  Whilst most of those interviewed had some access to these tools (biassed as the original call was to those with this experience), access across the NHS is varied but still prohibited in many trusts.  
 
### Need access to git (and github)
Git was mentioned as a key tool required for working in a reproducible and transparent way which would allow sharing of innovation across the NHS.  Git requires access to admin privileges which is prohibited on most machines that have access to NHS data.  This prohibition is in-place to protect the data and thus an appropriate solution to use version control in the NHS is required.  
 
### Awareness/Knowledge of necessary tools
The serious lack of understanding and awareness from IT and general managers of open-source tooling (e.g. R, Python, Git, Docker,...) crucial to the analysts’ jobs came up multiple times during the interviews.  This lack of knowledge is present amongst IT administrators, senior general managers and the requesting developers/analysts.  This gap in awareness leads to a great deal of wasted time but most importantly appears to hamper the process of accessing the tools as the decision makers are not confident in committing to using the tools.  This lack of knowledge combined with a culture of risk-aversion means that access to certain data, platforms, and tools becomes too impractical for analysts to deal with.

### Request Process
There either isn’t a clear request process for open-source software or the current request process doesn’t work with open-source software.  This can lead to the requester going around in loops with half-promises of a solution but many dead ends.  It can also lead to many miss-understandings about expectations and wastes a significant amount of time for all involved.  

### Burden of updates and package management
One respondent pointed out that maintaining and monitoring a tool is sometimes not thought through when requesting the tool ending up in an either out-of-date tool or an individual conducting this task informally for an entire organisation.
   
### Risk aversion culture
Mentioned a couple of times was a feeling of a risk-aversion culture in the NHS leading to continuing to use outdated software and resources when safer and more efficient solutions were available.

### Shutting out talent
Not having access to these tools doesn’t just affect the ability to analyse data in the NHS but also impacts the retention of talent as the frustrations of limited tool bases and the offer of more flexible working on cutting edge tech draws people aware.

### Precedent and example use-cases
The learning curve involved in deploying/utilising open-source tools for the first time was mentioned as a major contributing factor to NHS trust’s failure to adopt them.  There are few if any examples of end-to-end implementation of open source tooling in the NHS available to learn from.  This, the respondent thought, was due to each successful implementation being too bespoke and complex to articulate clearly.


## Suggestion
Fast access to virtual machines within a secure and structured environment for analysts would be hugely beneficial.
More education and examples of:
- open-source tooling and security.
- how to properly justify requirements for open source tooling and clear example request processes.
- Virtualisation (particularly in a cloud environment) would allow tools to be web-based removing some of the issues around maintenance, updating and initial installation, as well as requiring less technical knowledge and maintenance to utilise them.
- Servers containing necessary tools and data should be accessible from home, which of course needs a secure authentication method.
- There should be a central, national level, curated library of verified-as-secure tools for staff with the correct permissions. Local organisations should have the freedom to implement their own versions for the sake of competition.
- A central NHS repository/library containing quality assured code/tools would be useful. This ties into their idea of having a means of sharing code for review and improvement to reduce security risks and increase efficiency.
- There should be a “fast track” communication channel for developers and analysts to talk directly with both one another, and with IT. This would help reduce the time and resources spent navigating security-related procedures. A part of this solution may involve having members of staff who are specifically knowledgeable about certain tools.
- There should be staff members with specific knowledge of operating systems, platforms, (open-source) tools, etc who are available to mentor and support new users. The interviewee thought this would be especially important as without a track record of using open-source solutions, it is even more difficult to get their use approved when requesting them from IT. 
- More resources should be funnelled towards open-source tool development teams.
- In the long term a culture of responsibility amongst analysts must be encouraged, so as to make sure they do not misuse any open-source tooling they are given, and to improve the working relationship between them and IT. 
- Linux should be considered for both practical and security reasons. 







