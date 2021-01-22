OVERVIEW:
    Using machine learning, we will project occupational growth/decline in the next 10 years in California. 

QUESTION TO ANSWER:
    Which occupation will be highest in demand in California in the next 10 years?

DATA SOURCES WE USE:
•	https://data.edd.ca.gov/Industry-Information-/Current-Employment-Statistics-CES-/r4zm-kdcg
Current Employment Statistics (CES)
**USE FOR MACHINE LEARNING**
•	https://data.edd.ca.gov/Wages/Occupational-Employment-Statistics-OES-/pwxn-y2g5
Occupational Survey data 20 years
Occupational_Employment_Statistics__OES_.csv
•	https://data.edd.ca.gov/Wages/Occupational-Employment-Statistics-OES-/pwxn-y2g5
Occupational Survery data 20 years
Occupational_Employment_Statistics__OES_.csv
•	https://data.edd.ca.gov/Labor-Force-and-Unemployment-Rates/Local-Area-Unemployment-Statistics-LAUS-/e6gw-gvii/data
Local_Area_Unemployment_Statistics__LAUS_.csv
•	https://data.edd.ca.gov/Labor-Force-and-Unemployment-Rates/Unemployment-Rate-by-Age-Groups/bcij-5wym
Unemployment_Rate_by_Age_Groups.csv


FEATURES:
    Tableau
    Postgres (AWS)
    
LANGUAGES/INSTALLATONS:  
    HTML/CSS
    Python Pandas
    Python Matplotlib 
    Scikit-Learn
    SQLAlchemy


STEPS -

1. Copy APIs from EDD files.
2. Import one CSV file on AWS and use the URL in Google Collaboration.
3. In Google Collaboration, clean up data and create dataframes.
4. Codes under "Posgres Setup" was used to create database in pgAdmin by connecting to AWS.
5. Create the server "occupation_trends_rds" and connect to AWS by using the following:
host: occupation-trends.cppwghmqrqzq.us-west-1.rds.amazonaws.com
port: 6432
username : root
pwd : data1234
6. Select the pgAdmin server as the connection in Tableau.
7. Visualizations were made using tables in pgAdmin.
8. Machine learning was ran with the following files:
* modelDatajobs.ipynb
* modelDatajobs2020.ipynb
* modelRestaurants.ipynb
* modelRestaurants2020.ipynb
The slope, y-intercept, testing score, and training scores were saved for Datajobs2020 and Restaurants2020.
9. Created a calculated field in Tableau using slope and y-intercepts for Datajobs2020 and Restaurants2020 and linear regression line was added to data.
10. Created sheets of visualizations, dashboards from the sheets, and a story with all dashboards that were created.

<!-- CREATE USER admin22 with Password '12345'
Alter User admin22 With SuperUser;

IF EXISTS(SELECT *
FROM dbo.occupation-trends)
DROP TABLE dbo.unemployment_rate_by_age
DROP TABLE dbo.local_area_unemployment_stats
DROP TABLE dbo.longterm_occupational_employment
DROP TABLE dbo.occupational_employment_stats
DROP TABLE dbo.current_employment_stats

CREATE TABLE unemployment_rate_by_age(
area_name VARCHAR,
year INT,
age_16_19 FLOAT,
age_20_24 FLOAT,
age_25_34 FLOAT,
age_35_44 FLOAT,
age_45_54 FLOAT,
age_55_64 FLOAT,
age_65 FLOAT
);

CREATE TABLE local_area_unemployment_stats(
area_name VARCHAR,
year INT,
month VARCHAR,
employment INT,
unemployment INT,
unemployment_rate FLOAT
);

CREATE TABLE longterm_occupational_employment(
area_name VARCHAR,
period VARCHAR, 
occupational_title VARCHAR, 
percentage_change FLOAT,
median_hourly_wage FLOAT,
median_annual_wage FLOAT,
entry_level_education VARCHAR
);

CREATE TABLE occupational_employment_stats(
area_name VARCHAR,
year INT,
wage_type VARCHAR,
occupational_title VARCHAR,
mean_wage FLOAT
);

CREATE TABLE current_employment_stats(
area_name VARCHAR,
year INT,
month VARCHAR, 
industry_title VARCHAR,
current_employment INT
);

CREATE TABLE restaurant2020(
y_intercept FLOAT,
slope FLOAT,
training_score FLOAT,
testing_score FLOAT
);


