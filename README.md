# Cars Dataset - Data Cleaning, Feature Engineering & EDA

This repository contains a Jupyter Notebook for rigorous data cleaning, missing value imputation, advanced feature engineering, and exploratory data analysis (EDA) on a cars marketplace dataset.

## Project Overview
The goal of this project is to fix significant data inconsistencies, impute missing technical specifications, build predictive features from complex raw text strings, and discover key marketplace trends driving car prices.

## Key Steps & Implementation

### 1. Data Inspection & Missing Value Imputation
* Loaded the dataset and adjusted pandas display options to handle a large number of rows and columns without wrapping.
* Checked the overall structural overview via `.info()`, `.describe()`, and `.isnull()`.
* Imputed missing values in categorical columns like `DealType` using the **mode**.

### 2. Deep Data Cleaning & Inconsistency Fixes
* **MPG Columns Logic Fix**: Identified records where `MinMPG` was larger than `MaxMPG` and swapped their values to maintain physical logic.
* **Zero-Value Treatment**: Replaced impossible zero values (`0`) in `MinMPG` and `MaxMPG` with `NaN`. Grouped by combinations of `Year`, `Make`, `Model`, and `Drivetrain` to sequentially impute these values using group-level **medians**.
* **Target Feature Scrubbing (`Price`)**: Extracted and dropped target rows containing placeholders like `"Not Priced"`. Formatted the column by removing raw currency strings (`$`, `,`) and converted the column into a proper numeric data type.
* **Outliers & Duplicates**: Found extreme pricing anomalies by sorting, dropping rows with pricing errors exceeding $400,000. Checked for exact duplicates and removed them to ensure sample integrity.

### 3. Feature Engineering & Standardizing Complex Attributes
* **Used/Certified Conversion**: Simplified the complex `Used/New` column into a clear binary label `Used/Certified` where `0` represents used and `1` stands for company-certified vehicles.
* **Drivetrain & Fuel Type Mapping**: Standardized messy shorthand categories into explicit, unified groups (`FWD`, `AWD`, `4WD`, `RWD`). Mapped overlapping fuel terms (`Gasoline Fuel`, `Flexible Fuel`, etc.) into neat identifiers (`Gasoline`, `E85 Flex Fuel`, `Diesel`, `Electric`). Explicitly corrected a structural data anomaly where certain Tesla vehicles were mislabeled with gasoline engines.
* **Transmission Categories**: Applied regex string matching to consolidate endless naming synonyms into fixed macro groups: `Automatic`, `CVT`, `Manual`, and `Single-speed` (assigned uniformly to pure electric vehicles).
* **Cylinders Extraction**: Used complex regular expressions to extract cylinder configurations directly out of the raw `Engine` text block (e.g., pulling `I4`, `V6`, `V8`, `V10`, `V12`, `H4`) and marked electric engines explicitly.
* **Turbo/Supercharged Flag**: Extracted charging tags directly from engine data into an engineered flag indicating whether a car is `Turbo`, `Twin Turbo`, `Supercharged`, or `Not Charged`.

### 4. Exploratory Data Analysis (EDA) Insights
* **Price Distribution**: Most car marketplace values scale heavily within the $10,000 to $100,000 baseline, showing an expected right-skewed distribution that stabilizes on a log-scale.
* **Year & Depreciation**: Plotting line and boxen plots shows a clear upward trend in prices over time, capturing vehicle depreciation patterns.
* **Condition & Seller Types**: Certified vehicles maintain a significantly higher median price compared to standard used models. Private sellers list cars at noticeably lower prices compared to commercial vehicle dealers.
* **Consumer Ratings Correlations**: Regressions and joint plots reveal that highly-priced luxury vehicles inversely score lower on `ValueForMoneyRating` and `ReliabilityRating`, whereas affordable options score much higher.
* **Mileage Influence**: Regressions show a steep, negative trend verifying that market value scales down consistently as accumulated vehicle mileage increases.
* **Powertrain, Drivetrain, & Layout Mechanics**: Rear-wheel drive (`RWD`) profiles lean closely toward a higher cluster of luxury selections. Multi-cylinder engines like `V10`, `V12`, and `W12` are isolated strictly within high-end luxury classes, while electric models occupy premium price spaces without cheap entries.

## Tech Stack
* **Language**: Python
* **Libraries**: Pandas, NumPy, Seaborn, Matplotlib
