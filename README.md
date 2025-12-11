# Nutrition Dataset Cleaning & Preprocessing in Python

This project presents a complete end to end cleaning and preprocessing workflow for a large, inconsistent nutrition dataset using Jupyter Notebook.  
The dataset originally stored nutrient values as *text mixed with units* (e.g., “7 g”, “30 mg”), making numeric analysis impossible.  
This project converts it into a **fully numeric, standardized, analysis-ready dataset**.

---

## Table of Contents
- Project Overview  
- Dataset Description  
- Technologies Used  
- Cleaning Challenges  
- Step-by-Step Workflow  
- Egg Sub-Analysis Example  
- Quality Checks  
- Files Included  
- How to Run This Project  
- Future Enhancements  
- Conclusion & Next Steps  
- What This Project Demonstrates  

---

## Project Overview

The nutrition dataset contained thousands of food items with nutrient values stored as inconsistent text strings.  
The primary goal was to:

1. Extract units correctly  
2. Clean and convert all values to floating-point numbers  
3. Standardize column names  
4. Handle missing values  
5. Create a reproducible preprocessing pipeline  
6. Export a clean dataset ready for analysis or machine-learning tasks  

The final cleaned file is exported as:

**`cleaned_nutrition.xlsx`**

---

## Dataset Description

The raw dataset includes:

- **7,889 rows**  
- **77 nutrient-related columns**  
- Nutrient groups: minerals, vitamins, fats, amino acids, sugars, carbs, proteins, and more  
- A `name` column representing each food item  

### Common issues found:

- Values stored as strings mixed with units  
- Columns not numeric  
- Missing values in key nutrient fields  
- No standardized column naming convention  
- Multiple unit types across columns (g, mg, mcg, IU, etc.)

---

## Technologies Used

- **Python 3**  
- **Pandas**  
- **NumPy**  
- **Jupyter Notebook**

---

## Cleaning Challenges

### 1. Mixed Units Within Values
Examples:  
- `"7 g"`  
- `"45 mg"`  
- `"1.2 mcg"`  

These prevented any numeric operations.

### 2. No Unit Labels in Column Names  
Units needed to be extracted automatically and appended to column names.  
Examples:  

- `cholesterol` → `cholesterol_mg`  
- `fat` → `fat_g`  

### 3. Missing Values  
Some nutrient fields were incomplete and required imputation.

### 4. Subsetting a Category  
Egg-related foods needed to be filtered for an additional demonstration.

---

## Step-by-Step Workflow

### 1. Import Libraries
```python
import pandas as pd
import numpy as np

### 2. Load Dataset

df = pd.read_csv("nutrition.csv")

### 3. Remove Unnecessary Columns

Dropped columns:
	•	serving_size
	•	unnamed index-like columns

df = df.loc[:, ~df.columns.str.contains("unnamed", case=False)]
df = df.drop(columns=["serving_size"], errors="ignore")

### 4. Extract Units From a Complete Row

Row 24 was selected as a fully populated reference row.
sample_row = df.iloc[24]


### 5. Create New Column Names With Units

Automatically extracted units and appended them to column names.
Examples:
	•	cholesterol → cholesterol_mg
	•	sodium → sodium_mg

### 6. Strip Units and Convert Values to Floats

Converted text values like "7 mg" to 7.0.

df[col] = df[col].str.replace("[A-Za-z]", "", regex=True).astype(float)

### 7. Convert Entire Dataset to Numeric Format

All nutrient columns converted to numeric (float64).

### 8. Subset Egg-Related Foods

df["name"] = df["name"].str.lower()
eggs = df[df["name"].str.contains("egg", regex=True)]

### 9. Handle Missing Values (Egg Subset Example)

eggs["saturated_fat_g"].fillna(eggs["saturated_fat_g"].median(), inplace=True)

### 10. Export Final Cleaned Dataset

df.to_excel("cleaned_nutrition.xlsx", index=False)

## Egg Sub-Analysis Example

The egg subset contains 155 rows.

## Cleaning actions included:
	•	Converting all nutrient columns to float
	•	Handling missing values
	•	Removing units
	•	Standardizing column names
	•	Ensuring clean, consistent values

⸻

## Quality Checks

Before export, the following validations were performed:
	•	Dataset shape confirmed as (7889, 75)
	•	Verified all nutrient fields are numeric
	•	Ensured all values contain no alphabetic characters
	•	Confirmed correct unit suffixes on column names
	•	Verified missing values were handled

⸻

## Files Included
	•	nutrition.csv — raw dataset
	•	nutrition.ipynb — full preprocessing notebook
	•	nutrition.xlsx — intermediate working file
	•	cleaned_nutrition.xlsx — final processed dataset

⸻

## How to Run This Project
	1.	Clone or download the repository
	2.	Open nutrition.ipynb in Jupyter Notebook
	3.	Run all cells from top to bottom
	4.	The cleaned file will be generated automatically as:

cleaned_nutrition.xlsx

## Future Enhancements
	•	Automated unit detection module
Identify units even when inconsistent across rows.
	•	Predictive modeling
Use machine learning to estimate missing nutrient values.
	•	Visualization module
Add histograms, distribution plots, and nutrient comparison charts.
	•	API-ready formatting
Convert cleaned data into a structured format for nutrition apps.
	•	Unit-conversion automation
Convert all nutrients to a single scale (e.g., everything to grams).

⸻

## Conclusion & Next Steps

This project successfully transformed a large, messy, unit-mixed dataset into a clean, numeric, standardized file ready for serious analysis.
All preprocessing steps were automated to ensure reproducibility, reliability, and scalability.

With this foundation, the dataset can now support:
	•	Nutrient analysis dashboards
	•	Statistical modeling
	•	Clustering of similar foods
	•	Machine-learning predictions
	•	Nutrition recommendation systems

⸻

## What This Project Demonstrates
	•	Strong data-cleaning skills using Pandas
	•	Regex proficiency for extracting units
	•	End-to-end pipeline creation
	•	Clean dataset export for business or ML use
	•	Ability to handle large, inconsistent real-world data








