## ETL Decisions

### Decision 1 – Standardizing Date Formats
**Problem:**  
The raw dataset contained date entries in multiple inconsistent formats, including 'DD/MM/YYYY', 'DD-MM-YYYY', and 'YYYY-MM-DD'. This variation makes it challenging to carry out time-based analysis and grouping within SQL queries.

**Resolution:**  
All date values were unified into the standard 'YYYY-MM-DD' format prior to loading into the 'dim_date' table. This guarantees consistency and enables accurate extraction of day, month, and year components for analytical purposes.

### Decision 2 – Standardizing Category Values
**Problem:**  
The 'category' column contained inconsistent entries such as 'electronics', 'Electronics', 'Groceries', and 'Grocery'. These variations produce incorrect aggregation results when data is grouped by category.

**Resolution:**  
All category values were normalized into a uniform format:
- 'electronics' → 'Electronics'
- 'Groceries' → 'Grocery'  
This correction ensured precise grouping and reliable reporting across analytical queries.

### Decision 3 – Handling Missing Values
**Problem:**  
Certain records contained missing or NULL values in fields such as 'store_city'. These gaps can disrupt joins and degrade the overall quality of data within the warehouse.

**Resolution:**  
Missing values were addressed by substituting them with a default placeholder such as '"Unknown"', or by deriving the correct value where it could be reasonably inferred. This approach ensured that all dimension tables preserve referential integrity and that no NULL values interfere with the analysis.