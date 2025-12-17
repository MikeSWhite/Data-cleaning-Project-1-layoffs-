----- Data Cleaning

Global Layoffs Data Cleaning (SQL)
Project Overview
This project focuses on cleaning and standardizing a global layoffs dataset using MySQL. The objective was to prepare the raw data for accurate analysis by removing duplicates, standardizing inconsistent values, handling nulls and blanks, correcting data types, and eliminating unusable records.

All data transformations were performed using SQL to reflect real-world data engineering and analytics workflows.

Data Cleaning Workflow
1. Creating a Staging Environment
A staging table (layoffs_staging) was created to preserve the original dataset.

All cleaning operations were performed on staging tables to ensure the raw data remained unchanged.

A second staging table (layoffs_staging2) was created to support duplicate tracking using window functions.

2. Duplicate Identification and Removal
Duplicate records were identified using the ROW_NUMBER() window function.

Rows were partitioned by a combination of business-key fields including:

Company

Location

Industry

Layoff metrics

Date

Stage

Country

Funds raised

Records with a row_num greater than 1 were classified as duplicates.

Duplicate rows were safely deleted, preserving one unique record per layoff event.

3. Standardizing Text Data
Company Names
Leading and trailing whitespace was removed using TRIM() to ensure consistent company naming.

Industry Values
Inconsistent industry labels (e.g., Crypto Currency, Crypto/Web3) were standardized to a single value:
Crypto

Country Names
Country values containing trailing punctuation (e.g., United States.) were cleaned using TRIM().

This ensured consistent country naming for grouping and analysis.

4. Date Formatting and Type Conversion
The date column was originally stored as text.

Dates were converted to proper DATE format using STR_TO_DATE().

The column type was altered to DATE to enable accurate time-based analysis.

5. Handling NULL and Blank Values
Industry Imputation
Blank industry values were converted to NULL.

Missing industry values were populated by self-joining on company name when a valid industry existed elsewhere for the same company.

Removing Unusable Records
Records where both:

total_laid_off

percentage_laid_off
were NULL

These rows were removed, as they provided no meaningful layoff information.

6. Schema Cleanup
Temporary helper columns (such as row_num) were removed after duplicate cleanup.

The final table contains only relevant, analysis-ready fields.

Skills Demonstrated
SQL staging and data preservation

Window functions (ROW_NUMBER)

Duplicate detection and removal

String standardization

Date parsing and data type conversion

NULL handling and data imputation

Safe deletion practices

Real-world data cleaning workflows

Final Result
The cleaned layoffs dataset is:

Free of duplicate records

Consistent across text, date, and numeric fields

Properly typed for analytical queries

Ready for downstream analysis and visualization
