

```python
import os
import glob
import pandas as pd
import time
import datetime
```


```python
os.chdir('/Users/sinakhalili/7gate/homework4/homework04_data')
```


```python
all_csvs = [i for i in glob.glob('*.{}'.format('csv'))]
```


```python
data = pd.concat([pd.read_csv(f) for f in all_csvs])
data.to_csv('data.csv' , index = False, encoding='utf-8-sig')
```


```python
data.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>total sleep/night</th>
      <th>caloric intake</th>
      <th>steps taken</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>F</td>
      <td>$5760.0</td>
      <td>54</td>
      <td>BLUE</td>
      <td>5</td>
      <td>9th</td>
      <td>25secs</td>
      <td>3:59:11.385AM</td>
      <td>10:29:28.290AM</td>
      <td>10.50</td>
      <td>2250</td>
      <td>2250225022502250225022502250225022502250225022...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>M</td>
      <td>$2054.0</td>
      <td>60</td>
      <td>blue</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>2:6:19.190AM</td>
      <td>5:20:2.927AM</td>
      <td>4.88</td>
      <td>2750</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>$12533.0</td>
      <td>11</td>
      <td>reD</td>
      <td>0</td>
      <td>4th</td>
      <td>24secs</td>
      <td>3:38:48.885AM</td>
      <td>12:53:26.341PM</td>
      <td>-3.37</td>
      <td>3500</td>
      <td>3500350035003500350035003500350035003500350035...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>f</td>
      <td>$15731.999999999998</td>
      <td>72</td>
      <td>blue</td>
      <td>3</td>
      <td>2nd</td>
      <td>21secs</td>
      <td>8:58:45.95PM</td>
      <td>6:2:46.490AM</td>
      <td>-6.57</td>
      <td>2000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>f</td>
      <td>$1503.0</td>
      <td>62</td>
      <td>red</td>
      <td>2</td>
      <td>4th</td>
      <td>27secs</td>
      <td>4:12:54.207AM</td>
      <td>12:2:2.987PM</td>
      <td>9.83</td>
      <td>1500</td>
      <td>1500150015001500150015001500150015001500150015...</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.shape
```




    (7000000, 14)




```python
rows = data.drop_duplicates()
```


```python
rows.shape
```




    (1000000, 14)




```python
rows['sex'].unique()
```




    array(['F', 'M', 'Female', 'f', 'X', 'female', 'Male', 'm', 'male', '0'],
          dtype=object)




```python
rows[rows['sex'] == '0'].shape
```




    (7726, 14)



### We will map the random values to consistent ones
For the `sex` and `favourite colour`


```python
s_rows = rows.copy()
s_rows['sex'] = rows['sex'].map({
    'F': 'Female',
    'f': 'Female',
    'female': 'Female',
    'M': 'Male',
    'Female': 'Female',
    'male': 'Male',
    'Male': 'Male',
    'm': 'Male',
    'X': 'Other',
    '0': 'Other',
});
```


```python
s_rows['sex'].unique()
```




    array(['Female', 'Male', 'Other'], dtype=object)




