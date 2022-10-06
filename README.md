# Colorado Licensed Professionals and Demographics Correlation :mountain_snow:
### I asked the question: For various licensed professionals in the state of Colorado, are there any geographic characteristics (e.g., household income levels) at the county level that are highly associated with various professions?
 - For example: are Colorado dentists more likely to be licensed in high-income counties?
 - In order to do this project I joined tables from the US Census Bureau that contained Colorado Counties Demographics and Colorado Licensed Professional tables
###
#### I began the by going to the [Colorado Division of Professions and Occupations webiste](https://apps.colorado.gov/DORA/licensing/Lookup/GenerateRoster.aspx) to access tables of various licensed professionals. I extracted tables for Dentists, Plumbers, and Architects.
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/LicensedProfWebsite.png)

#### Next, I reviewed the tables in Microsoft SQL Server and combined the 3 tables using Union statements into one table 'CO_Professional'
![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/combining3Tables.png)

#### I deleted columns that I was not going to use for this analysis:
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

#### I have created a new column ‘SplitCounty’ and this will be the primary key to join CO_professional  and CO_census table

![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/FirstJoinOverview.png)

#### How many Dentists are in each of the counties? 
![]()


#### Which counties have relatively high numbers of dentists? In order to do this I have divide the Population / Count of dentists. Let's also pull in Mean Household Income per county. 

![](https://github.com/cdauksas/PortfolioProjects/blob/main/images/PrcntDentistsandMeanIncome.png)
