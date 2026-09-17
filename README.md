# ECE-2112-PA4

This repository contains the implementation for ECE 2112 - Experiment 4: Data Wrangling and Data Visualization. It demonstrates multi-condition Boolean filtering, column selection, group-based statistical aggregation, and multi-panel data visualization in Python using the board_exam.csv (ECE Board Exam 2) dataset. Key tasks include extracting specific student demographics based on categorical criteria, calculating class performance averages across different attributes, and generating informative bar charts to illustrate score trends without altering source data integrity.

Code: `import pandas as pd`

First, import the Pandas library into the Python environment using the standard alias to enable DataFrame operations and structured data manipulation.

## **A. VISAYAS COMMUNICATION DATAFRAME**

Load the raw student dataset (`board2.xlsx`) into Pandas and prepare the primary DataFrame by computing each student's overall exam average across all subjects (`Math`, `Electronics`, `GEAS`, `Communication`).

Using explicit multi-condition Boolean filtering via `.loc[]`, extract students whose `Hometown` is Visayas and whose `Track` is Communication. Retain only the required feature subset (`Name`, `Gender`, `Math`, `Electronics`, `Average`) in the output DataFrame and output the total count using `.shape[0]`.

## **B. VISAYAS FEMALE DATAFRAME**

Isolate female students from Visayas using multi-condition Boolean filtering on the primary DataFrame, selecting only key academic attributes (`Name`, `Track`, `GEAS`, `Electronics`, `Average`). Afterwards, execute a non-destructive conditional filter to extract students with an `Average` score of 60 or higher without modifying the parent `VisFemale` DataFrame.

Code Explanation:

`(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')`: Evaluates two Boolean conditions simultaneously using the element-wise & operator to identify qualifying rows.

`.loc[..., ['Name', 'Track', ...]]`: Slices both the matching rows and the specific list of columns in one step.

`VisFemale['Average'] >= 60`: Creates a secondary Boolean mask applied directly to VisFemale to filter for passing scores while leaving the source dataset intact.

## **C. CATEGORY-AVERAGE VISUALIZATION**

Calculate the mean `Average` score across categorical features (`Track`, `Gender`, `Hometown`), construct individual summary DataFrames for each, and generate a 3-panel bar chart figure. Finally, dynamically extract the highest-performing category for each feature using .idxmax() and print the analytical conclusions.

Code Explanation:

`df.loc[df['Track'] == 'Communication', 'Average'].mean()`: Isolates specific row groups per category mask and computes scalar mean values directly for manual table aggregation.

`pd.DataFrame({...})`: Packages calculated category metrics into explicit structured summary tables.  

`plt.subplots(1, 3, figsize=(15, 5))`: Initializes a 1-row by 3-column sub-plot grid layout to hold all bar chart visualizations side-by-side.  

`.idxmax()`: Returns the index location of the maximum score entry within each summary table, allowing `Track_table.loc[...]` to dynamically pull top-performing labels without hard-coding text outputs.  
