# MMA Event Masterlist Data Cleaning Pipeline

This program is designed to clean and preprocess an MMA fight dataset, specifically an event masterlist. 
It performs several cleaning steps to ensure that key columns in the dataset are standardized, any missing values 
in critical fields are handled appropriately, and the final dataset is prepared for analysis. The pipeline focuses 
on cleaning columns such as 'weightclass', 'winner', 'height', and 'reach', as well as dropping rows with missing 
values in essential columns. The cleaned dataset is then saved to a new file.

## Functionality Overview:

### 1. **Weightclass Cleaning**:
   - The function `clean_weightclass` is responsible for standardizing the values in the 'weightclass' column. 
     It maps various keywords in the 'weightclass' field (e.g., 'straw', 'fly', 'bantam', etc.) to a set of predefined, 
     valid weight classes (e.g., 'Strawweight', 'Flyweight', 'Bantamweight', etc.). If no valid match is found, the 
     value is set to `NaN`.

### 2. **Winner Column Cleaning (No Contest and Draw Handling)**:
   - The function `clean_no_contest_and_draws` processes the 'winner' column. It handles cases where the 'winner' value 
     is 'N/A', indicating a No Contest or Draw scenario. If the method of victory includes 'Decision', the 'winner' is 
     changed to 'Draw'. Otherwise, the value is updated to 'NC' (No Contest). This ensures that the 'winner' column 
     reflects accurate outcomes for fights that did not have a clear winner.

### 3. **Height and Reach Cleaning**:
   - The function `clean_height_and_reach` removes double quotes from the 'reach' columns (e.g., 'X"') and converts both 
     height and reach values to floats. This ensures that the data for fighters' height and reach are in a standardized 
     format for easier analysis.

### 4. **Dropping Rows with Missing Values**:
   - The function `drop_nans` removes rows with missing values in critical columns. It focuses on essential fields such 
     as 'event_name', 'event_date', 'winner', 'fighter_a_name', 'fighter_b_name', 'weightclass', 'method_of_victory', 
     'round_of_victory', 'time_of_victory', 'time_format', and 'gender'. The program prints the number of rows dropped 
     and identifies which columns caused the rows to be removed.

### 5. **Diagnostics and Unique Value Checks**:
   - The program prints unique values from both the 'weightclass' and 'method_of_victory' columns for diagnostic purposes, 
     allowing the user to verify that the cleaning steps were applied correctly. If no rows with NaN values are found in 
     'method_of_victory', the program will print a message indicating this.

### 6. **Saving the Cleaned Dataset**:
   - After all the cleaning steps are applied, the program saves the cleaned dataset to a specified file path. 
     The cleaned file is saved in CSV format, and the path to the saved file is printed at the end of the process.

Pipeline Execution:
- The file path to the dataset is specified in the 'file_path' variable, and the main pipeline function `main_pipeline` 
  is responsible for calling each of the cleaning steps in the correct order. The cleaned data is saved to a new file 
  after the entire cleaning process is complete.

Example Usage:
1. Specify the path to the dataset in the `file_path` variable.
2. Run the `main_pipeline(file_path)` function to clean and preprocess the data.
3. Check the console output to see progress and diagnostic messages, including any rows dropped due to missing values 
   and which columns caused the drops.
4. The cleaned data will be saved to a new file, and the path will be printed to the console.

Key Notes:
- The handling of 'N/A' values in the 'winner' column assumes that 'N/A' signifies a No Contest or Draw.
- Height and reach values are cleaned by removing any double quotes and converting the remaining values to floats for 
  numerical analysis.

"""

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

