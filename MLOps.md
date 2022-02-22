layout	title	permalink
base
MLOps
MLOps.html
{{page.title}}
Date: February 2021

Post author: 

Paul Carroll - Senior Data Scientist, NHS Transformation Directorate (formally NHSX)

Purpose

Examine and explore the difficulties and possibilites in setting up a MLOps framework as a Data Scientist, and leave resources for other NHS Data Scientists to follow, should they not have a developer at hand for this work. 


Sources

A whole range of excellent github pages, books, webpage resources and online video guides. 


Week One - Initial Task

The first task in MLOps to set up Continuous Integration (CI) for the project. 
This is a github repo where your model, your running code, shell scripts, gitignores, and yml files can be stored.
With these set up, the process can be run and tested using Github actions. 
Any updates or changes can be branched, run and tested, before pushing to the main branch. 
The CI process is vital in MLOps as this allows code to be run and tested ahead of deployment.

Step One -  

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
  



Spreading expertise and success
      

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

