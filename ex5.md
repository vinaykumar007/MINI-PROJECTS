
#  One-to-many merge

```
Exercise ID 1122341
```

##  Assignment 

A business may have one or multiple owners. In this exercise, you will continue to gain experience with one-to-many merges by merging a table of business owners, called `biz_owners`, to the `licenses` table. Recall from the video lesson, with a one-to-many relationship, a row in the left table may be repeated if it is related to multiple rows in the right table. In this lesson, you will explore this further by finding out what is the most common business owner title. (i.e., secretary, CEO, or vice president)

The `licenses` and `biz_owners` DataFrames are loaded for you.

##  Pre exercise code 

```
from pickle import load
import urllib.request
import pandas as pd

fn_lic = 'https://assets.datacamp.com/production/repositories/5486/datasets/2a4d8e5d91f6f2b41477fa6ea81da91e4f09305e/licenses.p'
fn_own = 'https://assets.datacamp.com/production/repositories/5486/datasets/fc3c75b236ed090f487b044603c0f7ff6825d911/business_owners.p'
licenses = load(urllib.request.urlopen(fn_lic))
biz_owners = load(urllib.request.urlopen(fn_own))
```



##  Instructions 

- Starting with the `licenses` table on the left, merge it to the `biz_owners` table on the column `account`, and save the results to a variable named `licenses_owners`.
- Group `licenses_owners` by `title` and count the number of accounts for each title. Save the result as `counted_df`
- Sort `counted_df` by the number of **accounts** in **descending order**, and save this as a variable named `sorted_df`.
- Use the `.head()` method to print the first few rows of the `sorted_df`.



```
# Merge the licenses and biz_owners table on account
licenses_owners = ____

# Group the results by title then count the number of accounts
counted_df = licenses_owners.groupby(____).agg({'account':'count'})

# Sort the counted_df in desending order
sorted_df = counted_df.sort_values(____)

# Use .head() method to print the first few rows of sorted_df
print(____)
```

##  Hints 

- Your merge should have a pattern similar to `df1.merge(df2, on='col')`.
- Set the `ascending` argument to `False` in the `.sort_values()` method to sort values in descending order.
- Inside the `print()` function, enter the `sorted_df` variable and add `.head()` behind it.



##  Solution 

```
# Merge the licenses and biz_owners table on account
licenses_owners = licenses.merge(biz_owners, on='account')

# Group the results by title then count the number of accounts
counted_df = licenses_owners.groupby('title').agg({'account':'count'})

# Sort the counted_df in desending order
sorted_df = counted_df.sort_values(by='account', ascending=False)

# Use .head() method to print the first few rows of sorted_df
print(sorted_df.head())
```


