# Data Cleaning Report: Athlete Performance Analysis

## Overview
This report details the data cleaning process applied to an athlete performance dataset for a professional marathon runner. The dataset contains training metrics including speed, distance, heart rate, food intake, hydration levels, and environmental conditions. Several data quality issues were identified and addressed through a systematic cleaning process to prepare the data for meaningful analysis.

## Dataset Description
The original dataset contained 110 training session records with 22 variables, including:
- Session identifiers (ID, Date, Time)
- Performance metrics (Distance, Speed, Heart Rate, Calories Burned)
- Physiological factors (Food Item, Calorie Intake, Hydration Level)
- Environmental conditions (Temperature, Humidity)
- Subjective assessments (Training Effort, Session Rating, Recovery Score)
- Miscellaneous information (Shoe Brand, Notes, Social Media Followers, etc.)

## Data Quality Issues
Several data quality issues were identified in the original dataset:

1. **Missing Values**: Approximately 10-15% of values were missing in the Heart_Rate (13.64%), Calorie_Intake (9.09%), and Hydration_Level (11.82%) columns.

2. **Duplicate Records**: 20 records (10 unique session duplicates) had identical Session_ID, Date, and Time values.

3. **Inconsistent Formats**:
   - Time recorded in both 24-hour (45%) and 12-hour (55%) formats
   - Distance recorded in both miles (49%) and kilometers (51%)

4. **Outliers**: 2 records had speed values outside the expected range (below 1.56 m/s or above 7.34 m/s)

5. **Incorrect Data Entries**:
   - 16 food items had incorrect calorie values (e.g., "Banana" with 2000 calories)
   - 1 record had a negative hydration level

6. **Irrelevant Columns**: 4 columns (Athlete_Social_Media_Followers, Weather_Forecast_Accuracy, Local_Race_Participants, Training_Plan_Version) were not relevant to the athlete's performance analysis.

## Data Cleaning Methodology

### 1. Handling Missing Data

**Approach and Implementation:**
- **Heart_Rate**: Missing values were imputed using the median heart rate from similar training sessions based on distance bins. This approach leverages the relationship between exercise intensity (distance) and heart rate.
- **Calorie_Intake**: Missing values were imputed using the median calorie value for the same food item, preserving the relationship between specific foods and their typical calorie content.
- **Hydration_Level**: Missing values were imputed with the median hydration level after excluding negative values, ensuring physiologically plausible values.
- **Notes**: Missing values were left as is since they are descriptive and not critical for analysis.

**Justification:**
The imputation strategy preserved the logical relationships between variables. Using group-specific medians rather than global values maintains the natural patterns in the data, respecting the athlete's specific physiological responses to different training conditions. Median was chosen over mean to minimize the effect of outliers or extreme values that could skew imputations.

### 2. Removing Duplicate Records

**Approach and Implementation:**
- Identified duplicate training sessions based on identical Session_ID, Date, and Time values
- When duplicates were found, kept the record with fewer missing values
- Removed 10 duplicate records, reducing the dataset to 100 records

**Justification:**
Duplicate records would artificially weight certain training sessions in analysis, potentially biasing results. The strategy of keeping the most complete record ensures maximal data retention while eliminating redundancy. Preserving the record with fewer missing values minimizes the need for imputation in subsequent steps.

### 3. Standardizing Data Formats

**Approach and Implementation:**
- **Time Format**: Converted all times to 24-hour format using a custom function that handled special cases like 12 AM/PM
- **Distance Units**: Standardized all distance measurements to kilometers by applying the conversion factor of 1.60934 to values recorded in miles

**Justification:**
Standardized formats are essential for consistent time-series analysis and accurate comparisons between training sessions. The 24-hour time format was chosen as it aligns with scientific standards and eliminates AM/PM ambiguity. Kilometers were selected as the distance unit to align with the international standard for running metrics, facilitating comparison with benchmark data.

### 4. Identifying and Handling Outliers

