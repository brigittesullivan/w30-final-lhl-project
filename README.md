# TailTides: Predictive Insights of Canadian Lobster Exports to US

By: Brigitte Sullivan</br>
Completed on:  19 January 2024 </br>
Lighthouse Labs Data Science Program</br>

----
I would like to acknowledge, honour, and pay respect to the traditional owners and custodians (from all four directions), of the land on which I live and work. It is upon the unceded ancestral lands of the Mi’kmaw people that I live. While this area is known as Cap-Pelé, NB the territory is part of the greater territory of Mi'kma'ki.

I chose this topic as a project as lobster has significant importance to myself and my local community of Cap Pele, NB.  

# Overview

The purpose of this project is to uncover insights into canadian lobster exports over the past 40 years, and develop a time series model to forecast future lobster export demand using the Facebook Prophet model. 

## Business Problem
* Can the monthly value of lobster that will be exported to the US for the next 3 years (2023-2025) be predicted?

## Rationale / Importance

More canadian lobster is exported to the US than any other country combined. In 2022, US exports represented 59% of the total value of lobster exports alone. 

![Chart](https://github.com/brigittesullivan/w30-final-lhl-project/blob/main/images/Percent_Export_US.png)

As other countries demand (appetite) for canadian lobster grows in the last decade, we see a slight decline in the percent of total value exported to the US.

Having forecasted export demand is important because:
* Facilitate trade negotiations, (offering volume incentives)
* Inform and improve the extensive lobster fishing regulations 
    * Licenses cost over ~ $1M 
    * Fishing seasons restricted geographically ![Helpful Map](https://www.fisherkingseafoods.com/wp-content/uploads/2021/01/Lobster-Tear-Sheet-map.pdf)
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

### Extract Data:
1. Export Data: 
* Export data was collected using Canadian International Merchandise Trade Web Application from Statistics Canada.
2. CPI Data - to adjust values for inflation
  
### Cleaning and EDA
* Data was already fairly clean.
* Adjusted values exported to canadian dollars, renamed some features
* Explored distributions

### Modelling

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
* To see the details of the modelling process, the params used, and each of their metrics, see the [Modelling_Process.md](https://github.com/brigittesullivan/w30-final-lhl-project/blob/main/Modelling_Process.md) file in this repo. 
* 
### Predictions
Used same parameters from best tuned model, however provided model with data from the complete date range 1988 - 2022. Model made predictions for 36 months (2023 - 2025). 

#### Annual view:

![Annual Predictions](https://github.com/brigittesullivan/w30-final-lhl-project/blob/main/images/Annual_Forecast_.png)

* Chart shows the aggregated monthly predictions annually. 
* Model is generally following the same trend as actuals, indicates the model is not overfitting.

#### Monthly: 

![MonthlyPredictions](https://github.com/brigittesullivan/w30-final-lhl-project/blob/main/images/Monthly_forecast_.png)

* Model follows same seasonality as actuals, with peaks in June and December/January. With lowest exports in April. 


# Conclusion

## Wins

1. Time Series Analysis was not covered as part of LHL's Data Science program. However, I knew I wanted to work with a data set with local importance. Given the important seasonality of lobster exports, using time series analysis became essential to being able to complete the project. I took the initiative to learn several different time series models (auto-arima, Prophet) to be able to complete this project.
2. I was able to iterate several times during the modelling process, which allowed me to acheive a MAPE of 10% for the model. 

## Next Steps

* Add more features into the model. Currently the model only takes in Date and Value exported (CAD$). Adding more features like could reveal further insights
    * Commoditity type - fresh, frozen, live, prepared/processed
    * Destination country GDP for period
    * Province of origin
* Expand models to other countries. The US remains Canada's #1 Customer for Canadian Lobster, China and South Korea are importing more and more each year.
  ![Annual Exports by Country](https://github.com/brigittesullivan/w30-final-lhl-project/blob/main/images/Annual_exports_country.png)
* Explore the relationship between current GDP and next years export values.

# References

* I want to acknowledge the dispute between indegenous and non-indigenous fishers on Mik'maw lands these past years. [Article: The Attacks On Mi’kmaq Lobster Fishers In Nova Scotia, Explained](https://www.refinery29.com/en-ca/2020/10/10111352/nova-scotia-lobster-dispute-explained#:~:text=For%20five%20weeks%20now%2C%20Mi,outside%20the%20province's%20commercial%20season.)
