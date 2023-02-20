## How to spread data


```python
import pandas as pd
```

Imagine we have the following data about participants' demographic and linguistic background.


```python
sample = pd.read_csv('./sample_ppt_data.csv')
sample
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
      <th>SubjID</th>
      <th>Question</th>
      <th>Answer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>input_age</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>input_gender</td>
      <td>male</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>second_lang</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>input_age</td>
      <td>21</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>input_gender</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>second_lang</td>
      <td>Spanish</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3</td>
      <td>input_age</td>
      <td>42</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3</td>
      <td>input_gender</td>
      <td>male</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3</td>
      <td>second_lang</td>
      <td>Mandarin</td>
    </tr>
  </tbody>
</table>
</div>



The following code mutates the data (akin to the `spread` function in R) such that the values under the `Question` column has their own columns.


Note the use of `aggfunc` parameter - we need it in order to deal with NaNs in some cells. 


```python
sample = sample.pivot_table(index=['SubjID'], columns='Question', values='Answer', aggfunc='first').reset_index()
sample
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
      <th>Question</th>
      <th>SubjID</th>
      <th>input_age</th>
      <th>input_gender</th>
      <th>second_lang</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>30</td>
      <td>male</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>21</td>
      <td>NaN</td>
      <td>Spanish</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>42</td>
      <td>male</td>
      <td>Mandarin</td>
    </tr>
  </tbody>
</table>
</div>


