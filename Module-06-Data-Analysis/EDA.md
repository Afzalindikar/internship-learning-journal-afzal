# Module 5 – Session 1  
## Model the Data: Correlation & Regression in Excel

---

## 1. Enable Data Analysis ToolPak
1. Go to **File → Options**  
2. Click **Add-ins**  
3. At the bottom select **Manage: Excel Add-ins → Go**  
4. Check **Analysis ToolPak** → Click **OK**

Now you can access **Data → Data Analysis** in the ribbon.

---

# Correlation Analysis

## Step 1: Prepare Data
Keep only these columns:
- New Cases
- New Deaths
- New Vaccinations

Remove unnecessary columns.

## Step 2: Generate Correlation Matrix
1. Go to **Data → Data Analysis**
2. Select **Correlation → OK**
3. **Input Range:** Select the three columns  
4. Check **Labels in first row**
5. Choose **Output Range** in the same sheet
6. Click **OK**

## Interpretation
Correlation values range from **-1 to +1**.

- **New Cases vs New Deaths = 0.84**  
  → Very **strong positive correlation**

- **New Vaccinations vs New Deaths = 0.23**  
  → **Weak positive correlation**

---

# Scatterplot Visualization

## Plot 1: New Cases vs New Deaths
1. Select **New Cases (X-axis)** and **New Deaths (Y-axis)**
2. Go to **Insert → Charts → Scatter Plot**
3. Add **Trendline**

**Insight:**  
Trendline is steep → confirms **strong positive correlation (0.84)**.

---

## Plot 2: New Vaccinations vs New Deaths
1. Select **New Vaccinations (X-axis)** and **New Deaths (Y-axis)**
2. Insert **Scatter Plot**
3. Add **Trendline**

**Insight:**  
Trendline slope is small → **weak correlation (0.23)**.  
As vaccinations increased, deaths slightly decreased.

---

# Regression Analysis

## Variables
**Dependent Variable (Y):**
- New Deaths

**Independent Variables (X):**
- New Cases
- New Tests
- New Vaccinations
- Stringency Index

---

## Step 1: Data Preparation
Create new columns:
- New Cases per 1000
- New Tests per 1000
- New Vaccinations per 1000

Formula:
Value ÷ 1000


---

## Step 2: Run Regression
1. Go to **Data → Data Analysis**
2. Select **Regression**
3. **Input Y Range:** New Deaths
4. **Input X Range:**  
   - New Cases per 1000  
   - New Tests per 1000  
   - New Vaccinations per 1000  
   - Stringency Index
5. Check **Labels**
6. Select **New Worksheet Ply**
7. Click **OK**

---

# Interpreting Results

## 1. Adjusted R²
**Value: 0.816**

Meaning:
- **81.6% of variation in deaths** is explained by the model.

---

## 2. Significance F
- Value **< 0.05**

Meaning:
- The **overall regression model is statistically significant**.

---

## 3. P-values (Variable Importance)

| Variable | Result |
|--------|--------|
| New Cases | Significant |
| New Tests | Significant |
| New Vaccinations | Significant |
| Stringency Index | Not significant (P = 0.11) |

Only variables with **P < 0.05** should be trusted.

---

## 4. Coefficients (Impact on Deaths)

| Variable | Coefficient | Meaning |
|--------|--------|--------|
| New Cases /1000 | ~7 | 1000 cases → 7 more deaths |
| New Tests /1000 | 0.69 | 1000 tests → 0.69 more deaths |
| New Vaccinations /1000 | -0.07 | 1000 vaccinations → deaths decrease slightly |
| Stringency Index | 2.71 | Appears to increase deaths, but **not statistically valid** |

---

## Session 2
Forecast Functions in Excel (Linear Regression & Time Series)
Introduction
In this tutorial, we explore the FORECAST function in Microsoft Excel.

The FORECAST function performs linear regression behind the scenes and uses it to predict future values.

A synonym for this function is: FORECAST.LINEAR

