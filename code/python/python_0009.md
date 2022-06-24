## Create a new column based on existing ones


```python
import pandas as pd
import numpy as np
```


```python
df = pd.DataFrame(["STD, City    State",
                   "33, Kolkata    West Bengal",
                   "44, Chennai    Tamil Nadu",
                   "40, Hyderabad    Telengana",
                   "80, Bangalore    Karnataka"], columns=['row'])
df
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
      <th>row</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>STD, City    State</td>
    </tr>
    <tr>
      <th>1</th>
      <td>33, Kolkata    West Bengal</td>
    </tr>
    <tr>
      <th>2</th>
      <td>44, Chennai    Tamil Nadu</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40, Hyderabad    Telengana</td>
    </tr>
    <tr>
      <th>4</th>
      <td>80, Bangalore    Karnataka</td>
    </tr>
  </tbody>
</table>
</div>



### split a column into two 


```python
df = df['row'].str.split(',', expand=True)
df
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
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>STD</td>
      <td>City    State</td>
    </tr>
    <tr>
      <th>1</th>
      <td>33</td>
      <td>Kolkata    West Bengal</td>
    </tr>
    <tr>
      <th>2</th>
      <td>44</td>
      <td>Chennai    Tamil Nadu</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40</td>
      <td>Hyderabad    Telengana</td>
    </tr>
    <tr>
      <th>4</th>
      <td>80</td>
      <td>Bangalore    Karnataka</td>
    </tr>
  </tbody>
</table>
</div>



### make a column based on an exisitng one where its values are shifted by one row


```python
df[2] = df[0].shift(-1) #shifted up
df[3] = df[0].shift(1) #shifted down
df
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>STD</td>
      <td>City    State</td>
      <td>33</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>33</td>
      <td>Kolkata    West Bengal</td>
      <td>44</td>
      <td>STD</td>
    </tr>
    <tr>
      <th>2</th>
      <td>44</td>
      <td>Chennai    Tamil Nadu</td>
      <td>40</td>
      <td>33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40</td>
      <td>Hyderabad    Telengana</td>
      <td>80</td>
      <td>44</td>
    </tr>
    <tr>
      <th>4</th>
      <td>80</td>
      <td>Bangalore    Karnataka</td>
      <td>NaN</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>



### make a column based on a condition on another column


```python
df[4] = np.where(df[2].fillna(0).astype(int) < 40, 'low', 'high')
df
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>STD</td>
      <td>City    State</td>
      <td>33</td>
      <td>NaN</td>
      <td>low</td>
    </tr>
    <tr>
      <th>1</th>
      <td>33</td>
      <td>Kolkata    West Bengal</td>
      <td>44</td>
      <td>STD</td>
      <td>high</td>
    </tr>
    <tr>
      <th>2</th>
      <td>44</td>
      <td>Chennai    Tamil Nadu</td>
      <td>40</td>
      <td>33</td>
      <td>high</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40</td>
      <td>Hyderabad    Telengana</td>
      <td>80</td>
      <td>44</td>
      <td>high</td>
    </tr>
    <tr>
      <th>4</th>
      <td>80</td>
      <td>Bangalore    Karnataka</td>
      <td>NaN</td>
      <td>40</td>
      <td>low</td>
    </tr>
  </tbody>
</table>
</div>


