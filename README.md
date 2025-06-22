# Hospital-Emergency-Room-Analysis

# Purpose

We need to creat a hospital emergency room analysis dashboard. This dashboard will help stakeholders to monitor, analise and improve hospital services. 

# KPIs

Primary
1. Number of Patients: Total number of visits to the ER everyday.
2. Average Wait Time: Find the average wait time to attend the patient.
3. Patient Satisfaction Score: Find average satisfaction score to access the service quality.

Secondry
1. Patient admission status: how many were admitted vs not admitted.
2. Patient age distribution: Goupe patients age for the age wise analysis.
3. Wait time analysis: Howmany paitents were attended with 30mints and beyond.
4. Gender Analysis: Number of patients based on gender (Male/Female).
5. Department Referrals: Which department referred maximum referrals.

# Raw Data

1. The data was downloaded from
2. The file has 11 columns and 9217 rows including the header.

# Observation

1. Patients Date column had date and time together. As we do not have any use of time as per the KIP, will split and remove the time.
2. Patient first name column just has name innitials along with a seperate column with the last name. Hence, will merge them for easy use.
3. Patient gender column needs normalisation as it has inconsistant values like Male, Female, M, and F.
4. Patient age column must have another column with the age group as per the KPI requirement.
5. Patient admission flag columns has test values line True/Fales that needs to be convertend into admitted or not admitted.
6. Patients wait time column must have another column indicating how many of them were attended within 30mints and beyond for the KPI analysis.
7. Patient wait time column as a duplicate column which must be removed.
8. Department referral column has "None" values that neither be pupulated nor can be removed. Hence, keeping them as is.
9. Patient satisfaction score column has blank cells too which neither be populated nor deleted. Hence, keeping it as is. 

# Data Loading

1. Importing the CSV file through Data Tab > Get Data> From File > From Text/CSV.
2. Check the details in Navigator Box and Transform Data to cleaning and preperation.

# Data Cleaning And Transformation

1. Error and Column Quality:

  * Checkign for errors and correcting them with the Column Quality Option under the View Tab.
  * Found Empty in Patient Satisfaction Score column.
  * Not removing them as we need both the data. 
   
2. Patient Admission Date Column:

  * Splitting Patient Admission Date column into two with date and time seperately. 
  * Select Column > Transform Tab > Split Column > By Delimeter > Select - Customer - Space (as the delimeter between date and time is space), Split At - Each Occurance of the  Delimeter.
  * Checking the data type and correcting it.
  * Removing second column created with time as do not need it for any analysis.

3. Date Calendar Creation:
  * Creating a date calender with the help of new query from Home > New Source > Other Source > Blank Query.
  * DAX Formula : =list.dates(#date(2023,01,01), 371, #duration(1,0,0,0))
  * 2023,01,01 -
  * 731 -
  * 1,0,0,0

  * With To Table option under new Transofrm Tab, converted the Date Calender List Into a table and change name of the column along with given Date Calender name to the Query/Table.
  * Corrected the Data Type for the column.
  * Close and Load To option used to Create Data Connection and Add it to Data model.
  * Created connection between both the tables through Manage Data Model under Data and Diagram View.

4. Name Column Merging:

  * Selected both the columns (FName and LName) and chose option Merge Column from Transform Tab.
  * Chose Customer from Seperator dropdown and used . space in the blank cell to get H. Hammilton format.
  * Checkd and corrected the data time and gave name to the column.

5. Gender Coluam Normalisation:
 
  * Seplaced M & F with Male and Female by using Replace Value option from Transform tab.

6. Patient Age Group Creation:
 
  * Created new column by using Conditional Column option from Add Column tab (If and Else).

7. Patient Admision Correction:

  * Replaced True to Admitted and False to Not Admitted by using Replace Value under Transform Tab post converting the data type Boolean to Text.

8. New Waittime categorisation:

   * Used Customer Column option under Add Column and created the categorisation.
   * Checked the data type and named the column.
  
9. Duplicate Column:

   * Removed duplicate Patient Admission Flag column by Removed Column option under the Home Tab.
  
# EDA (Exploratory Data Analysis)

1. Created Pivot Table from Data Model.
2. Put all the tables in the Details Sheet along with all the charts.


# Dashboard Layout Creation

1. Page zoom braught to 100%.
2. Removed the gridlines.
3. Gave dark colour to the background to use light coloured shape.


  


   
