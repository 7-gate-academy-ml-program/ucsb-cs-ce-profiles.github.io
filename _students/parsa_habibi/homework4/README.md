

```python
import os
import glob
import pandas as pd
import numpy as np
import math as m 
os.chdir(r'C:\Users\parsa\Desktop\7gate\Homework4\data')
```


```python
ex = 'csv'
all_csvs = [i for i in glob.glob('*.{}'.format(ex))]
```


```python
! rm -fr data.csv
```


```python
print (all_csvs)
```

    ['0.csv', '1.csv', '10.csv', '11.csv', '12.csv', '13.csv', '14.csv', '15.csv', '16.csv', '17.csv', '18.csv', '19.csv', '2.csv', '20.csv', '21.csv', '22.csv', '23.csv', '24.csv', '25.csv', '26.csv', '27.csv', '28.csv', '29.csv', '3.csv', '30.csv', '31.csv', '32.csv', '33.csv', '34.csv', '35.csv', '36.csv', '37.csv', '38.csv', '39.csv', '4.csv', '40.csv', '41.csv', '42.csv', '43.csv', '44.csv', '45.csv', '46.csv', '47.csv', '48.csv', '49.csv', '5.csv', '50.csv', '51.csv', '52.csv', '53.csv', '54.csv', '55.csv', '56.csv', '57.csv', '58.csv', '59.csv', '6.csv', '60.csv', '61.csv', '62.csv', '63.csv', '64.csv', '65.csv', '66.csv', '67.csv', '68.csv', '69.csv', '7.csv', '70.csv', '71.csv', '72.csv', '73.csv', '74.csv', '75.csv', '76.csv', '77.csv', '78.csv', '79.csv', '8.csv', '80.csv', '81.csv', '82.csv', '9.csv']
    


```python
#this is only needed to be done once.
data_ = pd.concat([pd.read_csv(f) for f in all_csvs])
data_.to_csv('data.csv' , index = False, encoding='utf-8-sig')
```


```python
data = data_.drop_duplicates()
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
      <td>1</td>
      <td>11</td>
      <td>male</td>
      <td>$3058.0</td>
      <td>19</td>
      <td>green</td>
      <td>4</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
      <td>2000200020002000200020002000200020002000200020...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>33</td>
      <td>m</td>
      <td>0</td>
      <td>53</td>
      <td>BLUE</td>
      <td>5</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>37</td>
      <td>m</td>
      <td>$3108.0</td>
      <td>27</td>
      <td>gReeN</td>
      <td>5</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
      <td>2250225022502250225022502250225022502250225022...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>88</td>
      <td>male</td>
      <td>$23408.0</td>
      <td>12</td>
      <td>gReeN</td>
      <td>0</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
      <td>1750175017501750175017501750175017501750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>M</td>
      <td>$17840.0</td>
      <td>50</td>
      <td>None</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
      <td>3750375037503750375037503750375037503750</td>
    </tr>
  </tbody>
</table>
</div>




```python
data = data.drop('steps taken' , axis=1)
```


```python
print(data.describe())
print('============================')
print(data.dtypes)
```

                       ID             age  work hours/week        siblings  \
    count  1000000.000000  1000000.000000   1000000.000000  1000000.000000   
    mean    500000.500000       48.140979        41.700051        4.466983   
    std     288675.278932       24.513761        21.876296        2.888980   
    min          1.000000        0.000000         0.000000        0.000000   
    25%     250000.750000       27.000000        23.000000        2.000000   
    50%     500000.500000       48.000000        42.000000        4.000000   
    75%     750000.250000       69.000000        61.000000        7.000000   
    max    1000000.000000       90.000000        79.000000        9.000000   
    
           total sleep/night  caloric intake  
    count     1000000.000000  1000000.000000  
    mean           -0.004699     2604.819000  
    std             7.182218      750.914137  
    min           -12.500000        0.000000  
    25%            -6.200000     2000.000000  
    50%             0.000000     2500.000000  
    75%             6.190000     3250.000000  
    max            12.500000     3750.000000  
    ============================
    ID                        int64
    age                       int64
    sex                      object
    monthly income           object
    work hours/week           int64
    favourite colour         object
    siblings                  int64
    top finish placement     object
    last time                object
    bed time                 object
    wake up time             object
    total sleep/night       float64
    caloric intake            int64
    dtype: object
    

# Sex

### get rid of inalid entres


```python
data['sex'].astype(str)

