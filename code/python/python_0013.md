## How to group data and check values by group

I recently ran into a situation where I needed to group data by name and, for each group, check if *any* of the rows contains a particular value (in my case, a membership renewal date) under a different column. This is how I accomplished it:


```python
import pandas as pd

data = {'Name': ['John Smith', 'Jane Miller', 'John Smith', 'Adam Sue', 'Jane Miller', 'John Smith'], 
        'Renewal Date': ['Oct 31, 2023', 'Oct 31, 2022', 'Oct 31, 2021', 'Oct 31, 2022', 'Oct 31, 2023', 'Oct 31, 2021']}
df = pd.DataFrame(data)

grouped = df.groupby('Name').apply(lambda x: 'Oct 31, 2023' in x['Renewal Date'].values)

print(grouped)
```

    Name
    Adam Sue       False
    Jane Miller     True
    John Smith      True
    dtype: bool


Or if I want to get a list of names whose value turned out to be false:


```python
grouped = grouped.to_frame().reset_index()
grouped[grouped[0]==False]['Name'].tolist()
```




    ['Adam Sue']


