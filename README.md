The original dataset (banking_finance_dirty_dataset.csv) contained significant inconsistencies, missing values, and invalid entries. The data was cleaned and preprocessed using Python, Pandas, NumPy, and TheFuzz to prepare it for Exploratory Data Analysis (EDA) and Machine Learning.

The following cleaning operations were performed:

1. Structural Cleansing
Duplicates Removal: Dropped identical rows to prevent skewed analysis.
String Standardization: Applied str.strip() and str.title() across categorical columns. Replaced inconsistent abbreviations (e.g., 'Fd' → 'Fixed Deposit', 'Atm' → 'ATM').
Location Mapping: Standardized branch names (e.g., mapped 'Chi' to 'Chicago', 'La' to 'Los Angeles').
2. Fuzzy Matching for Categorical Grouping
Occupation Normalization: Used the thefuzz library to match misspelled and chaotic occupation entries to a master list (Engineer, Doctor, Teacher, Lawyer, Accountant) using an 80% similarity threshold. Unmatched entries were labeled as 'Unknown'.
3. Outlier and Invalid Data Handling
Age Validation: Removed physically impossible age values (negative numbers and ages > 100).
Credit Score Validation: Filtered out invalid FICO/VantageScore entries dropping scores below 350 or above 850.
Date Parsing: Converted account_open_date and transaction_date to standard datetime objects, coercing mixed formatting errors into NaT.
4. Missing Value Imputation
Numerical Imputation: Handled missing values for robust numerical columns (age, credit_score, balance_amount, loan_amount, annual_income, transaction_amount) by filling them with the median value to avoid skewing by outliers.
Categorical Imputation: Filled missing text data (gender, loan_status, loan_approved, occupation, email, notes) with the placeholder 'Unknown'.
Mode Imputation: Filled arbitrary missing branch locations using the statistical mode.
5. Feature Engineering & Flagging
Negative Income Flagging: Realized negative annual_income values existed. Rather than dropping them outright, created a boolean flag column (has_negative_income) to preserve the data anomaly, then replaced the negative amounts with the median for statistical normalcy.
Income Categorization: Created an income_flag column to categorize accounts as 'Suspicious - Negative', 'Suspicious - Extreme' (>$10M), or 'Normal'.
Output: The fully sanitized dataset was exported as Bank_financial_cleaned.csv for downstream analysis.
