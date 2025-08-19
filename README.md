# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 19.08.25

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
#NAME: SUNIL KUMAR T
#REG: 212223240164

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
from statsmodels.tsa.stattools import adfuller

data=pd.read_csv('usedcars.csv')
data.head()
data['Year'] = pd.to_datetime(data['Year'], format='%Y')
# Aggregate by Year (mean kilometers per year)
yearly_data = data.groupby(data['Year'].dt.year)['Kilometers_Driven'].mean()
yearly_data = yearly_data.asfreq('Y')
data['km_diff'] = data['Kilometers_Driven'] - data['Kilometers_Driven'].shift(1)
# Seasonal decomposition (original km)
result = seasonal_decompose(data['Kilometers_Driven'], model='additive', period=1)  
data['km_seasonal_diff'] = result.resid
# Log transform
data['km_log'] = np.log(data['Kilometers_Driven'].replace(0, np.nan))
# Log difference
data['km_log_diff'] = data['km_log'] - data['km_log'].shift(1)

plt.figure(figsize=(16, 16))
# 1. Original Data
plt.subplot(6, 1, 1)
plt.plot(data['Year'], data['Kilometers_Driven'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('Kilometers Driven')

# 2. Regular Difference
plt.subplot(6, 1, 2)
plt.plot(data['Year'], data['km_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced KMs')

# 3. Seasonal Adjustment
plt.subplot(6, 1, 3)
plt.plot(data['Year'], data['km_seasonal_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted KMs')

# 4. Log Transformation
plt.subplot(6, 1, 4)
plt.plot(data['Year'], data['km_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(KMs)')

# 5. Log Transformation + Differencing
plt.subplot(6, 1, 5)
plt.plot(data['Year'], data['km_log_diff'], label='Log Diff')
plt.legend(loc='best')
plt.title('Log Transformation + Differencing')
plt.xlabel('Year')
plt.ylabel('Diff(Log(KMs))')

plt.tight_layout()
plt.show()
```


### OUTPUT:
## ORIGINAL DATA:
<img width="628" height="172" alt="Screenshot 2025-08-19 101023" src="https://github.com/user-attachments/assets/3b72db10-e76d-4715-a9c3-d7b8b127bfeb" />

## REGULAR DIFFERENCING:
<img width="624" height="181" alt="Screenshot 2025-08-19 101032" src="https://github.com/user-attachments/assets/b8f65557-7bfc-441e-9d3e-c330b886ea8a" />

## SEASONAL ADJUSTMENT:
<img width="614" height="182" alt="Screenshot 2025-08-19 101038" src="https://github.com/user-attachments/assets/d49ff1f6-e9e7-4e84-9e35-ff41ae64603f" />

## LOG TRANSFORMATION:
<img width="598" height="184" alt="Screenshot 2025-08-19 101045" src="https://github.com/user-attachments/assets/e64372f9-dbc3-48f5-accd-ea0956810942" />

## LOG TRANSFORMATION + DIFFERENCING:
<img width="662" height="122" alt="Screenshot 2025-08-19 101050" src="https://github.com/user-attachments/assets/04fcd4fa-3f28-414e-85bf-a62b353b2a10" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
