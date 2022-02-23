---
layout: base
title: MLOps Framework
permalink: MLOps.html
---

<h2> {{page.title}} </h2>

Date: February 2022\ Post author: Paul Carroll - Senior Data Scientist, NHS Transformation Directorate.

#Purpose

Examine and explore the difficulties and possibilites in setting up a MLOps framework as a Data Scientist, and leave resources for other NHS Data Scientists to follow, should they not have a developer at hand for this work. 


#Initial Task

The first task in MLOps to set up Continuous Integration (CI) for the project. 
This is a github repo https://github.com/pauliecarroll/MLOps-1 where your model, your makefile, any shell scripts, the gitignore file, and yml files can be stored.
With these set up, the process can be run and tested using Github actions. 
Any updates or changes can be branched, run and tested to check the flow works, before pushing to the main branch. 
The CI process is vital in MLOps as this allows code to be run and tested ahead of deployment.


#Part One -  

Create a new repo. Here you can either follow my instructions and set up your repo as per below, clone the github repo I've set up, or do both and codealong as you clone and adapt the repo to your own code. 
Your repo needs to have the following construct:

#A gitignore file. This tells the repo which files to ignore. 

.gitignore

1 python

2

3 .Python

#A python function file, or your python function file

hello.py 

1 def multiply(a,b,c):

2     

3     return a * b * c

4

5 print(multiply(3,4,5))

6 #this function should give the answer to 3 * 4 * 5 = 60.

#requirements.txt file. Lists the repo packages needed

requirements.txt

1 pytest

2 pylint

3 pytest-cov

4 click

#test_hello.py file. This tests the function. 
test_hello.py
1 from hello import multiply
2

3 def test_multiply():
      assert 60 == multiply(3,4,5)
      
#Makefile. This file runs commands and is essential in CI.

Makefile

1 install:

2         pip install --upgrade pip && pip install -r requirements.txt

3

4 install-gcp:

5         pip install --upgrade pip && pip install -r requirements-gcp.txt

6

7 install-aws:

8         pip install --upgrade pip && pip install -r requirements-aws.txt

9

10 lint: 

11        pylint --disable=R,C hello.py


12 format:

13        black *.py

14 test:

15       python -m pytest -vv --cov=hello test_hello.py 

These are the files needed to build a CI platform. 

Once these files are in place, a .yml file needs to be created in order to configure Continuous Integration using Github Actions.
path for this is: <your-repo>/.github/workflows/<your-repo>.yml
      
Create your .yml file there.
  
1 name: Azure Python 3.7
      
2 
      
3 on: [push]
      
4 
      
5 jobs:
      
6   build:
      
7     runs-on: ubuntu-latest
      
8     
      
9     steps:
      
10     
      
11       - uses: actions/Checkout@v2
      
12       
      
13       - name: Set up Python 3.7.12
      
14      
      
15         uses: actions/setup-python@v1
      
16         with:
      
17           python-version: 3.7.12
      
18          
      
19       - name: Install dependencies
      
20          run: |
      
21           make install
      
22          
      
23       - name: Lint
      
24         run: |
      
25           make lint
      
26           
      
27       - name: Test
      
28         run: |
      
29           make test
  
Committing the .yml file to the workflow folder should trigger github actions to run, and the build to take place. If this doesn't happen click on actions in the menu repo, then click on the name of the .yml file in the centre of the screen, then top right, re-run all jobs. If you then click 'build' you will see the jobs taking place, and within each of these the executed code. 
      
This is a very simple example of how to view Continuous Integration. The files can be edited and re-tested at any point on the main branch, or better on a different branch, before being merged into the main branch. 


Part Two to follow, involving Docker and automating the pipeline.
      
## References

[1] Practical MLOps (2021). Noah Gift. O'Reilly

[2] Practitioner's Guide to MLOps. Whitepaper. Google 

[3] Graviraja. MLOps-Basics. [Online] [https://github.com/graviraja/MLOps-Basics]
      
[4] Visenger. Awesome-mlops, curated list [Online] [https://github.com/visenger/awesome-mlops]