```python
s_rows.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>total sleep/night</th>
      <th>caloric intake</th>
      <th>steps taken</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>Female</td>
      <td>$5760.0</td>
      <td>54</td>
      <td>BLUE</td>
      <td>5</td>
      <td>9th</td>
      <td>25secs</td>
      <td>3:59:11.385AM</td>
      <td>10:29:28.290AM</td>
      <td>10.50</td>
      <td>2250</td>
      <td>2250225022502250225022502250225022502250225022...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>Male</td>
      <td>$2054.0</td>
      <td>60</td>
      <td>blue</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>2:6:19.190AM</td>
      <td>5:20:2.927AM</td>
      <td>4.88</td>
      <td>2750</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>$12533.0</td>
      <td>11</td>
      <td>reD</td>
      <td>0</td>
      <td>4th</td>
      <td>24secs</td>
      <td>3:38:48.885AM</td>
      <td>12:53:26.341PM</td>
      <td>-3.37</td>
      <td>3500</td>
      <td>3500350035003500350035003500350035003500350035...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>Female</td>
      <td>$15731.999999999998</td>
      <td>72</td>
      <td>blue</td>
      <td>3</td>
      <td>2nd</td>
      <td>21secs</td>
      <td>8:58:45.95PM</td>
      <td>6:2:46.490AM</td>
      <td>-6.57</td>
      <td>2000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>Female</td>
      <td>$1503.0</td>
      <td>62</td>
      <td>red</td>
      <td>2</td>
      <td>4th</td>
      <td>27secs</td>
      <td>4:12:54.207AM</td>
      <td>12:2:2.987PM</td>
      <td>9.83</td>
      <td>1500</td>
      <td>1500150015001500150015001500150015001500150015...</td>
    </tr>
  </tbody>
</table>
</div>




```python
s_rows['age'].min()
```




    0



### Replacing NaN
With the mean - remembering to use the mean of the values without NaN


```python
s_rows['age'].max()
```




    90




```python
s_rows['age'].map(lambda x: None if x == 0 else x).mean(skipna=True)
```




    48.51111883672421




```python
s_rows['age'].mean()
```




    48.140979




```python
s_rows['age'] = s_rows['age'].replace(0, 48)
```


```python
s_rows['age'].min()
```




    7




```python
s_rows.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>total sleep/night</th>
      <th>caloric intake</th>
      <th>steps taken</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>Female</td>
      <td>$5760.0</td>
      <td>54</td>
      <td>BLUE</td>
      <td>5</td>
      <td>9th</td>
      <td>25secs</td>
      <td>3:59:11.385AM</td>
      <td>10:29:28.290AM</td>
      <td>10.50</td>
      <td>2250</td>
      <td>2250225022502250225022502250225022502250225022...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>Male</td>
      <td>$2054.0</td>
      <td>60</td>
      <td>blue</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>2:6:19.190AM</td>
      <td>5:20:2.927AM</td>
      <td>4.88</td>
      <td>2750</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>$12533.0</td>
      <td>11</td>
      <td>reD</td>
      <td>0</td>
      <td>4th</td>
      <td>24secs</td>
      <td>3:38:48.885AM</td>
      <td>12:53:26.341PM</td>
      <td>-3.37</td>
      <td>3500</td>
      <td>3500350035003500350035003500350035003500350035...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>Female</td>
      <td>$15731.999999999998</td>
      <td>72</td>
      <td>blue</td>
      <td>3</td>
      <td>2nd</td>
      <td>21secs</td>
      <td>8:58:45.95PM</td>
      <td>6:2:46.490AM</td>
      <td>-6.57</td>
      <td>2000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>Female</td>
      <td>$1503.0</td>
      <td>62</td>
      <td>red</td>
      <td>2</td>
      <td>4th</td>
      <td>27secs</td>
      <td>4:12:54.207AM</td>
      <td>12:2:2.987PM</td>
      <td>9.83</td>
      <td>1500</td>
      <td>1500150015001500150015001500150015001500150015...</td>
    </tr>
  </tbody>
</table>
</div>




```python
s_rows['favourite colour'].unique()
```




    array(['BLUE', 'blue', 'reD', 'red', 'None', 'yellow', 'gReeN', 'green',
           '0'], dtype=object)




```python
c_rows = s_rows.copy()
c_rows['favourite colour'] = s_rows['favourite colour'].map({
    'BLUE': 'Blue',
    'blue': 'Blue',
    'reD': 'Red',
    'red': 'Red',
    'yellow': 'Yellow',
    'gReeN': 'Green',
    'green': 'Green',
    'None': 'Unknown',
    '0': 'Unknown',
});
```


```python
def convert_to_seconds(x):
    if(x is not None and not x == '0'):
        x_split = x.split('.')
        x_clean = x_split[0] + x[-2:]
        t = time.strptime(x_clean,'%I:%M:%S%p')
        t_seconds = datetime.timedelta(
            hours=t.tm_hour,
            minutes=t.tm_min,
            seconds=t.tm_sec
        ).total_seconds()
        extra_time = '0.' + x_split[1][:-2]
        return t_seconds + float(extra_time)
    return None
```


```python
seconds_rows = c_rows.copy()
seconds_rows['bed time'] = c_rows['bed time'].map(convert_to_seconds)
seconds_rows['wake up time'] = c_rows['wake up time'].map(convert_to_seconds)
```


