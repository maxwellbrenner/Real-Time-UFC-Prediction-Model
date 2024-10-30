# MMA Event Masterlist Data Cleaning Pipeline

## Overview

This program is designed to clean and preprocess an MMA fight dataset, specifically an event masterlist. It ensures that key columns in the dataset are standardized, critical missing values are handled appropriately, and the final dataset is prepared for analysis. This pipeline covers cleaning columns such as 'weightclass', 'winner', 'height', and 'reach', as well as dropping rows with missing values in essential columns. The cleaned dataset is saved to a new file for further analysis.

## Function Descriptions (Ordered by Execution in `main_pipeline()`)

### 1. `clean_weightclass(df)`
- **Description**: Standardizes values in the 'weightclass' column. This function maps keywords found in the 'weightclass' field (e.g., 'straw', 'fly', 'bantam') to valid weight classes (e.g., 'Strawweight', 'Flyweight', 'Bantamweight'). If no valid match is found, the value is set to `NaN`.

### 2. `clean_no_contest_and_draws(df)`
- **Description**: Processes the 'winner' column to handle No Contest and Draw cases. If 'winner' is marked as 'N/A' and the method of victory includes 'Decision', the 'winner' is set to 'Draw'; otherwise, it is set to 'NC' (No Contest). This function ensures that the 'winner' column reflects accurate outcomes for fights without a clear winner.

### 3. `clean_height_and_reach(df)`
- **Description**: Cleans the 'height' and 'reach' columns by removing double quotes and converting values to floats. This standardizes height and reach data for numerical analysis.

### 4. `clean_title_fight(df)`
- **Description**: Corrects the 'title_fight' column based on the 'time_format' column. If 'title_fight' is marked as `True` but 'time_format' does not indicate a 5-round fight, the value is changed to `False`.

### 5. `clean_time_format(df)`
- **Description**: Cleans the 'time_format' column by extracting the number of rounds from the beginning of the string and converting it to an integer. If extraction fails, the value is set to `NaN`.

### 6. `drop_nans(df)`
- **Description**: Drops rows with missing values in essential columns. Focuses on columns such as 'event_name', 'event_date', 'winner', 'fighter_a_name', 'fighter_b_name', 'weightclass', 'method_of_victory', 'round_of_victory', 'time_of_victory', 'time_format', 'gender', and 'title_fight'. This function prints the number of rows dropped and identifies columns responsible for missing values.

---

## Execution Flow in `main_pipeline(file_path)`

1. **Load Dataset**: Reads the dataset from the specified file path.
2. **Weightclass Cleaning**: Calls `clean_weightclass()` to standardize values in the 'weightclass' column.
3. **Winner Column Cleaning**: Uses `clean_no_contest_and_draws()` to handle cases where 'winner' is marked as 'N/A'.
4. **Height and Reach Cleaning**: Cleans height and reach columns with `clean_height_and_reach()`.
5. **Title Fight Cleaning**: Calls `clean_title_fight()` to ensure the 'title_fight' column aligns with the number of rounds.
6. **Time Format Cleaning**: Cleans the 'time_format' column using `clean_time_format()`.
7. **Drop Rows with Missing Values**: Drops rows with `NaN` values in essential columns using `drop_nans()`.
8. **Save Cleaned Dataset**: Saves the cleaned dataset to a new file path and prints the file location.

---

## Example Usage

1. **Specify Dataset Path**: Set the file path of the dataset in the `file_path` variable.
2. **Run Cleaning Pipeline**: Call `main_pipeline(file_path)` to initiate data cleaning and preprocessing.
3. **Console Output**: Check console messages for progress updates, diagnostics, and dropped rows.
4. **Output File**: The cleaned data will be saved in CSV format, and the file path will be printed.

---

## Important Considerations

- **Expected Columns**: The program assumes the dataset contains columns such as 'weightclass', 'method_of_victory', 'winner', 'fighter_a_height', 'fighter_b_height', etc.
- **Winner Column Handling**: 'N/A' in the 'winner' column signifies a No Contest or Draw.
- **Height and Reach Formatting**: The program removes double quotes in height and reach values and converts the values to floats for numerical analysis.

---

## File Path and Output

The program saves the cleaned dataset to a specified file path in CSV format. Ensure the file path is correctly set in the `output_file_path` variable.

Example:
```python
output_file_path = r"C:\Users\EditZ\UFC Research\New Pipeline\event_masterlist_initial_clean.csv"

