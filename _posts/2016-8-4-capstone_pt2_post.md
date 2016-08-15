---
layout: post
title: Capstone Project -- Context and EDA
---

EDA Highlights and Project Summary

Hello there! Regardless of whether it was intentional or by chance, I'm very excited that you have come across my blog post for my Capstone Project! In this post, I will describe the final project I have chosen to complete my Data Science Immersive journey at General Assembly. I will also summarize the highlights of the Exploratory Data Analysis (EDA). 

Here we go!

_______________________________________________________________________________________

### Capstone Proposal: 
Identify services that lead to positive outcomes for foster care youth who age out of the system.


#### --Context--

##### Public Health Issue: Negative outcomes experienced by foster care youth who age out of the system

There is a sub-population of children in the foster care system (~10% of the foster care population) who experience a phenomenon known as foster care drift and end up aging out of the system (at age 18) with no permanent home. Because these youth experience extreme instability and usually lack knowledge and skills that lead to self-sufficiency in adulthood, this sub-population is at a higher risk of experiencing negative outcomes such as homelessness, unemployment, incarceration, and mental health issues.  

The John H. Chafee Foster Care Independence Program (CFCIP) was initiated to address this public health issue by providing federal funds to states for the design and administration of services geared towards helping these youth transition into adulthood successfully.

CFCIP considers a former foster youth as successfully transitioned into adulthood if he or she is able to obtain positive well-being, health, education, and finanacial outcomes. 


##### The services that are supported by these funds should:

 - Identify youth who are likely to remain in foster care until 18 years of age (age out of the system)

 - Help these youth:

   - Make the transition to self-sufficiency by providing education, training, and services necessary to obtain employment

   - Prepare for and enter postsecondary training and education institutions, by providing services

   - Receive personal and emotional support through mentors and the promotion of interactions with dedicated adults

   - Identify former foster care recipients between 18 and 21 years of age to complement their own efforts to achieve self-sufficiency by:

   - Providing financial, housing, counseling, employment, education, and other appropriate support and services

   - Making available vouchers for education and training, including postsecondary ￼training and education



##### For a more detailed breakdown of the program, check out the logic model below: 

![CFCIP Logic Model]({{ site.url }}/images/capstone/cfcip_logic_model.png)


_________________________________________________________________________________________________


#### --Capstone Project Specific Aim and Goals--

Build and develop a predictive model in order to:
    
  1) Evaluate the John H. Chafee Foster Care Independence Program (CFCIP)
  2) Identify which services provided lead to what outcomes
  3) Identify outcomes experienced by former foster youth who receive services
  4) Recommend which services to focus funds on
_________________________________________________________________________________________________


#### --Problem statement--

Which services provided by Chafee funded counties or agencies lead to positive (well-being, health, financial, and educational) outcomes for foster youth who age out of the system?

_________________________________________________________________________________________________


#### --Data Cleaning and Munging Approach--

#### Raw Data Source:

Raw data obtained from the National Youth in Transition Database (NYTD)

##### Starting datasets:

###### A) Services and demographic data for Fiscal Years (FY) 2011 - 2014 (Baseline populations for each FY)
        
- cross-sectional data collected over 8 six-month-periods

- for all foster youth receiving independent living services funded through CFCIP for each fiscal year

- data collected from all 50 states (my data excludes data from Connecticut) and D.C. and Puerto Rico

- Total of 675645 rows, and 31 columns
        
###### B) Outcomes data for Wave 1 and Wave 2 of Cohort 1
            
- cohort 1 consists of foster youth who received services in FY 2011 AND participated in surveys

- longitudinal data collected, 2 follow-up periods (every 2 years)

- about 5% of baseline population (Dataset A, FY 2011)

- Wave 1 = Outcomes Survey collected in FY 2011, within 45 days of youth's 17th birthday, from 49 states and D.C. and Puerto Rico (data excludes data from Connecticut) 

- Wave 2 = Outcomes Follow-Up Survey collected in FY 2013, within 45 days of youth's 19th birthday, from 48 states and D.C. (data excludes data from Connecticut, New York and Puerto Rico)

- Missing: Wave 3 = Outcomes Follow-Up Survey collected in FY 2015, within 45 days of youth's 21st birthday

- Total of 22811 rows, and 48 columns

![Cohort 1 Wave Distribution]({{ site.url }}/images/capstone/c1_wave_dist.png)

        
###### C) Outcomes data for Wave 1 of Cohort 2
            
- cohort 2 consists of foster youth who received services in FY 2014 AND participated in surveys

- longitudinal data collected, 2 follow-up periods (every 2 years)

- about 5% of baseline population (Dataset A, FY 2014)

- data collected from 49 states and D.C. and Puerto Rico (data excludes data from Connecticut) 

- Wave 1 = Outcomes Survey collected in FY 2014, within 45 days of youth's 17th birthday

- Missing: Wave 2 = Outcomes Follow-Up Survey to be collected in FY 2016, within 45 days of youth's 21st birthday

- Missing: Wave 3 = Outcomes Follow-Up Survey to be collected in FY 2018, within 45 days of youth's 21st birthday

- Total of 23775 rows, and 49 columns




##### Data Cleaning and Munging Plan:
    
1) Load 3 starting datasets into pandas dataframe for each

- As described in cell above: Dataset A, Dataset B, Dataset C

