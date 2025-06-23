# Hospital Emergency Room Analysis

## The Table Of Contents

- [The Table Of Contents](#the-table-of-contents)
- [Purpose](#purpose)
- [KPIs](#kpis)
- [Data Overview](#data-overview)
- [Observation](#observation)
- [Data Loading](#data-loading)
- [Data Cleaning And Transformation](#data-cleaning-and-transformation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Dashboard Layout Creation](#dashboard-layout-creation)
- [Dashboard](#dashboard)
  
## Purpose

We need to creat a hospital emergency room analysis dashboard. This dashboard will help stakeholders to monitor, analise and improve hospital services. 

## KPIs

### Primary
* Number of Patients: Total number of visits to the ER everyday.
* Average Wait Time: Find the average wait time to attend the patient.
* Patient Satisfaction Score: Find average satisfaction score to access the service quality.

### Secondry
* Patient admission status: how many were admitted vs not admitted.
* Patient age distribution: Goupe patients age for the age wise analysis.
* Wait time analysis: Howmany paitents were attended with 30mints and beyond.
* Gender Analysis: Number of patients based on gender (Male/Female).
* Department Referrals: Which department referred maximum referrals.

## Data Overview

* The data was downloaded from
* The file has 11 columns and 9217 rows including the header.

## Observation

* Patients Date column had date and time together. As we do not have any use of time as per the KIP, will split and remove the time.
* Patient first name column just has name innitials along with a seperate column with the last name. Hence, will merge them for easy use.
* Patient gender column needs normalisation as it has inconsistant values like Male, Female, M, and F.
* Patient age column must have another column with the age group as per the KPI requirement.
* Patient admission flag columns has test values line True/Fales that needs to be convertend into admitted or not admitted.
* Patients wait time column must have another column indicating how many of them were attended within 30mints and beyond for the KPI analysis.
* Patient wait time column as a duplicate column which must be removed.
* Department referral column has "None" values that neither be pupulated nor can be removed. Hence, keeping them as is.
* Patient satisfaction score column has blank cells too which neither be populated nor deleted. Hence, keeping it as is. 

## Data Loading

* Importing the CSV file through Data Tab > Get Data> From File > From Text/CSV.
* Check the details in Navigator Box and Transform Data to cleaning and preperation.

## Data Cleaning And Transformation

### Error and Column Quality:

  * Checkign for errors and correcting them with the Column Quality Option under the View Tab.
  * Found Empty in Patient Satisfaction Score column.
  * Not removing them as we need both the data. 
   
### Patient Admission Date Column:

  * Splitting Patient Admission Date column into two with date and time seperately. 
  * Select Column > Transform Tab > Split Column > By Delimeter > Select - Customer - Space (as the delimeter between date and time is space), Split At - Each Occurance of the  Delimeter.
  * Checking the data type and correcting it.
  * Removing second column created with time as do not need it for any analysis.

### Date Calendar Creation:
  * Creating a date calender with the help of new query from Home > New Source > Other Source > Blank Query.
  * DAX Formula : =list.dates(#date(2023,01,01), 371, #duration(1,0,0,0))
  * 2023,01,01 -
  * 731 -
  * 1,0,0,0

  * With To Table option under new Transofrm Tab, converted the Date Calender List Into a table and change name of the column along with given Date Calender name to the Query/Table.
  * Corrected the Data Type for the column.
  * Close and Load To option used to Create Data Connection and Add it to Data model.
  * Created connection between both the tables through Manage Data Model under Data and Diagram View.

### Name Column Merging:

  * Selected both the columns (FName and LName) and chose option Merge Column from Transform Tab.
  * Chose Customer from Seperator dropdown and used . space in the blank cell to get H. Hammilton format.
  * Checkd and corrected the data time and gave name to the column.

### Gender Coluam Normalisation:
 
  * Seplaced M & F with Male and Female by using Replace Value option from Transform tab.

### Patient Age Group Creation:
 
  * Created new column by using Conditional Column option from Add Column tab (If and Else).

### Patient Admision Correction:

  * Replaced True to Admitted and False to Not Admitted by using Replace Value under Transform Tab post converting the data type Boolean to Text.

### New Waittime categorisation:

   * Used Customer Column option under Add Column and created the categorisation.
   * Checked the data type and named the column.
  
### Duplicate Column:

   * Removed duplicate Patient Admission Flag column by Removed Column option under the Home Tab.
  
## Exploratory Data Analysis

1. Created Pivot Table from Data Model.
2. Put all the tables in the Details Sheet along with all the charts.


## Dashboard Layout Creation

1. Page zoom braught to 100%.
2. Removed the gridlines.
3. Gave dark colour to the background to use light coloured shape.

## Dashboard
  


   
