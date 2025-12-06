# heart-disease-data-analysis

This project focuses on analysing a **Heart Disease dataset** to understand the relationship between various clinical features such as age, cholesterol, chest pain, and target condition.  
The dataset was processed using **Jupyter Notebook**, stored on **AWS S3**, queried through **AWS Athena**, and visualised using **Power BI**.  

The main goal is to perform **data cleaning, cloud-based querying, and interactive visualisation** to support decision-making in healthcare analytics.

---

## 2. Dataset Information
- **Source:** Kaggle – Heart Disease UCI Dataset  
- **File used:** `heart_disease_uci_cleaned.csv`  
- **Total Records:** 920  
- **Attributes:** Age, Gender, Cholesterol, Blood Pressure, Chest Pain Type, Target (disease status), etc.
  
---

## 3. Tools and Technologies
| Tool | Purpose |
|------|----------|
| **Jupyter Notebook** | Data cleaning, preprocessing, and validation |
| **AWS S3** | Cloud storage for the cleaned dataset |
| **AWS Athena** | Querying the dataset using SQL in a serverless environment |
| **Power BI** | Visualising the processed data through dashboards |
| **CSV Export** | Used to store Athena query results for Power BI import |

---

## 4. Execution Steps

### Step 1: Data Cleaning (Jupyter Notebook)
1. Open the file **`heart_disease_uci_cleaning.ipynb`** in Jupyter Notebook.  
2. Run all cells to:
   - Check for missing values and data inconsistencies.  
   - Validate column types.  
   - Generate the cleaned file:  
     ```
     heart_disease_uci_cleaned.csv
     ```
3. Verify that the cleaned file is correctly saved in your working directory.

---

### Step 2: Upload Dataset to AWS S3
1. Sign in to your **AWS Management Console**.  
2. Open **S3 Service** → Create a new bucket (e.g., `heart-disease-project-aiswarya`).  
3. Upload the cleaned dataset `heart_disease_uci_cleaned.csv`.  
4. Copy the S3 path (e.g., `s3://heart-disease-project-aiswarya/data/`).

---

### Step 3: Query Data in AWS Athena
1. Open **AWS Athena** and set up a new database:
   ```sql
   CREATE DATABASE heart_project;
   
2. Create a table connected to your S3 file:
   ```sql
   CREATE EXTERNAL TABLE heart_disease (...columns...)
   ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
   LOCATION 's3://heart-disease-project-aiswarya/data/';
   
3. Run SQL queries such as:
   ```sql
   SELECT COUNT(*) AS total_records FROM heart_project.heart_disease;
   SELECT sex, AVG(chol) AS avg_chol FROM heart_project.heart_disease GROUP BY sex;
   SELECT target, AVG(age) AS avg_age FROM heart_project.heart_disease GROUP BY target;
   SELECT cp, COUNT(*) AS count FROM heart_project.heart_disease GROUP BY cp;
   
4. Download each result as a CSV file (click “Download results CSV”).

---

### Step 4: Visualisation in Power BI
1. Open **Microsoft Power BI Desktop** or **Power BI Service**.  
2. Import the CSV files downloaded from AWS Athena (for total records, average age, average cholesterol, and chest pain type).  
3. Create the following visuals:
   - **Card** → Displays total number of records (920).  
   - **Waterfall/Column Chart** → Shows average cholesterol by gender.  
   - **Donut Chart** → Displays average age grouped by heart condition.  
   - **Line Chart** → Visualises chest pain type distribution among patients.  
   - **Area Chart** → Shows cholesterol variations across patient categories.  
4. Format the charts with clear titles, colours, and labels.  
5. Save the dashboard as `Heart_Disease_Dashboard.pbix`.

---

### Step 5: Publish Dashboard Online
1. In Power BI, go to **File → Publish → To Power BI Service**.  
2. Once the upload completes, click **File → Publish to Web**.  
3. Copy the generated link and share it publicly for viewing.  
   Example:  
   👉 [Heart Disease Dashboard - Power BI](https://app.powerbi.com/view?r=eyJrIjoiNzMwOGMyMmItNTNkNC00MzQwLWE1NzgtZmZkYWZmZDFkOTkxIiwidCI6IjQyMGVjNTg5LWE4NjYtNGFkMC05YTU3LWU2MDQ5ZTBkM2JjMCIsImMiOjh9)
---

## 6. Output Summary
- **Total Records:** 920  
- **Average Cholesterol:** 132.09 (Female), 132.14 (Male)  
- **Average Age by Target:** Reversible defect – 55.9, Fixed defect – 54.3, Normal – 53.2  
- **Most Common Chest Pain Type:** Cleveland (304 cases)

---

## 7. Conclusion
This project demonstrates how a cloud-based data analysis workflow can integrate **AWS S3**, **Athena**, and **Power BI** for efficient healthcare analytics.  
The analysis provided insights into how factors like age, cholesterol, and chest pain types correlate with heart disease occurrences.  
The Power BI dashboard visually summarises the findings and offers an intuitive way to interpret patient health data.
