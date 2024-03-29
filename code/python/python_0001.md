## how to find and deal with NaN values in a pandas dataframe


```python
import pandas as pd
import numpy as np
```


```python
df = pd.DataFrame({'Date':['10/2/2011', np.nan, '11/2/2011', '12/2/2011', '13/2/2011'],
                   'Product':['umbrella', 'matress', 'badminton', 'shuttle', np.nan],
                   'Updated_Price':[np.nan, 1250, 1450, 1550, 400],
                   'Discount':[10, 8, np.nan, 15, 10]})
```


```python
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
      <th>Date</th>
      <th>Product</th>
      <th>Updated_Price</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10/2/2011</td>
      <td>umbrella</td>
      <td>NaN</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>matress</td>
      <td>1250.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>badminton</td>
      <td>1450.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>shuttle</td>
      <td>1550.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13/2/2011</td>
      <td>NaN</td>
      <td>400.0</td>
      <td>10.0</td>
    </tr>
  </tbody>
</table>
</div>



### display rows with NaN values from any of the columns


```python
df[df.isnull().any(axis=1)]
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
      <th>Date</th>
      <th>Product</th>
      <th>Updated_Price</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10/2/2011</td>
      <td>umbrella</td>
      <td>NaN</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>matress</td>
      <td>1250.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>badminton</td>
      <td>1450.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13/2/2011</td>
      <td>NaN</td>
      <td>400.0</td>
      <td>10.0</td>
    </tr>
  </tbody>
</table>
</div>



### display number of rows with NaN values per column


```python
df.isnull().sum()
```




    Date             1
    Product          1
    Updated_Price    1
    Discount         1
    dtype: int64



### fill NaN values with the mean of a column they belong


```python
cols = ['Updated_Price', 'Discount']
df[cols] = df[cols].fillna(df.mean()) 
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
      <th>Date</th>
      <th>Product</th>
      <th>Updated_Price</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10/2/2011</td>
      <td>umbrella</td>
      <td>1162.5</td>
      <td>10.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>matress</td>
      <td>1250.0</td>
      <td>8.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>badminton</td>
      <td>1450.0</td>
      <td>10.75</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>shuttle</td>
      <td>1550.0</td>
      <td>15.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13/2/2011</td>
      <td>NaN</td>
      <td>400.0</td>
      <td>10.00</td>
    </tr>
  </tbody>
</table>
</div>



### fill NaN values with the mean of the values before and after NaN


```python
df['Discount'] = df['Discount'].interpolate()
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
      <th>Date</th>
      <th>Product</th>
      <th>Updated_Price</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10/2/2011</td>
      <td>umbrella</td>
      <td>NaN</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>matress</td>
      <td>1250.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>badminton</td>
      <td>1450.0</td>
      <td>11.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>shuttle</td>
      <td>1550.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13/2/2011</td>
      <td>NaN</td>
      <td>400.0</td>
      <td>10.0</td>
    </tr>
  </tbody>
</table>
</div>



### fill NaN values with the value of the previous row


```python
df['Date'] = df['Date'].fillna(method='ffill')
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
      <th>Date</th>
      <th>Product</th>
      <th>Updated_Price</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10/2/2011</td>
      <td>umbrella</td>
      <td>NaN</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10/2/2011</td>
      <td>matress</td>
      <td>1250.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>badminton</td>
      <td>1450.0</td>
      <td>11.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>shuttle</td>
      <td>1550.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13/2/2011</td>
      <td>NaN</td>
      <td>400.0</td>
      <td>10.0</td>
    </tr>
  </tbody>
</table>
</div>



### delete rows with NaN values


```python
df.dropna(subset=['Product'], inplace=True)
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
      <th>Date</th>
      <th>Product</th>
      <th>Updated_Price</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10/2/2011</td>
      <td>umbrella</td>
      <td>1162.5</td>
      <td>10.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10/2/2011</td>
      <td>matress</td>
      <td>1250.0</td>
      <td>8.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>badminton</td>
      <td>1450.0</td>
      <td>10.75</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>shuttle</td>
      <td>1550.0</td>
      <td>15.00</td>
    </tr>
  </tbody>
</table>
</div>


