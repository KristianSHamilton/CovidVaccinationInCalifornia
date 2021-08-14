# CovidVaccinationInCalifornia
David's notebooks:

sources: 
Center for Disease Control
https://data.cdc.gov/Case-Surveillance/COVID-19-Case-Surveillance-Public-Use-Data-with-Ge/n8mc-b4w4
usafacts.org
https://usafacts.org/visualizations/coronavirus-covid-19-spread-map/state/california
California Secretary of State
https://elections.cdn.sos.ca.gov/ror/60day-recall-2021/
United States Census Bureau
https://data.census.gov/cedsci/table?t=Disability%3AEducational%20Attainment%3AFamilies%20and%20Living%20Arrangements%3AHealth%3AHousing%3APopulations%20and%20People&g=0400000US06,06.050000&tid=ACSDP5Y2019.DP02&hidePreview=true
California Health and Human Services:
https://data.chhs.ca.gov/dataset/vaccine-progress-dashboard/resource/130d7ba2-b6eb-438d-a412-741bde207e1c


cdc_data_cleaning_notebook.ipynb: jupyter notebook which reads the entire csv of CDC data on COVID cases in the US, and returns only cases in CA and the case month, county of residence, age group, sex, race, and ethnicity of each individual case. The original csv is 4GB, so this notebook makes the size of the data far more workable for the future notebooks.

ca_cases_data.ipynb: takes case totals for individual months from the csv written out by the cdc_data_cleaning_notebook. It also returns the month name from strings with numerical month values (ex: 2021-01 would return 'January). It also writes out csvs showing total monthly cases for counties, total cases by county, and cases by county and month. The matplotlib section of the notebook makes a bar chart for state case totals by month, a bar chart for cases by race/ethnicity, a pie chart of cases by age group, and a pie chart of cases by sex. These are all stored in the Resources/CA_cases_by_county/Images.

ca_covid_deaths_data.ipynb: This notebook takes the data of COVID deaths by CA county from USAfacts.org. This data is reported daily, and since my group was examining monthly totals I extracted the data for the last day of each month. After doing so, the format gets switched from numeric to month name ('2021-01': 'January). This data is then written out to a csv for later use.

ca_cases_deaths_vaccines_combined.ipynb: this notebook reads in the cleaned vaccine monthly totals created by Tikaram (ca_fully_partially_vaccinated_by_month, the CA data for total_monthly_cases.csv, uncleaned vaccine data, and the ca_covid-deaths_by_county.csv. Since the death data read in is cumulative for the entire pandemic, this notebook uses monthly summing and subtraction to get the monthly death counts, and writes them into a simple dataframe formatted for later merging. The notebook extracts montly cumulative totals for the number of people fully vaccinated and the number of people who have had at l shot from the uncleaned vaccine data. Finally, all of the data for deaths, cases, vaccines by month, and cumulative vaccine totals gets merged into one dataframe. This dataframe is grouped by month and ordered by historical occurence (ex: Dec 2020 before Feb 2021). The rest of the notebook runs linear regressions comparing columns in this dataframe to one another. I wrote about what I considered to be the most interesting of charts in the project writeup, but all of the regression charts are available to see both in the notebook itself, and in Resources/CA_covid_deaths_vaccines_combo/Images.

date_cleaning_notebook.ipynb: A bit of code I wrote to help Tikaram extract the month a vaccine was administered from the day(ex: '2021-01-27': '2021-01'). However, he learned about pandas DatetimeIndex, which can do the exact same thing in one line of code. In our cleaning/analysis notebooks we used DatetimeIndex instead of the code in this notebook.

DemographicsNotebook.upynb:
We used data from the United States Census Bureau to collect demographic information. We used the 5 years estimate American Community Survey (ACS) data that creates population estimates based on 60 months of data beginning in 2015. The other choice was the 1 year estimate ACS which has the advantage of being more current, but only reliable for analysis on large populations. The 5 years ACS seemed mandatory because some counties in California are much smaller than the recommended 65,000 limit. Scatter plot regressions based Highest Education Attained showed significant correlation between education level and vaccination rates within a county.

We used r values from the above scatter plots to create a divergence chart showing the education levels that have increasing relationships with vaccination rates in a county against the education levels that have a decreasing relationship.
We also used data from the California Secretary of State to analyze demographic relationships with counties’ vaccination rates. We created a series of plots based on political party preference that fit the same mold as the education data.

We used r values from the above scatter plots to create a divergence chart showing the Political Party Preferences that have increasing relationships with vaccination rates in a county against the party preferences that have a decreasing relationship.
Based upon strong r values, well over 50% for some categories, it seems clear that demographics do influence vaccination rates in counties. 

A more detailed breakdown of the project is in the finalProject1Report.docx in the main branch.
