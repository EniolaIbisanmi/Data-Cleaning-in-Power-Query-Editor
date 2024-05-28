# Data-Cleaning-in-Power-Query-Editor

# DATA CLEANING : FIFA 2021

![FIFA Image](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/182f9e05-e52b-4d31-9620-9df31686c7f1) 

## Introduction 

Every data analysis project starts with collecting relevant datasets. These datasets often contain errors that result in incorrect calculations and interpretations when carrying out analyses. Using error-filled datasets can skew analysis results and should be avoided at all costs.

In this project, I will use the Microsoft Power Query Editor available in Excel and Power BI to clean a messy FIFA 21 dataset downloaded from Kaggle. I will remove special characters, irrelevant columns, extra spaces, and incorrect data types, and modify the dataset for further analysis. All steps taken to correct the errors will be well documented [here](https://www.kaggle.com/datasets/yagunnersya/fifa-21-messy-raw-dataset-for-cleaning-exploring). The dataset also comes with a data dictionary that helps to understand the data for more seamless data cleansing.

## Overview of the Dataset

The FIFA 21 dataset is a compilation of the details of the world's best football players. It contains their profile information and performance evaluations. It was downloaded from Kaggle, originally sourced from https://sofifa.com via web scraping. The data has 18,979 rows and 77 columns, containing information about 18,979 players and their attributes: Unique ID, Names, Wages, Value, Contracts, and others.


## Objective

The objective of this data cleaning project is to perform data cleaning procedures on the FIFA 21 dataset to ensure clean and well-structured data. Issues like missing data, spelling mistakes, incorrect measurements, duplicate values, null values, wrong data types, and other data problems will be resolved.


## 1. Data Exploration

The data was extracted from a zipped folder and imported into Microsoft Power Query Editor via the ‘Get Data’ ribbon. After a successful upload, I previewed the first 200 rows to familiarize myself with the raw data. I noticed special characters in the Name, Club, Value, Wage, Release Clause, W/F, SM, A/W, D/W, and IR columns. To improve data quality, I changed the file origin to Unicode (UTF-8) encoding to eradicate the characters. I loaded the data and trimmed it to remove extra spaces.

![Data Exploration](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/61c528ce-d1e7-430c-bdd8-48559579ced1) 
Before cleaning

## 2. Data Transformation

 Special Characters

Despite changing the encoding of the data to remove special characters, an error still showed in one of the names in the Name and LongName columns. I researched the correct spelling and removed the error.
 
![Special character before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/9f66fc9a-7820-4ee3-aa31-92327e576e65) 

 Special Character before

![Special character after](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/2dc565ce-6c52-4181-934c-bc19ade6a4d6)

Special Character after

## 3.Data Cleaning

#### 1. Duplicates

The relevant columns, ID and Name, were used to check for duplicates. The data did not contain duplicates. I converted the ID column into text to avoid summation in that column. 
However, the Name and LongName columns are in their correct data types; I renamed them for better appearance.
  
#### 2. Contract column

 The Contract column had a mix of data types. The relevant data needed to be extracted for further analysis. I created a conditional column to form a new column called ‘Contract     
 Status’ to categorize the contracts into ‘Loan’, ‘Free’, and ‘Contract’. To further clean the Contract column, I split the column with the ‘~’ delimiter to form two new columns ‘ 
 Contract Start’ and ‘Contract End’. I replaced the errors in the Contract Start column with ‘null’. After that was done, I finally changed the data type to text.

![Contract Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query/assets/130236779/0d721643-7600-426f-b08a-de3e0c33ca64)

Contract column before

![Contract Start and End](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/f8c836f9-c257-43a8-9a03-415b02f0cff8)

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
   
![Height condition](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query/assets/130236779/55912260-bbc3-4ba8-ae67-3a807d121395)
 
Height condition 1

![Height condition 2](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query/assets/130236779/41ff8fd9-55a9-40bd-b36c-b93d8bf2a988)

Height condition 2

![Height Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/6c727486-1182-4696-b6e3-8f4cb37316a6) 

Height column before

![Height After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/d4713132-15e9-4a6b-b1f7-f65c342f5541)

Height column after

#### 4. Weight Column
This column is measured in kg and lbs. I had to convert the entire column to lbs. To achieve this, I created a conditional column to multiply the data measured in kg by 2.205 in order to convert it into lbs. 

![Weight Condition](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query/assets/130236779/99e7ae13-b690-4883-9237-b42244e693b4)

Weight column condition

![Weight Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/d264298c-e7e3-4ba3-9a4e-f189e3a4bf82)  

Weight coulmn before

![Weight After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/5e66fe46-a182-458e-85b9-782557b1eaed)

Weight column after


#### 5. Value, Wage, and Release Clause Columns

These columns are measured in thousands (K) and millions (M) and have to be converted into figures. The currency sign (€) has to be removed. I removed the € sign and created a conditional column named ‘Multiply’:
* If ‘Value’ ends with ‘K’ output 1000
* If ‘Value’ ends with ‘M’ output 1000000
* Else output 1
After that, I removed the ‘K’ and ‘M’ to multiply the column by the Value column. I repeated the same procedures for the Wage and Release Clause columns.

![Value Column conditional statement](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/6d469cdc-cb8b-4cac-b473-5b744bd9371a)

Value column condition

![Wages, Value and Release column Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query/assets/130236779/19bb544c-90a3-4df2-ba1e-f57b8b2a03d9)

Wage, Value and Release column before

![Value, Wage and Release Clause After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/ef5ec1e6-6787-47da-864b-a71c44bbf6d4)

Wage, Value and Release column After


#### 6. Hits Column
The data in the Hits column was stored as text and some numbers had ‘K’ at the end and needed to be converted into thousands. I created a conditional column to address this issue:
* If ‘Hits’ ends with ‘K’ output 1000
* Else output 1

![Hits Column Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query/assets/130236779/4b392d07-8239-463b-90f6-8a3e4ec5292a)

Hits column before


![Hits column After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/d3d816b6-7790-4a6f-9790-3f3b3d7164a5)

Hits column after

#### 7. OVA, POT, and BOV Columns

It was observed that these columns had the wrong data type. According to the FIFA dataset dictionary, it should be in percentage. I changed the data type to whole number and created a custom column to divide the numbers by 100.

![OVA and POT Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/80ecc79a-35c0-4ff0-b0c6-29b4d2bd277e)       

OVA and POT before

#### 8. IR, SM, and W/F Columns

These columns contain a star character. I used Replace Values to remove the character and changed the data type to whole number.

![IR,SM AND WF Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Power-Query/assets/130236779/4f044c97-5e92-4a27-8efb-152e5429eca3)
    
IR,SM and W/F coulmn before

![IR,SM and WF After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/3486c3de-b23d-47f9-80ef-8d813d26832e)

IR,SM and W/F coulmn before

##### 9. Loan Date End Column

The blanks in this column were replaced with ‘No Loan’.

![Loan End Date Before](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/b021ef5c-9441-473f-889f-179c0c8db367)     

Loan End Date Before


![Loan End Date After](https://github.com/EniolaIbisanmi/Data-Cleaning-in-Excel/assets/130236779/cf4e6918-acac-4d59-b777-f8549f7d5693)

Loan End Date after

# Conclusion

Cleaning this FIFA 21 dataset shows that too many errors can be embedded in datasets and can end up disrupting the data analysis process. It can lead to incorrect calculations and interpretations. This highlights the importance of data cleaning as it prepares the data for further exploration and analysis. Data cleaning remains a crucial stage in any data analysis project. Here is the Thank you for reading!















































































































































