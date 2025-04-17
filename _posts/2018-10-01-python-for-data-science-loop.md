---
layout: post
title: 'Python for Data Science: Loop'
description: Datacamp notes -- loop
tags:
  - python
  - data science
  - cheat sheet
categories:
  - Notes
date: 2018-10-01 00:46:43
---

## While loop
```
while condition :
  expression
# loop while the condition is true
```
## For loop

```
# basic for loop
for a in list:
  expression

# access to index
for index, a in enumerate(list):
  expression

# stings
```

## Looping data structures
dict, numpy array, pandas

### Dictionary

```
for key, value in dict.items():
  print(key + "--" + str(value))
```

### Numpy array

```
for a in my_array:
  print(a)
# for 1D numpy array elements will be printed out one by one
# for 2D numpy array arrays will be printed out one by one

for a in np.nditer(my_array):
  print(a)
# elements will be printed out one by one
# notice that np.nditer() is a function, while dict.items is a method
```

### Pandas
- By default

```
import pandas as pd
my_data = pd.read_csv("my_data", index_col = 0)
for a in my_data:
  print(a)
# column names will be printed out.
```

- iterrows

```
for label,row in my_data.iterrows():
  print(label)
  print(row)
# selective print, use row[index], or loc, iloc
```

- add column
```
# for example
for lab, row in my_data.iterrows()：
  my_data[lab, "new_column"] = my_data["column1"].upper()
```
- apply
```
# for example
cars['COUNTRY'] = cars['country'].apply(str.upper)
cars['COUNTRY'] = cars['country'].apply(len)
```

## Reference
[1. Datacamp: Intermediate Python for Data Science][1]

[1]: https://www.datacamp.com/courses/intermediate-python-for-data-science