```python
seconds_rows.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>total sleep/night</th>
      <th>caloric intake</th>
      <th>steps taken</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>Female</td>
      <td>$5760.0</td>
      <td>54</td>
      <td>Blue</td>
      <td>5</td>
      <td>9th</td>
      <td>25secs</td>
      <td>14351.385</td>
      <td>37768.290</td>
      <td>10.50</td>
      <td>2250</td>
      <td>2250225022502250225022502250225022502250225022...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>Male</td>
      <td>$2054.0</td>
      <td>60</td>
      <td>Blue</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7579.190</td>
      <td>19202.927</td>
      <td>4.88</td>
      <td>2750</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>$12533.0</td>
      <td>11</td>
      <td>Red</td>
      <td>0</td>
      <td>4th</td>
      <td>24secs</td>
      <td>13128.885</td>
      <td>46406.341</td>
      <td>-3.37</td>
      <td>3500</td>
      <td>3500350035003500350035003500350035003500350035...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>Female</td>
      <td>$15731.999999999998</td>
      <td>72</td>
      <td>Blue</td>
      <td>3</td>
      <td>2nd</td>
      <td>21secs</td>
      <td>75525.950</td>
      <td>21766.490</td>
      <td>-6.57</td>
      <td>2000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>Female</td>
      <td>$1503.0</td>
      <td>62</td>
      <td>Red</td>
      <td>2</td>
      <td>4th</td>
      <td>27secs</td>
      <td>15174.207</td>
      <td>43322.987</td>
      <td>9.83</td>
      <td>1500</td>
      <td>1500150015001500150015001500150015001500150015...</td>
    </tr>
  </tbody>
</table>
</div>



### Sanity check...
Looks like the final column `steps taken` is just the `caloric intake` colunmn repeated an arbritrary amount of times... for that reason I will drop this column. Perhaps there is something to this column, but it is unclear, and I would probably consult my data source for this number.


```python
drop_rows = seconds_rows.drop('steps taken', axis=1)
```


```python
drop_rows.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>total sleep/night</th>
      <th>caloric intake</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>Female</td>
      <td>$5760.0</td>
      <td>54</td>
      <td>Blue</td>
      <td>5</td>
      <td>9th</td>
      <td>25secs</td>
      <td>14351.385</td>
      <td>37768.290</td>
      <td>10.50</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>Male</td>
      <td>$2054.0</td>
      <td>60</td>
      <td>Blue</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7579.190</td>
      <td>19202.927</td>
      <td>4.88</td>
      <td>2750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>$12533.0</td>
      <td>11</td>
      <td>Red</td>
      <td>0</td>
      <td>4th</td>
      <td>24secs</td>
      <td>13128.885</td>
      <td>46406.341</td>
      <td>-3.37</td>
      <td>3500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>Female</td>
      <td>$15731.999999999998</td>
      <td>72</td>
      <td>Blue</td>
      <td>3</td>
      <td>2nd</td>
      <td>21secs</td>
      <td>75525.950</td>
      <td>21766.490</td>
      <td>-6.57</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>Female</td>
      <td>$1503.0</td>
      <td>62</td>
      <td>Red</td>
      <td>2</td>
      <td>4th</td>
      <td>27secs</td>
      <td>15174.207</td>
      <td>43322.987</td>
      <td>9.83</td>
      <td>1500</td>
    </tr>
  </tbody>
</table>
</div>




```python
sleep_rows = drop_rows.copy()
sleep_rows['sleep_diff'] = (drop_rows['wake up time'] - drop_rows['bed time']) / 3600
sleep_rows['sleep_diff'] = sleep_rows['sleep_diff'].map(lambda x: x if x>0 else x+24)
```


```python
sleep_rows['sleep_diff'].max()
```




    23.9999425




```python
sleep_rows['sleep_diff'].min()
```




    4.722222222173716e-06




