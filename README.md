# Healthcare Dashboard

### Dashboard Link : Will be updated soon

## Project Overview

This project involves the development of an end-to-end healthcare dashboard using Power BI. The focus is on managing and analyzing patient waiting list data (both Inpatient and Outpatient) from 2018 to 2021. The project includes identifying stakeholders, understanding business objectives, conducting a high-level data study, and defining the scope, such as documenting KPIs, timelines, and expectations.

## Problem Statement

The goal of this project is to provide a comprehensive view of the patient waiting list through various visualizations and analyses. Specifically, the objectives are to:

Track the current status of the patient waiting list.

Analyze historical monthly trends of the waiting list for Inpatient and Outpatient categories.

Perform detailed specialty-level and age profile analyses.

### Process

- Requirement Gathering
    - Identified key stakeholders.
    - Defined business objectives and expectations.
    - Documented KPIs and timelines.
- Data Collection & Cleaning
    - Collected data covering the period from 2018 to 2021.
    - Cleaned and prepared the data for analysis.
- Transformation and Modeling
    - Transformed the data using Power Query.
    - Created necessary data models to facilitate analysis.
- Visualization Blueprint
    - Designed a blueprint for the dashboard, detailing the visualizations and their placements.
- Layout and Design Workflow
    - Developed the layout and design for the dashboard.
    - Ensured a user-friendly interface and smooth navigation.
- Adding Interactivity and Navigation
    - Implemented interactive elements such as slicers and drill-down features.
    - Ensured seamless navigation across different views.

### Steps followed

- Step 1 : Load data into Power BI Desktop, dataset contains two different folders Inpatient and Outpatient. Each has four csv format excel files. So, loading the files using folder connector is optimal. Select 'Combine and load' to appear all data in ingle table
- Step 2 : Transform the data. Ensure both data having same number of columns.
    - Update the 'Specialty_Name' column name in outpatient data to match the columns in inpatient data
    - Add column 'Case_type' after the 'Specialty_Name' column in outpatient data  
