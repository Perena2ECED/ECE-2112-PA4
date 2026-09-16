# ECE-2112-PA4
Paulene Anne V. Pereña <br>
2ECE-D

This repository contains the Programming Assignment 2 for the course Advanced Computer Programming (ECE2112). This project consists of three Python problems assigned to __Module 4: Data Wrangling and Visualization.__

The specific functions and syntax structures utilized throughout the codebase were implemented as follows:

* The statement `import pandas as pd` loads an external data library into the environment. The pd creates a shortened namespace handle to lessen typing time.
* The function `pd.read_excel("file name")` syntax is used to load an Excel file and automatically convert its rows and columns into a two-dimensional pd.DataFrame data structure.

  ```
  ECE_Board_Exam_2 = pd.read_excel('board2.xlsx')
  ECE_Board_Exam_2

  This evaluates to the two-dimensional DataFrame created for the excel file.
  ```

# A. Visayas Communication DataFrame
The problem asks to create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track is Communication, retaining only Name, Gender, Math, Electronics, and Average, and display the number of rows.

* Since the problem asks for an average and the given DataFrame doesn't have a column for the average, the `ECE_Board_Exam_2['Average'] = ECE_Board_Exam_2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)` syntax is used to calculate the arithmetic mean or average across specific subjects for each student and store under a new column named `Average.`
  * `ECE_Board_Exam_2[['Math', 'Electronics', 'GEAS', 'Communication']]` --> it functions to select a subset of columns containing the target subject requested from the DataFrame, as requested from the problem, to isolate them for calculation.
  * `.mean(axis=1`)` --> it functions as a parameter instructing pandas to compute the average horizontally (row-wise across columns) rather than vertically (column-wise).
 
    ```
    ECE_Board_Exam_2['Average'] = ECE_Board_Exam_2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
    ECE_Board_Exam_2['Average']

    This evaluates to the average of the subjects of Math, Electronics, GEAS, and Communication of each      student.
    ```

* The `VisComm = ECE_Board_Exam_2[(ECE_Board_Exam_2['Hometown'] == 'Visayas') & (ECE_Board_Exam_2['Track'] == 'Communication')]` is used to extract a specific subset of data by applying multiple conditional filters simultaneously stored under an arbitrary variable named `VisComm.`
  * The `ECE_Board_Exam_2['Hometown'] == 'Visayas'` --> This functions to isolate records  from the DataFrame where the student's hometown is specifically from the Visayas region.
  * `&` --> It functions as a logical `AND` operator, ensuring that a row is only kept if both criteria are satisfied at the same time.
  * `ECE_Board_Exam_2['Track'] == 'Communication'` --> It functions to isolate records from the DataFrame on which student's specialization track is explicitly set to communication. 

 <img width="758" height="220" alt="image" src="https://github.com/user-attachments/assets/4ad6c9c2-1317-4a77-a3d3-c890922f12b4" />




* The `VisComm = VisComm[['Name', 'Gender', 'Math', 'Electronics', 'Average']]` functions to create a subset DataFrame by selecting only specific relevant columns filtered from the larger dataset.
  * `[['Name', 'Gender', 'Math', 'Electronics', 'Average']]` --> It functions to serve as a structural column filter, removing unnecessary fields to isolate only the asked demographics and subject scores.
 
  
   <img width="472" height="236" alt="image" src="https://github.com/user-attachments/assets/2da86318-e7d3-4aaa-a366-29641eeeb52f" />


* The `rows =len(VisComm)` function serves as a built-in Python function that measures the total number of rows or the vertical length of the final dataset stored under the arbitrary variable `rows`.
  ```
  rows = len(VisComm)
  rows

  5
  ```

# B. Visayas Female DataFrame
The problem asks to display a second DataFrame named VisFemale whose Hometown is Visayas and is a Female, while retaining only the Name, Track, GEAS, Electronics, Average, and also displaying the rows whose Average is at least 60.

* The `VisFemale = ECE_Board_Exam_2[(ECE_Board_Exam_2['Hometown'] == 'Visayas') & (ECE_Board_Exam_2['Gender'] == 'Female')][['Name', 'Track', 'GEAS', 'Electronics', 'Average']]` functions to extract the asked columns from a certain demographic group and store it under an arbitrary variable `VisFemale.`
  * The `ECE_Board_Exam_2['Gender'] == 'Female'` --> It functions to isolate records of students whose identity matches the female criteria.
  * `[['Name', 'Track', 'GEAS', 'Electronics', 'Average']]` --> It functions to select columns that are asked by the problem and store them in the DataFrame.
 
  <img width="1525" height="350" alt="image" src="https://github.com/user-attachments/assets/f84cbe70-4d67-49de-9f55-969c1c2f3430" />


* The `VisFemale.loc[(VisFemale['Average'] > 60)]` is used to filter out students from the isolated demographic group based on a numerical threshold of at least 60.
  * `.loc[]` --> It functions as a label-based data selector that scans the rows of the DataFrame to find positions where the given condition evaluates to true.
  * `VisFemale['Average'] > 60` --> It validates each student's average grade and isolates rows where the value strictly starts and exceeds 60.
  ```
  VisFemale.loc[(VisFemale['Average']>=60)]
  ```
  <img width="475" height="202" alt="image" src="https://github.com/user-attachments/assets/104c0c59-6c60-40b8-934a-99a8c501fe63" />




# C. Category Average Visualization
The problem asks to display the summary of Track, Gender, and Hometown, and to create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown, and to provide an interpretation for the group with the largest sample size for each feature.

a. 
* The `Summary_of_AskedColumn = ECE_Board_Exam_2.groupby('AskedColumn')['Average'].mean().reset_index()` is used to break down the main dataset by student track categories and calculate the average score for each academic track stored under the `Summary_of_AskedColumn`.
  
 * `ECE_Board_Exam_2.groupby()`--> It functions to split the original DataFrame into subsets based on the categories asked per column.
 * `[Average]` --> It functions to isolate the numerical average grade column from the grouped data subset so that subsequent calculations are restricted to this variable.
 * `.mean()` --> It functions as an aggregation operation that computes the average score for each group.
 * `.reset_index()` --> It functions to convert the grouped category names back from index labels into regular DataFrame columns while resetting the row index to a standard sequence of numbers starting from zero.

For the ('AskedColumn'):
* `('Track')` --> used to get the mean average score for each specialization track.
* `('Gender')` --> used to get the mean average score for student gender demographics.
* `('Hometown')` --> used to get the mean average score by geographic hometown regions.

b. 
The display of all three summary tables asked:

<img width="266" height="547" alt="image" src="https://github.com/user-attachments/assets/ee87391f-f2c9-4572-9b8a-ace6323a301f" />


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
* The `plt.title()` function displays a Text string at the top of the axes to indicate the subject of the plot.
* The `plt.xlabel()` function applies a descriptive text label on the horizontal axis to define the metric being plotted on it.
* The `plt.ylabel()` function applies a descriptive text label on the vertical axis to define the metric being plotted on it. 
  ```
  import matplotlib.pyplot as plt

  plt.figure(figsize=(18,5))

  plt.subplot(1, 3, 1)
  plt.bar(Summary_of_Track['Track'], Summary_of_Track['Average'])
  plt.ylim(0, 100)
  plt.title('Summary of Track')
  plt.xlabel('Track')
  plt.ylabel('Mean Average Score')

  plt.subplot(1, 3, 2)
  plt.bar(Summary_of_Gender['Gender'], Summary_of_Gender['Average'])
  plt.ylim(0, 100)
  plt.title('Summary of Gender')
  plt.xlabel('Gender')
  plt.ylabel('Mean Average Score')
  
  plt.subplot(1, 3, 3)
  plt.bar(Summary_of_Hometown['Hometown'], Summary_of_Hometown['Average'])
  plt.ylim(0, 100)
  plt.title('Summary of Hometown')
  plt.xlabel('Hometown')
  plt.ylabel('Mean Average Score')

  plt.tight_layout()
  ```

<img width="1485" height="406" alt="image" src="https://github.com/user-attachments/assets/0685edac-2341-4cbb-aa90-c267b9f9ebe3" />


The problem also asked to create an interpretation, and in terms of __Track__, Communication achieved the highest, followed by Microelectronics, with Instrumentation the lowest. In terms of __Gender__, Male performed well in comparison to Female takers. In terms of __Hometown__, Luzon had the highest number, followed by Mindanao and the Visayas, with the fewest takers.  
 


# Version History

* 13 September 2026 --> The README file was created and is continuously being updated.
* 16 September 2026 --> The README file is still continuously being updated.
* 17 September 2026 --> The README file was finalized and the .ipynb file was uploaded. 