```python
sleep_rows.head(10).boxplot(column=['sleep_diff'], by='age')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x115a78a90>




```python
sleep_rows.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>total sleep/night</th>
      <th>caloric intake</th>
      <th>sleep_diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>Female</td>
      <td>$5760.0</td>
      <td>54</td>
      <td>Blue</td>
      <td>5</td>
      <td>9th</td>
      <td>25secs</td>
      <td>14351.385</td>
      <td>37768.290</td>
      <td>10.50</td>
      <td>2250</td>
      <td>6.504696</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>Male</td>
      <td>$2054.0</td>
      <td>60</td>
      <td>Blue</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7579.190</td>
      <td>19202.927</td>
      <td>4.88</td>
      <td>2750</td>
      <td>3.228816</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>$12533.0</td>
      <td>11</td>
      <td>Red</td>
      <td>0</td>
      <td>4th</td>
      <td>24secs</td>
      <td>13128.885</td>
      <td>46406.341</td>
      <td>-3.37</td>
      <td>3500</td>
      <td>9.243738</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>Female</td>
      <td>$15731.999999999998</td>
      <td>72</td>
      <td>Blue</td>
      <td>3</td>
      <td>2nd</td>
      <td>21secs</td>
      <td>75525.950</td>
      <td>21766.490</td>
      <td>-6.57</td>
      <td>2000</td>
      <td>9.066817</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>Female</td>
      <td>$1503.0</td>
      <td>62</td>
      <td>Red</td>
      <td>2</td>
      <td>4th</td>
      <td>27secs</td>
      <td>15174.207</td>
      <td>43322.987</td>
      <td>9.83</td>
      <td>1500</td>
      <td>7.819106</td>
    </tr>
  </tbody>
</table>
</div>



### Human intervention again
Not exactly sure what the `total sleep/night` column is measuring since it's not wake up time - bed time... So I'm going to be dropping that column and adding a new column called sleep diff


```python
sleep_drop = sleep_rows.drop('total sleep/night', axis=1)
```


```python
sleep_drop.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>caloric intake</th>
      <th>sleep_diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>Female</td>
      <td>$5760.0</td>
      <td>54</td>
      <td>Blue</td>
      <td>5</td>
      <td>9th</td>
      <td>25secs</td>
      <td>14351.385</td>
      <td>37768.290</td>
      <td>2250</td>
      <td>6.504696</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>Male</td>
      <td>$2054.0</td>
      <td>60</td>
      <td>Blue</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7579.190</td>
      <td>19202.927</td>
      <td>2750</td>
      <td>3.228816</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>$12533.0</td>
      <td>11</td>
      <td>Red</td>
      <td>0</td>
      <td>4th</td>
      <td>24secs</td>
      <td>13128.885</td>
      <td>46406.341</td>
      <td>3500</td>
      <td>9.243738</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>Female</td>
      <td>$15731.999999999998</td>
      <td>72</td>
      <td>Blue</td>
      <td>3</td>
      <td>2nd</td>
      <td>21secs</td>
      <td>75525.950</td>
      <td>21766.490</td>
      <td>2000</td>
      <td>9.066817</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>Female</td>
      <td>$1503.0</td>
      <td>62</td>
      <td>Red</td>
      <td>2</td>
      <td>4th</td>
      <td>27secs</td>
      <td>15174.207</td>
      <td>43322.987</td>
      <td>1500</td>
      <td>7.819106</td>
    </tr>
  </tbody>
</table>
</div>




```python
sleep_drop['monthly income'] = sleep_drop['monthly income'].map(
    lambda x: x.split('$')[-1]
).astype(float)
```


```python
sleep_drop.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>caloric intake</th>
      <th>sleep_diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>Female</td>
      <td>5760.0</td>
      <td>54</td>
      <td>Blue</td>
      <td>5</td>
      <td>9th</td>
      <td>25secs</td>
      <td>14351.385</td>
      <td>37768.290</td>
      <td>2250</td>
      <td>6.504696</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>Male</td>
      <td>2054.0</td>
      <td>60</td>
      <td>Blue</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7579.190</td>
      <td>19202.927</td>
      <td>2750</td>
      <td>3.228816</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>12533.0</td>
      <td>11</td>
      <td>Red</td>
      <td>0</td>
      <td>4th</td>
      <td>24secs</td>
      <td>13128.885</td>
      <td>46406.341</td>
      <td>3500</td>
      <td>9.243738</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>Female</td>
      <td>15732.0</td>
      <td>72</td>
      <td>Blue</td>
      <td>3</td>
      <td>2nd</td>
      <td>21secs</td>
      <td>75525.950</td>
      <td>21766.490</td>
      <td>2000</td>
      <td>9.066817</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>Female</td>
      <td>1503.0</td>
      <td>62</td>
      <td>Red</td>
      <td>2</td>
      <td>4th</td>
      <td>27secs</td>
      <td>15174.207</td>
      <td>43322.987</td>
      <td>1500</td>
      <td>7.819106</td>
    </tr>
  </tbody>
