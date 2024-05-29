# DATA CLEANING : FIFA 2021

![FIFA Image](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/5b7cb2c9-9754-4cfa-98fa-71566228e08d)

## Introduction 

Every data analysis project starts with collecting relevant datasets. These datasets often contain errors that result in incorrect calculations and interpretations when carrying out analyses. Using error-filled datasets can skew analysis results and should be avoided at all costs.

In this project, I will use the Microsoft Power Query Editor available in Excel and Power BI to clean a messy FIFA 21 dataset downloaded from Kaggle. I will remove special characters, irrelevant columns, extra spaces, and incorrect data types, and modify the dataset for further analysis. The link to the data source can be found [here](https://www.kaggle.com/datasets/yagunnersya/fifa-21-messy-raw-dataset-for-cleaning-exploring). The dataset also comes with a data dictionary to help understand the data for more seamless data cleansing.


## Overview of the Dataset

The FIFA 21 dataset is a compilation of the details of the world's best football players. It contains their profile information and performance evaluations. It was downloaded from Kaggle, originally sourced from https://sofifa.com via web scraping. The data has 18,979 rows and 77 columns, containing information about 18,979 players and their attributes: Unique ID, Names, Wages, Value, Contracts, and others.


## Objective

The objective of this data cleaning project is to perform data cleaning procedures on the FIFA 21 dataset to ensure clean and well-structured data. Issues like missing data, spelling mistakes, incorrect measurements, duplicate values, null values, wrong data types, and other data problems will be resolved.


## 1. Data Exploration

The data was extracted from a zipped folder and imported into Microsoft Power Query Editor via the ‘Get Data’ ribbon. After a successful upload, I previewed the first 200 rows to familiarize myself with the raw data. I noticed special characters in the Name, Club, Value, Wage, Release Clause, W/F, SM, A/W, D/W, and IR columns. To improve data quality, I changed the file origin to Unicode (UTF-8) encoding to eradicate the characters. I loaded the data and trimmed it to remove extra spaces.

![Data Exploration](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/0ec40d24-7874-4a91-8fb8-25f97b490e0e)

                                                          Before cleaning

## 2. Data Transformation

 Special Characters

Despite changing the encoding of the data to remove special characters, an error still showed in one of the names in the Name and LongName columns. I researched the correct spelling and removed the error.
 
![Special character before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/6d3a85f4-8450-45cc-b1e1-da17f7b312e6)

 Special Character before

![Special character after](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/57ebe2f9-76c4-4e4f-a0f2-524bb53f484a)

Special Character after

## 3.Data Cleaning

#### 1. Duplicates

The relevant columns, ID and Name, were used to check for duplicates. The data did not contain duplicates. I converted the ID column into text to avoid summation in that column. 
However, the Name and LongName columns are in their correct data types; I renamed them for better appearance.
  
#### 2. Contract column

 The Contract column had a mix of data types. The relevant data needed to be extracted for further analysis. I created a conditional column to form a new column called ‘Contract     
 Status’ to categorize the contracts into ‘Loan’, ‘Free’, and ‘Contract’. To further clean the Contract column, I split the column with the ‘~’ delimiter to form two new columns ‘ 
 Contract Start’ and ‘Contract End’. I replaced the errors in the Contract Start column with ‘null’. After that was done, I finally changed the data type to text.

![Contract Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/12c2426d-6538-4b48-aa35-90c02790e217)

Contract column before

![Contract Start and End](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/7b8156ab-7fa8-4d3d-869c-d086671955b4)

Contract column after

#### 3. Height column

 This column has data in three measurements - cm, feet, and inches. I decided to convert the ft and inches to cm for uniformity. Converting this data to one measurement involves using 
 conditional columns to set conditions for a seamless conversion. This involves using these steps:
 1. I split the Height column using the inverted comma (‘) delimiter to separate the inches from the feet and replaced the null values in Height.2 with zero (0).
 2. Next, I created a conditional column named ‘Multiply by 12’:
    * If ‘Height’ ends with ‘cm’ output ‘1’
    * Else output ‘12’
 3. Furthermore, I created another conditional column named ‘Divide by 0.3937’ to allow a final conversion into cm.
 4. I proceeded to replace the ‘cm’ in the Height.1 column with an empty space to enable its multiplication with the ‘Multiply by 12’ column in order to convert feet to inches. I had to 
 convert the data type to a whole number to achieve this. Thereafter, I added this new column with the Height.2 column using a custom column.
 5. Finally, I divided this new column by ‘Divide by 0.3937’ using a custom column to achieve this.
   
![Height condition](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/5b2f2cef-61c1-4135-a9ee-93d2042ef895)

Height condition 1

![Height condition 2](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/7c34a128-55f2-4f79-998b-06268dd7e4db)

Height condition 2

![Height Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/2f065c31-5336-4050-8532-2df6cd68e51f)

Height column before

![Height After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/03df6592-6c91-4cb5-9a89-b3055a7b7a93)

Height column after

#### 4. Weight Column
This column is measured in kg and lbs. I had to convert the entire column to lbs. To achieve this, I created a conditional column to multiply the data measured in kg by 2.205 in order to convert it into lbs. 

![Weight Condition](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/42275cc9-8d2b-4960-b847-94f0f2c1e464)

Weight column condition

![Weight Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/66610315-a16c-48f8-a835-e31491db0027)

Weight coulmn before

![Weight After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/7c83a091-de27-4681-b4a3-67eefe3d4813)

Weight column after

#### 5. Value, Wage, and Release Clause Columns

These columns are measured in thousands (K) and millions (M) and have to be converted into figures. The currency sign (€) has to be removed. I removed the € sign and created a conditional column named ‘Multiply’:
* If ‘Value’ ends with ‘K’ output 1000
* If ‘Value’ ends with ‘M’ output 1000000
* Else output 1
After that, I removed the ‘K’ and ‘M’ to multiply the column by the Value column. I repeated the same procedures for the Wage and Release Clause columns.

![Value Column conditional statement](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/cafbf891-9ef3-4882-87dd-f93adbfdd766)

Value column condition

![Wages, Value and Release column Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/a1b7d75c-15c8-42d5-a6c2-fc12913a605f)

Wage, Value and Release column before

![Value, Wage and Release Clause After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/3d5f25e6-8234-4bc6-85a5-f40de30cb71e)

#### 6. Hits Column
The data in the Hits column was stored as text and some numbers had ‘K’ at the end and needed to be converted into thousands. I created a conditional column to address this issue:
* If ‘Hits’ ends with ‘K’ output 1000
* Else output 1

![Hits Column Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/a6f55ddd-41eb-4538-b54e-66a9f30d7127)

Hits column before


![Hits column After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/245ec015-1f3d-4778-ae1d-4e07590abcd8)

Hits column after

#### 7. OVA, POT, and BOV Columns

It was observed that these columns had the wrong data type. According to the FIFA dataset dictionary, it should be in percentage. I changed the data type to whole number and created a custom column to divide the numbers by 100.

![OVA and POT Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/a5bdf6f0-8d19-4522-b53f-d3c2f782c741)
 
OVA and POT before

![OVA and POT After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/3e710f40-24c6-496d-a8f3-510436bbd6d0)

OVA and POT after

#### 8. IR, SM, and W/F Columns

These columns contain a star character. I used Replace Values to remove the character and changed the data type to whole number.

![IR,SM AND WF Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/c8758f78-ade1-4fc7-a924-6b4f292b7bc0)
    
IR,SM and W/F coulmn before

![IR,SM and WF After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/09036bf6-564e-4474-9748-58716e8ff397)

IR,SM and W/F coulmn after

##### 9. Loan Date End Column

The blanks in this column were replaced with ‘No Loan’.

![Loan End Date Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/55fbd200-70a2-446b-942f-153657502597)
    
Loan End Date Before

![Loan End Date After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query-Editor/assets/130236779/abf36f80-0b7f-42ca-abf4-0f8b9744e8a4)

Loan End Date after

# Conclusion

Cleaning this FIFA 21 dataset shows that too many errors can be embedded in datasets and can end up disrupting the data analysis process. It can lead to incorrect calculations and interpretations. This highlights the importance of data cleaning as it prepares the data for further exploration and analysis. Data cleaning remains a crucial stage in any data analysis project. You can find the cleaned dataset [here](https://docs.google.com/spreadsheets/d/1kN1pKFUulugjFitUjh5-o-Q0VxcFbvKISR13rPA4zTs/edit?usp=sharing).Thank you for reading!














