conv_m = lambda x: 'm' if(x[0].lower() == 'm') else x
conv_f = lambda x: 'f' if(x[0].lower() == 'f') else x
conv_o = lambda x: 'other' if(x[0].lower() == 'x' or x[0].lower() == '0' ) else x

data['sex']=data['sex'].map(conv_m).map(conv_f).map(conv_o)

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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>11</td>
      <td>m</td>
      <td>$3058.0</td>
      <td>19</td>
      <td>green</td>
      <td>4</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>33</td>
      <td>m</td>
      <td>0</td>
      <td>53</td>
      <td>BLUE</td>
      <td>5</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>37</td>
      <td>m</td>
      <td>$3108.0</td>
      <td>27</td>
      <td>gReeN</td>
      <td>5</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>88</td>
      <td>m</td>
      <td>$23408.0</td>
      <td>12</td>
      <td>gReeN</td>
      <td>0</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>m</td>
      <td>$17840.0</td>
      <td>50</td>
      <td>None</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
  </tbody>
</table>
</div>



# Age

### Replace 0s and invalid enteres with the mean


```python
data['age'] = data['age'].replace(0,np.nan)
mean = data['age'].mean(skipna=True)

#now we just replace the nans with the mean

data['age'] = data['age'].replace(np.nan, 48) 
data['age'] = data['age'].astype('int64')
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>11</td>
      <td>m</td>
      <td>$3058.0</td>
      <td>19</td>
      <td>green</td>
      <td>4</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>33</td>
      <td>m</td>
      <td>0</td>
      <td>53</td>
      <td>BLUE</td>
      <td>5</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>37</td>
      <td>m</td>
      <td>$3108.0</td>
      <td>27</td>
      <td>gReeN</td>
      <td>5</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>88</td>
      <td>m</td>
      <td>$23408.0</td>
      <td>12</td>
      <td>gReeN</td>
      <td>0</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>48</td>
      <td>m</td>
      <td>$17840.0</td>
      <td>50</td>
      <td>None</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
  </tbody>
</table>
</div>



### Normilize


```python
min_ = min(data['age'])
max_ = max(data['age'])

