# Project Title: Data Transformation using Python
The data set that is provided for this assignment shows the video game sales for different years, genre, platform and locations. The focus is to analyse the average global sales before and after 2005.  The format of the data set is csv and the analysis is done using Python and is also used to modify the database. 

## Getting Started

### Objective

There are a total of 4 objectives of this assignment which are described below. The task is to perform using video game sales in 2016 data and using Python  to perform data transformation. 

1)	To analyse the video game sales in 2016 database and identify whether the average of global sales was higher before or after 2005 using Python and creating a link between Python and SQL.
2)	To create a new column that labels records before 2005 as ‘pre-2005’ and after 2005 as  ‘post-2005’.
3)	To create a 1-page report about the reasoning of the task performed in above two points and stating if any challenges faced.
4)	To prepare a log file of the work done representing the contributions of each team member. 

### Pre requisites

Connection of python query to SQL Database using sqlachemy package

### Installing 

The following packages will be required to perfrom the analysis:

``` python
import pandas as pd
from sqlalchemy import create_engine
import pymysql
``` 

## Performing Analysis

The code mentioned below was used to perform the analysis:

Reading Dataset :

``` python
df = pd.read_sql("SELECT * FROM world.`vgsales-2016`", conn)
```

1.	Was the average of global sales higher before or after 2005 ?

``` python
# Getting sales pre and post 2005 in pything using where, group by and case in python
avg_sales_segregation = pd.read_sql('''
            select 2005_segregation,avg(Global_Sales) as avg_sales 
            from (select Global_Sales,
                  case when Year_of_Release < 2005 then 'Pre_2005' else 'Post_2005'
                  end as 2005_Segregation from world.`vgsales-2016`) as sub_query 
            group by 2005_segregation
            order by 1 desc''', conn);
print(avg_sales_segregation)
```

2.	Create a new column that labels records before 2005 as 'pre-2005' and after 2005 as 'post-2005'
``` python
#Modifying the table to add the column that labels record before 2005 as pre_2005 and after 2005 as post_2005
Modified_vg_sales = pd.read_sql('''select *,
                  case when Year_of_Release < 2005 then 'Pre_2005' else 'Post_2005'
                  end as 2005_Segregation from world.`vgsales-2016`''', conn);
print(Modified_vg_sales.head())
```

## Author
**Avish Shah**
