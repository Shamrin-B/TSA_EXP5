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


<img width="431" height="137" alt="image" src="https://github.com/user-attachments/assets/0555d50d-ed93-4edb-a412-17b7fc827418" />




TREND PLOT REPRESENTATION :


<img width="441" height="137" alt="image" src="https://github.com/user-attachments/assets/b6e203e2-2548-4e24-811d-62cf86ad5c79" />



RESIDUAL REPRESENTATION:


<img width="441" height="128" alt="image" src="https://github.com/user-attachments/assets/0fc990dc-d632-451d-aa7b-42a3f9071447" />




### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
