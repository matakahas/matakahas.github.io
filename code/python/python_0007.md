## How to group data, assign values to them, and ungroup them


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



The following code groups the data by two conditions (Island, Distance), assigns the mean and the standard deviation of acceptability scores per group, and ungroups them:


```python
sample['mean_response'] = sample.groupby(['Island','Distance'])['Score'].transform('mean')
sample['sd_answer_z'] = sample.groupby(['Island','Distance'])['Score'].transform('std')
```


```python
sample.iloc[:5, [2, 3, -3, -2, -1]] #showing only relevant columns
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
      <th>Island</th>
      <th>Distance</th>
      <th>Score</th>
      <th>mean_response</th>
      <th>sd_answer_z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>non</td>
      <td>sh</td>
      <td>6</td>
      <td>4.585938</td>
      <td>1.709295</td>
    </tr>
    <tr>
      <th>1</th>
      <td>non</td>
      <td>sh</td>
      <td>2</td>
      <td>4.585938</td>
      <td>1.709295</td>
    </tr>
    <tr>
      <th>2</th>
      <td>non</td>
      <td>sh</td>
      <td>3</td>
      <td>4.585938</td>
      <td>1.709295</td>
    </tr>
    <tr>
      <th>3</th>
      <td>non</td>
      <td>sh</td>
      <td>7</td>
      <td>4.585938</td>
      <td>1.709295</td>
    </tr>
    <tr>
      <th>4</th>
      <td>non</td>
      <td>sh</td>
      <td>2</td>
      <td>4.585938</td>
      <td>1.709295</td>
    </tr>
  </tbody>
</table>
</div>



## How to aggregate data
Now I will aggregate the data based on the two conditions and make a summary dataset that shows the mean, the standard deviation, and the standard error of the mean of each group's acceptability.


```python
data_summary = sample.groupby(['Island','Distance'])['Score'].agg(['mean','std','sem']).reset_index()
data_summary
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
      <th>Island</th>
      <th>Distance</th>
      <th>mean</th>
      <th>std</th>
      <th>sem</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>isl</td>
      <td>lg</td>
      <td>2.593750</td>
      <td>1.180134</td>
      <td>0.104310</td>
    </tr>
    <tr>
      <th>1</th>
      <td>isl</td>
      <td>sh</td>
      <td>3.531250</td>
      <td>1.128985</td>
      <td>0.099789</td>
    </tr>
    <tr>
      <th>2</th>
      <td>non</td>
      <td>lg</td>
      <td>3.890625</td>
      <td>1.920607</td>
      <td>0.169759</td>
    </tr>
    <tr>
      <th>3</th>
      <td>non</td>
      <td>sh</td>
      <td>4.585938</td>
      <td>1.709295</td>
      <td>0.151082</td>
    </tr>
  </tbody>
</table>
</div>


