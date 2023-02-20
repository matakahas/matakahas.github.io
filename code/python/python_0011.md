## How to check for counterbalancing


```python
import pandas as pd
```


```python
sample = pd.read_csv('./sampledata.csv')
sample.head(3)
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
      <th>Movement</th>
      <th>Island_Type</th>
      <th>Island</th>
      <th>Distance</th>
      <th>Item</th>
      <th>Sentence</th>
      <th>Subj_id</th>
      <th>List</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>WH</td>
      <td>whe</td>
      <td>non</td>
      <td>sh</td>
      <td>1</td>
      <td>Who thinks that Paul stole the necklace?</td>
      <td>1</td>
      <td>1</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>WH</td>
      <td>whe</td>
      <td>non</td>
      <td>sh</td>
      <td>2</td>
      <td>Who thinks that Matt chased the bus?</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WH</td>
      <td>whe</td>
      <td>non</td>
      <td>sh</td>
      <td>3</td>
      <td>Who thinks that Tom sold the television?</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



Checking for counterbalancing (i.e., how many participants were assigned to each experimental list) on python is pretty simple - we can use `nunique()` function.


```python
sample.groupby('List')['Subj_id'].nunique()
```




    List
    1    4
    2    4
    3    4
    4    4
    Name: Subj_id, dtype: int64



We can see that the counterbalancing was perfect - there are 4 participants in each list.
