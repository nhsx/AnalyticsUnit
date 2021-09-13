---
layout: base
title: How-to
description: Instructions, SOPs and guides
permalink: howto.html
---

## Review Policy for adding content
- Only public github repos are to be added as projects.
- Only the related individual to update their team content.
- All "content" needs to go through an offline gateway (as creating a branch is still public) before pushing work to github.
  - This gateway is currently a G-Drive folder in the Analytics Unit folders.
  - Add content as a google doc.
  - A content review (see below) is required by another member of the team before progressing the content to github.
- When the branch is published, create a pull request with another member of the team as a reviewer to conduct a technical review focussed on the interaction with the website.

**Content Review** (focus on ensuring the content is accurate, appropriate and clear)
- No non-public insights.
- If an opinion/experience piece this needs to be clear at the start.
- Clear reference to other work and contributions?
- Are there any sensitive issues or potential fallout?
- Are any statements likely to reflect badly on the NHS or impact public trust?
- Is the content focussed on the topic?
- Are there other stakeholders that need to be informed or included?
- Are any statements incorrect?
- Are statements backed up with evidence?
- Are there other stakeholders that need to be informed or included?

**Technical Review** (focus on appearance on the website)
- No data (unless public {in which case reference data rather than copying} or fake/synthetic) or sensitive strings. 
- Working Links?
- Content appearing as expected?
- Content in line with the Digital service manual where possible?
- Is markdown formatting correct?
- Assets added and linked?

## Update this website

1. Install Ruby, Jekyll and Bundle on your system (For Mac see https://jekyllrb.com/docs/installation/macos/ for help and use homebrew; For Windows see https://idratherbewriting.com/documentation-theme-jekyll/mydoc_install_jekyll_on_windows.html)
2. Clone <https://github.com/nhsx/AnalyticsUnit>
2. Create a new branch
3. In ther terminal, navigate to the repo folder and execute `bundle`
4. Execute `bundle exec jekyll serve`
   
      <div class="alert alert-success" role="alert">
        The website should be available locally on `http://localhost:4000` now, or on the Server Address provided on the terminal
      </div>
   
5. Make changes to your code using your IDE.  Save and refresh the page to see the changes locally.
6. If required, submit content to internal gateway and await content review
7. Once happy, commit your code and publish your branch
8. On github, make a new `Pull request` (PR)
9. Ask another team member to review the PR and merged into the live website!

**Alternatively**, for small changes such as the addtions listed below, you can ammend the `.ymls` and add assets/markdowns directly on github but please do this within a branch and pull request rather than directly on to the main.

## Add Projects

To add/edit projects, simply definie them in `_data/project.yml` and link them to a github repo or io page.  See the kanban.yml in _data for the stage catergories you can assign a project into.

## Add Posts

You can add/edit posts by defining them in `_data/thinking.yml` and add the text as a markdown file in the root folder.  Any images need to be stored in assets.  

## Add Team Members

You can add/edit team members by defining them in `_data/team.yml`.  Any images need to be stored in assets.