- Step 3 : Combine both tables into single table. Append the table and rename it as 'All_Data' and save the changes.
- Step 4 : Since tables are appended, in Model view, hide the Inpatient and Outpatient data table. 
- Step 5 : It is better to map table which has large number of Specialties into a certain Specialty_Group. Load the Mapped document in the name of Mapping_Specialty as well.   
- Step 6 : In Model view, ensure that All_data and Mapping_Specialty are linked. Else, link the table by dragging Specialty_Name from All-All_Data to Mapping_Specialty.
- Step 7 : Design the blueprint based on the problem statement. 
- Step 8 : Dashboard Layout and Design.
- Step 9 : Create Total wait list of current month vs. same month previous year using Card visualization. Creating measures using DAX query to get the values on two cards.
    - Query 1 : Latest Month Wait List = CALCULATE(SUM(All_Data),All_Data[Archive_Date] = MAX(All_Data[Archive_Date])) + 0
    - Query 2 : PY Latest Month Wait List = CALCULATE(SUM(All_Data),All_Data[Archive_Date] = EDATE(MAX(All_Data[Archive_Date]),-12) + 0

   ![Card-TWL_comparison](https://github.com/user-attachments/assets/fad40551-ba13-4b3e-883a-b61182be6311)

- Step 10 : Creating two metrics Average and Median in the same chart, able to toggle on both for Dynamic Measures.
    - Create a blank table which will host the value of the metrics (Avg & Median) in the name of 'Calcumation Method'. Table contains a column Header Calc Method and values will be 'Average' and 'Median'
    - Use Slicer, select the 'Calculation Method' and change the style as 'tile'. Turn off the slicer header. Turn on the Single Select in the Selection.
    - Query 1: Average Wait List = AVERAGE(All_Data[Total])
    - Query 2: Median Wait List = MEDIAN(All_Data[Total])
    - Query 3: Avg/Med Wait List = SWITCH(VALUES('Calculation Method'[Calc Method]),'Average',[Average Wait List], 'Median', [Median Wait List])

    ![Avg_Med_slicer](https://github.com/user-attachments/assets/81d97393-d91a-4f67-8163-300ca55c405f)

- Step 11 : Create a Donut Chart with 'Case_type' in Legend and 'Avg/Med Wait List' in Values. (Verify: Toggle the Average and Median slicer and check the output is interactive)

    ![Case_type](https://github.com/user-attachments/assets/98fd7044-09c2-4521-895d-6ad0787f9157)

- Step 12 : Create a Stacked column chart with Time_Bands in X-axis, 'Avg/Med Wait List' in Y-axis, Age_profile in the Legend.
    - Found some duplicates in the 'Time_Bands' so go to transform data and make it as unique. Also, alter the blanks with 'No Input' in both 'Time_Bands' & 'Age_profile' columns. Save the changes.
    - Within Filters > Time_Bands & Age_profile unselect the 'No Input' value.

    ![Time_Band_Age_Profile](https://github.com/user-attachments/assets/484c7642-1556-4162-935b-a87d961a6800)

- Step 13 : Creating Top Specialty Grid. Use Multi-Row card with 'Specialty_Name' & 'Avg/Med Wait List' in Fields. Within Filters > Filter type > select 'Top N', Show Items as '5' and By Value as 'Avg/Med Wait List'. Apply filter.

    ![Top_5_specialty](https://github.com/user-attachments/assets/101865a0-08df-4b76-a688-96c4266d691c)

- Step 14 : Create two line charts. 
    - Chart 1: Is with Archive_Date in X-axis, Total in Y-axis, Case_type in Legend and filter with only Day Case and Inpatient
    - Chart 2: Is with Archive_Date in X-axis, Total in Y-axis, Case_type in Legend and filter with only Day Case and Outpatient

    ![Trend_Analysis](https://github.com/user-attachments/assets/e8d1a2c7-26be-447f-a783-d0bd935bf49b)

- Step 15: Create three slicers of Archive_Date, Case_type and Specialty_Name like the image shown below.

    ![Filters](https://github.com/user-attachments/assets/0b0ac18f-a2fb-4b24-8fab-bac85c6c5a5b)

- Step 16: Create New page in the name of 'Detail'
- Step 17: Copy the Archive_Date, Case_type and Specialty_Name slicers from the Summary page to this detail page and sync the views. And add two more slicers Age_profile and Time_Bands.

    ![Detail_filters](https://github.com/user-attachments/assets/34da2930-00e8-4f3a-b67f-0d4bb1651238)

- Step 18: Select the Matrix visualization, Archive_Date, Specialty_Name, Age_profile, Time_Bands in Rows. Case_type in Columns, Total in Values.

    ![Detail_table](https://github.com/user-attachments/assets/f7dd2222-4445-4274-b866-3940abdf1764)

- Step 19: Now, lets make the dashboard aesthetically pleasing. Design a creative dashbord. Refer the below dashboard.
    - Personal Creative Workflow,
        1. Draw inspiration from (Google images, Adobe stock images, etc.)
        2. Extract Themes or Colors using Adobe Colors
        3. Take Screenshot of the report
        4. Paste it in a PPT
        5. Design Power BI background using the colors from the reference image.
        6. After designing, extract the PPT slides as image
        7. Apply the image as a Canvas background image on Power BI. Format the charts accordingly.
- Step 20: Create a Overall Average and Median value for the Donut chart using cards with 'Avg/Med Wait List' as 'Overall' in Fields on summary page.
- Step 21: Provide the suitable title for the charts on summary page.
- Step 22: Create dynamic titles for Average & Median slicers using the Dax query.
    - Dynamic Title = Switch(VALUES('Calculation Method'[Calc Method]),'Average','Key Indicators - Patient Wait List (Average)','Median','Key Indicators - Patient Wait List (Median)')
- Step 23: Create a dynamic title using card with 'Dynamic Title' in Fields.
- Step 24: Disable the interactiviy of Case_type slicers on both line graphs, by selecting Froamt > Edit Interactions > None on respective for the slicer.
- Step 25: When selecting the Specialty_Name on the slicer, any one of the line graph will become empty. So, add a message using DAX query when it is blank.
    - NoData Left = if(ISBLANK(CALCULATE(SUM(All_Data[Total]), All_Data[Case_type]<>'Outpatient'), "No data for selected criteria","")
    - NoData Right = if(ISBLANK(CALCULATE(SUM(All_Data[Total]), All_Data[Case_type]='Outpatient'), "No data for selected criteria","")
    - Create cards using this measures NoData Left for left line graph and NoData Right for right line graph. Send the cards to the back of the line graphs. View > Selection > Drag the cards below to the graph.
- Step 26: Create a button to navigate from Summary page to Detail page and vise versa.
    - Navigate to Detail page: Insert > Add button > Select Information button
    - Format the button. Enable action, Action > Type - Page Navigation > Destination - Detail
    - Enable Tooltip. Within Text - 'Click here to view Detailed page'
    - Navigate to Summary page: Repeat the same process on Detail page and change the Destination - Summary

    ![Navigation_buttons](https://github.com/user-attachments/assets/f1bf3da4-b7b6-49d3-b5e4-489d75b22d62)

- Step 27: Lets create a Custom tooltip chart for the Summary page line graphs. Add one more page as DrillDown.
- Step 28: Within the page, add a Stacked Bar chart with Specialty_Group in Y-axis and Totals in X-axis. Also create a card for the same. Format the Charts as well. Visual settings for the page, Canvas setting > Type - Letter, Canvas Background > Image fit - Fit, Transparency > 0 %
- Step 29: Click on the canvas, select Fromat page > Page Information > enable Allow use as tooltip.
- Step 30: On Summary page, click the Left line graph and go to Format visual > Tooltips > Page - DrillDown

# Summary View (Power BI Desktop)

![Summary_page](https://github.com/user-attachments/assets/84d6b40d-17df-4bde-a38d-4e9314b00e07)

# Detailed View

![Detailed_page](https://github.com/user-attachments/assets/07fe158f-8d0d-4c2c-b732-01da0dd082e1)

## DrillDown Page

![DrillDown](https://github.com/user-attachments/assets/8d43bf59-b01e-4f67-9ca2-924c4016989b)


# Insights

A single page report was created on Power BI Desktop.

Following inferences can be drawn from the dashboard;

## [1] Total waiting list comparison

Total Number of Patient wiating list of Latest Month = 708729

Total Number of Patient wiating list of Previous year's Latest Month = 640441

## [2] Case Type Split

### Average of Case Type per month

Overall average of all type of cases = 54

Number of Outpatient on an Average = 80 (72%)

Number of Day case on an Average = 19 (17%)

Number of Inpatient on an Average = 12 (11%)

           thus, higher number of patient are Outpatient.

### Median of Case Type per month

Overall median of all type of cases = 13

Number of Outpatient on a Median = 29 (74%)

Number of Day case on a Median = 6 (16%)

Number of Inpatient on Average = 4 (10%)

           thus, the higher number of Case Type registered in a month is Outpatient.

## [3] Top 5 Specialty Cases

### Average

    1. Number of Accident & Emergency cases = 111
    2. Number of Paed Cardiology = 102
    3. Number of Paed Orthopaedic cases = 115
    4. Number of Paediatric Dermatology cases = 168
    5. Number of Paediatric ENT cases = 147 

### Median

    1. Number of Accident & Emergency cases = 70
    2. Number of Cardiology cases = 28
    3. Number of Clinical Genetics cases = 29
    4. Number of Dermatology cases = 35
    5. Number of Pain Releif cases = 27 
