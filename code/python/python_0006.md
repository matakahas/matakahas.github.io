## How to normalize acceptability scores
In acceptability judgment experiments, participants make use of an acceptability scale (most commonly the 7-point Likert scale) in various ways; some people use 1 and 7 exclusively, while other people stick to 3 through 5. In order to normalize their scores, it is common to convert raw acceptability to z-scores (standard scores). In python, I will use the `scipy` package to achieve this.


```python
import pandas as pd
from scipy.stats import zscore
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




```python
sample['Z_score'] = sample.groupby('Subj_id').Score.transform(lambda x : zscore(x,ddof=1))
```


```python
sample['Score'][:5]
```




    0    6
    1    2
    2    3
    3    7
    4    2
    Name: Score, dtype: int64




```python
sample['Z_score'][:5]
```




    0    1.265785
    1   -0.734468
    2   -0.234405
    3    1.765848
    4   -0.734468
    Name: Z_score, dtype: float64


