# Customer-segmentation-Interactive-Dashboard
## **Project-Overview**
#### This report categorizes customers into various segments based on factors such as gender, family size, income, and more. It then assesses the purchasing performance of each group.
![cus_seg_darktheme](https://github.com/alexazuog/Customer-segmentation-Interactive-Dashbord/assets/115574934/f183bffa-809a-4d98-9650-d51bb7f24c0a)

## **Switch to Light Theme**
![Customer_seg_lighttheme](https://github.com/alexazuog/Customer-segmentation-Interactive-Dashbord/assets/115574934/b97a2dd4-5e24-4f90-80b8-2edfec7d0e01)


## **Understanding The Data-set**
#### The data set contains records of customers' such as names, dates of birth, country, order details, income level, etc.

## **Data Cleaning Process** 
- Data was exported to power query for data cleaning. 
- The column quality was checked to assess for duplicates and missing or null values. 
- Some columns were created to give the data context better. For example
- The Age category column was created  to identify which age category a customer belongs to. 
- The Full name was created column by merging the two columns that contain the last names and first names.
## **Exploratory Data Analysis**
Using Dax / Calculated Column to create some important measures that could be used as  metrics in the visualization and also to give more perspective to the data
### *Total Transactions*
``` dax
  COUNTROWS(FactInternetSales)
```

### *Total Revenue From Males* 
```dax
CALCULATE([Total Revenue],
DimCustomer[Gender] = "M"
)
```
### *Total Revenue From Females* 
```dax
  CALCULATE(
    AVERAGE('dataset'[patient_sat_score]),'dataset'[patient_sat_score]<>BLANK())
```
### *%_non_responders (PERCENTAGE OF PATIENT THAT DID NOT RESPOND TO THE SURVEY)* 
```dax
   VAR no_rating = 
      CALCULATE([Total_Patients],'dataset'[patient_sat_score]=BLANK()
      RETURN
      DIVIDE(no_rating,[Total_Patients])
```
    	
### *Created a calculated column of different patient age bucket*
```dax
  SWITCH(
          TRUE(),
          'Hospital ER'[patient_age]<=10,"0-10",
          'Hospital ER'[patient_age]<=20,"11-20",
          'Hospital ER'[patient_age]<=30,"21-30",
          'Hospital ER'[patient_age]<=40,"31-40",
          'Hospital ER'[patient_age]<=50,"41-50",
          'Hospital ER'[patient_age]<=60,"51-60",
          'Hospital ER'[patient_age]<=70,"61-70",
```

### *Created another column to depict whether the visit  was a weekday or weekend*
```dax
  Addcolumn(calenderauto(),
  			"YEAR",YEAR([Date]),
  "MONTH",FORMAT([Date],"mmm"),
  "MonthNum",MONTH([Date]),
  "WeekType", IF(WEEKDAY([Date]) = 1, "Weekend", IF(WEEKDAY([Date])= 7, "Weekend", "WeekDay")),
  "WeekDay",FORMAT([Date],"ddd")
  )
```
### *Calculated a measure for %_patients that was not referred by any department*   
```dax
   var _filteredPatients = 
   CALCULATE([Total_Patients],
  'Hospital ER'[department_referral]="none")

```

### The following data model illustrates the one-to-many relationship between the fact table and the dimension table.

![cus_seg_data model](https://github.com/alexazuog/Customer-segmentation-Interactive-Dashbord/assets/115574934/fdbc8e3c-9a93-404a-9362-9d6331f68e7a)





