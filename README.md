# Data Analyst Internship Assessment
This repository contains the [excel file](https://github.com/zinnydigits/internship-assessment/blob/main/excel.xlsx) , [power bi file](https://github.com/zinnydigits/internship-assessment/blob/main/powerbi.pbix) and [SQL codes & output](https://github.com/zinnydigits/internship-assessment/blob/main/sql.ipynb) (in a jupyter notebook) which are my submissions for a data analyst internship role.

Go to:

[Excel Assessment](#excel-assessment)

[Power BI Assessment](#power-bi-assessment)

[SQL Assessment](#sql-assessment)

## Excel Assessment
### Task 1:
Extract all the headers below from the data in column A. Please note that they are separated with"_".  The data in COLUMN D-G contains all the Data you need to answer Task 2-Task 6
>>>>> DO NOT USE TEXT TO COLUMN INSTEAD USE FORMULA TO EXTRACT

Excel Formulas Used for Extraction:
```
=LEFT(A5, FIND("_", A5) - 1)
=TEXT(MID(A5, FIND("_", A5) + 1, FIND("_", A5, FIND("_", A5) + 1) - FIND("_", A5) - 1), "mmmm-yy")
=MID(A5, FIND("_", A5, FIND("_", A5) + 1) + 1, FIND("_", A5, FIND("_", A5, FIND("_", A5) + 1) + 1) - FIND("_", A5, FIND("_", A5) + 1) - 1)
=VALUE(RIGHT(A5, LEN(A5) - FIND("_", A5, FIND("_", A5, FIND("_", A5) + 1) + 1)))
```
### Task 2:
What is the total transaction Value for each of these customers in each month? 
Use advanced filtering to extract unique customer_id, next:
```
=SUMIFS($G$4:$G$35546,  $D$4:$D$35546,  J4, $E$4:$E$35546, "May-20")
=SUMIFS($G$4:$G$35546,  $D$4:$D$35546,  J4, $E$4:$E$35546, "June-20")
=SUMIFS($G$4:$G$35546,  $D$4:$D$35546,  J4, $E$4:$E$35546, "July-20")
```
Find the average for each customer across the 3 months? 
```
=AVERAGE(J4:M4)
```
What is the Total sum for each customer across the 3months?
```
=SUM(K4:M4)
```
### Task 3:
BASED ON THE AVERAGE VALUE YOU CALCULATED IN TASK 1,
CLASSIFY EACH CUSTOMERS INTO THE DIFFERENT 4 CATEGORIES IN TASK 3. 
(To avoid spelling mistakes, reference the categories in task 3. DO NOT TYPE BEST CUSTOMER, GOOD CUSTOMER, AVERAGE CUSTOMER & POOR CUSTOMER).                                                                                                           If the customer average value is above 1.5million, BEST CUSTOMER. 
If the average value is between 1million and 1.5million, GOOD CUSTOMER. 
If the customer transaction value is less than 1million but above 500k, AVERAGE CUSTOMER. 
All customers from 500k and below are "POOR CUSTOMERS".

```
=IF(N4>1500000,"BEST CUSTOMER",
IF(N4>=1000000, "GOOD CUSTOMER",
IF(N4>500000, "AVERAGE CUSTOMER",
"POOR CUSTOMER")))
```
### Task 4
How many customers from Task 2 fall into each category?
```
=COUNTIF(S4:S35546, V4)
```
### Task 5
How many times did each of these customers did a transaction in each month?
Use Advanced Filtering to get the unique customer_id once again
```
=COUNTIFS($D$4:$D$35546,  Z4, $E$4:$E$35546, "May-20")
=COUNTIFS($D$4:$D$35546,  Z4, $E$4:$E$35546, "June-20")
=COUNTIFS($D$4:$D$35546,  Z4, $E$4:$E$35546, "July-20")
```
### Task 6
Using Vlookup, from Task 2, what category does the customer with the Customer ID ''"&AG3&"'' fall into?
```
=VLOOKUP("1fc2-413a", R:S, 2, FALSE)
```
### Task 7
Clean up the date. Using the first one below as example, the right format that excel will recognize is 2020-05-27 23:53:39 as it is in this format of "year-month-day hours:min:sec"
>>>>>Don't Use Text to Column, Use Functions only.
```
=TEXT(SUBSTITUTE(SUBSTITUTE(LEFT(AL4, 19), "T", " "), "Z", ""), "yyyy-mm-dd hh:mm:ss")
```
## Power BI Assessment
![Employees Dashboard](https://github.com/zinnydigits/internship-assessment/blob/main/powerbi.PNG)
### Data Preparation
#### ETL Process:
- The dataset was imported and transformed using Power Query to prepare it for analysis.
#### Data Cleaning:
- **Handling Null Values:** The `Previous_Year_Rating` column had some null values, which were addressed by replacing them with the mean rating of all employees.
#### Columns Modifications:
- Education: Standardized the value `bsc` to `Bachelors`.
- Gender: Replaced `Fem` with `Female` and `M` with `Male`. The column was formatted to capitalize each word.
- Renamed `Recruitment_Channell` to `Recruitment_Channel`.
- Renamed `FT/PT` to `Full/Part_Time` for clarity. Additionally, replaced the values `FT` and `PT` with `Full Time` and `Part Time`, respectively.
- KPIs_met > 80%: Converted the column’s data type from WHOLE NUMBER to TEXT and replaced values `1` and `0` with `Yes` and `No`, respectively. The same transformation was applied to the `awards_won` column.
#### New Column: 
Career Stage: Added a conditional column to categorize employees by career stage:
- **20-30:** Early Career
- **31-40:** Mid Career
- **41-50:** Senior Career
- **50-60:** Near Retirement
#### Visualizations:
- **Bar Chart:** Displays top 3 employee locations, age demographics, educational levels, and work status breakdown (Part Time/Full Time).
- **Clustered Bar Chart:** Shows KPI success by department with `KPI Value` (`Yes` or `No`) as the legend.
- **Text Box:** Added for the dashboard title.
- **Single Cards:** Show total number of employees, average age of employees, and average years of service.
- **Gauge Chart:** Visualizes the average rating and average score.
- **Pie Chart:** Illustrates gender distribution, KPI success, awards won, and recruitment by channels.
#### Recommendations:
1. **Employee Development:** Implement targeted training programs, especially for departments with lower KPI success rates, to improve overall performance.
2. **Gender Diversity Initiatives:** Given the gender distribution, consider initiatives that promote gender diversity, particularly in departments or roles where there is an imbalance.
3. **Retention Strategies:** For employees in the near-retirement stage, develop retention strategies that utilize their experience while planning for succession.
4. **Continuous Monitoring:** Regularly update and monitor key metrics such as employee satisfaction, KPI success, and awards won to ensure ongoing improvement and alignment with company goals.
5. **Transportation Support:** Based on the top employee locations, consider providing a company bus service to reduce transportation challenges and improve punctuality and employee satisfaction. This can also be an incentive in recruitment and retention, especially for those commuting from distant locations.

## SQL Assessment
Postgre database was connected to Jupyter Notebook for this task. The SQL codes used and output is available [here](https://github.com/zinnydigits/internship-assessment/blob/main/sql.ipynb). The notebook contains codes for tables creation, insertion of values and queries for the analysis.
