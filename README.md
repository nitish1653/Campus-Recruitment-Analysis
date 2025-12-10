Statistical Analysis of Campus Recruitments
Using PySpark | Azure Databricks | Azure Data Lake | Azure Blob Storage
Project Overview

This project focuses on analyzing large-scale campus recruitment data using PySpark on Azure Databricks.
The goal is to clean, transform, and analyze placement datasets to derive meaningful insights such as:

Year-wise college rankings

Company-wise hiring performance

Percentage selection of students

Quarter-wise placement trends

Overall recruitment patterns across institutions

The project demonstrates end-to-end cloud-based data engineering and analytics using Microsoft Azure.

Technologies Used

PySpark

Azure Databricks

Azure Data Lake Storage Gen2 (ADLS)

Azure Blob Storage

Azure Storage Accounts

Spark SQL

Python

Databricks Notebooks

Dataset Description

The project uses three CSV datasets stored in Azure Blob Storage:

Campus_Source1_Company.csv
Contains company-wise campus recruitment details.
Columns include: Date, College_Name, Company_Name, Package, Students_Selected, Students_Participated, Criteria, etc.

Campus_Source2_College.csv
Contains college survey information.
Columns include: College, Location, No. of Students (Indian & Foreign), Fees, Rank, Survey_Name, etc.

DIM.Date.Table.csv
A date dimension file to support time-based analytics.
Columns include: Full_Date, Year, Quarter, Month_Name, Day_Name.

Data Engineering Workflow
1. Data Ingestion

Uploaded all CSV datasets to Azure Blob Storage.

Read them into Azure Databricks using abfss:// data paths.

2. Data Cleaning & Preparation

Performed transformations such as:

Standardizing text fields with upper() and trim()

Converting dates using to_date()

Casting numeric columns (Package, Student_Selected, etc.)

Handling null values

3. Data Modeling (Star Schema)

Created:

4 Dimension Tables → College, Company, Survey, Time

2 Fact Tables → College_Fact, Survey_Fact

Used monotonically_increasing_id() to generate surrogate keys.

4. Analytical Report Generation

Generated five analytical reports using PySpark aggregations:

Report 1 – Year-wise College Ranking

Average rank of each college per year.

Report 2 – College-wise Percentage Selection

Selection efficiency of students (Selected ÷ Participated).

Report 3 – Year-wise Quarter-wise Placement

Total students placed per quarter, per year.

Report 4 – Company-wise Total Students Selected

Shows hiring volume of companies per year along with package.

5. Exporting Outputs

All reports were exported as CSV files into the reports/ directory for further visualization.

Sample Code Snippet (PySpark)
report2 = fact_college_details.join(time_dim, "Date_clean") \
    .join(college_dim, "CollegeID") \
    .join(company_dim, "CompanyID") \
    .withColumn("Percentage_Selection",
                round((col("Student_Selected") / col("Student_Participated")), 4)) \
    .select("Year", "College", "Company_Name", "Percentage_Selection") \
    .orderBy("Year", "College")

Key Insights

TCS, Cognizant, Wipro, and Infosys were top recruiters in the dataset.

Some colleges consistently ranked top across multiple years.

Certain quarters showed higher recruitment peaks (seasonal hiring trends).

Percentage selection highlighted efficiency of student performance across colleges.

Conclusion

This project demonstrates the power of PySpark and Azure Databricks in performing scalable data processing and analytics.
By integrating Azure Blob Storage and Data Lake, the project replicates real-world data engineering workflows.
The analytical reports generated provide actionable insights into recruitment patterns and college performance.

Nitish S P
Aspiring Data Engineer | Azure | PySpark | ETL Pipelines

#Azure #Databricks #PySpark #DataEngineering #BigData #ETL #Analytics #CampusRecruitment