Both functions work exactly the same.

Dataset Used
We will use a Height and Weight dataset from Kaggle.

The dataset contains information about 25,000 people, including:

Height (in inches)
Weight (in pounds)
For demonstration purposes, we will only use 1,000 rows.

Example data:

Height (inches)	Weight (pounds)
65	120
68	140
70	155
Converting Units to Metric
Since the dataset uses inches and pounds, we convert them to metric units.

Convert Height (Inches → Centimeters)
Formula:


Height_cm = Height_inches * 2.54

Example Excel formula:

=A2 * 2.54
Convert Weight (Pounds → Kilograms)
Formula:

Weight_kg = Weight_pounds / 2.20462
Example Excel formula:

=B2 / 2.20462
After conversion, drag the formulas down to apply them to the entire dataset.

Visualizing the Data
To understand the relationship between height and weight, we create a scatter plot.

Steps:

Select the Height (cm) column.
Select the Weight (kg) column.
Insert → Chart → Scatter Plot
Observation:

Height ranges roughly 160 cm to 185 cm
Weight ranges roughly 50 kg to 65 kg
There is a positive linear relationship between height and weight.
Using the FORECAST Function
The syntax of the function is:

=FORECAST(x, known_y's, known_x's)
Where:

x → Value we want to predict for
known_y's → Dependent variable (target)
known_x's → Independent variable
Example: Predict Weight from Height
Suppose we want to predict the weight of a person who is 170 cm tall.

=FORECAST(170, WeightRange, HeightRange)
Example result:

170 cm → predicted weight ≈ 56 kg
Reverse Prediction (Height from Weight)
We can also reverse the variables.

Example:

Predict height for a person weighing 75 kg.

=FORECAST(75, HeightRange, WeightRange)
Example result:

75 kg → predicted height ≈ 180 cm (≈ 6 feet)
Forecasting Multiple Values
Suppose we want predictions for several heights:

Height
150
155
160
165
170
One way is to copy the formula:

=FORECAST(A2, WeightRange, HeightRange)
Then drag the formula down.

However, this approach is inefficient because each formula calculates regression independently.

Using the TREND Function
A better approach is using the TREND function.

Syntax:

=TREND(known_y's, known_x's, new_x's)
Example:

=TREND(WeightRange, HeightRange, NewHeightRange)
Benefits:

Computes regression once
Applies predictions to the entire array
Automatically fills the column
TREND returns the same values as FORECAST.

Compatibility with Google Sheets
These functions are also available in Google Sheets:

FORECAST
FORECAST.LINEAR
TREND
You can:

Save the Excel file
Open in Google Sheets
Edit
Save and reopen in Excel
Everything works perfectly.

Limitation of Linear Regression
Linear regression works well for simple linear relationships.

However, it performs poorly for cyclical or seasonal data.

Example:

Traffic data across time.

Dataset:

DateTime	Number of Vehicles
01-01 08:00	25
01-01 09:00	40
01-01 10:00	32
When plotted, traffic data shows:

Daily peaks
Weekly patterns
Weekend drops
Holiday effects
This pattern is seasonal, not linear.

Linear Prediction on Traffic Data
Using TREND:

=TREND(VehicleValues, DateTimeValues, FutureDateTimes)
Result:

Predicts around 20 vehicles
Slight upward slope
Fails to capture peaks and valleys
This shows linear regression is not suitable for seasonal data.

Using FORECAST.ETS (Time Series Forecasting)
For cyclical data, Excel provides:

FORECAST.ETS
This uses Exponential Triple Smoothing (ETS).

Syntax:

=FORECAST.ETS(target_date, values, timeline, [seasonality], [data_completion], [aggregation])
Example Usage
=FORECAST.ETS(A2, $B$2:$B$1000, $A$2:$A$1000)
Where:

A2 → Target date
B2:B1000 → Vehicle counts
A2:A1000 → Timeline
Optional Parameters
Seasonality
Defines the repeating cycle.

Example:

24 → season repeats every 24 data points
Example for hourly traffic data:

24 = daily pattern
If omitted, Excel automatically detects seasonality.

Data Completion
Handles missing values.

Options:

1 → Interpolation (default)
0 → Missing values treated as zero
Comparing Predictions
When plotted together:

Line	Meaning
Blue	Actual data
Orange	Linear forecast
Green	ETS forecast
Observations:

Linear prediction → almost flat line
ETS prediction → follows seasonal patterns better
Key Takeaways
FORECAST / FORECAST.LINEAR
Uses linear regression
Works well for linear relationships
Poor for seasonal data
TREND
Same as FORECAST
More efficient for multiple predictions
FORECAST.ETS
Designed for time series forecasting
Captures seasonality
Better for cyclical data
Outlier Detection in Excel
Introduction
In data analysis, it is important to identify outliers — values that are significantly higher or lower than the rest of the dataset.

Outliers may occur because of:

Data entry mistakes
Measurement errors
Rare but valid observations
These values can distort statistical analysis such as mean, regression, or forecasting, so detecting them early is important. :contentReference[oaicite:1]{index=1}

What is an Outlier?
An outlier is a data point that lies far away from the majority of data values.

Example dataset:

Values
10
12
13
14
15
200
Here 200 is clearly far away from the rest of the values and is considered an outlier.

Outliers can significantly impact the average and statistical interpretation of data. :contentReference[oaicite:2]{index=2}

Dataset Example in Excel
Suppose we have a dataset like this:

Student	Score
A	52
B	55
C	60
D	58
E	95
In this dataset, 95 may be an outlier depending on the statistical distribution.

Method 1: Detect Outliers Using Sorting
The simplest method:

Steps
Select the dataset
Go to Data → Sort
Sort values Ascending or Descending
Look for unusually large or small numbers
Example sorted dataset:

Score
52
55
58
60
95
The value 95 stands out as a potential outlier.

Method 2: Detect Outliers Using Quartiles (IQR Method)
A more statistical approach uses the Interquartile Range (IQR).

Step 1: Calculate Quartiles
Use Excel's QUARTILE function.

=QUARTILE(A2:A20,1)
This calculates Q1 (First Quartile).

=QUARTILE(A2:A20,3)
This calculates Q3 (Third Quartile).

Step 2: Calculate IQR
=Q3 - Q1
Example:

IQR = Q3 - Q1
Step 3: Calculate Outlier Limits
Lower Limit:

=Q1 - 1.5 * IQR
Upper Limit:

=Q3 + 1.5 * IQR
Any values outside this range are considered outliers.

Statistically, values beyond 1.5 × IQR above Q3 or below Q1 are typically classified as outliers. ([Excel Maven][1])

Example Calculation
Dataset:

Values
10
12
14
15
18
19
200
Suppose:

Q1 = 12
Q3 = 18
IQR = 6
Lower Bound:

12 - (1.5 × 6) = 3
Upper Bound:

18 + (1.5 × 6) = 27
Since 200 > 27, it is an outlier.

Method 3: Highlight Outliers with Conditional Formatting
Excel can automatically highlight outliers.

Steps
Select the dataset
Go to Home → Conditional Formatting
Choose New Rule
Use a formula
Example formula:

=OR(A2<$LowerLimit, A2>$UpperLimit)
Then apply a color such as red to highlight the outliers.

Visualizing Outliers Using Charts
Outliers become easier to see in charts.

Use:
Scatter plots
Box plots
Box plots are especially useful because they show:

Median
Quartiles
Outliers visually
Why Outlier Detection Matters
Outliers can distort:

Mean
Regression models
Machine learning models
Forecasting accuracy
Therefore, identifying them is a critical step in data cleaning and preprocessing.

When to Remove Outliers
Do not always remove outliers automatically.

You should check whether they are:

Data entry errors
Sensor measurement errors
Legitimate rare events
Sometimes outliers contain valuable information.

## Session 3 

Data Analysis using Python and Pandas
This notebook demonstrates how to perform basic data analysis using Python and Pandas on a dataset of card transactions.

Pandas is a powerful Python library used for data manipulation and analysis.

Resources to learn Pandas:

https://pandas.pydata.org/
https://pandas.pydata.org/docs/user_guide/10min.html
https://youtube.com/playlist?list=PL-osiE80TeTsWmV9i9c58mdDCSskIFdDS
Dataset
We analyze a card transactions dataset stored in Parquet format.

Parquet is a column-based storage format that is:

Faster than CSV
Smaller in size
Efficient for analytics
Step 1: Download Dataset
# Download dataset
!curl -C- -o transactions.parquet "https://drive.usercontent.google.com/download?id=1XGvuFjoTwlybkw0cc9u34horMF9vMhrB"
Step 2: Import Required Library
import pandas as pd
Pandas is used to load, clean, and analyze tabular data.

Step 3: Load Dataset
df = pd.read_parquet("transactions.parquet")
This reads the parquet file into a Pandas DataFrame.

Step 4: View First Few Rows
df.head()
head() displays the first 5 rows of the dataset.

Step 5: Inspect Dataset Structure
df.info()
This shows:

number of rows
column names
data types
memory usage
missing values
Step 6: Summary Statistics
df.describe()
This generates statistical information such as:

count
mean
standard deviation
minimum value
maximum value
quartiles
For all numerical columns.

Step 7: View Column Names
df.columns
This lists all columns present in the dataset.

Step 8: Check Unique Values
Example:

df["merchant"].unique()
This shows all unique merchants present in the dataset.

Step 9: Count Unique Values
df["merchant"].nunique()
This returns the number of unique merchants.

Step 10: Value Counts
df["merchant"].value_counts()
Shows how many transactions occurred for each merchant.

Step 11: Filter Data
Example: Transactions greater than 1000

df[df["amount"] > 1000]
This filters rows where transaction amount is greater than 1000.

Step 12: Select Specific Columns
df[["merchant", "amount"]]
This selects only the specified columns.

Step 13: Group By Operation
Group transactions by merchant:

df.groupby("merchant")["amount"].sum()
This calculates total spending per merchant.

Step 14: Average Transaction Per Merchant
df.groupby("merchant")["amount"].mean()
This calculates average transaction amount per merchant.

Step 15: Sorting Values
df.sort_values("amount", ascending=False)
Sorts the dataset based on transaction amount.

Step 16: Top Transactions
df.sort_values("amount", ascending=False).head()
Displays the largest transactions.

Step 17: Basic Data Filtering Example
Transactions from a specific merchant:

df[df["merchant"] == "Amazon"]
Step 18: Multiple Conditions
df[(df["amount"] > 500) & (df["merchant"] == "Amazon")]
Filters rows where:

amount > 500
merchant is Amazon
Step 19: Save Processed Data
df.to_csv("transactions_cleaned.csv", index=False)
Exports the DataFrame into a CSV file.

Data Analysis with Databases
Databases are where most transactional data resides.
Instead of exporting everything into CSV files, analysts often query the database directly.

In this notebook we demonstrate how to:

Connect to a database
Run SQL queries from Python
Analyze the results using Pandas
Query the Database
There are many ways to connect to and query a database.

In Python, a common approach is using:

SQLAlchemy → database connection
Pandas → executing queries and analyzing results
Step 1: Database Connection
stats_connection = "mysql+pymysql://guest:relational@db.relational-data.org/stats"
This connection string contains:

Database type → mysql
Driver → pymysql
Username → guest
Password → relational
Database host → db.relational-data.org
Database name → stats
Step 2: Create Engine and Connect
import pandas as pd
import sqlalchemy as sa

engine = sa.create_engine(
    "mysql+pymysql://guest:relational@db.relational-data.org/stats"
)

pd.read_sql("SELECT COUNT(*) FROM posts", engine)
This verifies that we successfully connected to the database and counts the rows in the posts table.

Step 3: Helper Function for Queries
Instead of writing pd.read_sql() every time, we create a helper function.

def query(sql):
    return pd.read_sql(sql, engine)
Now we can easily run SQL queries.

Example Query
query(
"""
SELECT
OwnerUserId,
COUNT(*) as PostCount
FROM posts
GROUP BY OwnerUserId
ORDER BY PostCount DESC
"""
)
This query:

Groups posts by user
Counts how many posts each user made
Sorts users by post count
Dataset Note
The user names are None because the dataset is anonymized.

How Concentrated Are the Posts?
A common question in online communities:

Do 20% of users create 80% of the content?

This is related to the Pareto Principle (80/20 rule).

Step 4: Count Posts per User
post_count = query(
"""
SELECT
OwnerUserId,
COUNT(*) as PostCount
FROM posts
GROUP BY OwnerUserId
ORDER BY PostCount DESC
"""
)
This produces a table showing:

User	Number of Posts
Step 5: Compare Top 20% Users
post_count.PostCount.iloc[:len(post_count)//5].sum() / post_count.PostCount.sum()
Explanation:

len(post_count)//5 → top 20%
.sum() → total posts by those users
divide by total posts
Result:

Top 20% of users generate ~76% of posts

This is close to the Pareto distribution.

Does Age Predict Reputation?
The users table contains:

Age
Reputation
We want to check whether age influences reputation.

Step 6: Fetch Aggregated Statistics
import numpy as np

stats_query = """
SELECT
COUNT(*) as n,
SUM(Age) as sum_age,
SUM(Reputation) as sum_rep,
SUM(Age * Reputation) as sum_age_rep,
SUM(Age * Age) as sum_age_sq,
SUM(Reputation * Reputation) as sum_rep_sq
FROM users
WHERE Age IS NOT NULL
"""

stats = query(stats_query)
stats
This query retrieves aggregated statistics needed to compute correlation.

Correlation Result
The calculated correlation is about:

~1.7%
Interpretation:

Age and reputation have almost no relationship.

This means older users do not necessarily have higher reputation.

How Many Views Increase Reputation by 1 Point?
Hypothesis:

More profile views may increase user reputation.

Step 7: Fetch Required Aggregates
sql = """
SELECT
COUNT(*) as n,
SUM(Views) as sum_views,
SUM(Reputation) as sum_rep,
SUM(Views * Reputation) as sum_views_rep,
SUM(Views * Views) as sum_views_sq
FROM users
"""

query(sql)
This gathers statistics needed to estimate the relationship between views and reputation.

Inspect the Data Directly
To better understand the relationship:

reputation = query("SELECT Views, Reputation FROM users")
reputation
Calculate Mean Values
reputation.mean()
This computes the average views and reputation across users.

Interpretation
The analysis suggests that:

Users with more profile views tend to have higher reputation
However, the relationship is not perfectly linear
Reputation depends on many other factors like:

Answers posted
Question quality
Community voting
Lessons
This notebook demonstrates how to combine:

SQL for querying data
Pandas for analysis
SQLAlchemy for database connections
Together they form a powerful workflow for data analysis directly from databases.

Useful libraries:

https://pandas.pydata.org/
https://docs.sqlalchemy.org/
What Else Should You Know for Exams?
You should also know about SQLite.

SQLite is:

A lightweight database
Serverless
Stored in a single file
Website:

https://sqlite.org/

It is widely used in:

Mobile apps
Embedded systems
Small applications

---

## Session 4

Data Analysis with Datasette
Datasette is an open-source multi-tool created by Simon Willison for exploring and publishing data. It instantly turns any SQLite database into a web interface with powerful exploration features, built-in JSON APIs, and visualization capabilities—all without requiring you to write any code upfront. It is highly effective for data journalism, analysis workflows, and sharing datasets with both technical and non-technical audiences.

Installation and Quickstart
You can install Datasette and its companion tools using standard Python package managers like pip or uv, or via Homebrew:

pip install datasette
To start Datasette with a SQLite database, simply run:

datasette your_database.db
This will launch a web server at http://localhost:8001, giving you an instant interface to explore your data.

Core Analysis Features
The Interactive Interface
The database homepage displays all available tables, row counts, and a SQL query box. Clicking on any table name opens a view equipped with interactive features:

Sorting: Sort data simply by clicking the column headers.
Pagination: Easily navigate through large datasets.
Column Menus: Access faceting and filtering options via the cog icon next to column headers.
Faceting for Discovery
Faceting is a core feature for exploratory analysis. It allows you to see the distribution of values within a column.

By selecting "Facet by this", Datasette generates clickable counts of each category (e.g., showing how many orders are "completed", "pending", or "cancelled").
You can apply multiple facets simultaneously to reveal deeper patterns in your data, such as looking at product categories across different regions.
Filtering Data
Datasette provides robust filtering options to drill down into specific subsets of data. You can stack these filters to answer specific questions. Supported filter types include:

Exact match
Text contains
Numeric comparisons (e.g., quantity > 1)
Date ranges
Advanced Analysis
Running SQL Queries
While Datasette does not require SQL knowledge for basic exploration, it offers a built-in SQL editor for complex analysis. You can safely execute custom SQL queries because the database is opened in read-only mode. Just like standard tables, your query results can be faceted, filtered, and exported.

Creating Canned Queries
If you have frequently run analyses, you can save them as named "canned queries." By defining these in a metadata.json file and launching Datasette with the -m flag, these queries will appear in the sidebar, effectively turning Datasette into a self-service analytics portal.

Exporting and Publishing
Exporting Data and API Access
Everything you see in the Datasette interface can be exported as raw data.

Links at the bottom of the page allow you to export the current view (respecting all active filters) to CSV, JSON, or newline-delimited JSON.
Datasette includes built-in API access; you can simply append .json to any URL to retrieve the data programmatically.
Publishing to the Web
Datasette includes a publish command that allows you to bundle your SQLite database into a Docker container and deploy it directly to the internet using serverless hosting providers like Google Cloud Run or Heroku.

datasette publish cloudrun your_database.db
Once deployed, your database becomes a public API and interactive web interface for anyone to explore.

Ecosystem Tools
Plugins
Datasette supports custom templates, CSS, and an extensive ecosystem of plugins to enhance your analysis:

datasette-cluster-map: Visualizes records with latitude and longitude data on an interactive map.
datasette-vega: Allows you to plot line charts and graphs (e.g., tracking date-time data against case numbers).
datasette-copyable: Generates copy-and-pasteable data formats, such as LaTeX tables.
Data Preparation with sqlite-utils
Before analyzing data in Datasette, you can use a companion CLI tool called sqlite-utils. It is designed to manipulate SQLite databases, making it easy to:

Insert large CSV files into SQLite database tables.
Extract columns with duplicate strings into separate joined tables to clean the data.
Enable full-text search on specific columns.
Data Analysis with DuckDB and Parquet
1. What is DuckDB?
DuckDB is an in-process analytical SQL database designed for fast analytical queries.
It is optimized for OLAP (Online Analytical Processing) workloads and works efficiently with large datasets.

Key Features
Runs inside Python, R, or applications (no server required).
Optimized for analytical queries on large datasets.
Uses columnar storage, which improves performance for analytics.
Supports SQL queries directly on files like:
CSV
Parquet
JSON
Pandas DataFrames
Very fast compared to Pandas for large data processing.
DuckDB is often called the "SQLite for analytics".

2. What This Code Is About
This notebook demonstrates:

Using Parquet as a data storage format
Comparing file formats (CSV, JSON, SQLite, Parquet)
Comparing performance of Pandas vs DuckDB
Running SQL queries directly on Parquet files
Combining Pandas and DuckDB operations
The dataset used is:

2015 Flights Dataset

It contains flight information such as:

Departure delay
Arrival delay
Flight distance
Other flight metrics
The goal is to show that:

DuckDB can perform analytical queries much faster and with less memory than Pandas.

3. Step-by-Step Implementation
Step 1 – Install Required Libraries
!pip install duckdb pandas sqlalchemy sqlite3
Step 2 - Download Dataset
!curl https://github.com/plotly/datasets/raw/master/2015_flights.parquet --output 2015_flights.parquet
Step 3 – Load Data Using Pandas
import pandas as pd

df = pd.read_parquet('2015_flights.parquet')
df.head()
Step 4 – Compare Storage Formats
Convert to CSV

%timeit df.to_csv('2015_flights.csv', index=False)
Convert to JSON

%timeit df.to_json('2015_flights.json', orient='records')
Convert to SQLite

%timeit df.to_sql('2015_flights', 'sqlite:///2015_flights.db', index=False, if_exists='replace')
Save as Parquet

%timeit df.to_parquet('2015_flights.saved.parquet')
Step 5 – Check File Sizes
!ls -la 2015_flights.*
Comparision of file size :

Format	Size	Performance
CSV	Large	Slow
JSON	Very Large	Slow
SQLite	Medium	Moderate
Parquet	Small	Fast
Step 6 – Perform Analysis Using Pandas
Find the number of unique flight distances for each departure delay.

delays = df.groupby('DEPARTURE_DELAY')['DISTANCE'].nunique()
delays[delays.index > 0]
Measure Pandas Performance

%timeit df.groupby('DEPARTURE_DELAY')['DISTANCE'].nunique()
Typical execution time: ~5 seconds

Step 7 – Perform Same Query Using DuckDB
import duckdb

delays = duckdb.query("""
SELECT
    DEPARTURE_DELAY,
    COUNT(DISTINCT DISTANCE)
FROM "2015_flights.parquet"
GROUP BY DEPARTURE_DELAY
ORDER BY DEPARTURE_DELAY
""").df()
DuckDB is ~20–25x faster than Pandas.

Step 8 – Run DuckDB Using a Connection
conn = duckdb.connect(database=':memory:', read_only=False)

delays = conn.execute("""
SELECT
DEPARTURE_DELAY,
COUNT(DISTINCT DISTANCE)
FROM "2015_flights.parquet"
GROUP BY DEPARTURE_DELAY
ORDER BY DEPARTURE_DELAY
""").df()
Explanation

Creates an in-memory DuckDB database and executes SQL queries.
Advantages:

No external database required

Very fast processing

Step 9 – Query Pandas DataFrame Using DuckDB
DuckDB can query Pandas DataFrames directly.

df = pd.read_parquet('2015_flights.parquet')

delays = duckdb.sql("""
SELECT
DEPARTURE_DELAY,
COUNT(DISTINCT DISTANCE)
FROM df
GROUP BY DEPARTURE_DELAY
ORDER BY DEPARTURE_DELAY
""").df()
DuckDB treats the Pandas DataFrame df as a SQL table.

Much faster than Pandas.

Step 10 – Combine DuckDB and Pandas
Example:
Segment flights by distance:

SELECT
CASE
WHEN DISTANCE < 1000 THEN 'Short'
WHEN DISTANCE < 2000 THEN 'Medium'
ELSE 'Long'
END AS flight_type
This categorizes flights into:

Category	Distance
Short	< 1000
Medium	1000–2000
Long	> 2000

---

## Session 5

Vibe Analysis
Vibe analysis is analyzing data as if the analysis itself doesn't exist—you focus only on business outcomes, skipping intermediate steps. This approach emerged from vibe coding, where you code as if code doesn't exist. With vibe analysis, you give an LLM full context, state your goal, and review only the answers. The LLM handles exploration, cleaning, modeling, visualization, and deployment.

Core Vibe Analysis Workflow
From data to deployed insights without manual coding.

Automated exploration: Using LLMs to generate and test hypotheses.
Data quality automation: Detecting non-obvious issues and creating validation rules.
Visual storytelling: Building publication-ready data stories with style transfer.
Meta-prompting techniques: Improving prompts before execution.
The Traditional Data Science Workflow vs. Vibe Analysis
A data scientist typically:

Explores the data (EDA, profiling, types, missing values)
Cleans it (deduping, anomalies, schemas)
Models it (features, algorithms, parameters)
Explains it (narratives, visualizations, slides)
Deploys it (APIs, dashboards, reports)
Anonymizes it (synthetic data for case studies)
Vibe analysis automates most of this cycle.

What's Dying (Automated Tasks)
EDA: Profiling, types, missing values, deduping, anomaly detection.
Scaffolds: Loaders, schemas, docstrings, README files, tests.
AutoML: Feature selection, model choice, parameter tuning, metrics.
Code writing: LLMs can fill in 80% from specifications.
Explainers: Generating narratives, visuals, presentations.
Forms: Project reports, timesheets, documentation.
What's Rising (Critical Skills)
Leadership: Setting the right goal and allocation across human and AI teams.
Problem framing: Precise prompts that reduce iteration cycles.
Eval design: Automated validation with binary checks and LLM-as-judge.
Invariants: Defining ontologies, declaring truths and constraints.
Verticalization: Domain-specific datasets and workflows as competitive moats.
Trust & taste: Auditing AI output, telling compelling stories.
Automated Hypothesis Generation
Instead of manually exploring data, use LLMs to generate business hypotheses automatically. Let the LLM test everything in parallel. When done, have it craft an executive summary you can directly present.

Vibe Analysis Workflow Steps
1. Provide Context
Upload your dataset to ChatGPT, Claude, or Codex. Give it business context.

2. Request Comprehensive Analysis
Ask for specific analyses OR ask it to discover insights. The LLM will write Pandas/NumPy code, run statistical tests, generate visualizations, and create summaries.

3. Let it Work Autonomously
Use Agent Full Access mode to eliminate approval prompts. Run multiple agents in parallel—one for analysis, one for planning, one for visualization.

4. Find Non-Obvious Insights
Have the LLM focus on surprising patterns, such as data errors, anomalies, or quality issues.

Visual Data Stories
Create beautiful, interactive visualizations styled after leading publications.

Style Transfer Technique: Instead of specifying every detail, reference a style (e.g., "in the style of the New York Times").
Generate and Publish: The agent generates index.html, style.css, and script.js. You can then publish this directly to GitHub Pages.
Creating Synthetic Data with Hypotheses
Don't generate random fake data. Instead, align synthetic data with business hypotheses. The LLM creates data where these patterns hold, making it useful for demos and case studies without exposing real data.

Meta-Prompting
Use LLMs to optimize your prompts before running analysis.

Write your initial prompt.
Add: "Suggest an improved prompt for this".
Review the improved version.
Run the improved prompt in a fresh session.
Parallel Chat Strategy
Run multiple chats in parallel so you don't wait for agents to finish:

Chat 1: Main analysis and coding.
Chat 2: "What interesting, useful analysis can I run on this dataset?"
Chat 3: "Find the most interesting, useful, non-obvious insights."
Error Detection and Validation
Multi-model review: Ask different models to find errors. Many eyes make bugs shallow.
Checksum validation: Ask the LLM to provide category totals that sum to the overall total.
Post-validation prompts: After analysis, ask the LLM to find errors in its own analysis.
Context Management and Session Hygiene
Reset over repair: Long conversations accumulate bad assumptions ("context rot"). Start a fresh chat with a clean prompt instead of iterating through broken context.
Summarize and restart: Have the LLM summarize the prompt that will yield the exact final result, and run it in a new window.
Meta-Analysis
Analyze your analysis process by reviewing LLM action logs to continuously improve prompts, tools, and workflows.

Risk Mitigation Strategies
When shipping LLM insights to executives:

Frame safe questions: Focus on general business recommendations, options with tradeoffs, or directional insights.