normilize = lambda x : (x-min_)/(max_- min_)
data['age'] = data['age'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>$3058.0</td>
      <td>19</td>
      <td>green</td>
      <td>4</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0</td>
      <td>53</td>
      <td>BLUE</td>
      <td>5</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>$3108.0</td>
      <td>27</td>
      <td>gReeN</td>
      <td>5</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>$23408.0</td>
      <td>12</td>
      <td>gReeN</td>
      <td>0</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>$17840.0</td>
      <td>50</td>
      <td>None</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>$26820.0</td>
      <td>45</td>
      <td>green</td>
      <td>3</td>
      <td>4th</td>
      <td>24secs</td>
      <td>2:15:13.319AM</td>
      <td>11:2:57.944AM</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>$3161.0000000000005</td>
      <td>71</td>
      <td>blue</td>
      <td>0</td>
      <td>7th</td>
      <td>23secs</td>
      <td>10:52:44.176PM</td>
      <td>9:17:41.3AM</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



# Monthly Income


```python
remove_dolla = lambda x: x[1:] if(x[0] == '$') else x
data['monthly income'] = data['monthly income'].map(remove_dolla)

# convert to float and round up or down accordingly.
data['monthly income'] = data['monthly income'].astype(float)
np.around(data['monthly income'] ,  decimals = 5)

#convert to int

data['monthly income'] = data['monthly income'].astype('int32')

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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>3058</td>
      <td>19</td>
      <td>green</td>
      <td>4</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0</td>
      <td>53</td>
      <td>BLUE</td>
      <td>5</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>3108</td>
      <td>27</td>
      <td>gReeN</td>
      <td>5</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>23408</td>
      <td>12</td>
      <td>gReeN</td>
      <td>0</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>17840</td>
      <td>50</td>
      <td>None</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
  </tbody>
</table>
</div>



### Calculate the Mean and Replace the 0s with it


```python
data['monthly income'] = data['monthly income'].replace(0,np.nan)
mean = data['monthly income'].mean(skipna=True)
data['monthly income'] = data['monthly income'].replace(np.nan,int(mean))
data['monthly income'] = data['monthly income'].astype('int32')
data.head(7)

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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>3058</td>
      <td>19</td>
      <td>green</td>
      <td>4</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>7760</td>
      <td>53</td>
      <td>BLUE</td>
      <td>5</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>3108</td>
      <td>27</td>
      <td>gReeN</td>
      <td>5</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>23408</td>
      <td>12</td>
      <td>gReeN</td>
      <td>0</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>17840</td>
      <td>50</td>
      <td>None</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>26820</td>
      <td>45</td>
      <td>green</td>
      <td>3</td>
      <td>4th</td>
      <td>24secs</td>
      <td>2:15:13.319AM</td>
      <td>11:2:57.944AM</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>3161</td>
      <td>71</td>
      <td>blue</td>
      <td>0</td>
      <td>7th</td>
      <td>23secs</td>
      <td>10:52:44.176PM</td>
      <td>9:17:41.3AM</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



### Normilize


```python
min_ = min(data['monthly income'])
max_ = max(data['monthly income'])

normilize = lambda x : (x-min_)/(max_- min_)
data['monthly income'] = data['monthly income'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>19</td>
      <td>green</td>
      <td>4</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>53</td>
      <td>BLUE</td>
      <td>5</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>27</td>
      <td>gReeN</td>
      <td>5</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>12</td>
      <td>gReeN</td>
      <td>0</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>50</td>
      <td>None</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>45</td>
      <td>green</td>
      <td>3</td>
      <td>4th</td>
      <td>24secs</td>
      <td>2:15:13.319AM</td>
      <td>11:2:57.944AM</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>71</td>
      <td>blue</td>
      <td>0</td>
      <td>7th</td>
      <td>23secs</td>
      <td>10:52:44.176PM</td>
      <td>9:17:41.3AM</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



# Work Hours/Week

### Normilize


```python
min_ = min(data['work hours/week'])
max_ = max(data['work hours/week'])

normilize = lambda x : (x-min_)/(max_- min_)
data['work hours/week'] = data['work hours/week'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>4</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>BLUE</td>
      <td>5</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>gReeN</td>
      <td>5</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>gReeN</td>
      <td>0</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>None</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>3</td>
      <td>4th</td>
      <td>24secs</td>
      <td>2:15:13.319AM</td>
      <td>11:2:57.944AM</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0</td>
      <td>7th</td>
      <td>23secs</td>
      <td>10:52:44.176PM</td>
      <td>9:17:41.3AM</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



# Fav Color

### get rid of invalids and make them all catagorical


```python

data['favourite colour'].astype(str)
rm_bad =  lambda x: 'none' if(x == '0' or x == 'None') else x.lower()
data['favourite colour'] = data['favourite colour'].map(rm_bad)


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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>4</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>5</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>5</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>3</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

# SIblings


```python
min_ = min(data['siblings'])
max_ = max(data['siblings'])

normilize = lambda x : (x-min_)/(max_- min_)
data['siblings'] = data['siblings'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>5th</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>1st</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>8th</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>6th</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>9th</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>4th</td>
      <td>24secs</td>
      <td>2:15:13.319AM</td>
      <td>11:2:57.944AM</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>7th</td>
      <td>23secs</td>
      <td>10:52:44.176PM</td>
      <td>9:17:41.3AM</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



# top finish placement


```python
# Removing st
rm_st = lambda x : x.replace('st' , '')
#Removing th
rm_th = lambda x : x.replace('th' , '')
#Removing rd 
rm_rd = lambda x : x.replace('rd' , '')
#Removing nd
rm_nd = lambda x : x.replace('nd' , '')

data['top finish placement'] = data['top finish placement'].map(rm_st)
data['top finish placement'] = data['top finish placement'].map(rm_th)
data['top finish placement'] = data['top finish placement'].map(rm_rd)
data['top finish placement'] = data['top finish placement'].map(rm_nd)
data['top finish placement'] = data['top finish placement'].astype('int32')
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>5</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>1</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>8</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>6</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>9</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
  </tbody>
</table>
</div>



### Normilize


```python
min_ = min(data['top finish placement'])
max_ = max(data['top finish placement'])

normilize = lambda x : (x-min_)/(max_- min_)
data['top finish placement'] = data['top finish placement'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>27secs</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>29secs</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>22secs</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>26secs</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>27secs</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>24secs</td>
      <td>2:15:13.319AM</td>
      <td>11:2:57.944AM</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>23secs</td>
      <td>10:52:44.176PM</td>
      <td>9:17:41.3AM</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



# Last Time

### Get rid of Secs


```python
rm_sec = lambda x : x.replace('secs' , '')
data['last time'] = data['last time'].map(rm_sec)
data['last time'] = data['last time'].astype('int32')
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>27</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>29</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>22</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>26</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>27</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
  </tbody>
</table>
</div>



### Normilize


```python
min_ = min(data['last time'])
max_ = max(data['last time'])

normilize = lambda x : (x-min_)/(max_- min_)
data['last time'] = data['last time'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>11:45:32.334PM</td>
      <td>10:41:17.64AM</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>8:3:40.514PM</td>
      <td>8:56:47.711AM</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>11:21:53.189PM</td>
      <td>10:21:49.198AM</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>2:37:12.32AM</td>
      <td>7:27:14.54AM</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>7:31:1.947PM</td>
      <td>11:20:15.527AM</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>2:15:13.319AM</td>
      <td>11:2:57.944AM</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>10:52:44.176PM</td>
      <td>9:17:41.3AM</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



# Bed time and Wake up time

### Get rid of AM , PM 


```python
rp_AM = lambda x: x.replace('AM' , '')
rp_PM = lambda x: x.replace('PM' , '')

data['bed time'] = data['bed time'].map(rp_AM)
data['bed time'] = data['bed time'].map(rp_PM)

data['wake up time'] = data['wake up time'].map(rp_AM)
data['wake up time'] = data['wake up time'].map(rp_PM)

data.head()
# f = lambda x : x.split(':')
# h = data['bed time'].map(f)
# print (h)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>11:45:32.334</td>
      <td>10:41:17.64</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>8:3:40.514</td>
      <td>8:56:47.711</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>11:21:53.189</td>
      <td>10:21:49.198</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>2:37:12.32</td>
      <td>7:27:14.54</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>7:31:1.947</td>
      <td>11:20:15.527</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
  </tbody>
</table>
</div>



### Convert to Secs


```python
f = lambda x :  x.split(':')  if(x != '0') else x
data['bed time'] = data['bed time'].map(f)
```


```python
h_to_sec = lambda x : int(x[0])*3600 + int(x[0])*60 + float(x[2]) if(len(x) > 1) else x
```


```python
data['bed time'] = data['bed time'].map(h_to_sec)
```


```python
data['wake up time'] = data['wake up time'].map(f)
data['wake up time'] = data['wake up time'].map(h_to_sec)
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>40292.3</td>
      <td>36617.6</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>29320.5</td>
      <td>29327.7</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>40313.2</td>
      <td>36649.2</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>7332.32</td>
      <td>25634.5</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>25621.9</td>
      <td>40275.5</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
  </tbody>
</table>
</div>




```python
data['bed time'] = data['bed time'].astype('float64')
data['wake up time'] = data['wake up time'].astype('float64')
```

### Replace 0s with Mean


```python
mean_b = data['bed time'].mean(skipna = True)
mean_w = data['wake up time'].mean(skipna = True)

data['bed time'] = data['bed time'].replace(0,mean_b)
data['wake up time'] = data['wake up time'].replace(0,mean_w)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>40292.334</td>
      <td>36617.640</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>29320.514</td>
      <td>29327.711</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>40313.189</td>
      <td>36649.198</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>7332.320</td>
      <td>25634.540</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>25621.947</td>
      <td>40275.527</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>7333.319</td>
      <td>40317.944</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>36644.176</td>
      <td>32981.300</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



### Normilize


```python
min_ = min(data['bed time'])
max_ = max(data['bed time'])

normilize = lambda x : (x-min_)/(max_- min_)
data['bed time'] = data['bed time'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>0.908540</td>
      <td>36617.640</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>0.636421</td>
      <td>29327.711</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>0.909057</td>
      <td>36649.198</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>0.091079</td>
      <td>25634.540</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>0.544691</td>
      <td>40275.527</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>0.091104</td>
      <td>40317.944</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>0.818060</td>
      <td>32981.300</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(data[data['wake up time'] == 0.0 ].shape)
```

    (0, 13)
    


```python
min_ = min(data['wake up time'])
max_ = max(data['wake up time'])

normilize = lambda x : (x-min_)/(max_- min_)
data['wake up time'] = data['wake up time'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>0.908540</td>
      <td>0.713304</td>
      <td>-5.01</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>0.636421</td>
      <td>0.429428</td>
      <td>8.35</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>0.909057</td>
      <td>0.714533</td>
      <td>-1.78</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>0.091079</td>
      <td>0.285613</td>
      <td>11.44</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>0.544691</td>
      <td>0.855745</td>
      <td>11.44</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>0.091104</td>
      <td>0.857397</td>
      <td>-11.49</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>0.818060</td>
      <td>0.571702</td>
      <td>5.53</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



# Total sleep/night 

### Normilize


```python
min_ = min(data['total sleep/night'])
max_ = max(data['total sleep/night'])

normilize = lambda x : (x-min_)/(max_- min_)
data['total sleep/night'] = data['total sleep/night'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>0.908540</td>
      <td>0.713304</td>
      <td>0.2996</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>0.636421</td>
      <td>0.429428</td>
      <td>0.8340</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>0.909057</td>
      <td>0.714533</td>
      <td>0.4288</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>0.091079</td>
      <td>0.285613</td>
      <td>0.9576</td>
      <td>1750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>0.544691</td>
      <td>0.855745</td>
      <td>0.9576</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>0.091104</td>
      <td>0.857397</td>
      <td>0.0404</td>
      <td>2250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>0.818060</td>
      <td>0.571702</td>
      <td>0.7212</td>
      <td>3500</td>
    </tr>
  </tbody>
</table>
</div>



# Caloric intake

### Getting rid of 0s 


```python
data['caloric intake'] = data['caloric intake'].replace(0,np.nan)
mean_ = data['caloric intake'].mean(skipna = True)
mean_ = data['caloric intake'].replace(np.nan , mean_)
# data['caloric intake'] = data['caloric intake'].astype('int64')
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>0.908540</td>
      <td>0.713304</td>
      <td>0.2996</td>
      <td>2000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>0.636421</td>
      <td>0.429428</td>
      <td>0.8340</td>
      <td>3750.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>0.909057</td>
      <td>0.714533</td>
      <td>0.4288</td>
      <td>2250.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>0.091079</td>
      <td>0.285613</td>
      <td>0.9576</td>
      <td>1750.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>0.544691</td>
      <td>0.855745</td>
      <td>0.9576</td>
      <td>3750.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>0.091104</td>
      <td>0.857397</td>
      <td>0.0404</td>
      <td>2250.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>0.818060</td>
      <td>0.571702</td>
      <td>0.7212</td>
      <td>3500.0</td>
    </tr>
  </tbody>
</table>
</div>



### Normilize


```python
min_ = min(data['caloric intake'])
max_ = max(data['caloric intake'])

normilize = lambda x : (x-min_)/(max_- min_)
data['caloric intake'] = data['caloric intake'].map(normilize)
data.head(7)
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
      <td>1</td>
      <td>0.048193</td>
      <td>m</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>0.908540</td>
      <td>0.713304</td>
      <td>0.2996</td>
      <td>0.222222</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>m</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>0.636421</td>
      <td>0.429428</td>
      <td>0.8340</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>m</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>0.909057</td>
      <td>0.714533</td>
      <td>0.4288</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>m</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>0.091079</td>
      <td>0.285613</td>
      <td>0.9576</td>
      <td>0.111111</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>m</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>0.544691</td>
      <td>0.855745</td>
      <td>0.9576</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>m</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>0.091104</td>
      <td>0.857397</td>
      <td>0.0404</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>m</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>0.818060</td>
      <td>0.571702</td>
      <td>0.7212</td>
      <td>0.888889</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

# One Hot Encodes (Fav colour and sex)

### sex


```python
dums = pd.get_dummies(data['sex'])
```


```python
data = data.drop('sex' , axis = 1)
```


```python
dums.head(7)
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
      <th>f</th>
      <th>m</th>
      <th>other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.reset_index(drop = True, inplace = True)
dums.reset_index(drop = True , inplace =True)
```


```python
data = pd.concat([data,dums], axis = 1, sort = False)
```


```python
data.head(7)
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
      <th>total sleep/night</th>
      <th>caloric intake</th>
      <th>f</th>
      <th>m</th>
      <th>other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.048193</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>green</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>0.908540</td>
      <td>0.713304</td>
      <td>0.2996</td>
      <td>0.222222</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>blue</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>0.636421</td>
      <td>0.429428</td>
      <td>0.8340</td>
      <td>1.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>green</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>0.909057</td>
      <td>0.714533</td>
      <td>0.4288</td>
      <td>0.333333</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>green</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>0.091079</td>
      <td>0.285613</td>
      <td>0.9576</td>
      <td>0.111111</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>none</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>0.544691</td>
      <td>0.855745</td>
      <td>0.9576</td>
      <td>1.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>green</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>0.091104</td>
      <td>0.857397</td>
      <td>0.0404</td>
      <td>0.333333</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>blue</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>0.818060</td>
      <td>0.571702</td>
      <td>0.7212</td>
      <td>0.888889</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



### Favourite Color


```python
dums = pd.get_dummies(data['favourite colour'])
```


```python
data = data.drop('favourite colour' , axis = 1)
```


```python
data.reset_index(drop = True, inplace = True)
dums.reset_index(drop = True , inplace =True)
```


```python
data = pd.concat([data,dums], axis = 1, sort = False)
```


```python
data.head(7)
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
      <th>total sleep/night</th>
      <th>caloric intake</th>
      <th>f</th>
      <th>m</th>
      <th>other</th>
      <th>blue</th>
      <th>green</th>
      <th>none</th>
      <th>red</th>
      <th>yellow</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.048193</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>0.908540</td>
      <td>0.713304</td>
      <td>0.2996</td>
      <td>0.222222</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.313253</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>0.636421</td>
      <td>0.429428</td>
      <td>0.8340</td>
      <td>1.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.361446</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>0.909057</td>
      <td>0.714533</td>
      <td>0.4288</td>
      <td>0.333333</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.975904</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>0.091079</td>
      <td>0.285613</td>
      <td>0.9576</td>
      <td>0.111111</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0.493976</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>0.544691</td>
      <td>0.855745</td>
      <td>0.9576</td>
      <td>1.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>1.000000</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>0.091104</td>
      <td>0.857397</td>
      <td>0.0404</td>
      <td>0.333333</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>0.265060</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>0.818060</td>
      <td>0.571702</td>
      <td>0.7212</td>
      <td>0.888889</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.to_csv('/Users/parsa/Desktop/7gate/Week1/Synopsis/_students/parsa_habibi/homework4/data.csv')
new_data = pd.read_csv('/Users/parsa/Desktop/7gate/Week1/Synopsis/_students/parsa_habibi/homework4/data.csv')
new_data.head(7)
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
      <th>Unnamed: 0</th>
      <th>ID</th>
      <th>age</th>
      <th>monthly income</th>
      <th>work hours/week</th>
      <th>siblings</th>
      <th>top finish placement</th>
      <th>last time</th>
      <th>bed time</th>
      <th>wake up time</th>
      <th>total sleep/night</th>
      <th>caloric intake</th>
      <th>f</th>
      <th>m</th>
      <th>other</th>
      <th>blue</th>
      <th>green</th>
      <th>none</th>
      <th>red</th>
      <th>yellow</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0.048193</td>
      <td>0.108637</td>
      <td>0.240506</td>
      <td>0.444444</td>
      <td>0.555556</td>
      <td>0.900000</td>
      <td>0.908540</td>
      <td>0.713304</td>
      <td>0.2996</td>
      <td>0.222222</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>0.313253</td>
      <td>0.283693</td>
      <td>0.670886</td>
      <td>0.555556</td>
      <td>0.111111</td>
      <td>0.966667</td>
      <td>0.636421</td>
      <td>0.429428</td>
      <td>0.8340</td>
      <td>1.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>0.361446</td>
      <td>0.110499</td>
      <td>0.341772</td>
      <td>0.555556</td>
      <td>0.888889</td>
      <td>0.733333</td>
      <td>0.909057</td>
      <td>0.714533</td>
      <td>0.4288</td>
      <td>0.333333</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>4</td>
      <td>0.975904</td>
      <td>0.866270</td>
      <td>0.151899</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.866667</td>
      <td>0.091079</td>
      <td>0.285613</td>
      <td>0.9576</td>
      <td>0.111111</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>5</td>
      <td>0.493976</td>
      <td>0.658972</td>
      <td>0.632911</td>
      <td>0.333333</td>
      <td>1.000000</td>
      <td>0.900000</td>
      <td>0.544691</td>
      <td>0.855745</td>
      <td>0.9576</td>
      <td>1.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>6</td>
      <td>1.000000</td>
      <td>0.993299</td>
      <td>0.569620</td>
      <td>0.333333</td>
      <td>0.444444</td>
      <td>0.800000</td>
      <td>0.091104</td>
      <td>0.857397</td>
      <td>0.0404</td>
      <td>0.333333</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>7</td>
      <td>0.265060</td>
      <td>0.112472</td>
      <td>0.898734</td>
      <td>0.000000</td>
      <td>0.777778</td>
      <td>0.766667</td>
      <td>0.818060</td>
      <td>0.571702</td>
      <td>0.7212</td>
      <td>0.888889</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
