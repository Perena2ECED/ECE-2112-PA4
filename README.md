# ECE-2112-PA4
Paulene Anne V. Pereña <br>
2ECE-D

This repository contains the Programming Assignment 2 for the course Advanced Computer Programming (ECE2112). This project consists of three Python problems assigned to Module 4: Data Wrangling and Visualization.

The specific functions and syntax structures utilized throughout the codebase were implemented as follows:
** import pandas
** df
  

# A. Visayas Communication DataFrame
The problem asks to create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track is Communication, while retaining only Name, Gender, Math, Electronics, and Average, displaying the number of rows.

* Since the problem asks for an average and the given DataFrame doesn't have a column for the average, the `df['Average'] = df[['Math', 'Electronics', 'GEAS']].mean(axis=1)` syntax is used to calculate the arithmetic mean or average across specific subjects for each student and store under a new column named `Average.`
  * `df[['Math', 'Electronics', 'GEAS']]` --> it functions to select a subset of columns containing the target subject requested from the DataFrame as requested from the problem to isolate them for calculation.
  * `.mean(axis=1`) --> it functions as a parameter instructing pandas to compute the average horizontally (row-wise across columns) rather than vertically (column-wise).
 
    ```
    df['Average'] = df[['Math', 'Electronics', 'GEAS']].mean(axis=1)
    df['Average']

    This evaluates to the average of the subjects of Math, Electronics, and GEAS of each      student.
    ```

* The `filtered_df = df[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')]` is used to extract a specific subset of data by applying multiple conditional filters simultaneously stored under an arbitrary variable named `filtered-df.`
  * The `df['Hometown'] == 'Visayas' --> This functions to isolate records  from the DataFrame where the student's hometown is specifically from the Visayas region.
  * `&` --> It functions as a logical `AND` operator, ensuring that a row is only kept if both criteria are satisfied at the same time.
  * `df['Track'] == 'Communication'` --> It functions to isolate records from the DataFrame on which student's specialization track is explicitly set to communication. 

  <img width="567" height="177" alt="image" src="https://github.com/user-attachments/assets/e0c007d2-5e0f-455b-9e45-aee922ff8995" />

* The `Viscomm = filtered_df[['Name', 'Gender', 'Math', 'Electronics', 'Average']]` functions to create a subset DataFrame by selecting only specific relevant columns filtered from the larger dataset.
  * `'Name', 'Gender', 'Math', 'Electronics', 'Average'` --> It functions to serve as a structural column filter, removing unnecessary fields to isolate only the asked demographics and subject scores.
    <img width="281" height="163" alt="image" src="https://github.com/user-attachments/assets/4403f07e-4995-41e1-a01e-fcdf91207e94" />

* The `rows =len(Viscomm)` function serves as a built-in Python function that measures the total number of rows or the vertical length of the final dataset stored under the arbitrary variable `rows`.
  ```
  rows = len(Viscomm)
  rows

  5
  ```

# B. Visayas Female DataFrame
The problem asks to display a second DataFrame named VisFemale whose Hometown is Visayas and is a Female while retaining only the Name, Track, GEAS, Electronics, Average also displaying the rows of whose Average is at least 60.

* The `VisFemale = df[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')][['Name', 'Track', 'GEAS', 'Electronics', 'Average']]` functions to extract the asked columns from a certain demographic group and store it under an arbitrary variable `VisFemale`.
  * The `df['Gender'] == 'Female'` --> It functions to isolate records of students whose identity matches the female criteria.
  * [['Name', 'Track', 'GEAS', 'Electronics', 'Average']] --> It functions to select columns that are asked by the problem and store them in a DataFrame.
 
  <img width="322" height="177" alt="image" src="https://github.com/user-attachments/assets/b51d4bf5-901a-4700-b792-e0d1153a4aa0" />

* The `VisFemale.loc[(VisFemale['Average'] > 60)]` is used to filter out students from the isolated demographic group based on a numerical threshold of at least 60.
  * `.loc[]` --> It functions as a label-based data selector that scans the rows of the DataFrame to find positions where the given condition evaluates to true.
  * `.VisFemale['Average'] > 60` --> It checks each student's average grade and isolates rows where the value strictly exceeds 60.
 
    <img width="332" height="157" alt="image" src="https://github.com/user-attachments/assets/21b38629-1b50-482e-b3c9-60fa4956ed2a" />


# C. Category Average Visualization
The problem asks to display the summary of Track, Gender, and Hometown, and to create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown, also providing an interpretation for the group with the largest sample size for each feature.

a. 
* The `Summary_of_AskedColumn = df.groupby('AskedColumn')['Average'].mean().reset_index()` is used to break down the main dataset by student track categories and calculate the average score for each academic track stored under the `Summary_of_Track`.
 * `df.groupby()`--> It functions to split the original DataFrame into subsets based on the categories asked per column.
 * '[Average]` --> It functions to isolate the numerical average grade column from the grouped data subset so that subsequent calculations are restricted to this variable.
 * `.mean()` --> It functions as an aggregation operation that computes the average score for each group.
 * `.reset_index()` --> It functions to convert the grouped category names back from index labels into a flat DataFrame columns while resetting the row index to a standard sequence of numbers starting from zero.

For the ('AskedColumn'):
* `('Track')` --> used to get the mean average score grouped by each specialization track.
* `('Gender')` --> used to get the mean average score grouped by student gender demographics.
* `('Hometown')` --> used to get the mean average score by geographic hometown regions.

b. 
The display of all three summary tables asked:

<img width="237" height="411" alt="image" src="https://github.com/user-attachments/assets/f43cfd88-dbe3-4f72-b029-a403866cc0ab" />

c. 
* The `import matplotlib.pyplot as plt` functions to import the necessary visualization framework and establish a shorthand prefix for all graphing operations.

* The `plt.figure(figsize=18,5))` function initializes the structural plot window size to a custom frame width of 18 inches and a height of 5 inches.
  
* The `plt.subplot(1, 3, 1)` function splits the active canvas area into a multi-graph grid layout with 1 row and 3 columns, while designating the target workspace slot.
  * `(1, 3, 1)` --> used to declare the first positional grid slot designated for the specialization track bar plot.
  * `(1, 3, 2)` --> used to declare the second positional grid slot designated for the student gender distribution bar plot.
  * `(1, 3, 3)` --> used to declare the third positional grid slot designated for the geographic hometown breakdown bar plot.
    
* The `plt.bar()` functions as a geometric plotting operation that translates inoque feature values onto horizontal categories and matches their mean values to vertical bar heights.
  * `Summary_of_AskedColumn['AskedColumn'], Summary_of_AskedColumn['Average']` --> is used together as the primary inputs to map the unique categorical labels onto the horizontal X-axis and match them directly with their corresponding numerical performance means on the vertical Y-axis.
   
* The `plt.ylim(0, 100)` function clamps the vertical numeric axis from a minimum baseline of 0 up to a standardized max ceiling of 100.
* The `plt.tight_layout` function auto-calculates structural border margins and adjusts spaces to completely eliminate text and label clipping overlaps.


<img width="852" height="216" alt="image" src="https://github.com/user-attachments/assets/5582f6ed-b694-4d36-af1b-47af1aae5903" />

**INTERPRETATION 
 


# Version History

* 13 September 2026 --> The README file was created and is continuously being updated.
* 16 September 2026 --> The README file is still continuously being updated.  
