# Predicting the effect of nursing home quality measures on long-stay emergency department outpatient visits 
Author: Erica Pinto <br>
CIND820: Big Data Analytics Project <br>
Dr. Sedef Akinli Kocak <br>

## Repository Contents
This repository contains the code required to evaluate the impact of select nursing home quality measures on the long-stay emergency department outpatient visit rate within the United States utilizing a Stepwise Linear Regression Model, a Gradient Boosted (XGBoost) Regression Model, and a Kernel Ridge Regression Model. 

### Nursing Homes within the United States: 
![CMS_NH_Map](https://user-images.githubusercontent.com/99699157/156967715-5ac8c81f-924c-48b5-b8a9-e4f149dae4b6.png)<br>
 Reference: https://data.cms.gov/covid-19/covid-19-nursing-home-data


# Table of Contents
1. [Abstract](#abstract)
2. [Requirements](#requirements)
3. [Repository Content](#repository-content)
4. [Data Preparation](#data-preparation)
5. [Methodology](#methodology) 
6. [Results](#results)
7. [Study Conclusions](#study-conclusions)

# Abstract 
### Context
As of 2016, approximately 11% of the United States’ 85 years and older population lives within nursing homes on a long-term basis, 69% of which have at least one disability that affects their quality of life – hearing, vision, cognitive, ambulation (Roberts et al., 2018). Frequent unplanned avoidable and unavoidable transfers from the nursing home to the emergency department can further negatively impact residents’ health status, can hinder care due to gaps in communication during transition, and can be costly for Medicaid programs (Moccia & Keyes, 2021; Walsh et al., 2010). Utilizing machine learning techniques, the relationship between nursing home quality measures in the clinic, operational and safety domains and the rate of outpatient emergency department visits for long-stay nursing home patients will be explored. 
### Problem Statement
The initial research question for this study is as follows: 
1.	Which measures within the following nursing home quality measure categories significantly affect the outpatient emergency department visit rate from nursing homes for long-stay patients?
- Nursing home ownership type
- Bed numbers and occupancy rate
- Staffing complement and turnover 
- Reported incidents, complaints and citations 
- Long-stay patient quality management rating 
- Inspection survey observed deficiencies 
- RAI-MDS 3.0 clinical quality measures 
- COVID-19 Incidence and Death Rate <br>

Additionally, this study will be exploring the use of machine learning for prediction within the domain of nursing home quality. Thus, this study has an addition research question as follows: <br>

2.	Through utilization of machine learning techniques, is it possible to predict the outpatient emergency department rate for long-stay patients utilizing long-stay nursing home quality measures? 
### Data
Nursing home demographics and attributes are from:
- The Centers for Medicare & Medicaid Services (CMS) Provider Information dataset
- The CMS MDS Quality Measures dataset
- The CMS Medicare Survey Summary Measures dataset
- The CMS COVID-19 dataset
<br>
The independent variables were chosen from the following quality domains to create a holistic representation of nursing home quality status: <br>

- Operational
- Clinical
- Safety

Aside from facility ownership type, which is a categorical variable, the independent variables are numeric and continuous.
The dependant variable, ‘Number of outpatient emergency department visits per 1000 long-stay resident days’, is from the CMS Medicare Claims Quality Measures dataset (Measure Code 552). It is a numeric, continuous variable that is calculated as a proportion of outpatient emergency department visits per 1000 long-stay resident days. 

### Techniques and Tools
Python will be used across the lifecycle of this study. Three approaches will be adopted: 
1.	Stepwise Linear Regression – will be used for model building and prediction. Chosen due to high number of features that may be highly correlated. 
2.	Gradient Boosting (XGBoost) Regression - will be used for model building and prediction. Chosen due to robustness of algorithm for potentially semi-/non-parametric data.  
3.	Kernel Ridge Regression – will be used for model building and prediction. Chosen due to potentially semi-parametric dataset requiring smoothing for improved performance. 

### Evaluation
Model evaluation metrics will be:
- R2   
- Mean Absolute Error (MAE)
- Root Mean Square Error (RMSE)


# Requirements

- Python 3.0 

Required packages are as follows: 
- Pandas
- Numpy 
- OS
- Matplotlib.pyplot
- Seaborn
- Stasmodel.api 
- Scipy.stats
- XGBoost


# Repository Content
The repository content is as follows: 
- The 'Constructed_Dataset' folder contains the dataset constructed from the data sources listed above. 
- The 'Checkpoints' folder contains the checkpoints of the study to date. Each model has one Python notebook checkpoint. 

# Data Preparation 
### Datasets
Datasets were obtained from the CMS website at the following addresses for the year 2020 (as available): 
- CMS Medicare Claims Quality Measures: https://data.cms.gov/provider-data/dataset/ijh5-nb2v
- CMS MDS Quality Measures: https://data.cms.gov/provider-data/dataset/djen-97ju
- CMS Provider Information: https://data.cms.gov/provider-data/dataset/4pq5-n9py
- CMS Survey Summary: https://data.cms.gov/provider-data/dataset/tbry-pc2d
- CMS COVID-19 Nursing Home Data: https://data.cms.gov/covid-19/covid-19-nursing-home-data

The following attributes were extracted from the above datasets as the independent variables within the dataset: 
- Federal Provider Number
- Provider Name
- Ownership Type 
- Number of Certified Beds
- Average Number of Residents per Day
- Long-Stay QM Rating
- Total nursing staff turnover
- Registered Nurse turnover 
- Adjusted Nurse Aide Staffing Hours per Resident per Day                                            
- Adjusted LPN Staffing Hours per Resident per Day                                                  
- Adjusted RN Staffing Hours per Resident per Day
- Number of Facility Reported Incidents
- Number of Substantiated Complaints
- Number of Citations from Infection Control Inspections
- Percentage of high risk long-stay residents with pressure ulcers
- Percentage of long-stay residents assessed and appropriately given the pneumococcal vaccine
- Percentage of long-stay residents assessed and appropriately given the seasonal influenza vaccine
- Percentage of long-stay residents experiencing one or more falls with major injury
- Percentage of long-stay residents who have depressive symptoms 
- Percentage of long-stay residents who lose too much weight
- Percentage of long-stay residents who received an antianxiety or hypnotic medication
- Percentage of long-stay residents who received an antipsychotic medication
- Percentage of long-stay residents who were physically restrained
- Percentage of long-stay residents whose ability to move independently worsened
- Percentage of long-stay residents whose need for help with daily activities has increased
- Percentage of long-stay residents with a catheter inserted and left in their bladder
- Percentage of long-stay residents with a urinary tract infection
- Percentage of low risk long-stay residents who lose control of their bowels or bladder
- Total Number of Health Deficiencies
- Total Number of Fire Safety Deficiencies
- Confirmed COVID-19 Cases Per Occupied Beds
- COVID-19 Deaths Per Occupied Beds

The dependent variable for this study was also extracted from the CMS Claims Data Set: 
- Adjusted Score (Number of outpatient emergency department visits per 1000 long-stay resident days)

The dataset from the 'Constructed_Dataset' folder may be used at this point for the next stages of the study. 

# Methodology 
The study methdology was as follows: 
| Step | Description |
| ------------- | ------------- |
| PROBLEM AND OBJECTIVE DEFINITION | Identify business context, define problem and related objectives. |
| DATA PREPARATION | Identify data sources and gather datasets in similar time periods.  Merge data sources and prepare data set for exploration. |
| DATA PREPROCESSING & EXPLORATION | Data cleaning (duplication elimination, missing value detection, error detection, outlier detection), transformation and normalization, descriptive statistics, univariate distribution analysis, bivariate correlation analysis (if required). |
| MODEL BUILDING & TESTING | Assumption testing for linear regression (Normality, linearity of IV-DV relationship, multicollinearity, homoscedasticity, autocorrelation, normal distribution of errors (Q-Q plots)), dimension reduction (as required), hyperparameter tuning, model fitting. |
| ANALYSIS | Split model into training and testing sets, conduct predictive analysis. |
| RESULTS & VALIDATION | Present results for all models include measures of model effectiveness, efficiency and stability. |
| INTERPRET & COMMUNICATE | Interpret results against evaluation metrics and present findings (report, presentation etc.). |

# Results
The following 3 models were built and evaluated: 
•	Stepwise Linear Regression
•	Gradient Boosted (XG Boost) Regression 
•	Kernel Ridge Regression 

<b>Summary performance measures for each model is as follows: </b>
| Model  | Stepwise Linear Regression | Gradient Boosted (XG Boost) Regression | Kernel Ridge Regression |
| ------------- | ------------- | ------------- | ------------- |
| Mean Absolute Error  | 0.05  | 0.05 | 0.05 |
| Root Mean Squared Error  | 0.004 | 0.005 | 0.005 | 
| R^2  | 0.138 | 0.262 | 0.305 |
| Training time  | 0.005s | 0.07s | 4.35s | 
| Prediction time | 0.001s | 0.003s | 0.23s |

The attributes with the most information gain in relation to the dependent variable are as follows: 
| Model  | Gradient Boosted (XG Boost) Regression | Kernel Ridge Regression |
| ------------- | ------------- | ------------- | 
| 1  | Long-Stay QM Rating (33.0)  | Total nursing staff turnover (0.908) | 
| 2  | Average Number of Residents per Day (31.0) | Percentage of long-stay residents whose need for help with daily activities has increased (0.100) | 
| 3 | Percentage of long-stay residents whose ability to move independently worsened (28.0) | Long-Stay QM Rating (0.084) | 
| 4  | Percentage of long-stay residents whose need for help with daily activities has increased (27.0) | Percentage of long-stay residents who were physically restrained (0.045) | 


# Study Conclusions
This study explored the relationship between which nursing home measures significantly affected the long-stay patient outpatient ED Visit rate and attempted to predict the ED Visit rate for long-stay patients based on the quality measures. Three models were built using Stepwise Regression, Gradient Boosted (XG Boost) Regression and Kernel Ridge Regression. The models were able to identify relationships between nursing home measures and outpatient ED Visit rate however a significant relationship was not established. The selected nursing home quality measures had 13% - 30% ability to predict the ED Visit rate, demonstrating that nursing home quality measures are not able to fully describe the ED Visit rate by itself. The Gradient Boosted (XG Boost) Regression and Kernel Ridge Regression models outperformed the Stepwise Regression model by a significant margin and were able to provide better predictive performance due to the model approaches to semi-parametric (or skewed data). 

This study contributes to the body of knowledge regarding the impact of quality measures in the clinical, operational and safety domains on the outpatient ED Visit rate for long-stay patients within the nursing home environment. It identified that, while individual quality measures may contribute in part to the overall outpatient ED Visit rate for long-stay patients, there are many factors outside the realm of quality that predict ED Visit rate. However, this study was able to isolate a few quality-focused attributes such as ‘Long-Stay QM Rating’ and ‘Total Nursing Staff turnover’ that may have some impact on predicting the outpatient ED Visit rate within nursing homes that could be used in more comprehensive studies within this space. Additionally, a potential relationship between mobility and ED Visit rate was postulated, however additional research may be required. Clinical and operational quality measures were found to have a greater impact on predictive performance than safety measures. 

Further studies within this area can focus on exploring the relationship between clinical measures focused on mobility, ADLs and falls. Studies can additionally explore the relationship between aggregate quality measures and their predictive performance in relation to the ED Visit rate.
