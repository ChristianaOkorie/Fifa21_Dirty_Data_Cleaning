# Fifa21_Dirty_Data_Cleaning

![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/Data%20Cleaning%20image.jpg)

## Introduction
   #### Dirty data, or unclean data, is data that is in some way faulty: it might contain duplicates, or be outdated, insecure, incomplete, inaccurate, or inconsistent. Examples of dirty data include misspelled addresses, missing field values, outdated phone numbers, and duplicate customer records.
   #### According to Tableau, Data cleaning is the process that removes data that does not belong in your dataset. Data transformation is the process of converting data from one format or structure into another. Transformation processes can also be referred to as data wrangling, or data munging, transforming and mapping data from one "raw" data form into another format for warehousing and analyzing. This article focuses on the processes of cleaning that data.
   
## About Data
   #### The data set was gotten from Kaggle and it has 18,979 rows and 77 columns. It contains data of players Id, photoUrl, playerUrl, name, rating, their age, their nationality, the position that they play, their potentials for growth in game and so on.
## Data Claning Process
   #### I used the Microsoft Power BI for this data cleaning, First i imported the data as a CSV file and hit the transform button which brings up the Power Query. All unwanted filles were deleted, i checked for duplicated column and empty column and had them deleted. I renamed the columns that had abbreviated names.
### 1. Trimming column

Before Trim          |        After Trim
:-------------------:|:--------------------:
![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/big%20space%20before.png)  | ![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/bigspace%20after.png)

#### I unchecked the white space box under the view ribbon to trim column

### 2. Full Name Column

Before               |           After
:--------------------|:---------------------:
![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/LongName%20before.png)| ![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/corrected%20LongName.png)

#### I extracted the players long name from the Players url colum by extracting text before and after delimiter so i could get players names without special characters.

### 3. Contract Column

Before               |           After
:--------------------|:---------------------:
![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/contract%20before.png)| ![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/contract%20after.png)

#### From the  contract column, i was able to get the contract start and end date, contract type and duration, by using the conditional column to get contract that are free or paid, also i used the split column option to seperte the start date from the end date.

### 4. Height and Weight Column

Before               |           After
:--------------------|:---------------------:
![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/H%26W%20before.png)| ![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/H%26W%20after.png)

#### Here i converted the height column to cm and weight column to lbs.
Queries
for height=  if Text.Contains( [Height],"cm") then Number.From( Text.BeforeDelimiter([Height],"cm")) else null,
ft = Number.From ( Text.BeforeDelimiter([Height], "'")),
inch = Number.From ( Text.BetweenDelimiters( [Height], "'", """")),
Result = if cm is null then (ft*30.48) + (inch*2.54) else cm
in
Result
for weight= if Text.Contains([Weight], "kg") then Number.From(Text.BeforeDelimiter([Weight], "kg"))*2.20 else Text.BeforeDelimiter([Weight], "lbs")

### 5. Overall Rating and Potential Rating Column

Before               |           After
:--------------------|:---------------------:
![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/pot_before.png)| ![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/pot_after.png)

#### The OVA and POT column were converted to percentage by dividing the columns by 100 and data type changed to percentage.

### 6. Value, Wages and Release Clause Column

Before               |           After
:--------------------|:---------------------:
![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/VWR%20before.png)| ![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/VWR%20after.png)

#### The Euro sign was removed by replacing the value  option, while the M and K signs were converted to their respective values.
Value =if Text.Contains([Value], "M") then 
Number.From(Text.BeforeDelimiter([Value], "M"))* 1000000 else  Number.From(Text.BeforeDelimiter([Value], "K"))*1000

Wages =if Text.Contains([Wage], "M") then 
Number.From(Text.BeforeDelimiter([Wage], "M"))* 1000000 else  Number.From(Text.BeforeDelimiter([Wage], "K"))*1000

Release_Clause =if Text.Contains([Release_Clause], "M") then 
Number.From(Text.BeforeDelimiter([Release_Clause], "M"))* 1000000 else  Number.From(Text.BeforeDelimiter([Release_Clause], "K"))*1000

### 7. Weak Foot and Skill Move Rating Columns

Before               |           After
:--------------------|:---------------------:
![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/commit/2e65e3a10f8d2aea68d2a03fb793617fe25aea86)| ![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/star%20rating%20after.png)

#### These columns had the star sign so it had to be removed by the replace value option.

### 8. Hits Column

Before               |           After
:--------------------|:---------------------:
![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/hits%20before.png) | ![](https://github.com/ChristianaOkorie/Fifa21_Dirty_Data_Cleaning/blob/main/hits%20after.png)

#### The hit column had some values with the K sign, so i had to convert the K to ,000 by writing a query in a new column.
Hits= if Text.Contains([Hits],"K")then Number.From(Text.BeforeDelimiter([Hits],"K"))*1000 else Number.From([Hits])

## Conclusion
#### This excercise have really challenged me and tested my knowledge in data cleaning, i am glqad i was able to pull through, data cleaning is a critical part of data analysis. Soi present to you a CLEAN DATA!!!
