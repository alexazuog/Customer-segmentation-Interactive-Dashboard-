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
 CALCULATE([Total Revenue],
DimCustomer[Gender] = "F"
)
```
### *Ranking Of Customers Base On Total Revenue* 
```dax
   var _topCustomers =
    RANKX(
        ALL('DimCustomer'[Full_Name]),[Total Revenue],
        ,DESC
    )
    RETURN 
        IF(
            _topCustomers <= 'Dynamic Cust'[Dynamic Cust Value],
            [Total Revenue]
        )
```
    	
### *Total Number Of Customers*
```dax
 DISTINCTCOUNT(DimCustomer[CustomerKey]) 
```

### *Total Quantity Ordered*
```dax
  sum(FactInternetSales[OrderQuantity])
```
### *Total Revenue*   
```dax
   SUMX(FactInternetSales, FactInternetSales[OrderQuantity] * RELATED(DimProduct[ListPrice]))

```

### The following data model illustrates the one-to-many relationship between the fact table and the dimension table.

![cus_seg_data model](https://github.com/alexazuog/Customer-segmentation-Interactive-Dashbord/assets/115574934/fdbc8e3c-9a93-404a-9362-9d6331f68e7a)





