# Python Pandas

Pandas is a library for data analysis and manipulation.

## Installation

```bash
pip install pandas
```

## Import Pandas

```python
import pandas as pd
```

## Series

One-dimensional array:

```python
# From list
s = pd.Series([1, 2, 3, 4, 5])

# With index
s = pd.Series([1, 2, 3], index=['a', 'b', 'c'])
print(s['a'])  # 1

# From dict
s = pd.Series({'a': 1, 'b': 2, 'c': 3})
```

## DataFrame

Two-dimensional table:

```python
# From dict
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Paris', 'London']
}
df = pd.DataFrame(data)

# From list of lists
data = [
    ['Alice', 25, 'New York'],
    ['Bob', 30, 'Paris']
]
df = pd.DataFrame(data, columns=['Name', 'Age', 'City'])

# From CSV
df = pd.read_csv('data.csv')

# Display
print(df)
print(df.head())      # First 5 rows
print(df.tail())      # Last 5 rows
print(df.info())      # Info
print(df.describe())  # Statistics
```

## Accessing Data

```python
# Columns
print(df['Name'])
print(df[['Name', 'Age']])

# Rows by index
print(df.iloc[0])       # First row
print(df.iloc[0:2])     # First 2 rows

# Rows by label
print(df.loc[0])

# Specific cell
print(df.iloc[0, 1])    # Row 0, Column 1
print(df.loc[0, 'Age']) # Row 0, 'Age' column
```

## Filtering

```python
# Boolean indexing
filtered = df[df['Age'] > 25]

# Multiple conditions
filtered = df[(df['Age'] > 25) & (df['City'] == 'Paris')]

# Query
filtered = df.query('Age > 25 and City == "Paris"')
```

## Adding/Removing Columns

```python
# Add column
df['Country'] = 'USA'
df['Senior'] = df['Age'] > 30

# Remove column
df = df.drop('Country', axis=1)
del df['Senior']
```

## Modifying Data

```python
# Update value
df.loc[0, 'Age'] = 26

# Update column
df['Age'] = df['Age'] + 1

# Fill missing values
df.fillna(0, inplace=True)

# Drop missing values
df.dropna(inplace=True)
```

## Grouping and Aggregation

```python
# Group by
grouped = df.groupby('City')['Age'].mean()

# Multiple aggregations
df.groupby('City').agg({
    'Age': ['mean', 'max', 'min'],
    'Name': 'count'
})
```

## Sorting

```python
# Sort by column
df_sorted = df.sort_values('Age')

# Descending
df_sorted = df.sort_values('Age', ascending=False)

# Multiple columns
df_sorted = df.sort_values(['City', 'Age'])
```

## Merging and Joining

```python
df1 = pd.DataFrame({'ID': [1, 2], 'Name': ['Alice', 'Bob']})
df2 = pd.DataFrame({'ID': [1, 2], 'Age': [25, 30]})

# Merge
merged = pd.merge(df1, df2, on='ID')

# Join
df1.set_index('ID').join(df2.set_index('ID'))

# Concat
pd.concat([df1, df2], axis=0)  # Vertical
pd.concat([df1, df2], axis=1)  # Horizontal
```

## Export Data

```python
# To CSV
df.to_csv('output.csv', index=False)

# To Excel
df.to_excel('output.xlsx', index=False)

# To JSON
df.to_json('output.json')
```

---

**Related:** [[Python Libraries and Frameworks]] | [[Python NumPy]] | [[Python File Handling]]
