## how to iterate over rows without df.iterrows()

Using `iterrows()` in Pandas is often considered a bad idea for performance reasons (for instance, `iterrows()` converts each rows to a index and series pair, which slows down an execution).

I recently ran into a situation where I need to (i) check if each row in a certain column ("subscription_type") is NaN, (ii) if so, grab the their parent subscriber id under another column of the row ("is_plus_1_of"), and (iii) replace NaN with the subscription type of the parent subscriber. Here's how I managed to do these without relying on `iterrows()` - namely, I wrote a function and call the function for each row with `apply()`.


```python
import pandas as pd
import numpy as np
```


```python
df = pd.DataFrame({'subscriber_id':['21daf8cd', '3393eee6', 'e0c9b302', '1f0c4dbc', '7c49a7e8'],
                   'subscription_type':[np.nan, 'standard', np.nan, 'pro', 'standard'],
                   'is_plus_1_of':['1f0c4dbc', np.nan, '3393eee6', np.nan, np.nan],
                   'account_create_date':['12/2/2023', '12/4/2023', '12/8/2023', '12/10/2023', '12/15/2023']})
```


```python
def mark_plus1_type(row):
  if row['subscription_type'] != row['subscription_type']: # check for NaN
    parent_type = df[df['subscriber_id'] == row['is_plus_1_of']]['subscription_type'].iloc[0]
    return parent_type
  else:
    return row['subscription_type']

df['subscription_type'] = df.apply(mark_plus1_type, axis=1)
df
```





  <div id="df-cea17b39-6334-4570-bb48-8af118a8546e" class="colab-df-container">
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
      <th>subscriber_id</th>
      <th>subscription_type</th>
      <th>is_plus_1_of</th>
      <th>account_create_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21daf8cd</td>
      <td>pro</td>
      <td>1f0c4dbc</td>
      <td>12/2/2023</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3393eee6</td>
      <td>standard</td>
      <td>NaN</td>
      <td>12/4/2023</td>
    </tr>
    <tr>
      <th>2</th>
      <td>e0c9b302</td>
      <td>standard</td>
      <td>3393eee6</td>
      <td>12/8/2023</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1f0c4dbc</td>
      <td>pro</td>
      <td>NaN</td>
      <td>12/10/2023</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7c49a7e8</td>
      <td>standard</td>
      <td>NaN</td>
      <td>12/15/2023</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-cea17b39-6334-4570-bb48-8af118a8546e')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-cea17b39-6334-4570-bb48-8af118a8546e button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-cea17b39-6334-4570-bb48-8af118a8546e');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-2e4a18a2-1116-4620-a9d5-99177cbf7dca">
  <button class="colab-df-quickchart" onclick="quickchart('df-2e4a18a2-1116-4620-a9d5-99177cbf7dca')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-2e4a18a2-1116-4620-a9d5-99177cbf7dca button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>
    </div>
  </div>




You can see now that the subscription types of the first and third rows reflect those of their parent subscribers.
