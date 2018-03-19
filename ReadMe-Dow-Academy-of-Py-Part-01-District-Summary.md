

```python
# ********** GENERAL SET UP ****************************************************

# Import libraries
import pandas as pd
import numpy as ny

```


```python
# Define pathways to files
schools_csv = "raw_data/schools_complete.csv"
students_csv = "raw_data/students_complete.csv"
```


```python
# Read the pathways and define the dataframe(s) - Part 1
schools_df = pd.read_csv(schools_csv)
schools_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Read the pathways and define the dataframe(s) - Part 2
students_df = pd.read_csv(students_csv)
students_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# ********** SET COMMON COLUMN AND MERGE FILES *********************************
```


```python
#Rename School name in school_df to "school" so we can merge on "school" between the two dataframes
schools_df = schools_df.rename(columns={"name":"school"})
schools_df.head()



```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge the two dataframes into a new, single dataframe
combined_df = pd.merge(schools_df, students_df, on="school")
combined_df.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# ********** GET GENERAL STATS FROM DATA ***************************************
#count total schools
total_schools = schools_df["School ID"].count()
total_schools
```




    15




```python
#count total students
total_students = students_df["Student ID"].count()
total_students
```




    39170




```python
#sum total budget
total_budget = schools_df["budget"].sum()
total_budget
```




    24649428




```python
#average math score
ave_math_score = students_df["math_score"].mean()
ave_math_score

```




    78.98537145774827




```python
#average reading score
ave_reading_score = students_df["reading_score"].mean()
ave_reading_score
```




    81.87784018381414




```python
# ********** CREATE BINS AND GROUPS SO CAN CALC PERCENTAGES********************
# Start with "% passing math" first____________________________________________
# Create bins
bins = [0,60,70,80,90,100]
score_range =["F","D","C","B","A"]
pd.cut(students_df["math_score"],bins,labels=score_range).head()
                   
```




    0    C
    1    D
    2    F
    3    F
    4    B
    Name: math_score, dtype: category
    Categories (5, object): [F < D < C < B < A]




```python
# Place the data series into a new column inside of the DataFrame
students_df["Math Grade Group"] = pd.cut(students_df["math_score"],bins,labels=score_range)
students_df.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Math Grade Group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>C</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>D</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>F</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>B</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a GroupBy object based upon "Math Grade Group"
math_grade_group = students_df.groupby("Math Grade Group")

print(math_grade_group["Math Grade Group"].count())
```

    Math Grade Group
    F    3562
    D    7252
    C    9751
    B    9771
    A    8834
    Name: Math Grade Group, dtype: int64
    


```python


```


```python
math_grade_group.mean()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
    <tr>
      <th>Math Grade Group</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>F</th>
      <td>19511.761931</td>
      <td>80.899495</td>
      <td>57.517687</td>
    </tr>
    <tr>
      <th>D</th>
      <td>19531.180640</td>
      <td>81.664368</td>
      <td>66.055985</td>
    </tr>
    <tr>
      <th>C</th>
      <td>19573.217106</td>
      <td>81.969131</td>
      <td>75.475849</td>
    </tr>
    <tr>
      <th>B</th>
      <td>19692.039607</td>
      <td>82.134173</td>
      <td>85.453178</td>
    </tr>
    <tr>
      <th>A</th>
      <td>19551.107992</td>
      <td>82.063278</td>
      <td>94.975436</td>
    </tr>
  </tbody>
</table>
</div>




```python
students_df["Math Grade Group"].head()

```




    0    C
    1    D
    2    F
    3    F
    4    B
    Name: Math Grade Group, dtype: category
    Categories (5, object): [F < D < C < B < A]




```python
# Extract rows corresponding only to people who failed math
failed_math = students_df.loc[students_df["Math Grade Group"] == "F"]
failed_math.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Math Grade Group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>F</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>F</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>Donald Zamora</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>88</td>
      <td>55</td>
      <td>F</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Tracey Oconnor</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>80</td>
      <td>58</td>
      <td>F</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>Kelly James</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>73</td>
      <td>55</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Define the failed_math_count
failed_math_count = len(failed_math["Student ID"])
failed_math_count
```




    3562




```python
total_math_count = students_df.count()
percent_failed_math = (failed_math_count/total_math_count)*100
percent_failed_math
```




    Student ID          9.093694
    name                9.093694
    gender              9.093694
    grade               9.093694
    school              9.093694
    reading_score       9.093694
    math_score          9.093694
    Math Grade Group    9.093694
    dtype: float64




```python
percent_failed_math2 = percent_failed_math["Student ID"]
percent_failed_math2
```




    9.093694153689048




```python
percent_passed_math = 100 - percent_failed_math2
percent_passed_math = percent_passed_math.round(2)
percent_passed_math

```




    90.91




```python
# Now do "% passing reading" first____________________________________________
# Create bins
bins = [0,60,70,80,90,100]
score_range =["F","D","C","B","A"]
pd.cut(students_df["reading_score"],bins,labels=score_range).head()
```




    0    D
    1    A
    2    B
    3    D
    4    A
    Name: reading_score, dtype: category
    Categories (5, object): [F < D < C < B < A]