</table>
</div>




```python
sleep_drop['last time'] = sleep_drop['last time'].map(
    lambda x: x.replace('secs', '')
).astype(int)
```


```python
sleep_drop.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>caloric intake</th>
      <th>sleep_diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>Female</td>
      <td>5760.0</td>
      <td>54</td>
      <td>Blue</td>
      <td>5</td>
      <td>9th</td>
      <td>25</td>
      <td>14351.385</td>
      <td>37768.290</td>
      <td>2250</td>
      <td>6.504696</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>Male</td>
      <td>2054.0</td>
      <td>60</td>
      <td>Blue</td>
      <td>3</td>
      <td>9th</td>
      <td>27</td>
      <td>7579.190</td>
      <td>19202.927</td>
      <td>2750</td>
      <td>3.228816</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>12533.0</td>
      <td>11</td>
      <td>Red</td>
      <td>0</td>
      <td>4th</td>
      <td>24</td>
      <td>13128.885</td>
      <td>46406.341</td>
      <td>3500</td>
      <td>9.243738</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>Female</td>
      <td>15732.0</td>
      <td>72</td>
      <td>Blue</td>
      <td>3</td>
      <td>2nd</td>
      <td>21</td>
      <td>75525.950</td>
      <td>21766.490</td>
      <td>2000</td>
      <td>9.066817</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>Female</td>
      <td>1503.0</td>
      <td>62</td>
      <td>Red</td>
      <td>2</td>
      <td>4th</td>
      <td>27</td>
      <td>15174.207</td>
      <td>43322.987</td>
      <td>1500</td>
      <td>7.819106</td>
    </tr>
  </tbody>
</table>
</div>




```python
sleep_drop['top finish placement'] = sleep_drop['top finish placement'].map(
    lambda x: x.replace('nd', '')
               .replace('th','')
               .replace('st','')
               .replace('rd','')
).astype(int)
```


```python
sleep_drop.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>caloric intake</th>
      <th>sleep_diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>40</td>
      <td>Female</td>
      <td>5760.0</td>
      <td>54</td>
      <td>Blue</td>
      <td>5</td>
      <td>9</td>
      <td>25</td>
      <td>14351.385</td>
      <td>37768.290</td>
      <td>2250</td>
      <td>6.504696</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>26</td>
      <td>Male</td>
      <td>2054.0</td>
      <td>60</td>
      <td>Blue</td>
      <td>3</td>
      <td>9</td>
      <td>27</td>
      <td>7579.190</td>
      <td>19202.927</td>
      <td>2750</td>
      <td>3.228816</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>83</td>
      <td>Female</td>
      <td>12533.0</td>
      <td>11</td>
      <td>Red</td>
      <td>0</td>
      <td>4</td>
      <td>24</td>
      <td>13128.885</td>
      <td>46406.341</td>
      <td>3500</td>
      <td>9.243738</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>57</td>
      <td>Female</td>
      <td>15732.0</td>
      <td>72</td>
      <td>Blue</td>
      <td>3</td>
      <td>2</td>
      <td>21</td>
      <td>75525.950</td>
      <td>21766.490</td>
      <td>2000</td>
      <td>9.066817</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>9</td>
      <td>Female</td>
      <td>1503.0</td>
      <td>62</td>
      <td>Red</td>
      <td>2</td>
      <td>4</td>
      <td>27</td>
      <td>15174.207</td>
      <td>43322.987</td>
      <td>1500</td>
      <td>7.819106</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Thought I would save some time normalizing since we already learnt it...
from sklearn import preprocessing
```


```python
normalized_data = sleep_drop.drop(['ID', 'sex', 'favourite colour'], axis=1)
min_max_scaler = preprocessing.MinMaxScaler()
np_scaled = min_max_scaler.fit_transform(normalized_data)
normalized_data = pd.DataFrame(np_scaled, columns=[
    'age', 'monthly income', 'work hours/week', 'siblings', 'top finish placement', 
    'last time', 'bed time','wake up time', 'caloric intake', 'sleep_diff'
])

