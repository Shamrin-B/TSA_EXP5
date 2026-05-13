# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION



### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load data
data = pd.read_csv('/content/gold_rate_history.csv')

data.columns = data.columns.str.strip()

print("Columns in dataset:", data.columns)

# Convert Date column to datetime
data['Date'] = pd.to_datetime(data['Date'])

# Set Date as index
data.set_index('Date', inplace=True)

# Keep only numeric column
data = data[['Standard Gold (22 K)']]

# Convert yearly average
data = data.resample('YE').mean()

# Remove missing values
data = data.dropna()

# Select series
series = data['Standard Gold (22 K)']

# Period value
period_value = 2

# Seasonal decomposition
decomposition = seasonal_decompose(
    series,
    model='additive',
    period=period_value
)

# Plot results
plt.figure(figsize=(10, 12))

# Original Data
plt.subplot(411)

plt.plot(data['Standard Gold (22 K)'], label='Original data')

plt.legend(loc='upper left')

plt.title('Gold Rate')

# Trend Plot
plt.subplot(412)

plt.plot(decomposition.trend, label='Trend', color='orange')

plt.legend(loc='upper left')

plt.title('Linear Trend Plot')

# Seasonal Plot
plt.subplot(413)

plt.plot(decomposition.seasonal, label='Seasonal', color='green')

plt.legend(loc='upper left')

plt.title('Seasonality Plot')

# Residual Plot
plt.subplot(414)

plt.plot(decomposition.resid, label='Residual', color='red')

plt.legend(loc='upper left')

plt.title('Residual Plot')

plt.tight_layout()

plt.show()
```
















### OUTPUT:

PLOTTING THE DATA:



<img width="1246" height="365" alt="image" src="https://github.com/user-attachments/assets/6c8fdd73-f66a-4f03-8c61-2676c6f6b9f0" />


SEASONAL PLOT REPRESENTATION :

<img width="1225" height="362" alt="image" src="https://github.com/user-attachments/assets/cca3cef8-c217-44c3-92cf-3eeb1a022b35" />




TREND PLOT REPRESENTATION :


<img width="1231" height="382" alt="image" src="https://github.com/user-attachments/assets/b4ad04a0-9cab-4705-8657-d6c8b45e9ede" />



RESIDUAL REPRESENTATION:

<img width="1231" height="371" alt="image" src="https://github.com/user-attachments/assets/11e3ab47-1733-4485-990e-ce88d40e2f56" />





### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