**Approach and Implementation:**
- Used the Interquartile Range (IQR) method to identify outliers in the Speed column
- Calculated bounds: [Q1 - 1.5 * IQR, Q3 + 1.5 * IQR] = [1.56, 7.34] m/s
- Identified 2 outliers: one very slow (1.03 m/s) and one very fast (9.80 m/s)
- Capped extreme values at the calculated bounds rather than removing them

**Justification:**
The IQR method is robust for outlier detection as it's not influenced by extreme values. Capping rather than removing outliers preserves the record count and training session continuity while preventing extreme values from skewing statistical analyses. The bounds (1.56 to 7.34 m/s) represent reasonable speed ranges for marathon training, from slow recovery runs to sprint intervals.

### 5. Correcting Data Entry Errors

**Approach and Implementation:**
- **Food Calorie Corrections**: Identified 16 records with implausibly high calorie values (e.g., 2000 calories for a banana) and replaced them with accurate reference values from a nutrition database
- **Negative Hydration**: Converted 1 negative hydration level to its absolute value, maintaining the magnitude while correcting the sign error

**Justification:**
Correcting these errors was critical as they would severely impact nutritional and hydration analyses. For food calories, using reference values from established nutrition databases ensures accuracy. Converting negative hydration to positive preserves the recorded value's magnitude while making it physiologically plausible. These corrections maintain data integrity without sacrificing data points.

### 6. Dropping Irrelevant Columns

**Approach and Implementation:**
- Identified and removed 4 columns not relevant to performance analysis:
  - Athlete_Social_Media_Followers
  - Weather_Forecast_Accuracy
  - Local_Race_Participants
  - Training_Plan_Version

**Justification:**
These columns had no clear causal relationship with athletic performance and would introduce noise to analyses. Removing them simplifies the dataset, improves computational efficiency, and focuses the analysis on performance-relevant variables. This decision was made after careful consideration of which variables could theoretically impact training outcomes.

### 7. Final Dataset Preparation

**Approach and Implementation:**
- **Data Type Optimization**: Converted columns to appropriate data types (int, float, object)
- **Derived Metrics Creation**:
  - Calories_Per_Km: Calories burned per kilometer (efficiency metric)
  - Training_Efficiency: Speed relative to heart rate (cardiovascular efficiency)
  - Hydration_Ratio: Hydration level per kilometer (hydration strategy metric)
- **Data Sorting**: Arranged records chronologically by date and time
- **Final Quality Check**: Verified no remaining data issues

**Justification:**
Proper data types ensure accurate calculations and optimal storage. The derived metrics provide valuable performance insights beyond raw data, enabling deeper analysis of training efficiency and physiological responses. Chronological sorting facilitates time-series analysis and progression tracking.

## Results and Impact

The data cleaning process successfully addressed all identified issues, resulting in a high-quality dataset ready for analysis:

- **Completeness**: All critical variables now have 100% completeness
- **Consistency**: All times are in 24-hour format and distances in kilometers
- **Accuracy**: Food calorie values and hydration levels are now physiologically plausible
- **Relevance**: Dataset contains only performance-relevant variables
- **Enhanced Analysis Potential**: New derived metrics enable deeper performance insights

The final cleaned dataset contains 100 records with 21 columns, providing a comprehensive yet focused view of the athlete's training performance. This clean dataset will enable more accurate analysis of training patterns, physiological responses, and performance optimization strategies.

## Conclusion

The systematic data cleaning process transformed a problematic dataset with missing values, inconsistencies, and errors into a reliable foundation for athletic performance analysis. The careful consideration of domain knowledge in each cleaning step (e.g., using training intensity to guide heart rate imputation) ensures that the cleaned data maintains its physiological relevance while eliminating noise and errors.

This clean dataset will allow sports scientists to identify optimal training patterns, nutrition strategies, and recovery approaches, ultimately supporting the marathon runner's performance goals. 