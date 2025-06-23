# Hospital Emergency Room Analysis

## The Table Of Contents

- [Purpose](#purpose)
- [Performance Indicators](#performance-indicators)
- [Data Overview](#data-overview)
- [Initial Data Observations](#initial-data-observations)
- [Data Loading](#data-loading)
- [Data Cleaning And Transformation](#data-cleaning-and-transformation)
- [Data Exploration And Key Insights](#data-exploration-and-key-insights)
- [Dashboard Creation](#dashboard-creation)


## Purpose


In the high-pressure setting of a hospital emergency room, data-driven decisions can mean the difference between delay and decisive action. This project delivers a fully interactive analytics dashboard built exclusively in Microsoft Excel, using a powerful combination of Power Query, Power Pivot, DAX formulas, and PivotTables to uncover insights into patient flow, wait times, and service quality.

Designed with hospital decision-makers in mind, the dashboard transforms raw, unstructured data into a clear, filterable interface—supporting smarter resource allocation, improved triage strategies, and a deeper understanding of patient experience. All features were developed using Excel's built-in capabilities, making this solution scalable and accessible without the need for external BI platforms.


## Performance Indicators


### Primary
   - **Patient Volume**: Total number of individuals visiting the ER each day.
   - **Average Wait Time**: Time elapsed between patient check-in and initial medical consultation.
   - **Patient Satisfaction Score**: Average satisfaction rating provided by the patients to access the service quality.

### Secondary
  - **Admission Status**: Breakdown of patients admitted versus not admitted.
  - **Age Distribution**: Grouped age ranges for demographic and clinical analysis.
  - **Wait Time Analysis**: Number of patients attended within 30 minutes versus those who waited longer.
  - **Gender Distribution**: Total patient count segmented by gender (Male/Female).
  - **Department Referrals**: Identification of departments generating the highest number of ER referrals.

## Data Overview

This project is based on a publicly available dataset sourced from this GitHub [repository](https://raw.githubusercontent.com/SatishDhawale/Hospital_Emergency_Room_Dashboard/refs/heads/main/Hospital%20Emergency%20Room%20Data.csv). The dataset contains 9,217 records and 11 columns, each representing key attributes of emergency room visits such as patient demographics, wait times, admission status, and satisfaction scores.

### Dataset Summary
 - Source: Original GitHub commit
 - Format: CSV (Comma-Separated Values)
 - Rows: 9,217 (including header)
 - Columns: 11
 - Time Period Covered: April 2023 to October 2024 (based on admission dates)


## Initial Data Observations


During the initial review of the raw dataset, several data quality and formatting issues were identified that required transformation for accurate analysis:

 - Date-Time Formatting: The Patient Admission Date column contained both date and time, though only the date is relevant for analysis.
 - Name Structure: The First Name column included only initials, while the Last Name column provided full surnames, split across two fields.
 - Gender Normalization: The Gender column had inconsistent formats such as “Male”, “M”, “Female”, and “F”.
 - Age Grouping: Patient ages were listed as raw numbers without age ranges needed for grouped demographic insights.
 - Admission Status: The Admission Flag column used Boolean values (“True”/“False”), which may not be easily interpretable.
 - Wait Time Categorization: There was no indication of whether patients were attended to within or beyond a specific time threshold, such as 30 minutes.
 - Duplicate Column: Two Wait Time columns were present, leading to redundancy.
 - Department Referrals: The Department Referral field included “None” entries, lacking clarity on whether these reflect valid missing data.
 - Satisfaction Scores: The Patient Satisfaction Score column included blank entries in multiple rows.



## Data Loading
 - The dataset was imported into Excel using the following path: Data tab → Get Data → From File → From Text/CSV.
 - In the Navigator window, the file preview was verified to ensure correct column alignment and data types.
 - The data was then loaded into Power Query Editor for cleaning and transformation before being added to the data model.


## Data Cleaning and Transformation


The dataset underwent several cleaning and transformation steps in Power Query to ensure consistency, accuracy, and alignment with the project’s KPIs:

- **Error and Column Quality Check**
  - Used the Column Quality feature under the View tab to identify errors and missing values.
  - Found blanks in the Patient Satisfaction Score column. These were retained to preserve data integrity.

- **Splitting Admission Date and Time**
  - The Patient Admission Date column contained both date and time.
  - Used: Transform tab → Split Column → By Delimiter → Custom delimiter: space → Split at each occurrence.
  - Removed the time column, as it was not required for analysis.

- **Date Calendar Creation**
  - Created a dynamic Date Calendar using a blank query: Home → New Source → Other Sources → Blank Query
  - Applied the formula:
    
  ```= List.Dates(#date(2023, 01, 01), 731, #duration(1, 0, 0, 0))```
  
  - #date(2023, 01, 01): Start date.
  - 731: Covers two full years (including leap year).
  - #duration(1, 0, 0, 0): Daily intervals.
  - Converted the list to a table using To Table under the Transform tab.
  - Renamed the column and query to Date Calendar, set the data type to Date.
  - Loaded it as a connection-only query and added it to the data model.
  - Created a relationship with the fact table using Manage Data Model in Diagram View.

- **Merging Name Columns**
  - Merged First Name and Last Name using: Transform tab → Merge Columns → Separator: Custom (. ) → Result: e.g., H. Hamilton
  - Renamed the new column to Full Name.

- **Gender Normalization**
  - Standardized inconsistent gender values (M, F, Male, Female) using Replace Values in the Transform tab.

- **Creating Age Groups**
  - Added a new column using Add Column → Conditional Column to group patients by age brackets.
    ![image](https://github.com/aslamshkh/Hospital-Emergency-Room-Analysis/blob/main/Conditional%20Column%20Creation.png)

- **Admission Status Formatting**
  - Converted the Admission Flag column from Boolean to Text.
  - Replaced True with Admitted and False with Not Admitted.

- **Wait Time Categorization**
  - Created a new column using Add Column → Custom Column to classify patients based on whether they were attended within or beyond 30 minutes.
    ![image](https://github.com/aslamshkh/Hospital-Emergency-Room-Analysis/blob/main/Waittime%20Categorisation.png)

- **Removing Duplicate Columns**
  - Identified and removed a duplicate Admission Flag column using Remove Columns under the Home tab.

 
## Data Exploration And Key Insights


After cleaning and transforming the dataset in Power Query, I used PivotTables built from the Power Pivot data model to explore core metrics related to patient flow, wait time efficiency, satisfaction, and referral patterns. These findings shaped the KPI selection and dashboard layout, turning raw observations into actionable insights.

### Key Insights

 - Patient Volume: A total of 9,216 emergency visits were recorded between April 2023 and October 2024. Daily traffic ranged from 20 to 45, reflecting steady ER utilization without major fluctuations.
 - Admission Trends: The patient distribution was nearly equal, with 50.04% admitted and 49.96% not admitted—indicating a balanced triage outcome.
 - Wait Time Distribution: About 62% of patients experienced delays, waiting over 30 minutes, while 38% were attended within 30 minutes. This points to potential efficiency gaps in initial patient intake.
 - Satisfaction Scores: Despite the wait times, the average patient satisfaction score remained high at 4.99, suggesting that care quality or communication may have positively influenced perception.
 - Demographic Breakdown:
 - Gender: Nearly even split 4,729 male and 4,487 female patients.
 - Age: The highest concentration of visits came from patients aged 60–79, aligning with common ER usage trends in older populations.
 - Referral Analysis: The most common referring departments were General Practice, Orthopedics, and Physiotherapy. A significant portion of entries were marked “None,” likely reflecting either self-referrals or missing documentation.



> [!WARNING]
> Some patients had recorded wait times exceeding 180 minutes, which might be considered unusually long. As this is an independently executed project with no external source verification, these values have been left untouched and are reported as-is for transparency.


## Dashboard Creation


The dashboard was built in Excel with a clean, high-contrast design for better readability and user interaction. Key formatting steps included:
 - Zoom set to 100% and gridlines removed for a streamlined view.
 - A dark background to highlight visuals and slicers.
 - Slicers for Gender, Age Group, Admission Status, and Department to enable quick filtering.

### Visual Overview
 - KPI Cards: Displayed patient volume, satisfaction, and wait time breakdown for instant insights.
 - Bar Charts: Showed patient count by age group and referral sources.
 - Stacked Columns: Compared admission rates across age groups.
 - Pie & Doughnut Charts: Illustrated gender split and wait time proportions.
 - Satisfaction Comparison: Highlighted how wait time affected patient feedback.

All visuals were arranged logically to guide the reader from big-picture metrics to deeper operational patterns.
  
   ![image](https://github.com/aslamshkh/Hospital-Emergency-Room-Analysis/blob/main/Dashboard%20Layout.png)

   ![image](https://github.com/aslamshkh/Hospital-Emergency-Room-Analysis/blob/main/Hospital%20Emergency%20Room%20Dashboard.png)


   
