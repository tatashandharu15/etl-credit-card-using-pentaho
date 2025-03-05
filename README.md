<h1 align="center"> 💳 ETL Credit Card Data Set 💳 </h1>
<p align="center">using <b>Pentaho Data Integration (PDI)/Kettle ⚙</b><br><br>
.: 📄 Dataset taken from <b><a href="https://www.kaggle.com/rikdifos/credit-card-approval-prediction"> Kaggle </a></b> :.
</p>

## 📃 Table of Contents:
  - [About Project](#-about-project)
  - [Objectives](#-objectives)
  - [Data Set Description](#-data-set-description)
  - [ETL Process](#-etl-process)
      - [Application Record](#-application-record)
      - [Credit Record](#-credit-record)
      - [Creating Output File](#-output-file)
  - [Preview Output File](#-preview-output-file)
<br>

## 🖋 About Project
*   This repository contains:
    - ETL file using Pentaho Data Integration (PDI).
    - CSV file that has gone through ETL process.

*   This project will also:
    - Clean and transform both data sets (application record and credit record),
    - Merge, clean, and transform data sets into one data set (in CSV format).
<br><br>

## 📌 Objectives
*   Perform ETL using PDI for both datasets.
*   Create time dimension using PDI.
*   Create fact table using PDI.
<br><br>

## 🧾 Data Set Description
*   The dataset description can be seen <a href="https://www.kaggle.com/rikdifos/credit-card-approval-prediction/discussion/119320"><b>here</b></a>.
<br><br>

## ⚙ ETL Process
![Main ETL Flow](Screenshot/01%20-%20Main%20ETL%20Flow.png)

[![](https://img.shields.io/badge/back%20to%20top-%E2%86%A9-blue)](#-table-of-contents)
<br><br>

### 👨‍💼 Application Record
#### ▶ CSV file input
![CSV file input - Application](Screenshot/02%20-%20CSV%20File%20Input%20(Application%20Record).png)
   - Importing application record csv. <br>

#### ▶ Sort rows
![Sort rows - Application](Screenshot/03%20-%20Sort%20rows.png)
   - Sort data based on ID (in ascending order). <br>

#### ▶ Unique rows
![Unique rows - Application](Screenshot/04%20-%20Unique%20rows.png)
   - Filtering duplicate ID. <br>

#### ▶ Replace in string
![Replace in string - Application](Screenshot/05%20-%20Replace%20in%20string.png)
   - Replacing 'Y' with 1, and 'N' with 0. <br>

#### ▶ Add constants
![Add contants - Application](Screenshot/06%20-%20Add%20constants.png)
   - Adding 'Current_Date' column. <br>

#### ▶ Calculator
![Calculator - Application](Screenshot/07%20-%20Calculator.png)
   - Calculating applicant age and how long applicant have been working (in years). <br>

#### ▶ Filter rows
![Filter rows - Application](Screenshot/08%20-%20Filter%20rows.png)
   - Filtering applicant that is less than 21 y.o.
   - Filtering applicant with null/empty values <br>

[![](https://img.shields.io/badge/back%20to%20top-%E2%86%A9-blue)](#-table-of-contents)
<br><br>


### 💶 Credit Record
#### ▶ CSV file input
![CSV file input - Credit Record](Screenshot/09%20-%20CSV%20File%20Input%20(Credit%20Record).png)
   - Importing credit record csv. <br>

#### ▶ Sort rows 2
![Sort rows - Credit Record](Screenshot/10%20-%20Sort%20rows.png)
   - Sort data based on ID (in ascending order). <br>

#### ▶ Add constants 2
![Add contants - Credit Record](Screenshot/11%20-%20Add%20constants.png)
   - Adding 'Current_Date' column. <br>

#### ▶ Calculator 2
![Calculator - Credit Record](Screenshot/12%20-%20Calculator.png)
   - Calculating month loan payment.
   - Creating copy of 'STATUS' column. <br>

#### ▶ Replace in string 2
![Replace in string - Credit Record](Screenshot/13%20-%20Replace%20in%20string.png)
   - Replace C, X, 0 with 'Good Debt' (C: loan for that month is already paid; X: no loan for that month; 0: loan is 1 to 29 days overdue). 
   - Replace 1, 2, 3, 4, 5 with 'Bad Debt' (1: loan is 30 to 59 days overdue; 2: loan is 60 to 89 days overdue; 3: loan is 90 to 119 days overdue; 4: loan is 120 to 149 days overdue; 5: loan is more than 150 days overdue).<br>

#### ▶ Calculator 3
![Calculator2 - Credit Record](Screenshot/14%20-%20Calculator.png)
   - Creating 2 copies of 'STATUS2' column (Good_Debt and Bad_Debt).<br>

#### ▶ Replace in string 3
![Replace in string2 - Credit Record](Screenshot/15%20-%20Replace%20in%20string.png)
   - Good_Debt: Good Debt will be change to 1, while Bad Debt will be change to 0.
   - Bad_Debt: Good Debt will be change to 0, while Bad Debt will be change to 1.<br>

#### ▶ Group by
![Group by - Credit Record](Screenshot/16%20-%20Group%20by.png)
   - Calculating total of Good Debt and Bad Debt from each applicant (similar to group by function in SQL).<br>

#### ▶ Modified JavaScript value
![JavaScript - Credit Record](Screenshot/17%20-%20Modified%20JavaScript%20value.png)
   - If the total of Good Debt is higher than Bad Debt, then an applicant status will be eligible (1).
   - If the total of Bad Debt is higher than Good Debt, then an applicant status will be not eligible (0).<br>

[![](https://img.shields.io/badge/back%20to%20top-%E2%86%A9-blue)](#-table-of-contents)
<br><br>

### 📥 Output file
#### ▶ Stream lookup
![Stream lookup - Output file](Screenshot/18%20-%20Stream%20lookup.png)
   - Bad_Debt_CNT, Good_Debt_CNT, and STATUS will be merged based on applicant ID.<br>

#### ▶ Filter rows
![Filter rows - Output file](Screenshot/19%20-%20Filter%20rows.png)
   - Applicant with empty Bad_Debt_CNT, Good_Debt_CNT, and STATUS will be deleted.<br>

#### ▶ Select values 2
![Select values - Output file](Screenshot/20%20-%20Select%20values.png)
   - Select columns that will extracted.<br>

#### ▶ Text file output
![Text file output1 - Output file](Screenshot/21%20-%20Text%20file%20output_1.png)
![Text file output2 - Output file](Screenshot/22%20-%20Text%20file%20output_2.png)
   - Exporting cleaned and transformed data set into CSV file.<br>

[![](https://img.shields.io/badge/back%20to%20top-%E2%86%A9-blue)](#-table-of-contents)
<br><br>

## 👀 Preview Output File
![Preview Output File 1](Screenshot/23%20-%20Preview%20Output%20File%201.png)
![Preview Output File 2](Screenshot/24%20-%20Preview%20Output%20File%202.png)

[![](https://img.shields.io/badge/back%20to%20top-%E2%86%A9-blue)](#-table-of-contents)
<br><br>

## 🙌 Support me!

👉 If you find this project useful, **please ⭐ this repository 😆**!

---

👉 _More about myself: <a href="https://tatashandharu15.github.io/"> here </a>_
