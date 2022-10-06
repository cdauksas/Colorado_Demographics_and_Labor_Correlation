# Colorado Licensed Professionals and Demographics Correlation :mountain_snow:
### I asked the question: For various licensed professionals in the state of Colorado, are there any geographic characteristics (e.g., household income levels) at the county level that are highly associated with various professions?
 - For example: are Colorado dentists more likely to be licensed in high-income counties?
 - In order to do this project I joined tables from the US Census Bureau that contained Colorado Counties Demographics and Colorado Licensed Professional tables
###
#### I began the by going to the [Colorado Division of Professions and Occupations webiste](https://apps.colorado.gov/DORA/licensing/Lookup/GenerateRoster.aspx) to access tables of various licensed professionals. I extracted tables for Dentists, Plumbers, and Architects.
![](Photo of Colorado Website)

#### Next, I reviewed the tables in Microsoft SQL Server and combined the 3 tables using Union statemnets into one table 'CO_Professional'
![](Photo of Union statements)

#### I deleted columns that I was not going to use for this analysis:
![](Deleting columns)

#### Let me show you a brief overview of CO_Professional:
![](TOP 100 Overiew CO_Professional)

#### I notice there are folks who aren’t in CO, and there are null values in the county column. I’m going to eliminate those rows because I want to look at people just in Colorado and I need a county in Colorado to perform this analysis.

![](eliminate rows and nulls)

#### Next, I changed the values of Den -> Dentist, ARC -> Architect, and RP -> Plumber for the ‘License Type’ Column

![](Case If Statement)


#### I then went to the US Census Bureau to extract Colorado demogprahic data by county:
![](Photo of Census bureau Website)

#### Lets take a look at the table I downloaded from the United States Census Bureau that contains 2018 estimates for all counties from Colorado.
![](Brief overview of Colorado Data)
