## How to generate random datasets


```python
import pandas as pd
```


```python
sample_df = pd.util.testing.makeDataFrame()
sample_df.head()
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>57UYdLCAz9</th>
      <td>0.143324</td>
      <td>0.012548</td>
      <td>-1.501348</td>
      <td>-0.873817</td>
    </tr>
    <tr>
      <th>wxTnNfCFsX</th>
      <td>-1.200068</td>
      <td>-0.079628</td>
      <td>-0.101257</td>
      <td>-1.825547</td>
    </tr>
    <tr>
      <th>4PYx9lgmIg</th>
      <td>1.054539</td>
      <td>-1.463891</td>
      <td>0.282045</td>
      <td>-0.203671</td>
    </tr>
    <tr>
      <th>J7JCQvcH86</th>
      <td>1.323521</td>
      <td>1.695652</td>
      <td>-0.674408</td>
      <td>0.638206</td>
    </tr>
    <tr>
      <th>46tUB2L5Xm</th>
      <td>0.180413</td>
      <td>1.887923</td>
      <td>0.992859</td>
      <td>0.996487</td>
    </tr>
  </tbody>
</table>
</div>



As a default, the sample dataset contains 30 rows and 4 columns.

### include NaNs in a random dataset


```python
sample_df = pd.util.testing.makeMissingDataframe()
sample_df.head()
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>i3ExiwBU7S</th>
      <td>-1.212042</td>
      <td>-0.892190</td>
      <td>-0.039163</td>
      <td>0.010801</td>
    </tr>
    <tr>
      <th>zFzIsE2HUx</th>
      <td>0.842377</td>
      <td>-1.474449</td>
      <td>0.896692</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>lHoqmwixVC</th>
      <td>-0.432291</td>
      <td>-0.140856</td>
      <td>-0.820675</td>
      <td>-0.876261</td>
    </tr>
    <tr>
      <th>ZGtc7XPikQ</th>
      <td>-0.330881</td>
      <td>-2.578911</td>
      <td>NaN</td>
      <td>0.627988</td>
    </tr>
    <tr>
      <th>lXMCFHfcYz</th>
      <td>1.095504</td>
      <td>-0.670436</td>
      <td>1.614122</td>
      <td>-0.500160</td>
    </tr>
  </tbody>
</table>
</div>



### include timeseries in a random dataset


```python
sample_df = pd.util.testing.makeTimeDataFrame()
sample_df.head()
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-03</th>
      <td>-1.150055</td>
      <td>0.340213</td>
      <td>-0.193093</td>
      <td>1.140389</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>-0.116650</td>
      <td>-1.928765</td>
      <td>-1.934851</td>
      <td>1.065835</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>0.436392</td>
      <td>-1.976887</td>
      <td>0.124077</td>
      <td>-1.292386</td>
    </tr>
    <tr>
      <th>2000-01-06</th>
      <td>2.362524</td>
      <td>-0.733541</td>
      <td>-0.745991</td>
      <td>-0.600506</td>
    </tr>
    <tr>
      <th>2000-01-07</th>
      <td>-0.537766</td>
      <td>0.622937</td>
      <td>-1.650008</td>
      <td>-0.308583</td>
    </tr>
  </tbody>
</table>
</div>



### include mixed variables in a random dataset


```python
sample_df = pd.util.testing.makeMixedDataFrame()
sample_df.dtypes
```




    A           float64
    B           float64
    C            object
    D    datetime64[ns]
    dtype: object


