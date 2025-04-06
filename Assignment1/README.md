# Lifestyle Monitoring Dataset - Data Wrangling Project

This project demonstrates a comprehensive data wrangling process for a lifestyle monitoring dataset collected from wearable fitness trackers. The repository contains scripts to generate synthetic data, clean and transform the data, and visualize the results.

## Project Structure

```
├── data/
│   ├── lifestyle_monitoring.csv       # Original dataset with issues
│   ├── user_demographics.csv          # User demographic information
│   └── lifestyle_monitoring_cleaned.csv # Final cleaned dataset
├── visualizations/                    # Visualizations of the cleaned data
├── generate_dataset.py                # Script to generate synthetic data
├── data_wrangling.py                  # Script to clean and transform data
├── visualize_results.py               # Script to create visualizations
├── data_wrangling_report.md           # Detailed report on data wrangling methods
└── README.md                          # This file
```

## Requirements

- Python 3.7+
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

You can install the required packages using pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

## Usage Instructions

### 1. Generate the Dataset

To generate the synthetic dataset with intentional issues (missing values, inconsistencies, duplicates, outliers):

```bash
python generate_dataset.py
```

This will create:
- `data/lifestyle_monitoring.csv`: The main dataset with issues
- `data/user_demographics.csv`: Demographic information for merging

### 2. Clean and Transform the Data

To perform the data wrangling process:

```bash
python data_wrangling.py
```

This script:
- Handles missing values in Step_Count and Sleep_Duration
- Standardizes Device_Type names
- Removes duplicate records
- Detects and handles outliers in Heart_Rate
- Transforms the Activity_Level categorical variable
- Merges the main dataset with demographic information
- Creates the final cleaned dataset: `data/lifestyle_monitoring_cleaned.csv`

### 3. Visualize the Results

To create visualizations of the cleaned data:

```bash
python visualize_results.py
```

This generates several visualizations in the `visualizations/` directory:
- Activity level distribution
- Heart rate by activity level
- Device type distribution
- Steps vs. calories burned
- Age by activity level
- Steps per calorie by device type
- Correlation matrix of numeric variables

## Data Wrangling Tasks

The project addresses the following data wrangling tasks:

1. **Handling Missing Data**: Detection and imputation of missing values using group-based strategies
2. **Data Cleaning & Standardization**: Standardizing inconsistent naming conventions in Device_Type
3. **Removing Duplicates**: Identification and removal of duplicate records
4. **Outlier Detection**: Detection and handling of extreme values in Heart_Rate
5. **Data Transformation**: Conversion of Activity_Level categorical variable into numerical format
6. **Data Merging**: Merging with demographic details (age, gender, BMI)
7. **Final Dataset Preparation**: Final dataset cleaning and preparation

## Detailed Report

For a detailed explanation of the data wrangling methods and rationale, see [data_wrangling_report.md](data_wrangling_report.md).

## License

This project is available under the MIT License.

## Acknowledgments

This project is part of a data science assignment on data wrangling techniques. 