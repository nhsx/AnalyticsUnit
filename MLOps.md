---
layout: base
title: MLOps Framework
permalink: MLOps.html
---

<h2> {{page.title}} </h2>

Date: February 2022\ Post author: Paul Carroll - Senior Data Scientist, NHS Transformation Directorate.

#Purpose

Examine and explore the difficulties and possibilites in setting up a MLOps framework as a Data Scientist, and leave resources for other NHS Data Scientists to follow. 


#Initial Task

The first task in MLOps to set up Continuous Integration (CI) for the project. 
This is a github repo https://github.com/pauliecarroll/MLOps-1 where your model, your makefile, any shell scripts, the gitignore file, and yml files can be stored.
With these set up, the process can be run and tested using Github actions. 
Any updates or changes can be branched, run and tested to check the flow works, before pushing to the main branch. 
The CI process is vital in MLOps as this allows code to be run and tested ahead of deployment.


#Part One -  

Create a new repo. Here you can either follow my instructions and set up your repo as per below, clone the github repo I've set up, or do both and codealong as you clone and adapt the repo to your own code. 
Your repo needs to have the following construct:

#A gitignore file. This tells the repo to ignore the workflow files that are written in python, or .py files. 

.gitignore

![image](https://user-images.githubusercontent.com/97230649/156123731-06508e2c-97c7-4164-9f95-0cfc68666254.png)


#A python function file, or your python function file

hello.py 

![image](https://user-images.githubusercontent.com/97230649/156123046-a590de3d-2717-48ad-ab50-82749ba6ee57.png)


#requirements.txt file. Lists the repo packages needed

requirements.txt

![image](https://user-images.githubusercontent.com/97230649/156123125-687c83d5-e13b-4286-92c8-39eabaacc3c0.png)


#test_hello.py file. This tests the function. 

test_hello.py

![image](https://user-images.githubusercontent.com/97230649/156123541-3a1ed560-8cef-4f30-a124-44db2e90c9f7.png)
      
      
#Makefile. This file runs commands and is essential in CI.

Makefile

![image](https://user-images.githubusercontent.com/97230649/156123633-79115f91-66d8-4d3a-b4f3-6f5a611b29c8.png)


These are the files needed to build a CI platform. 

Once these files are in place, a .yml file needs to be created in order to configure Continuous Integration using Github Actions.
path for this is: <your-repo>/.github/workflows/<your-repo>.yml
      
Create your .yml file there.
  
![image](https://user-images.githubusercontent.com/97230649/156123868-fb341ffb-7962-4011-80f6-2762ac96e7e6.png)
  
Committing the .yml file to the workflow folder should trigger github actions to run, and the build to take place. If this doesn't happen click on actions in the menu repo, then click on the name of the .yml file in the centre of the screen, then top right, re-run all jobs. If you then click 'build' you will see the jobs taking place, and within each of these the executed code. 
      
This is a very simple example of how to view Continuous Integration. The files can be edited and re-tested at any point on the main branch, or better on a different branch, before being merged into the main branch. 


Part Two to follow, involving Docker and automating the pipeline.
      
## References

[1] Practical MLOps (2021). Noah Gift. O'Reilly

[2] Practitioner's Guide to MLOps. Whitepaper. Google 

[3] Graviraja. MLOps-Basics. [Online] [https://github.com/graviraja/MLOps-Basics]
      
[4] Visenger. Awesome-mlops, curated list [Online] [https://github.com/visenger/awesome-mlops]
