# TailTides: Predictive Insights of Canadian Lobster Exports

By: Brigitte Sullivan</br>
Completed on:  19 January 2024 </br>
Lighthouse Labs Data Science Program</br>

----
# Note:
Lobster fishing i

# Overview

The purpose of this project is to uncover insights into canadian lobster exports over the past 40 years, and develop a time series model to forecast future lobster export demand using the Facebook Prophet model. 

## Business Problem
* Can the monthly value of lobster that will be exported to the US for the next 3 years (2023-2025) be predicted?

## Rationale / Importance

More canadian lobster is exported to the US than any other country combined. In 2022, US exports represented 59% of the total value of lobster exports alone. 

[chart]
My Drive/0.Bootcamp/1._Data_Course/lighthouse-data-notes/9_Final_Project/Project /w30-final-lhl-project/images/Percent_Export_US.png


Having forecasted export demand …
* Facilitate trade negotiations, (offering volume incentives)
* Inform and improve the extensive lobster fishing regulations 
    * Licenses cost over ~ $1M 
    * Fishing seasons restricted geographically (Helpful Map)[https://www.fisherkingseafoods.com/wp-content/uploads/2021/01/Lobster-Tear-Sheet-map.pdf]
    * Strict harvesting quotas, regulations, fines
* Support conservation efforts


## Assumptions:
* Data set covers 1988 to 2022. Will assume that 2023 is future since no data available for the full year.
* Dollar will be adjusted to today's (2023) dollars
* Data for Homarus Americanus species of lobster(excludes Norway lobster and Rock lobster). Relevant HS Codes are: 
    * HS 030612 - Lobsters, nes, frozen, in shell, including boiled in shell
    * HS 030622 - Lobsters, (Homarus spp), not frozen, in shell, including boiled in shell (Retired 2016)
    * HS 030632 - Lobsters, live, fresh or chilled
    * HS 030692 - Lobsters, nes, dried/salted/in brine/smoked/cooked, w/n in shell 
    * HS 160530 - Lobster, prepared or preserved
* Export Data for lobster extracted from (Statistics Canada's Canadian International Merchandise Trade Web Application)[https://www150.statcan.gc.ca/n1/pub/71-607-x/2021004/exp-eng.htm]

## Process

High-level:

### Extract Data:

1. Export Data: 
* Export data was collected using Canadian International Merchandise Trade Web Application from Statistics Canada.
* extracted in late november 
https://www150.statcan.gc.ca/n1/pub/71-607-x/2021004/exp-eng.htm
2. GDP Data
3. CPI Data

### Modelling
Model
#### Develop Baseline Models:
* Baseline models using auto-arima and Prophet, and an ensemble method were all developped
* The baseline prophet model returned the best results, so chose to focus on tuning this model.
* Test / train split:
    * Training : 1988 - 2017
    * Test/Evaluation: 2018-2019
    * I intentionally left out data from 2020, and 2021 when training and tuning the models since there where unusually large and low export values during Covid. I did not want the model to train using these exceptional cases. 

#### Tune Prophet Model
* test / train split same as baseline models for comparability
* applied cross-validation and hyper-parameter tuning
* Best model received a Mean Absolute Percentage Error of 10.5% on unseen data (Evaluation 2018-2019)
* To see the details of the modelling process, the params used, and each of their metrics, see the Modelling_Process.md file in this repo. 
* 
#### Predictions
Used same parameters from best tuned model, however provided model with data from the complete date range 1988 - 2022. Model made predictions for 36 months (2023 - 2025). 


# Findings


# Conclusion

## Wins

1. Time Series Analysis was not covered as part of LHL's Data Science program. However, I knew I wanted to work with a data set with local importance. Given the important seasonality of lobster exports, using time series analysis became essential to being able to complete the project. I took the initiative to learn several different time series models (auto-arima, Prophet) to be able to complete this project.
2. I was able to iterate several times during the modelling process, which allowed me to acheive a MAPE of 10% for the model.

## Next Steps

* Add more features into the model 

# References
