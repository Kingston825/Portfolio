# README: Multi-Source Obesity & Nutrition Data Integration

---

## 🧐 Project Overview

This project involves the collection, cleaning, and integration of data related to nutrition, physical activity, and obesity in the United States from three distinct sources: a CSV file, an HTML table from Wikipedia, and a public API.

The primary goal is to perform Extract, Transform, Load (ETL) operations on each dataset, standardize the data, and load it into a central **SQLite database**. Finally, the integrated data is queried and used for analysis and visualization.

---

## 💾 Data Sources & Transformations

### Dataset 1: CSV

* **Source:** `Nutrition__Physical_Activity__and_Obesity.csv`.
* **Transformations:**
    * Removed data from U.S. territories (PR, GU, VI) to focus on states.
    * Dropped columns containing only null values or footnotes (`Data_Value_Footnote_Symbol`, `Data_Value_Footnote`, `Data_Value_Unit`).
    * Removed rows where the `Data_Value` was null.
    * Filtered out data from years 2020-2022, as it was considered potentially skewed by the COVID-19 pandemic.
    * Standardized values in the `Stratification1` column (e.g., 'Non-Hispanic Black' to 'Black, non-Hispanic', various income ranges) to ensure consistency for future joins.

### Dataset 2: HTML (Web Scraping)

* **Source:** Wikipedia article: "[Obesity in the United States](https://en.wikipedia.org/wiki/Obesity_in_the_United_States)".
* **Transformations:**
    * Used `pandas.read_html` to scrape the second table on the page.
    * Corrected the multi-index header by assigning new, clean column names (e.g., 'State', 'Obesity rank', 'adult_2020').
    * Set the 'State' column as the DataFrame index.
    * Removed data for territories (e.g., 'American Samoa', 'Guam').
    * Cleaned percentage columns (e.g., '30.1%') by removing the '%' symbol to allow for numerical analysis.

### Dataset 3: API

* **Source:** `data.cdc.gov` Socrata Open Data API, specifically the "Overweight and Obesity (BMI)" dataset.
* **Transformations:**
    * Data was fetched using the `sodapy` client library.
    * The resulting JSON data was converted into a pandas DataFrame (`Dataset3`) for processing.

---

## 🗃️ Database Integration

1.  A connection to a new SQLite database (`final_ms5.db`) was established.
2.  The three cleaned DataFrames (`Dataset1`, `Dataset2`, `Dataset3`) were written to the database as new tables:
    * `csv_data`
    * `html_data`
    * `api_data`

---

## 📊 Analysis & Visualization

* A final `combined_df` was created by executing a SQL query on the `final_ms5.db` database, joining the `csv_data`, `api_data`, and `html_data` tables.
* Data types for numerical columns in the combined data were converted to `float` to allow for calculations.
* The project includes generating at least five visualizations from the cleansed and combined data, demonstrating insights across the different sources.

---

## 🛠️ Dependencies

* `numpy`
* `pandas`
* `bs4` (BeautifulSoup)
* `requests`
* `sodapy` (for Socrata API)
* `sqlite3`
* `matplotlib.pyplot`