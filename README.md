# Colorado Licensed Professionals and Demographics Correlation Using SQL Server and Tableau :mountain_snow:
### I asked the question: For various licensed professionals in the state of Colorado, are there any characteristics (e.g., household income levels) at the county level that are highly associated with various professions?
 - For example: are Colorado dentists more likely to be licensed in high-income counties?
 - In order to do this project I joined tables from the US Census Bureau and Colorado Department of Regulatory Agencies
###
#### I began the by going to the [Colorado Division of Professions and Occupations website](https://apps.colorado.gov/DORA/licensing/Lookup/GenerateRoster.aspx) to access tables of various licensed professionals. I extracted tables for Dentists, Plumbers, and Architects.
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/LicensedProfWebsite.png)

#### Next, I reviewed the tables in Microsoft SQL Server and combined the 3 tables using Union statements into one table 'CO_Professional'
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/combining3Tables.png)

## Data Cleaning
#### I deleted columns that weren't going to be used for this analysis:
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/droppingColumns.png)

#### Let me show you a brief overview of CO_Professional:
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/briefOverviewCoProfessionals.png)

#### I notice there are folks who aren’t in CO, and there are null values in the county column. I’m going to eliminate those rows because I want to look at people just in Colorado and I need a county in Colorado to perform this analysis.

![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/DeleteOtherStatesandNulls.png)

#### Next, I changed the values of Den -> Dentist, ARC -> Architect, and RP -> Plumber for the ‘License Type’ Column

![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/caseIfs.png)


#### I then went to the US Census Bureau to extract Colorado demogprahic data by county. I used table DP03 (Selected Economic Characteristics) and filtered by Colorado:
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/USCensusWebsite.png)

#### Lets take a look at the table I downloaded from the United States Census Bureau that contains 2018 estimates for all counties from Colorado.
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/BriefOverviewCO_Census.png)

#### I noticed the county column has a different format from the profession’s table that I will be joining the tables on. This is a great data cleaning opportunity, and I need to split “County, Colorado” -> "County" so that the format of the counties is the same between the two tables

![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/CreateSplitCounty.png)

#### I have created a new column ‘SplitCounty’ and this will be the primary key to join the CO_professional  and CO_census tables

![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/FirstJoinOverview.png)

## Begin Analysis
#### How many Dentists are in each of the counties? 
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/DentistCount.png)

- Denver County has the highest count of dentists with 862 Licensed Dentists.

#### Which counties have relatively high numbers of dentists? 
  - For the percent of dentists in each county I calculated: Percent_dentists = ( [Count of Dentists] / [Population Over 16]) * 100. Let's also pull in [Mean Household Income] per county. I can then compare counties with high dentists to see if there is a correlation to larger household incomes.
  
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/SanJuan.755.png)

#### San Juan has .75% of its population over 16 as dentists! The total population is only 537. This seems to be an outlier, lets only consider counties where the population is greater than 10,000 and has more than 10 dentists.

![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/PrcntDentistsandMeanIncome.png)

#### Are there relatively more dentists in counties with a higher percentage of females?
 - I will create a column named Percent_Dentists (Population/Count of Dentists) , and also create a column Percent_female (Female Population / Population)
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/percentFemale.png)

 
#### Let's now take a look at the plumbers. Let's see what counties have a higher percentage of plumbers and compare that to average household income.
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/plumbersIncome.png)

#### Are there relatively more plumbers in counties with a higher percentage of females?
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/plumbersIncome.png)



# Visualizations
### Created using Tableau Public

#### Count of Dentists by County in Colorado

![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/CountDentists.png)

  - These are the top 10 counties by total number of Dentists.

#### Percetange of Dentists in each County vs Average Household Income

![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/IncomevsDentistPrcnt.png)

 - We can see there is a positive correlation between the percentage of dentists in each county and the Household income. This may be due to the fact that dentists prefer to live in higher income counties and will get their license in these counties.
 
 #### Percentage of Dentists in each County vs Percentage of Females
 
 ![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/prcntFemalevsDentsts.png)
 
  - There is a slight correlation between the two variables. As there are more females in a county, there is slightly more dentists practicing in that county. It doesn't seem to be signficant enough to draw any conclusions.
  
  
 #### Percntage of Plumbers by each County vs Average Household Income
 
 ![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/PlumbersIncome.png)
  
  - There is an inverse relationship between increasing household income by County and the amount of plumbers. More plumbers tend to be licensed in lower income counties, and it may be because they tend to live in cheaper areas of Colorado.
