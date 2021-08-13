---
layout: base
title: How-to
description: Instructions, SOPs and guides
permalink: /howto/
---


## Update this website

1. Install Ruby, Jekyll and Bundle on your system (See https://jekyllrb.com/docs/installation/macos/ for help and use homebrew)
2. Clone <https://github.com/nhsx/AnalyticsUnit>
2. Create a new branch
3. In ther terminal, navigate to the repo folder and execute `bundle`
4. Execute `bundle exec jekyll serve`
   
      <div class="alert alert-success" role="alert">
        The website should be available locally on `http://localhost:4000` now
      </div>
   
5. Make changes to your code using your IDE.  Save and refresh the page to see the changes locally.
6. Once happy, commit your code and publish your branch
7. On Github, make a new `Pull requests`
8. Ask another team member to review the PR and merged into the live website!

**Alternatively**, for small changes such as the addtions listed below, you can ammend the ymls and add assets/markdowns directly on github but please do this within a branch and pull rather than direct to the main.

## Add Projects

To add/edit projects, simply definie them in `_data/project.yml` and link them to a github repo or io page.  See the kanban.yml in _data for the stage catergories you can assign a project into.

## Add Posts

You can add/edit posts by defining them in `_data/thinking.yml` and add the text as a markdown file in the root folder.  Any images need to be stored in assets.  

## Add Team Members

You can add/edit team members by defining them in `_data/team.yml`.  Any images need to be stored in assets.



