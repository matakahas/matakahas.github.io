## How to reorder rows and columns in a pandas dataframe


```python
import pandas as pd
```


```python
df = pd.DataFrame({'Discount':[10, 8, 20, 15, 10],
                   'Product':['umbrella', 'matress', 'badminton', 'shuttle', 'jacket'],
                   'Updated_Price':[880, 1250, 1450, 1550, 400],
                   'Date':['10/2/2011', '10/2/2011', '11/2/2011', '12/2/2011', '13/2/2011']})
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
      <th>Discount</th>
      <th>Product</th>
      <th>Updated_Price</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>umbrella</td>
      <td>880</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>matress</td>
      <td>1250</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>badminton</td>
      <td>1450</td>
      <td>11/2/2011</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>shuttle</td>
      <td>1550</td>
      <td>12/2/2011</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>jacket</td>
      <td>400</td>
      <td>13/2/2011</td>
    </tr>
  </tbody>
</table>
</div>



### reorder columns


```python
new_index = ['Date','Updated_Price','Product_new','Discount']
df = df.reindex(new_index, axis="columns")
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
      <th>Updated_Price</th>
      <th>Product_new</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10/2/2011</td>
      <td>880</td>
      <td>NaN</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10/2/2011</td>
      <td>1250</td>
      <td>NaN</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>1450</td>
      <td>NaN</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>1550</td>
      <td>NaN</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13/2/2011</td>
      <td>400</td>
      <td>NaN</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



### reorder rows


```python
df.sort_values(by ='Updated_Price', ascending = 0, inplace=True)
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
      <th>Updated_Price</th>
      <th>Product_new</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>1550</td>
      <td>NaN</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>1450</td>
      <td>NaN</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10/2/2011</td>
      <td>1250</td>
      <td>NaN</td>
      <td>8</td>
    </tr>
    <tr>
      <th>0</th>
      <td>10/2/2011</td>
      <td>880</td>
      <td>NaN</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13/2/2011</td>
      <td>400</td>
      <td>NaN</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>


