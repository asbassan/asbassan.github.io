# Exploratory Data Analysis
- My go to methods initially.


## Numerical Analysis

#### Get unique values by count  for a column.
```python
    numerical_cols['NUMERICAL_10'].value_counts(normalize = True)
```

















## Graphing

#### Get the disttibution of Numerical Columns

```python
    #let us get the distribution graph of each columns
    columns_list = numerical_cols.columns
    number_of_columns = len(columns_list)
    plots_per_rows = 3
    number_of_rows = int(np.ceil(number_of_columns/plots_per_rows))


    colindex = 0
    fig, axis = plt.subplots(figsize = (20, 40), nrows = number_of_rows, ncols = plots_per_rows)
    plt.subplots_adjust(hspace = 0.5)

    for r in range(0,number_of_rows):
        for c in range(0,plots_per_rows):
            sns.distplot(numerical_cols[columns_list[colindex]], ax = axis[r][c])
            colindex += 1
            if colindex >= len(columns_list):
                break
```

#### Get the boxplot of Numerical Columns

```python
    #let us get the distribution graph of each columns
    columns_list = numerical_cols.columns
    number_of_columns = len(columns_list)
    plots_per_rows = 3
    number_of_rows = int(np.ceil(number_of_columns/plots_per_rows))


    colindex = 0
    fig, axis = plt.subplots(figsize = (20, 40), nrows = number_of_rows, ncols = plots_per_rows)
    plt.subplots_adjust(hspace = 0.5)

    for r in range(0,number_of_rows):
        for c in range(0,plots_per_rows):
            sns.boxplot(numerical_cols[columns_list[colindex]], ax = axis[r][c])
            colindex += 1
            if colindex >= len(columns_list):
                break
```

### Date Time functions - Extractions
[pandas datetime excersize](https://www.w3resource.com/python-exercises/pandas/datetime/pandas-datetime-exercise-8.php)



