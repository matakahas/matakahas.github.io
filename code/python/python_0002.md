## Subset/select rows and columns in a pandas dataframe


```python
import pandas as pd
```


```python
df = pd.DataFrame({'Date':['10/2/2011', '10/2/2011', '11/2/2011', '12/2/2011', '13/2/2011'],
                   'Product':['umbrella', 'matress', 'badminton', 'shuttle', 'jacket'],
                   'Updated_Price':[880, 1250, 1450, 1550, 400],
                   'Discount':[10, 8, 20, 15, 10]})
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
      <td>880</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10/2/2011</td>
      <td>matress</td>
      <td>1250</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>badminton</td>
      <td>1450</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>shuttle</td>
      <td>1550</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13/2/2011</td>
      <td>jacket</td>
      <td>400</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



### subset columns with column names


```python
df[['Product', 'Discount']]
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
      <th>Product</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>umbrella</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>matress</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>badminton</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>shuttle</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>jacket</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



### subset columns with column indexes


```python
df.iloc[:, [1,3]]
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
      <th>Product</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>umbrella</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>matress</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>badminton</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>shuttle</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>jacket</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



### subset rows with row indexes


```python
df.iloc[[1,3], :]
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
      <th>1</th>
      <td>10/2/2011</td>
      <td>matress</td>
      <td>1250</td>
      <td>8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>shuttle</td>
      <td>1550</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



### select rows that contain a particular value


```python
#perfect match
df[df['Product'] == 'shuttle']
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
      <th>3</th>
      <td>12/2/2011</td>
      <td>shuttle</td>
      <td>1550</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
#partial match
df[df['Product'].str.contains("ll", na=False)]
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
      <td>880</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



### select rows based on a condition


```python
df[df['Updated_Price'] > 1000]
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
      <th>1</th>
      <td>10/2/2011</td>
      <td>matress</td>
      <td>1250</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>badminton</td>
      <td>1450</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12/2/2011</td>
      <td>shuttle</td>
      <td>1550</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



### select both rows and columns with indexes


```python
df.iloc[0:2, 1:3]
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
      <th>Product</th>
      <th>Updated_Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>umbrella</td>
      <td>880</td>
    </tr>
    <tr>
      <th>1</th>
      <td>matress</td>
      <td>1250</td>
    </tr>
  </tbody>
</table>
</div>



### select every nth row


```python
df.iloc[::2, :] #every 2nd row
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
      <td>880</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11/2/2011</td>
      <td>badminton</td>
      <td>1450</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13/2/2011</td>
      <td>jacket</td>
      <td>400</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



### select columns of a certain data type


```python
df.select_dtypes(include = "number")
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
      <th>Updated_Price</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>880</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1250</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1450</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1550</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>400</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>


