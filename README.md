# Source Credibility, Belief, and Sharing Behavior  
## A Causal Machine Learning Analysis

This repository contains a reproducible R project analyzing how source credibility affects individuals’ belief in news reports and their intention to share them. The project is based on a fake-news experiment inspired by Bauer (2020) and combines conventional econometric methods with causal machine learning techniques.  

This project originally served as the final project for the course *Methods and Application of Machine Learning* during my Master’s studies.

---

## Project Overview

The main research questions are:

1. Does source credibility affect whether individuals believe a news report?  
2. Does source credibility affect whether individuals intend to share the report?  
3. Do these treatment effects vary across demographic groups such as age, education, income, and gender?  

The analysis first estimates average treatment effects using standard econometric tools, then explores treatment heterogeneity using machine learning methods.

---

## Methods

The project applies:

- t-tests and simple linear regression  
- multiple linear regression with demographic controls  
- quadratic specifications for nonlinear effects  
- logistic regression for binary sharing outcomes  
- Post-LASSO and Double LASSO  
- interaction models for conventional heterogeneity analysis  
- causal trees  
- T-learner  
- Double Machine Learning  

---

## Repository Structure

```text
Padua_CausalML_project/
├── data/
│   └── fakenewsdata.csv
├── output/
│   └── figures/
├── report/
│   ├── main_report.Rmd
│   └── final_report.pdf
├── README.md
└── .gitignore
```
Main Files:
report/main_report.Rmd — main reproducible analysis file

report/final_report.pdf — compiled report

data/fakenewsdata.csv — dataset used in the analysis

The report is written in R Markdown and can be reproduced by running:
rmarkdown::render("report/main_report.Rmd")

## Required R packages include:

tidyverse
stargazer
ggpubr
glmnet
hdm
causalTree
DoubleML
mlr3
mlr3learners
broom
sandwich
lmtest