```python
# Place the data series into a new column inside of the DataFrame
students_df["Reading Grade Group"] = pd.cut(students_df["reading_score"],bins,labels=score_range)
students_df.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Math Grade Group</th>
      <th>Reading Grade Group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>C</td>
      <td>D</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>D</td>
      <td>A</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>F</td>
      <td>B</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>F</td>
      <td>D</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>B</td>
      <td>A</td>
    </tr>
  </tbody>
</table>
</div>




```python
reading_grade_group = students_df.groupby("Reading Grade Group")

print(reading_grade_group["Reading Grade Group"].count())
```

    Reading Grade Group
    F        0
    D     6670
    C    11169
    B    11352
    A     9979
    Name: Reading Grade Group, dtype: int64
    


```python
reading_grade_group.mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
    <tr>
      <th>Reading Grade Group</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>F</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>D</th>
      <td>19731.886507</td>
      <td>66.822939</td>
      <td>77.918891</td>
    </tr>
    <tr>
      <th>C</th>
      <td>19625.103232</td>
      <td>75.529054</td>
      <td>79.161339</td>
    </tr>
    <tr>
      <th>B</th>
      <td>19550.430144</td>
      <td>85.460447</td>
      <td>79.197498</td>
    </tr>
    <tr>
      <th>A</th>
      <td>19479.298627</td>
      <td>94.970939</td>
      <td>79.259946</td>
    </tr>
  </tbody>
</table>
</div>




```python
students_df["Reading Grade Group"].head()
```




    0    D
    1    A
    2    B
    3    D
    4    A
    Name: Reading Grade Group, dtype: category
    Categories (5, object): [F < D < C < B < A]




```python
# Extract rows corresponding only to people who failed reading
failed_reading = students_df.loc[students_df["Reading Grade Group"] == "F"]
failed_reading.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Math Grade Group</th>
      <th>Reading Grade Group</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
# Define the failed_reading_count
failed_reading_count = len(failed_reading["Student ID"])
failed_reading_count
```




    0




```python
total_reading_count = students_df.count()
percent_failed_reading = (failed_reading_count/total_reading_count)*100
percent_failed_reading
```




    Student ID             0.0
    name                   0.0
    gender                 0.0
    grade                  0.0
    school                 0.0
    reading_score          0.0
    math_score             0.0
    Math Grade Group       0.0
    Reading Grade Group    0.0
    dtype: float64




```python
percent_failed_reading2 = percent_failed_reading["Student ID"]
percent_failed_reading2
```




    0.0




```python
percent_passed_reading = 100 - percent_failed_reading2
percent_passed_reading = percent_passed_reading.round(2)
percent_passed_reading

```




    100.0




```python
# Now average reading and math to get the Overall Passing Rate
overall_pass_rate=(percent_passed_reading+percent_passed_math)/2
overall_pass_rate

```




    95.455




```python
# ********** CREATE A SUMMARY TABLE (DISTRICT-LEVEL)***********************
district_summary = pd.DataFrame({"Total Schools":[total_schools],
                                 "Total Students":[total_students],
                                 "Total Budget":[total_budget], 
                                 "Average Math Score":[ave_math_score],
                                 "Average Reading Score":[ave_reading_score],
                                 "% Passed Math":[percent_passed_math],
                                 "% Passed Reading":[percent_passed_reading],
                                 "Overall Passing Rate":[overall_pass_rate]
})
district_summary
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>% Passed Math</th>
      <th>% Passed Reading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Overall Passing Rate</th>
      <th>Total Budget</th>
      <th>Total Schools</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>90.91</td>
      <td>100.0</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>95.455</td>
      <td>24649428</td>
      <td>15</td>
      <td>39170</td>
    </tr>
  </tbody>
</table>
</div>




```python
district_summary_ordered = district_summary[["Total Schools", 
                                             "Total Students", 
                                             "Total Budget",
                                             "Average Math Score",
                                             "Average Reading Score",
                                             "% Passed Math", 
                                             "% Passed Reading",
                                             "Overall Passing Rate"]]
district_summary_ordered

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passed Math</th>
      <th>% Passed Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39170</td>
      <td>24649428</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>90.91</td>
      <td>100.0</td>
      <td>95.455</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Improve formatting
district_summary_ordered["Total Students"]=district_summary_ordered["Total Students"].map("{0:,.0f}".format)
district_summary_ordered["Total Budget"]=district_summary_ordered["Total Budget"].map("${0:,.0f}".format)

district_summary_ordered = district_summary_ordered.round(2)
district_summary_ordered

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passed Math</th>
      <th>% Passed Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428</td>
      <td>78.99</td>
      <td>81.88</td>
      <td>90.91</td>
      <td>100.0</td>
      <td>95.46</td>
    </tr>
  </tbody>
</table>
</div>


