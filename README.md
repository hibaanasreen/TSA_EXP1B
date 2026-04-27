# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date:27/04/26

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy

2. Read the data using the pandas

3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.

4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.

5. Display the overall results.
### PROGRAM:
```python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load dataset
data = pd.read_csv('/content/student_performance.csv')

# Create artificial time index (monthly)
data['Month'] = pd.date_range(start='2020-01-01', periods=len(data), freq='M')

# Set index
data.set_index('Month', inplace=True)

# Use correct column
ts = data['final_score']

# Regular differencing
data['diff'] = ts - ts.shift(1)

# Seasonal decomposition (original)
result = seasonal_decompose(ts, model='additive', period=12)
data['seasonal_diff'] = result.resid

# Log transform
data['log'] = np.log(ts + 1)

# Log differencing
data['log_diff'] = data['log'] - data['log'].shift(1)

# Seasonal decomposition on log diff
result = seasonal_decompose(data['log_diff'].dropna(), model='additive', period=12)
data['log_seasonal_diff'] = result.resid

# Plotting
plt.figure(figsize=(16, 16))

# 1. Original
plt.subplot(6, 1, 1)
plt.plot(ts, label='Original')
plt.legend()
plt.title('Original Final Score')

# 2. Difference
plt.subplot(6, 1, 2)
plt.plot(data['diff'], label='Regular Difference')
plt.legend()
plt.title('Differencing')

# 3. Seasonal Adjustment
plt.subplot(6, 1, 3)
plt.plot(data['seasonal_diff'], label='Seasonal Adjustment')
plt.legend()
plt.title('Seasonal Adjustment')

# 4. Log Transform
plt.subplot(6, 1, 4)
plt.plot(data['log'], label='Log Transform')
plt.legend()
plt.title('Log Transformation')

# 5. Log Difference
plt.subplot(6, 1, 5)
plt.plot(data['log_diff'], label='Log + Difference')
plt.legend()
plt.title('Log + Differencing')

# 6. Log + Seasonal Difference
plt.subplot(6, 1, 6)
plt.plot(data['log_seasonal_diff'], label='Log + Seasonal Diff')
plt.legend()
plt.title('Log + Seasonal Differencing')

plt.tight_layout()
plt.show()

# Final overview plot
data[['final_score']].plot(figsize=(10,5), title='Final Score Time Series')
plt.show()
```


### OUTPUT:


REGULAR DIFFERENCING:

<img width="1659" height="545" alt="image" src="https://github.com/user-attachments/assets/35644381-6ddb-4727-a960-bfa038c61f02" />


SEASONAL ADJUSTMENT:


<img width="1651" height="269" alt="image" src="https://github.com/user-attachments/assets/c36e402c-3a6e-48b7-ab99-b4ba7738627a" />


LOG TRANSFORMATION:

<img width="1657" height="274" alt="image" src="https://github.com/user-attachments/assets/721a8cd5-670b-47c5-8769-293fb1c38d4f" />




### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
