## How to reformat and rename values in a pandas dataframe


```python
import pandas as pd
```


```python
df = pd.DataFrame({'Discount':[10, 8, 20, 15, 10],
                   'Product':[' UMbreLla', '  maTress', 'BeDmintoN ', 'Shuttle', 'jaCket  '],
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
      <td>UMbreLla</td>
      <td>880</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>maTress</td>
      <td>1250</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>BeDmintoN</td>
      <td>1450</td>
      <td>11/2/2011</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>Shuttle</td>
      <td>1550</td>
      <td>12/2/2011</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>jaCket</td>
      <td>400</td>
      <td>13/2/2011</td>
    </tr>
  </tbody>
</table>
</div>



here are some ways to (i) strip product names of whitespace and (ii) capitalize their first letter.


```python
#Example 1
ls = df['Product'].tolist()
new_ls = [item.strip().capitalize() for item in ls]
df = df.drop(['Product'], axis=1)
df.insert(1,'Product_new', new_ls)
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
      <th>Product_new</th>
      <th>Updated_Price</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>Umbrella</td>
      <td>880</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>Matress</td>
      <td>1250</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>Bedminton</td>
      <td>1450</td>
      <td>11/2/2011</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>Shuttle</td>
      <td>1550</td>
      <td>12/2/2011</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>Jacket</td>
      <td>400</td>
      <td>13/2/2011</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Example 2
df['Product'] = df['Product'].apply(lambda x: x.strip().capitalize())
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
      <td>Umbrella</td>
      <td>880</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>Matress</td>
      <td>1250</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>Bedminton</td>
      <td>1450</td>
      <td>11/2/2011</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>Shuttle</td>
      <td>1550</td>
      <td>12/2/2011</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>Jacket</td>
      <td>400</td>
      <td>13/2/2011</td>
    </tr>
  </tbody>
</table>
</div>



and the code below renames certain values using regex.


```python
df.replace(to_replace=r'^Be', value='Ba', regex=True, inplace=True)
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
      <th>Product_new</th>
      <th>Updated_Price</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>Umbrella</td>
      <td>880</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>Matress</td>
      <td>1250</td>
      <td>10/2/2011</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>Badminton</td>
      <td>1450</td>
      <td>11/2/2011</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15</td>
      <td>Shuttle</td>
      <td>1550</td>
      <td>12/2/2011</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>Jacket</td>
      <td>400</td>
      <td>13/2/2011</td>
    </tr>
  </tbody>
</table>
</div>


