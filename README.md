# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 12.08.2025

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
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import statsmodels.api as sm
from statsmodels.tsa.seasonal import seasonal_decompose

data=sm.datasets.sunspots.load_pandas().data

print(data.head())

plt.plot(data['YEAR'], data['SUNACTIVITY'])
plt.xlabel("Year")
plt.ylabel("Sunspot Count")
plt.show()

data['sunact_diff']=data['SUNACTIVITY']-data['SUNACTIVITY'].shift(1)
result = seasonal_decompose(data['SUNACTIVITY'], model='additive', period=12)
data['sunact_sea_diff']=result.resid
data['sunact_log'] = np.log1p(data['SUNACTIVITY'])
data['sunact_log_diff']=data['sunact_log']-data['sunact_log'].shift(1)
result = seasonal_decompose(data['sunact_log_diff'].dropna(), model='additive', period=12)
data['sunact_log_seasonal_diff']=result.resid

plt.figure(figsize=(16,16))

plt.subplot(6,1,1)
plt.title("Original")
plt.plot(data['YEAR'],data['SUNACTIVITY'], label='Original')
plt.legend(loc='best')

plt.subplot(6,1,2)
plt.title("Regular Differencing")
plt.plot(data['YEAR'],data['sunact_diff'], label='Differenced')
plt.legend(loc='best')

plt.subplot(6,1,3)
plt.title("Seasonal Adjustment")
plt.plot(data['YEAR'],data['sunact_sea_diff'], label='Seasonal Residual')
plt.legend(loc='best')

plt.subplot(6,1,4)
plt.title("Log Transformation")
plt.plot(data['YEAR'],data['sunact_log'], label='Log Transform')
plt.legend(loc='best')

plt.subplot(6,1,5)
plt.title("Log Transformation and Regular Differencing")
plt.plot(data['YEAR'],data['sunact_log_diff'], label='Log + Diff')
plt.legend(loc='best')

plt.subplot(6,1,6)
plt.title("Log Transformation, Regular Differencing and Seasonal Differencing:")
plt.plot(data['YEAR'],data['sunact_log_seasonal_diff'], label='Log + Diff + Seasonal Adj')
plt.legend(loc='best')

plt.tight_layout()
plt.show()

```

### OUTPUT:

ORIGINAL:

<img width="1240" height="209" alt="image" src="https://github.com/user-attachments/assets/40980802-6585-4bb2-9537-bb87f33efdd7" />

REGULAR DIFFERENCING:

<img width="1245" height="202" alt="image" src="https://github.com/user-attachments/assets/0a96fb20-05ec-4a99-815b-9d47c2e69580" />

SEASONAL ADJUSTMENT:

<img width="1238" height="197" alt="image" src="https://github.com/user-attachments/assets/8da6f41a-5fb2-4751-8043-f50e8dc096b0" />

LOG TRANSFORMATION:

<img width="1233" height="619" alt="image" src="https://github.com/user-attachments/assets/6f63894d-f150-4eba-ba39-d248f4d0fc23" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
