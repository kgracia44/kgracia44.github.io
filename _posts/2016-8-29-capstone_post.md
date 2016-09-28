---
layout: post
title: Capstone Project -- Factors That Impact Educational Attainment Among Foster Youth 
---

Hello there! 

Regardless of whether it was intentional or by chance, I'm very excited that you have come across my blog post for my Capstone Project! In this post, I will describe my final project for the Data Science Immersive program at General Assembly (Summer 2016 Cohort). I will start off with some context, then an overview of my methods and findings, and conclude with some insightful take-aways for the problem I chose to explore. 

Here we go!

_______________________________________________________________________________________


### -- Context --

##### Public Health Issue: Negative outcomes experienced by foster care youth who age out of the system

There is a sub-population of children in the foster care system (~10% of the foster care population) who experience a phenomenon known as foster care drift and end up aging out of the system (at age 18) with no permanent home. This sub-population is at a higher risk of experiencing negative outcomes such as homelessness, unemployment, incarceration, and mental health issues because these youth experience extreme instability and usually lack knowledge and skills that lead to self-sufficiency in adulthood.  

The John H. Chafee Foster Care Independence Program (CFCIP) was initiated to address this public health issue by providing federal funds to states for the design and administration of services geared towards helping these youth transition into adulthood successfully.

![CFCIP Funds]({{ site.url }}/images/capstone/funds_for_services.png)


CFCIP considers a former foster youth as successfully transitioned into adulthood if he or she is able to obtain positive well-being, health, education, and finanacial outcomes. 


##### For a more detailed breakdown of the program, check out the logic model below: 

![CFCIP Logic Model]({{ site.url }}/images/capstone/cfcip_logic_model.png)


_________________________________________________________________________________________________


### -- Capstone Project Specific Aims and Problem Statement --

Build and develop a predictive model in order to:
    
  1) Evaluate the John H. Chafee Foster Care Independence Program (CFCIP)
  

  2) Identify which services provided lead to positive educational outcomes
  
  
  3) Recommend which services to focus funds on


#### -- Problem Statement --

Which services geared towards foster youth aging out of the system lead to positive educational outcomes?

_________________________________________________________________________________________________


Before I discuss my approach to explore the problem statement, I will describe the dataset used in this analysis. 


### -- Data Used in the Analysis --

#### Raw Data Source and other references:

![Data Source and References]({{ site.url }}/images/capstone/sources.png)

Other Sources:


  - <a href= "http://www.acf.hhs.gov/cb/resource/cfcip-etv">Text of the Social Security Act regarding the Chafee Foster Care Independence (CFCIP) and Education and Training Vouchers (ETV) Programs</a>

  - <a href= "https://www.ssa.gov/OP_Home/ssact/title04/0477.htm">CFCIP: Compilation Of The Social Security Laws</a>

  - <a href= "http://thenationshealth.aphapublications.org/content/46/6/1.3.full">Article from APHA: Education attainment linked to health throughout lifespan...</a>

  - <a href= "http://www.casey.org/us-fact-sheet/">Foster Care Fact Sheet</a>


#### -- Sample Population Analyzed --

The diagram and tables below describe the population that was included in my analysis. The target population for this study--foster youth at risk of aging out of the system without a permanent home--is about 10% of the total U.S. Foster Care Population each year. 

This sub-popultaion of foster youth are eligible to receive services funded by the Chafee Foster Care Independence Program (CFCIP) mentioned above. The sampling frame comprises the baseline pop and sample...

The CFCIP policy requires that a subset of the foster youth population receiving services (i.e. the sampling frame) participates in an outcomes survey at age 17, and two follow-up surveys at age 19 and 21. This project analyzed outcomes data for those youth who participated in all three surveys, which is about 5% of the baseline population, as denoted by the purple circle.

For this study, I will be building a predictive model based on sample from Cohort 1 (2011) and later, when data becomes available, I will test model on sample from Cohort 2....

<iframe align= "center" src="//giphy.com/embed/yt0yrOkQrCKpW" width="480" height="271" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p></p>

![Population Diagram]({{ site.url }}/images/capstone/c1_pop_table.png)


![Population Diagram]({{ site.url }}/images/capstone/c2_pop_table.png)

#### -- Sampling Terminology Sources

#### -- Risks and Assumptions --

#### -- Data Dictionary
_________________________________________________________________________________________________

### -- Methodology --

  1) Exploratory Data Analysis (EDA)

  2) Select Target Variable

  3) Select Features
  
  4) Build Models
  
  5) Next Steps
  
  6) Recommendations

_________________________________________________________________________________________________

#### -- EDA Summary --

Soon to come: Selecting features, building the model, and recommendations.

_________________________________________________________________________________________________

### -- Selecting the target variable for the analysis --

![Many target variables]({{ site.url }}/images/capstone/many_outcomes.png)

The surveys administered to the foster youth to obtain outcomes data yielded many target variables. As can be seen above, I first attempted to group the data into four main outcome variables: well-being, health, educational, and financial outcomes. However, I still had to decide on one y-variable to focus the model on. I decided to conduct a PCA analysis and discovered that there was one main outcome that was explaining the majority of the variance in the data: Higher Education Certification. In other words, the PCA analysis over all the outcomes data (target variables) revealed that educational attainment was a proxy for all other outcomes. See diagrams below:

![PCA Analysis 3D]({{ site.url }}/images/capstone/pca_3D.png)

![PCA Analysis 2D]({{ site.url }}/images/capstone/pca_2D.png)

_________________________________________________________________________________________________

#### -- Selecting Features --

Soon to come: Selecting features, building the model, and recommendations.