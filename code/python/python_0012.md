## How to mutate the dataframe to add item mean and sd to each row


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



I want to create new columns `Score_mean` and `Score_sd`, which show the mean and standard deviation of a particular item's scores given by different subjects. Think `group_by` followed by `mutate` in R. Here's one way to accomplish it.


```python
sample = sample.assign(
    Score_mean = sample.groupby(['Sentence'])['Score'].transform('mean'),
    Score_sd = sample.groupby(['Sentence'])['Score'].transform('std'))
```


```python
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
      <th>Score_mean</th>
      <th>Score_sd</th>
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
      <td>4.875</td>
      <td>1.543805</td>
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
      <td>4.250</td>
      <td>1.914854</td>
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
      <td>4.250</td>
      <td>1.693123</td>
    </tr>
  </tbody>
</table>
</div>