# Add back in the categorical ones... 
sleep_drop['age'] = normalized_data['age']
sleep_drop['monthly income'] = normalized_data['monthly income']
sleep_drop['work hours/week'] = normalized_data['work hours/week']
sleep_drop['siblings'] = normalized_data['siblings']
sleep_drop['top finish placement'] = normalized_data['top finish placement']
sleep_drop['last time'] = normalized_data['last time']
sleep_drop['bed time'] = normalized_data['bed time']
sleep_drop['wake up time'] = normalized_data['wake up time']
sleep_drop['caloric intake'] = normalized_data['caloric intake']
sleep_drop['sleep_diff'] = normalized_data['sleep_diff']
```


```python
sleep_drop.head()
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
      <th>ID</th>
      <th>age</th>
      <th>sex</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>caloric intake</th>
      <th>sleep_diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>0.397590</td>
      <td>Female</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.000000</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.600000</td>
      <td>0.271029</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790282</td>
      <td>0.228916</td>
      <td>Male</td>
      <td>0.076074</td>
      <td>0.759494</td>
      <td>Blue</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>0.048057</td>
      <td>0.041765</td>
      <td>0.733333</td>
      <td>0.134534</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790283</td>
      <td>0.915663</td>
      <td>Female</td>
      <td>0.464185</td>
      <td>0.139241</td>
      <td>Red</td>
      <td>0.000000</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>0.115082</td>
      <td>0.986332</td>
      <td>0.933333</td>
      <td>0.385157</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790284</td>
      <td>0.602410</td>
      <td>Female</td>
      <td>0.582667</td>
      <td>0.911392</td>
      <td>Blue</td>
      <td>0.333333</td>
      <td>0.222222</td>
      <td>0.700000</td>
      <td>0.868671</td>
      <td>0.130778</td>
      <td>0.533333</td>
      <td>0.377785</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790285</td>
      <td>0.024096</td>
      <td>Female</td>
      <td>0.055667</td>
      <td>0.784810</td>
      <td>Red</td>
      <td>0.222222</td>
      <td>0.444444</td>
      <td>0.900000</td>
      <td>0.139784</td>
      <td>0.879270</td>
      <td>0.400000</td>
      <td>0.325797</td>
    </tr>
  </tbody>
</table>
</div>




```python
oh_data = sleep_drop.copy()
```


```python
oh_data = oh_data.join(pd.get_dummies(oh_data['sex']))
```


```python
# oh_data.drop('sex', inplace=True, axis=1)///////////////////////
```


```python
# This is basically where my computer dies, it won't get the favourite colour dummies :(
# So I will use a small (5000 row subset) of the data, called oh_data_small.csv
oh_data.to_csv('/Users/sinakhalili/7gate/homework4/oh_data.csv', index = None, header=True)
```


```python
load = pd.read_csv('/Users/sinakhalili/7gate/homework4/7gate_homework4/homework04_data/oh_data_small.csv')
```


```python
load.head()
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
      <th>ID</th>
      <th>age</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>caloric intake</th>
      <th>sleep_diff</th>
      <th>Female</th>
      <th>Male</th>
      <th>Other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
load.head()
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
      <th>ID</th>
      <th>age</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>favourite colour</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>caloric intake</th>
      <th>sleep_diff</th>
      <th>Female</th>
      <th>Male</th>
      <th>Other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>Blue</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>0.271029</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
load = load.join(pd.get_dummies(load['favourite colour'], 'Colour'))
```


```python
load.drop('favourite colour', inplace=True, axis=1)
```


```python
load.head()
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
      <th>ID</th>
      <th>age</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>caloric intake</th>
      <th>...</th>
      <th>Blue</th>
      <th>Green</th>
      <th>Red</th>
      <th>Unknown</th>
      <th>Yellow</th>
      <th>Colour_Blue</th>
      <th>Colour_Green</th>
      <th>Colour_Red</th>
      <th>Colour_Unknown</th>
      <th>Colour_Yellow</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>790281</td>
      <td>0.39759</td>
      <td>0.213333</td>
      <td>0.683544</td>
      <td>0.555556</td>
      <td>1.0</td>
      <td>0.833333</td>
      <td>0.129847</td>
      <td>0.686398</td>
      <td>0.6</td>
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>


