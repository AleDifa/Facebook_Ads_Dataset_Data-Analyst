# Facebook_Ads_Dataset_Data-Analyst
In this dataset we clean data, create KPI feature and show a final valutation for understand the better parameter to perfome in Facebook advertising


Steps:
* Cleaning data
* Marketing metrics (KPIs)missing we, creating additional features
    1. Click-through-rate (CTR)
    2. Cost Per Click (CPC)
    3. Cost Per Action
    4. Cost Per Thousand/Mille (CPM)
* Identifying the best parameters of each feature for efficient ads and High Roas
* Final suggestions for the ideal campaign

#### Cleaning Data

This for loop produces a list below showing the percentage of missing values for each of the features
```python
import numpy as np
for col in df.columns:
    pct_missing = np.mean(df[col].isnull())
    print('{} - {}%'.format(col, round(pct_missing*100)))
 ```   
campaign_id - 0.0% <br>
fb_campaign_id - 0.0%  <br>
PeopleWhoMatch - 71.0% <br>
age - 0.0% <br>
gender - 0.0% <br>
Politics - 100.0% <br>
AdSpendCurrency - 27.0% <br>
impressions - 0.0% <br>
clicks - 0.0% <br>
spent - 0.0% <br>
total_conversion - 33.0% <br>
approved_conversion - 33.0% <br>

replace values
```python
df['AdSpendCurrency'].value_counts(dropna=False)
df['AdSpendCurrency'].fillna('USD', inplace=True)
df['total_conversion'].fillna(0.0, inplace=True)
`This in Numpy replace all +inf -inf in df with nan`
df.replace([np.inf, -np.inf], np.nan,inplace=True)
```

Create KPI metrics
```python
df["CTR"] = df["clicks"]/ df["impressions"]*100
df["CPC"] = df["spent"]/ df["clicks"]
df["CPM"] = df["spent"]/ df["impressions"]*1000
df["CPA"] = df["spent"]/ df["total_conversion"]

df.round({"spent":2,'CTR': 2, 'CPC': 2, "CPM":2, "CPA":2}).head(1)
```
<img width="530" alt="Capture" src="https://user-images.githubusercontent.com/37181764/105889783-da1bdd80-600e-11eb-80e9-b88807196b4b.PNG">
#Top 5 ads by number of impressions
<img width="340" alt="Capture1" src="https://user-images.githubusercontent.com/37181764/105889963-09cae580-600f-11eb-8743-d890eebc6784.PNG">

best ads by CPC Cost per Click
```python
df2.nlargest(3, 'CPC')
```
<img width="337" alt="Capture2" src="https://user-images.githubusercontent.com/37181764/105890398-99709400-600f-11eb-8d19-27a6f20efcce.PNG">

find the ad with max Impressions and min CPC ( cpc is 0 because some data is not real)
```python
df.agg({'impressions': 'max', 'CPC':'min'})
```
<img width="164" alt="Capture3" src="https://user-images.githubusercontent.com/37181764/105890768-100d9180-6010-11eb-8c88-15dae97e4261.PNG">
#### Cost Analysis
```python
print('Campaign with more clicks')
print((df.groupby(['campaign_id'])).clicks.sum())
print('Campaign with more spent')
print((df.groupby(['campaign_id'])).spent.sum())
print('Campaign with more total conversions')
print((df.groupby(['campaign_id'])).total_conversion.sum())
print('Campaign with more ad count')
print((df.groupby(['campaign_id'])).ad_id.count())
```