2) Create dataframe for Cohort 1 Dataset:

- Services and demographic data for foster youth in FY 2011 from dataset A 

- Outcomes data for Wave 1 and Wave 2 from dataset B

- Only include foster youth who completed surveys in both Wave 1 and Wave 2

- Clean data:

    - Drop rows that have missing values in multiple columns (>10)

    - Convert data type of columns AgeMP, EduLevlSv, RaceDcl, RaceUnkn to int

    - Convert data types of columns RepDates_outcomes, RepDates_services and DOB to datetime

    - Identify categorical variable columns that may need to be dummified for later analysis

    - Get rid of special characters (that are not UTF-8) in column HighEdCert

    - Unfortunately, several states have badly encoded unique ID values, which prevents me from tracking those 
      records. Need to drop data rows from the following states due to data quality issue:
      ["HI", "IN", "KY", "MS", "OR", "TX", "TN"]

- Load cleaned dataset into local postgres DB

3) Create dataframe for Cohort 2 Dataset:

- Services and demographic data for foster youth in FY 2014 from dataset A

- Outcomes data for Wave 1 from dataset C

- Only include foster youth who completed surveys in Wave 1

- Clean data:
    
    - Convert data type of columns AgeMP, EduLevlSv, RaceDcl, RaceUnkn to int

    - Convert data types of columns RepDates_outcomes, RepDates_services, outcmdte and DOB to datetime

    - Identify categorical variable columns that may need to be dummified for later analysis

    - Unfortunately, several states have badly encoded unique ID values, which prevents me from tracking those 
      records. Need to drop data rows from the following states due to data quality issue:
      ["HI", "IN", "KY", "MS", "OR", "TX", "TN"]

- Load cleaned dataset into local postgres DB


_________________________________________________________________________________________________



#### -- Risks and Assumptions --

- Risk: Data incomplete
    
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
____________________________________________________________________________________________________________________

- Risk: Data not representative of baseline population; N vs n

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
____________________________________________________________________________________________________________________

- Risk: Non-standardization of survey administration and data collection

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
____________________________________________________________________________________________________________________


- Risk: Raw data/Initial dataset

  1) Raw data already had imputed values for data that was missing from initial reporting:
     - Missing values for covariates were imputed using a recursive hot deck algorithm seeded with a sort list of state by sex. 
    
  2) For services data (dataset A) only: County FIPS code with fewer than 1,000 records are recoded to 8 (LcLFIPSSv)
    
    
   - Assumptions: 
   
       - Assuming data imputation done correctly and based on valid methodology. 
       - Excluding LcLFIPSSv from analysis because I do not have codebook for values for this feature
           - Perhaps can use in future



_________________________________________________________________________________________________

#### -- Proposed Methods and Models --


Outline

- Hypothesis Testing between two populations and between changes within one population:

    - Hypothesis testing between baseline pop and cohort pops
    - Hypothesis testing between 2014 cohort and 2011 cohort
    - Hypothesis testing between outcomes of cohort_1, wave_1 and cohort_1, wave_2 (change in outcomes)
    - Hypothesis testing between outcomes of cohorts, between received vs did not receive

- Dimensionality Reduction and Models:

    - PCA and Feature Importance in order to reduce dimensionality
    - Preprocessing if needed for chosen modeling techniques
    - Build 3 classifiers, cross-validate on 2011 data; x = services_2011, y = outcomes_2013:
        - kNN neighbors
        - random forests (gradient boost?)
        - logistic regression
 
- Model Evaluation and Predictions:

    - Compare performance scores/metrics
    - Pick best model (or try all....if time permits)
    - Predict outcomes_2015 based on services_2011 (wave 3 of cohort 1)
    - Predict outcomes_2016 based on services_2014 (wave 2 of cohort 2)

- Next steps:

    - Get 2015 data
    - Evaluate performance of model predictions for outcomes_2015 on 2015 data



_________________________________________________________________________________________________

#### -- EDA Summary --

Currently making some super cool plots using Tableau! Until I have those ready, here are a few bar graphs that show distributions of some of the variables in the analysis:

COHORT 1:

Distribution of Youth by State, Wave 1:
![Dist by State]({{ site.url }}/images/capstone/w1_dist_state.png)

Distribution of Youth by State, Wave 2:
![Dist by State]({{ site.url }}/images/capstone/w2_dist_state.png)

Connection to adult, Wave 1:
![Connection to Adult W1]({{ site.url }}/images/capstone/w1_cnct_adult.png)

Connection to adult, Wave 2:
![Connection to Adult W2]({{ site.url }}/images/capstone/w2_cnct_adult.png)

Highest Education Certification, Wave 1:
![Education Certification]({{ site.url }}/images/capstone/w1_highest_ed.png)

Highest Education Certification, Wave 2:
![Education Certification]({{ site.url }}/images/capstone/w2_highest_ed.png)

COHORT 2:

Distribution of Youth by State, Wave 1:
![Dist by State]({{ site.url }}/images/capstone/c2_dist_state.png)

Connection to adult, Wave 1:
![Connection to Adult W1]({{ site.url }}/images/capstone/c2_cnct_adult.png)

Highest Education Certification, Wave 1:
![Education Certification]({{ site.url }}/images/capstone/c2_highest_ed.png)
