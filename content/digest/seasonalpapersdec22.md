---
layout: base
title: Seasonal Papers - Dec 22
permalink: seasonalpapersdec22.html
---

# Seasonal Papers  
*22nd December 2022*

To finish the year off we decided to have a quick virtual journal club with mulled wine.  First up we had: 

## DECAF: Generating Fair Synthetic Data Using Causally-Aware Generative Networks
*Boris van Breugel, Trent Kyono, Jeroen Berrevoets, Mihaela van der Schaar – May 2021*

Jonny presented this paper as one of great interest to an upcoming internship project.  The key to this paper is to focus on the description of direct and indirect fairness and follow the authors connection to how aspects of fairness can be controlled through the manipulation of a Direct Acyclic Graph in a generative architecture to synthesize sequentially.    

We discussed the main fairness definitions presented in the paper and if DAGs are casually sufficient for generating synthetic data (Jonny suggesting yes for static data as without the need to model changes over time the impact of confounders is effectively limited so cycles don’t need to be considered).  The benchmarked results were discussed to highlight the extent to which we need to balance utility against fairness. 

**Main points of interest:** The authors remarks that the work could be extended into a VAE and privacy setting were highlighted as these are the avenues we’d like to explore with our own code.   

**Points to note:** The paper does not attempt to go into depth around forming the DAG, the definition of the “sufficient set of edges”, and how the formation of the causal model may need to also be coupled into the fairness definitions.  

## Whirlwind (non-exhaustive) tour of generative pre-trained transformers (the GPT family)
*r"(Bio|Chat|Instruct)?GPT(\-\d)?(\.5)?"*

Dan decided to stay away from any specific paper and instead tackle the subject of the GPT family, especially considering a recent publication of interest, [Foresight](https://arxiv.org/abs/2212.08072).  To understand the GPT family Dan highlighted the need to understand how transformers models generate representation differently, such as by utilising attention, and the roles of the encoder and decoder stacks within.  [Jay Alammar’s illustrated-gpt2 blog](https://jalammar.github.io/illustrated-gpt2/) was a recommended read for this understanding as it gives a good overview of the GPT-2 approach.  Many recent developments have focussed heavily on increasing the sizes of the models, creating ever larger models (now so large they can’t be easily used widely!). 

GPT’s development has gone through many stages; with the original GPT not often discussed (as it was quickly superseded); through the OpenAI development of GPT-2 and GPT-3 and the addition of reinforcement through human feedback, to try stop the models hallucinating or misbehaving; and finally, into the future territory beyond GPT-3.5.  

**Main points of interest:** Domain specific GPT models are required as Dan highlighted has been shown in this [example](https://arxiv.org/abs/2210.10341) where BioGPT and GPT-2 were asked to write a description of Covid-19 with a large amount of hallucination from GPT-2 whilst BioGPT performed significantly better. 

[Foresight](https://arxiv.org/abs/2212.08072) was mentioned as using GPT-2 style models to predict next step in a patient journey. This then has two highlighted use cases of predicting the risk of the next event and generating synthetic patients from starter demographic information (we have an active interest in privacy and collisions of real individuals in this type of modelling – see for example this [PhD Internship project](https://nhsx.github.io/nhsx-internship-projects/language-model-privacy-leakage/)). 

ChatGPT was discussed as a route for generating both good and bad outputs and code.  The success of ChatGPT has been achieved through the iterative process of having humans give feedback on outputs, and then learning from these votes using a [PPO](https://openai.com/blog/openai-baselines-ppo/) approach.  This is a great example of an ML model with the ability to accept corrections, but unfortunately as it’s not open source we can’t probe the inner workings.  Luckily [Allenai rl4LMs](https://github.com/allenai/RL4LMs) have provided an open-source framework which can be investigated and will likely take up much of Dan’s reading time over Christmas. 

**Points to note:** 

- GPT-3 is open access but not open source and thus we don’t know what the model looks like. 
- These autoregressive models deal with sequential data well but don’t capture distance/time between points directly. 
- The scaling war (making ever larger models with increasing numbers of parameters) is limiting plausible local usage. 


## Moving Beyond Consent For Citizen Science in Big Data Health and Medical Research
*Anne S.Y. Cheung*

Kevin put forwards a recommendation for all to read this paper as he found this to be an engaging paper throughout and one which really gets the reader thinking about the issue of consent for healthcare data.   The paper sets out the landscape for consent of medical and health data and highlights good and poor examples of consent.  

**Main points of interest:** The paper highlights right from the start that the notion of consent may not be valid when big data is being used more and more for secondary purposes (beyond the original reason for collection).  It appears that consent is often and quickly abused to allow general use of data through the accountability of data usage being applied to an under-informed individual at one point in time when in fact the data is used for cases that would require expertise to understand their implications and often used for a long time with technology and approaches adapting so the data can be used in a wider variety of situations whilst still referring to the original consent.  

**Points to note:** The paper promotes greater accountability of the data users which requires significant time spent considering aspects of re-identification, disclosure, sensitive data.  Part of this accountability would be based in legal and contractual obligations to not re-identify.  
