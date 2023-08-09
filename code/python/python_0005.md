## How to assign subject IDs


```python
import pandas as pd
```


```python
sample = pd.read_csv('./sampledata1.csv')
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
      <th>Unnamed: 0</th>
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
      <td>0</td>
      <td>WH</td>
      <td>whe</td>
      <td>non</td>
      <td>sh</td>
      <td>1</td>
      <td>Who thinks that Paul stole the necklace?</td>
      <td>31WPPC</td>
      <td>1</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>WH</td>
      <td>whe</td>
      <td>non</td>
      <td>sh</td>
      <td>2</td>
      <td>Who thinks that Matt chased the bus?</td>
      <td>31WPPC</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>WH</td>
      <td>whe</td>
      <td>non</td>
      <td>sh</td>
      <td>3</td>
      <td>Who thinks that Tom sold the television?</td>
      <td>31WPPC</td>
      <td>1</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
sample['Subj_id'].unique()
```




    array(['31WPPC', 'MLOT0C', 'QUCYBY', '3HM9R4', 'TNZ93A', 'RE7119',
           'IKH3NF', '0R04SW', 'S7VOS9', 'JO1B7Q', '0HY4IC', 'MNSV2I',
           'IOEK50', 'LXP23M', '7NXUBG', '4EQFWR'], dtype=object)



Let's simplify the subject ids in this dataset by converting them to numbers only. Here is one way to accomplish this.


```python
sample['Subj_id'] = sample.groupby('Subj_id', sort=False).ngroup()
sample['Subj_id'] = sample['Subj_id'] + 1 #add 1 to each id if you do not want the first id to be 0
```


```python
sample['Subj_id'].unique()
```




    array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16])


