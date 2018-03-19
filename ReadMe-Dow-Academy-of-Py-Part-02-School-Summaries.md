

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
pd.cut(combined_df["math_score"],bins,labels=score_range).head()
                   
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
combined_df["Math Grade Group"] = pd.cut(combined_df["math_score"],bins,labels=score_range)
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
      <th>Math Grade Group</th>
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
      <td>C</td>
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
      <td>D</td>
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
      <td>F</td>
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
      <td>F</td>
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
      <td>B</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a GroupBy object based upon high school and "Math Grade Group"
math_grade_group = combined_df.groupby("Math Grade Group")

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
###################################################################################################
# The answers for each school can be collected via the .loc and groupby process below. I have been looking for ways to avoid having to do this for each school, but have not been succesful after much research. I am looking to do a groupby on the groupby and I have not been able to get this work yet. 
Bailey_filter = combined_df.loc[combined_df["school"] == "Bailey High School"]
print(Bailey_filter.count())

Bailey_math_grade_group = Bailey_filter.groupby("Math Grade Group")
print(Bailey_math_grade_group["Math Grade Group"].count())


```

    School ID           4976
    school              4976
    type                4976
    size                4976
    budget              4976
    Student ID          4976
    name                4976
    gender              4976
    grade               4976
    reading_score       4976
    math_score          4976
    Math Grade Group    4976
    dtype: int64
    Math Grade Group
    F     625
    D    1135
    C    1093
    B    1126
    A     997
    Name: Math Grade Group, dtype: int64
    


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
      <th>School ID</th>
      <th>size</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
    <tr>
      <th>Math Grade Group</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>F</th>
      <td>6.953116</td>
      <td>4059.609489</td>
      <td>2.609577e+06</td>
      <td>19511.761931</td>
      <td>80.899495</td>
      <td>57.517687</td>
    </tr>
    <tr>
      <th>D</th>
      <td>6.945119</td>
      <td>3680.766271</td>
      <td>2.352352e+06</td>
      <td>19531.180640</td>
      <td>81.664368</td>
      <td>66.055985</td>
    </tr>
    <tr>
      <th>C</th>
      <td>6.974156</td>
      <td>3134.985232</td>
      <td>1.983284e+06</td>
      <td>19573.217106</td>
      <td>81.969131</td>
      <td>75.475849</td>
    </tr>
    <tr>
      <th>B</th>
      <td>7.019650</td>
      <td>3154.723467</td>
      <td>1.996162e+06</td>
      <td>19692.039607</td>
      <td>82.134173</td>
      <td>85.453178</td>
    </tr>
    <tr>
      <th>A</th>
      <td>6.973964</td>
      <td>3170.097351</td>
      <td>2.007500e+06</td>
      <td>19551.107992</td>
      <td>82.063278</td>
      <td>94.975436</td>
    </tr>
  </tbody>
</table>
</div>




```python


```


```python


```


```python


```


```python


```


```python


```
