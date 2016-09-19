---
layout: post
title: Capstone Project -- Factors That Impact Educational Attainment Among Foster Youth 
---

EDA Highlights and Project Summary

Hello there! Regardless of whether it was intentional or by chance, I'm very excited that you have come across my blog post for my Capstone Project! In this post, I will describe my final project for the Data Science Immersive program at General Assembly (Summer 2016 Cohort). I will start off with some context, then an overview of my approach, and conclude with some insightful take-aways for the problem I chose to explore. 

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


#### -- Problem statement --

Which services geared towards foster youth aging out of the system lead to positive educational outcomes?

_________________________________________________________________________________________________


### -- Approach --

  1) Select Target Variable

  2) Select Features
  
  3) Build Models
  
  4) Recommendations
  
  5) Next Steps

_________________________________________________________________________________________________


### -- Data Used in the Analysis --

#### Raw Data Source and other references:

![Data Source and References]({{ site.url }}/images/capstone/sources.png)

Other Sources:


  - <a href= "http://www.acf.hhs.gov/cb/resource/cfcip-etv">Text of the Social Security Act regarding the Chafee Foster Care Independence (CFCIP) and Education and Training Vouchers (ETV) Programs</a>

  - <a href= "https://www.ssa.gov/OP_Home/ssact/title04/0477.htm>CFCIP: Compilation Of The Social Security Laws</a>

  - <a href= "http://thenationshealth.aphapublications.org/content/46/6/1.3.full">Article from APHA: Education attainment linked to health throughout lifespan...</a>

  - <a href= "http://www.casey.org/us-fact-sheet/">Foster Care Fact Sheet</a>


##### Population analyzed

The diagram below, obtained from the NYTD Outcome User Guide that was provided with the dataset, depicts the population that was included in my analysis. The green semi-circle represents all the foster care children in the system nationwide. The blue circle represents the foster youth who are about to age out of the system without a permanent home, which is about 10% of the foster care population. These 10% also represent the baseline population for CFCIP. The CFCIP policy requires that a subset of the foster youth population receiving services (i.e. the baseline population) participates in an outcomes survey at age 17, and two follow-up surveys at age 19 and 21. This project analyzed outcomes data for those youth who participated in all three surveys, which is about 5% of the baseline population, as denoted by the purple circle.

![Cohort 1 Wave Distribution]({{ site.url }}/images/capstone/cohort_1_popDiagram.png)


#### -- Risks and Assumptions --

##### Risk: Data incomplete
    
  1) Issue: Full complement of baseline data will not be complete until after May 15 of "A" pd for next FY
  
  2) Issue: For follow-up surveys (Waves 2+): responses collected anytime in 6 mo. period
  
  3) Issue: States are encouraged, but not required, to collect data early in period to avoid performing survey in 1 
     period and reporting results in next pd.
       
       
  - Assumptions:
    
      - Survey collected and reporting in same reporting period
      - Data is complete for each reporting period
      - Need to see if there is a way to check this using RepDates_services and RepDates_outcomes and OutcmDte
      - Either way, will need to make decision as to which date to use: date collected or date reported  

____________________________________________________________________________________________________________________

##### Risk: Data not representative of baseline population; N vs n

  1) Data sets exclude data from the following states:
        
     a) Connecticutt (due to Confidentiality Restrictions; excluded from raw dataset by National Data Archive on Child Abuse and Neglect (NDACAN))

     b) NY and Puerto Rico did not participate in wave 2 of cohort 1 dataset, so data for participants from those states are missing (Could be one reason why overall response rate for cohort 1, wave 2 was so low (averaged 27%))

     c) "HI", "IN", "KY", "MS", "OR", "TX", "TN" (I had to drop data from the following states because the unique ID column--the one I need for tracking participants from baseline to waves--for data from those states were corrupted. Could not use in my dataset and there is no way to impute or fix on my end).
    
  2) Self-selection bias:
       
     a) For baseline population data and services data: no sampling done; data collected for all population
     
     b) N = population consists of ALL youth in foster care at age 17 = baseline population
     
     c) Participation in survey is completely voluntary; no incentive to participate
     
     d) If respondents are significantly different from non-respondents (due to combination of response rate variation across states and survey design constraints), survey results are potentially biased and not representative of non respondents and overall, not adequately representative of outcomes of foster care youth population of 17 and 19 year old for whom survey is intended to assess.
     
     e) Cohorts population = n  
        
     - Cohort 1, Wave 1: 
         - Self-selected, non-probabilistic sample of youth in baseline
         - Self-selection because youth are not randomly selected

     - Cohort 1 and Cohort 2, Wave 2+:
         - Optional probabilistic sampling; choice is left up to state
         - If sampling method chosen, only done once (so wave 2 sampled pop. = wave 3 sampled pop.). Sample
           size calculation is standard (using Finite Population Correction; plus 30% of pop. size for 
           attrition). Sample size based on Baseline population.

     - In FY 2011 (cohort 1, wave 2 and 3): 12 states opted for sampling.
         - Only these 12 states employed sampling methods that address selection bias, and only for wave 2 
           participants

     - No states had more than 5,000 youth in their cohorts

         
         
   - Assumptions: 

       - The Children’s Bureau employed a weighting methodology with the NYTD survey responses to identify and
         correct potential non-response bias. 
       - Assuming that the weighting methodology was appropriate and effectiveo, then assuming no selection bias and 
         that cohorts are representative.
          
____________________________________________________________________________________________________________________

##### Risk: Non-standardization of survey administration and data collection

  1) There is only one regulation concerning survey administration: Surveys are administered to the participant 
     directly, meaning no one can answer for youth, nor can data from other sources be used to answer survey 
     questions.
        
     - However, nothing in place to enforce or ensure proper survey administration
    
  2) Surveys can be administered in person, via internet, via phone
    
  3) Data collection procedures are not standardized across states or local entities       
       
       
   - Assumptions: 
   
       - Responses are from foster youth participant and no one else
       - Response rates varied dramatically by state; this may be a reflection of variance in data collection procedures
        
____________________________________________________________________________________________________________________


##### Risk: Raw data/Initial dataset

  1) Raw data already had imputed values for data that was missing from initial reporting:
     - Missing values for covariates were imputed using a recursive hot deck algorithm seeded with a sort list of state by sex. 
    
  2) For services data (dataset A) only: County FIPS code with fewer than 1,000 records are recoded to 8 (LcLFIPSSv)
    
    
   - Assumptions: 
   
       - Assuming data imputation done correctly and based on valid methodology. 
       - Excluding LcLFIPSSv from analysis because I do not have codebook for values for this feature
           - Perhaps can use in future



_________________________________________________________________________________________________

### -- Selecting the target variable for the analysis --

![Many target variables]({{ site.url }}/images/capstone/many_outcomes.png)

The surveys administered to the foster youth to obtain outcomes data yielded many target variables. As can be seen above, I first attempted to group the data into four main outcome variables: well-being, health, educational, and financial outcomes. However, I still had to decide on one y-variable to focus the model on. I decided to conduct a PCA analysis and discovered that there was one main outcome that was explaining the majority of the variance in the data: Higher Education Certification. In other words, the PCA analysis over all the outcomes data (target variables) revealed that educational attainment was a proxy for all other outcomes. See diagrams below:

![PCA Analysis 3D]({{ site.url }}/images/capstone/pca_3D.png)

![PCA Analysis 2D]({{ site.url }}/images/capstone/pca_2D.png)

_________________________________________________________________________________________________

#### -- EDA Summary --

Soon to come: Selecting features, building the model, and recommendations.