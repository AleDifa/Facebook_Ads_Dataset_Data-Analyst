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
 
