# Data Preparation and Cleaning Notes

These are quick reference notes covering Excel, Unix Shell, DuckDB, and dbt for data preparation.

---

# 1. Data Cleaning in Excel

Excel is useful when datasets are small and quick manual cleaning is needed.

## Find and Replace
Used to remove or replace unwanted text.

Steps:
1. Press `Ctrl + H`
2. Enter text in **Find what**
3. Leave **Replace with** blank if you want to delete the text
4. Click **Replace All**

---

## Changing Data Format
Convert values to numeric format.

Steps:
1. Select the column
2. Go to the format dropdown
3. Change **General → Number**

---

## Remove Extra Spaces (TRIM)

```excel
=TRIM(D2)
```

Removes:
- leading spaces
- trailing spaces
- extra spaces between words

---

## Delete Blank Rows

Steps:
1. Select column
2. Go to **Find & Select → Go To Special**
3. Choose **Blanks**
4. Right click → Delete → Entire Row

---

## Remove Duplicates

Steps:

```
Data → Remove Duplicates
```

Keeps only unique values.

---

# 2. Data Transformation in Excel

## Create Ratios or Metrics

Example:

```excel
=G2/D2
```

Used for metrics like population density or comparisons.

---

## Pivot Tables

Used to summarize large datasets.

Steps:

```
Insert → Pivot Table
```

---

## Detect Duplicates Using Pivot

Drag fields:

Rows:
```
Country
```

Values:
```
Count of Country
```

Shows how many times each value appears.

---

## Data Aggregation

Example configuration:

Rows:
```
Country → City
```

Values:
```
Sum of Population
```

Provides hierarchical summaries.

---

## Pivot Charts

Used to identify trends and outliers.

Example:

```
Insert → Bar Chart
```

---

# 3. Text to Columns in Excel

Used to split a column into multiple columns using delimiters.

Example text:

```
John Doe (Democrat - NY)
```

---

## Steps

```
Data → Text to Columns
```

Choose:

```
Delimited
```

---

## Custom Delimiters

Examples:

```
(
-
)
,
```

Excel splits text based on these characters.

---

## Example Output

| Name | Party | State | Vote |
|-----|-----|-----|-----|
| John Doe | Democrat | NY | Yes |

---

# 4. Data Aggregation in Excel

Used to analyze and summarize datasets.

---

## Data Cleanup

Remove blank rows:

```
Find & Select → Go To Special → Blanks
```

Delete rows.

---

## Extract Time Features

Week

```excel
=WEEKNUM(A2,1)
```

Month

```excel
=TEXT(A2,"mmm")
```

Year

```excel
=TEXT(A2,"yyyy")
```

---

## Color Scales

```
Conditional Formatting → Color Scales
```

Helps identify high and low values quickly.

---

## Sparklines

Small charts inside cells.

```
Insert → Sparklines
```

Used for trend visualization.

---

## Data Bars

Shows numeric values as bars inside cells.

```
Conditional Formatting → Data Bars
```

---

# 5. Data Preparation Using Unix Shell

Unix commands are fast, lightweight, and scriptable.

---

## List Files

```bash
ls
```

Detailed list

```bash
ls -l
```

---

## Download Data

```bash
curl --location --output file.gz URL
```

Options:

| Option | Description |
|------|------|
| --location | follow redirects |
| --continue-at - | resume download |
| --output | save file |

---

## Decompress File

```bash
gzip --decompress file.gz
```

---

## View File

First lines

```bash
head -n 5 file
```

Last lines

```bash
tail -n 5 file
```

---

## Count Lines

```bash
wc -l file
```

---

## Extract Column

Example extracting IP address:

```bash
cut --delimiter " " --fields 1 file
```

---

## Sort Data

```bash
sort file
```

---

## Count Unique Values

```bash
sort file | uniq -c
```

---

## Search Text

```bash
grep "bot" file
```

Regex search

```bash
grep -o "\S*bot\S*" file
```

---

## Convert Logs to CSV

```bash
sed 's/\[\([^]]*\)\]/"\1"/g' file > log.csv
```

---

# 6. Data Preparation in DuckDB

DuckDB is a fast analytical SQL engine.

---

## Create Sample Data

```sql
CREATE TABLE orders AS
SELECT seq AS order_id
FROM range(1,50);
```

---

## Quick Data Exploration

Preview data

```sql
SELECT * FROM orders LIMIT 5;
```

Describe table

```sql
DESCRIBE orders;
```

---

## Convert Data Formats

CSV to JSON

```sql
COPY orders TO 'orders.json' (FORMAT JSON);
```

CSV to Parquet

```sql
COPY orders TO 'orders.parquet' (FORMAT PARQUET);
```

---

## Handle Missing Values

```sql
SELECT COALESCE(customer,'Unknown') FROM orders;
```

---

## Clean Text

```sql
SELECT TRIM(LOWER(product)) FROM orders;
```

---

## Regex Cleaning

```sql
SELECT REGEXP_REPLACE(product,'\\s+',' ');
```

---

## Date Processing

```sql
SELECT STRFTIME(order_date,'%Y-%m') FROM orders;
```

---

## Create Categories

```sql
CASE
WHEN amount > 700 THEN 'high'
WHEN amount > 300 THEN 'medium'
ELSE 'low'
END
```

---

## Aggregation

```sql
SELECT region, SUM(amount)
FROM orders
GROUP BY region;
```

---

## Pivot Example

```sql
SELECT * FROM orders
PIVOT(COUNT(*) FOR region IN ('US','EU'));
```

---

# 7. dbt (Data Build Tool)

dbt manages data transformation pipelines using SQL.

---

## Install dbt

```bash
pip install dbt
```

Check version

```bash
dbt --version
```

---

## Create Project

```bash
dbt init demo_dbt
```

Creates folders:

- models
- macros
- tests
- snapshots

---

## Configure Database

Edit:

```
~/.dbt/profiles.yml
```

Add database connection credentials.

---

## Test Connection

```bash
dbt debug
```

---

## Run Models

```bash
dbt run
```

---

## Push to GitHub

```bash
git add .
git commit -m "first commit"
git push
```

---

